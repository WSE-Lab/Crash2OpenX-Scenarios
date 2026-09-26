# Large turning vehicle at an intersection

Tests the interaction between an ADS vehicle starting through an intersection and a large turning vehicle.

## Recorded result

The turning vehicle contacted the ADS. Recorded ticks: **368**. Termination: **`collision_exit`**.

The starting/turning relationship is retained, but the vehicle model does not reproduce the original bus's front-mounted bicycle rack. The clearance metric covers the review window; contact occurred later.

## Files

| File | Use |
| --- | --- |
| [scenario.xosc](scenario.xosc) | OpenSCENARIO test entry point. |
| [map.xodr](map.xodr) | Road network; keep beside `scenario.xosc`. |
| [scene_seed.json](scene_seed.json) | Delivered scene parameters and behavior-check input. |
| [road_seed.json](road_seed.json) | Road parameters for the replay command. |
| [report.pdf](report.pdf) | Original crash report. |
| [preview.mp4](preview.mp4) | Full recorded CARLA RGB video. |
| **[openscenario_full.log](openscenario_full.log)** | **Full captured execution console log, from startup to the actual recorded stop.** |
| [summary.json](summary.json) | Recorded outcome, tick count, criteria, and termination. |

## Replay

Complete the [runtime setup](../../REPRODUCE.md) first. From the separate Crash2OpenX toolchain directory:

```sh
CASE_DIR="/absolute/path/to/crash2openx-scenarios/scenarios/120_Zoox_February_22_2024_(1)"
uv run python tools/carla_remote.py run \
  --xodr "$CASE_DIR/map.xodr" --xosc "$CASE_DIR/scenario.xosc" \
  --scene-seed "$CASE_DIR/scene_seed.json" --road-seed "$CASE_DIR/road_seed.json" \
  --pcla-agent if_if --sut-actor hero --rgb-actor-role hero --max-seconds 600
```

For a configured local Linux GPU host, use `tools/carla_local.py` with the same arguments. The log is the unchanged original wrapper log, including all scenario subprocess output; it records this run's actual termination, which can be collision exit or timeout. New runs may produce different ADS trajectories and outcomes.

[All scenarios](../../README.md)
