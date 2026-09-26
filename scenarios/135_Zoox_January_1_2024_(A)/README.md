# Three-vehicle intersection conflict

Case ID: `135_Zoox_January_1_2024_(A)`

Tests a straight-moving ADS vehicle, crossing traffic, and a stationary vehicle near a stop line.

## Full OpenSCENARIO log

**[Full recorded execution log](evidence/logs/openscenario_full.log)** · [Log file guide](evidence/README.md) · [Full per-tick actor trace](evidence/sim_trace_raw.jsonl) · [Storyboard/event stream](evidence/events.jsonl)

The recorded run contains **502 ticks** and ends with `scenario_completed`. The run records scenario completion; inspect the event and criteria results separately to assess its outcome.

## Recorded outcome

A crossing SUV contacted the ADS; the ADS departed its lane later in the episode.

## Scope and limitations

The accepted scope is the usable interaction. The complete accident chain, including the SUV rotating and then striking the stationary vehicle, was not reconstructed. The windowed metrics do not summarize every later event.

This is a crash-inspired ADS test variant with one recorded episode at the delivered parameter setting. Experimental onset, speed, and spacing may differ from the report. Read [manifest.json](evidence/manifest.json) for the source/derived parameters and [quality_review.json](evidence/quality_review.json) for the measured window and checks.

## Directory guide

| Directory | What is inside | Start here |
| --- | --- | --- |
| `simulation/` | The executable scenario, road network, and derived scene seed. | [scenario.xosc](simulation/scenario.xosc), [map.xodr](simulation/map.xodr), [scene_seed.json](simulation/scene_seed.json) |
| `preview/` | Interaction video, contact sheet, road views, and measured response plot. | [interaction.mp4](preview/interaction.mp4), [map_and_response.png](preview/map_and_response.png) |
| `source/` | Original report, extracted text, original seeds, and Chinese case note. | [report.pdf](source/report.pdf), [source_text.txt](source/source_text.txt) |
| `evidence/` | Full recorded video, traces, events, logs, quality review, and exact runtime code. | [Full execution log](evidence/logs/openscenario_full.log), [log guide](evidence/README.md), [quality_review.json](evidence/quality_review.json) |

See the [full directory reference](../../docs/structure.md) for the files inside each directory.

## Replay

Follow the [environment setup](../../docs/usage.md#prepare-the-execution-environment) first. Then run this from the full Crash2OpenX toolchain directory:

```sh
CASE_DIR="/absolute/path/to/crash2openx-scenarios/scenarios/135_Zoox_January_1_2024_(A)"
uv run python tools/carla_remote.py run \
  --xodr "$CASE_DIR/simulation/map.xodr" \
  --xosc "$CASE_DIR/simulation/scenario.xosc" \
  --pcla-agent if_if --sut-actor hero --rgb-actor-role hero --max-seconds 600 \
  --scene-seed "$CASE_DIR/simulation/scene_seed.json" \
  --road-seed "$CASE_DIR/source/road_seed.json"
```

For a configured local Linux GPU host, use `tools/carla_local.py` with the same arguments. Keep `scenario.xosc` beside `map.xodr` inside `simulation/`. Replays may produce different trajectories.

[All scenarios](../README.md) · [View the collection](../../preview/index.html) · [Usage guide](../../docs/usage.md)
