# Replay a scenario

The scenario collection contains data and recorded results. Install the execution toolchain separately at the fixed revision below.

## 1. Prepare the runtime

Use a Linux x86_64 host with an NVIDIA GPU, Docker, NVIDIA Container Toolkit, Git, uv, and ffmpeg. The runtime uses CARLA **0.9.16**, the Crash2OpenX-patched ScenarioRunner, and PCLA's **InterFuser (`if_if`)** agent.

On that GPU host:

```sh
git clone https://github.com/WSE-Lab/Crash2OpenX.git crash2openx-runtime
cd crash2openx-runtime
git checkout 6263110198042f7f3feb29a3765124e47b919091
git submodule update --init --recursive
uv sync --locked --python 3.12
scripts/setup_exec_env.sh
uv run python -m tools.prepare_runtime --output outputs/runtime
```

The setup script creates the Python 3.10 execution environment. `prepare_runtime` installs the pinned dependencies and reviewed ScenarioRunner/PCLA patches into a new directory. It refuses to overwrite an existing runtime; use a fresh output path if preparing another one.

Download the InterFuser weights according to the generated `outputs/runtime/PCLA/README.md`, placing them in the generated runtime's PCLA tree. Configure the toolchain's `.env.local` using its `.env.example`, including the absolute runtime path. For local execution:

```ini
CARLA_MODE=local
CARLA_LOCAL_PROJECT_DIR=/absolute/path/to/crash2openx-runtime/outputs/runtime
CARLA_LOCAL_MIN_FREE_GIB=10
```

Start CARLA from the toolchain directory:

```sh
docker compose -f docker/docker-compose.yml up -d
```

The fixed revision's [runtime setup guide](https://github.com/WSE-Lab/Crash2OpenX/blob/6263110198042f7f3feb29a3765124e47b919091/docs/reproduce.md) covers the environment and remote-host configuration. These scenarios need the project's condition and route extensions; use its prepared runtime. No language-model API key is needed for replaying the supplied inputs.

## 2. Run a case

Run this from the separate `crash2openx-runtime` toolchain directory after setup. Set `CASE_DIR` to the absolute path of a case in the scenario collection:

```sh
CASE_DIR="/absolute/path/to/crash2openx-scenarios/scenarios/013_Zoox_February_19_2025"
uv run python tools/carla_local.py run \
  --xodr "$CASE_DIR/map.xodr" --xosc "$CASE_DIR/scenario.xosc" \
  --scene-seed "$CASE_DIR/scene_seed.json" --road-seed "$CASE_DIR/road_seed.json" \
  --pcla-agent if_if --sut-actor hero --rgb-actor-role hero --max-seconds 600
```

For a remote GPU host, use the same toolchain revision on the client, run `uv sync --locked --python 3.12`, and configure its `CARLA_REMOTE_*` settings following the linked guide. After preparing the GPU host's runtime, deploy the remote wrapper from the client:

```sh
uv run python tools/carla_remote.py deploy-runner
```

Then run the same case through the remote driver:

```sh
CASE_DIR="/absolute/path/to/crash2openx-scenarios/scenarios/013_Zoox_February_19_2025"
uv run python tools/carla_remote.py run \
  --xodr "$CASE_DIR/map.xodr" --xosc "$CASE_DIR/scenario.xosc" \
  --scene-seed "$CASE_DIR/scene_seed.json" --road-seed "$CASE_DIR/road_seed.json" \
  --pcla-agent if_if --sut-actor hero --rgb-actor-role hero --max-seconds 600
```

Change `CASE_DIR` to select another case. Quote paths, including case IDs with parentheses. Keep `scenario.xosc` next to `map.xodr` so its relative map reference resolves. `hero` remains controlled by InterFuser.

## 3. Compare the result

Each case contains three recorded reference outputs:

| File | Purpose |
| --- | --- |
| `preview.mp4` | Full recorded CARLA RGB video. |
| **`openscenario_full.log`** | **Full captured execution console**, copied unchanged from the original wrapper log and including the scenario subprocess output. |
| `summary.json` | Actual termination, tick count, criteria, and outcome metrics. |

Save new run outputs separately. Compare their behavior, termination, and criteria with these references. The console log ends at the original attempt's actual stop: case 013 uses collision exit; case 038 timed out. Case 038 has no normal final console summary; its `summary.json` records `signal:15`. A complete log does not mean every planned action completed.

The fixed toolchain provides a supported replay environment; original runs used some differing runtime versions. A new run may produce different trajectories and outcomes. See each case README for its source-specific limits. The collection's [manifest.json](manifest.json) records the toolchain revision and SHA-256 hashes of the retained inputs and reference outputs.

[Scenario catalog](README.md#scenarios)
