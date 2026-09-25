# Cyclist cut-in during an ADS turn

Case ID: `144_Waymo_October_17_2023`

Tests avoidance when a cyclist approaches laterally while the ADS turns.

## Recorded outcome

The ADS braked and departed its lane. Minimum reviewed clearance was approximately 1.84 m, with no contact.

## Scope and limitations

Initial speed was experimentally calibrated. Avoiding contact does not establish that the complete driving task succeeded.

This is a crash-inspired ADS test variant with one recorded episode at the delivered parameter setting. Experimental onset, speed, and spacing may differ from the report. Read [manifest.json](evidence/manifest.json) for the source/derived parameters and [quality_review.json](evidence/quality_review.json) for the measured window and checks.

## Directory guide

| Directory | What is inside | Start here |
| --- | --- | --- |
| `simulation/` | The executable scenario, road network, and derived scene seed. | [scenario.xosc](simulation/scenario.xosc), [map.xodr](simulation/map.xodr), [scene_seed.json](simulation/scene_seed.json) |
| `preview/` | Interaction video, contact sheet, road views, and measured response plot. | [interaction.mp4](preview/interaction.mp4), [map_and_response.png](preview/map_and_response.png) |
| `source/` | Original report, extracted text, original seeds, and Chinese case note. | [report.pdf](source/report.pdf), [source_text.txt](source/source_text.txt) |
| `evidence/` | Full recorded video, traces, events, logs, quality review, and exact runtime code. | [quality_review.json](evidence/quality_review.json), [carla_rgb.mp4](evidence/carla_rgb.mp4) |

See the [full directory reference](../../docs/structure.md) for the files inside each directory.

## Replay

Follow the [environment setup](../../docs/usage.md#prepare-the-execution-environment) first. Then run this from the full Crash2OpenX toolchain directory:

```sh
CASE_DIR="/absolute/path/to/crash2openx-scenarios/scenarios/144_Waymo_October_17_2023"
uv run python tools/carla_remote.py run \
  --xodr "$CASE_DIR/simulation/map.xodr" \
  --xosc "$CASE_DIR/simulation/scenario.xosc" \
  --pcla-agent if_if --sut-actor hero --rgb-actor-role hero --max-seconds 600 \
  --scene-seed "$CASE_DIR/simulation/scene_seed.json" \
  --road-seed "$CASE_DIR/source/road_seed.json"
```

For a configured local Linux GPU host, use `tools/carla_local.py` with the same arguments. Keep `scenario.xosc` beside `map.xodr` inside `simulation/`. Replays may produce different trajectories.

[All scenarios](../README.md) · [View the collection](../../preview/index.html) · [Usage guide](../../docs/usage.md)
