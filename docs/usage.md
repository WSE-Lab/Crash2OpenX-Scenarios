# Inspect and replay a scenario

## View the recorded results

From this repository's root, run:

```sh
python3 -m http.server 8000 --bind 127.0.0.1
```

Visit **http://localhost:8000/preview/**, or open a case's `preview/interaction.mp4`, `preview/map_overview.png`, and `preview/map_and_response.png` directly. `evidence/carla_rgb.mp4` contains the full recorded RGB episode. Stop the local server with Ctrl+C.

## Prepare the execution environment

A new simulation requires **CARLA 0.9.16**, the Crash2OpenX-patched ScenarioRunner, PCLA's **InterFuser (`if_if`)** agent, and its pretrained weights. The execution host uses Linux x86_64, an NVIDIA GPU, Docker, and the NVIDIA Container Toolkit. A macOS laptop can view the evidence or submit a run to a configured GPU host.

Clone the full toolchain separately:

```sh
git clone --recurse-submodules https://github.com/WSE-Lab/Crash2OpenX.git crash2openx
cd crash2openx
uv sync --locked --python 3.12
```

Follow the toolchain's [runtime setup guide](https://github.com/WSE-Lab/Crash2OpenX/blob/main/docs/reproduce.md) to install the Python 3.10 execution environment, prepare the patched runtime, download the InterFuser weights, start CARLA, and configure `.env.local` for your execution host. The setup uses `scripts/setup_exec_env.sh` and `tools.prepare_runtime`; run the execution setup on the Linux GPU host.

Use the supported runtime: these scenarios depend on the project's simultaneous ADS conditions, actual vehicle-clearance checks, generated lane routes, and Act stop-condition handling. A stock ScenarioRunner install does not provide equivalent behavior. The partial `archive/implementation_snapshot/` directory is not a standalone installation.

No language-model API key is needed to inspect or replay these pre-generated scenarios. CARLA, third-party dependencies, and agent weights are not bundled here.

## Run one case

Run the commands below **from the full `crash2openx` toolchain directory**, after its runtime has been configured. Set `CASE_DIR` to the absolute path of a case in this collection. Quote paths, especially case IDs containing parentheses.

For CARLA on the configured local Linux GPU host:

```sh
CASE_DIR=/absolute/path/to/crash2openx-scenarios/scenarios/013_Zoox_February_19_2025
uv run python tools/carla_local.py run \
  --xodr "$CASE_DIR/simulation/map.xodr" \
  --xosc "$CASE_DIR/simulation/scenario.xosc" \
  --pcla-agent if_if \
  --sut-actor hero \
  --rgb-actor-role hero \
  --max-seconds 600 \
  --scene-seed "$CASE_DIR/simulation/scene_seed.json" \
  --road-seed "$CASE_DIR/source/road_seed.json"
```

For a configured remote GPU host, set your `CARLA_REMOTE_*` values in the toolchain's `.env.local`, deploy the runner as described in the setup guide, and use:

```sh
CASE_DIR=/absolute/path/to/crash2openx-scenarios/scenarios/013_Zoox_February_19_2025
uv run python tools/carla_remote.py run \
  --xodr "$CASE_DIR/simulation/map.xodr" \
  --xosc "$CASE_DIR/simulation/scenario.xosc" \
  --pcla-agent if_if \
  --sut-actor hero \
  --rgb-actor-role hero \
  --max-seconds 600 \
  --scene-seed "$CASE_DIR/simulation/scene_seed.json" \
  --road-seed "$CASE_DIR/source/road_seed.json"
```

Change `CASE_DIR` to select any of the ten cases. Keep `hero` under external ADS control. The `simulation/scenario.xosc` entry point resolves `map.xodr` relatively within the same directory; the archived `evidence/scenario.runtime.xosc` can contain paths specific to the original execution host and is for inspection.

The current toolchain provides a supported replay environment. The archived `evidence/runtime_code/` and `runtime_manifest.json` identify the original episode's implementation, including any differences from that environment. Rerunning can produce different ADS trajectories and outcomes; these commands do not promise a byte-identical historical replay.

## Read and compare the results

1. Read the case's `README.md`, `evidence/manifest.json`, and `evidence/quality_review.json` for the interaction, experimental parameter changes, measured window, and limitations.
2. Compare the derived `simulation/scene_seed.json` with the original `source/scene_seed.json`. The original road seed is `source/road_seed.json`.
3. Review the interaction clip, full RGB episode, traces, collision events, and termination logs together. Windowed clearance/TTC metrics can precede later contact shown in a clip.
4. Save new execution output separately from the archived evidence. Check the new run's actor behavior, contact records, lane departures, and termination before comparing outcomes.

Case 038's original full episode hit a wall-clock timeout; only its interaction window was accepted. Case 262 is a slowdown variant with a moving lead vehicle, not a reconstruction of a complete lead-vehicle stop. See all case guides for additional limits.

## Verify the original files

Run this from the collection repository root. It verifies all 743 original archive files at their new locations, using only Python's standard library:

```sh
python3 - <<'PYVERIFY'
import hashlib
import json
from pathlib import Path

root = Path.cwd()
files = json.loads((root / "archive/provenance/layout.json").read_text())["files"]
failures = []
for original, entry in files.items():
    path = root / entry["path"]
    if not path.is_file() or hashlib.sha256(path.read_bytes()).hexdigest() != entry["sha256"]:
        failures.append(entry["path"])
if failures:
    raise SystemExit("Missing or changed original files:\n" + "\n".join(failures))
print(f"Verified {len(files)} original files at their current paths.")
PYVERIFY
```

[Archive provenance](../archive/README.md) explains the preserved original manifest and path mapping. Historical records still contain the original paths; use the current scenario guides for replay. The archived packaging validator expects the old exact ZIP layout and the full source toolchain, so use the check above for this repository.
