# OpenSCENARIO logs

**For the full recorded execution console, open `scenarios/<case_id>/evidence/logs/openscenario_full.log`.** The [013 example](../scenarios/013_Zoox_February_19_2025/evidence/logs/openscenario_full.log) is a direct entry point.

For full per-tick actor states, use `evidence/sim_trace_raw.jsonl`. For episode boundaries, recorded storyboard transitions, and sensor events, use `evidence/events.jsonl`. These files describe different aspects of the same run.

## Direct links for all ten cases

| Case | Full console log | Recorded ticks | Termination | File guide |
| --- | --- | --- | --- | --- |
| 013 | [openscenario_full.log](../scenarios/013_Zoox_February_19_2025/evidence/logs/openscenario_full.log) (179 lines) | 259 | `collision_exit` | [Evidence README](../scenarios/013_Zoox_February_19_2025/evidence/README.md) |
| 035 | [openscenario_full.log](../scenarios/035_Zoox_January_26_2025/evidence/logs/openscenario_full.log) (190 lines) | 381 | `collision_exit` | [Evidence README](../scenarios/035_Zoox_January_26_2025/evidence/README.md) |
| 038 | [openscenario_full.log](../scenarios/038_Waymo_December_17_2024/evidence/logs/openscenario_full.log) (260 lines) | 1534 | `signal:15` | [Evidence README](../scenarios/038_Waymo_December_17_2024/evidence/README.md) |
| 055 | [openscenario_full.log](../scenarios/055_Waymo_November_3_2024_%281%29/evidence/logs/openscenario_full.log) (196 lines) | 440 | `collision_exit` | [Evidence README](../scenarios/055_Waymo_November_3_2024_%281%29/evidence/README.md) |
| 097 | [openscenario_full.log](../scenarios/097_Zoox_May_30_2024/evidence/logs/openscenario_full.log) (176 lines) | 259 | `collision_exit` | [Evidence README](../scenarios/097_Zoox_May_30_2024/evidence/README.md) |
| 120 | [openscenario_full.log](../scenarios/120_Zoox_February_22_2024_%281%29/evidence/logs/openscenario_full.log) (190 lines) | 368 | `collision_exit` | [Evidence README](../scenarios/120_Zoox_February_22_2024_%281%29/evidence/README.md) |
| 135 | [openscenario_full.log](../scenarios/135_Zoox_January_1_2024_%28A%29/evidence/logs/openscenario_full.log) (204 lines) | 502 | `scenario_completed` | [Evidence README](../scenarios/135_Zoox_January_1_2024_%28A%29/evidence/README.md) |
| 144 | [openscenario_full.log](../scenarios/144_Waymo_October_17_2023/evidence/logs/openscenario_full.log) (202 lines) | 502 | `scenario_completed` | [Evidence README](../scenarios/144_Waymo_October_17_2023/evidence/README.md) |
| 262 | [openscenario_full.log](../scenarios/262_Zoox_February_11_2023/evidence/logs/openscenario_full.log) (204 lines) | 502 | `scenario_completed` | [Evidence README](../scenarios/262_Zoox_February_11_2023/evidence/README.md) |
| 293 | [openscenario_full.log](../scenarios/293_Zoox_October_14_2022/evidence/logs/openscenario_full.log) (186 lines) | 329 | `collision_exit` | [Evidence README](../scenarios/293_Zoox_October_14_2022/evidence/README.md) |

## What “full” means

The primary file preserves the entire `run_scene_wrapper.log` captured for that selected attempt. The runtime redirects the wrapper’s stdout and stderr into that file; the scenario subprocess uses `tee` to send its output both to `demo.log` and to the wrapper log. Every case’s full `demo.log` is present byte-for-byte in the primary log. Outer-launcher setup and result details remain in `runner.log`.

The primary log includes only messages emitted by the original logger configuration. It is not a dump of every internal OpenSCENARIO condition evaluation. The original structured trace and event files are provided alongside it without filtering.

A complete captured log does not establish normal scenario completion. Collision-exit runs end at their configured stop; case 038 ended with `signal:15` after a wall-clock timeout. Each evidence README reports the actual termination and recorded frame/time interval. Per-tick trace counts were checked against `summary.json.total_ticks`.

## Auxiliary logs and provenance

The `evidence/logs/` directory also contains the original RGB recorder log, the paper/trajectory recorder log where present, and compressed CARLA server diagnostics. The server capture was explicitly limited to 50,000 tail lines; `server_log_capture.json` retains that limit and the capture result. These diagnostics are not substitutes for the OpenSCENARIO console or actor trace.

Each `logs/manifest.json` records the matching source run, exact file hashes, captured counts, and termination. The new primary filename is an unmodified copy of the existing wrapper log; original package files and their original hashes are preserved.

[Usage guide](usage.md) · [Directory reference](structure.md) · [Scenario catalog](../scenarios/README.md)
