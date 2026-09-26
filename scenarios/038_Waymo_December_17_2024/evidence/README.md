# OpenSCENARIO execution logs — 038

**Open [logs/openscenario_full.log](logs/openscenario_full.log) for the full recorded OpenSCENARIO execution console log.**

It contains 260 lines, from the CARLA readiness and recording setup through the scenario's emitted console output and the last captured termination/cleanup output. It is an **unmodified, byte-for-byte copy of [run_scene_wrapper.log](run_scene_wrapper.log)** and includes the complete [demo.log](demo.log) output. No lines were filtered, summarized, or reconstructed.

## Recorded coverage

- **Recorded termination:** `signal:15`. The run hit the recorded wall-clock timeout and ended with SIGTERM. The log covers that terminated attempt, not a normally completed storyboard.
- **Per-tick actor trace:** 1534 rows, matching `summary.json.total_ticks`; frames 32654933–32656466.
- **Simulation timestamps:** 2.314459–78.964460 s (76.650001 s between the first and last samples).
- **Recorded events:** 28 rows, including `episode_started`, recorded `storyboard_transition` events, and `episode_finished`.

“Full” means the full captured log for this particular run, through its actual termination. It does not imply that all planned OpenSCENARIO actions completed. The console is not a per-tick dump; use the actor trace and event stream below for structured execution data.

## Which file should I read?

| File | What it contains |
| --- | --- |
| **[logs/openscenario_full.log](logs/openscenario_full.log)** | **Primary full recorded execution console log. Start here.** |
| [sim_trace_raw.jsonl](sim_trace_raw.jsonl) | Full recorded per-tick actor states: positions, velocities, controls, bounding boxes, and lane data. This is the file for trajectory/motion analysis. |
| [events.jsonl](events.jsonl) | Episode boundaries, recorded OpenSCENARIO storyboard transitions, and sensor events. |
| [frame_states.jsonl](frame_states.jsonl) | Per-tick ADS ego state/control records. |
| [summary.json](summary.json) | Tick counts, termination reason, criteria results, and aggregate metrics. |
| [demo.log](demo.log) | Scenario subprocess stdout/stderr, already included in the primary log. |
| [run_scene_wrapper.log](run_scene_wrapper.log) | Original filename of the primary log, retained for compatibility and provenance. |
| [runner.log](runner.log) | Short outer-launcher status and result summary. It is not the full scenario console log. |

## Additional original diagnostic logs

These files were copied from the matching original run directory after verifying that its console logs, event stream, trace, summary, and execution metadata match this case's archived evidence.

| File | What it contains |
| --- | --- |
| [rgb_recorder.log](logs/rgb_recorder.log) | Camera recorder and video-encoding output. |
| [paper_recorder.log](logs/paper_recorder.log) | Auxiliary paper/trajectory recorder output present in this run. |
| [carla_server.log.gz](logs/carla_server.log.gz) | Compressed CARLA server diagnostics. The original capture was limited to the last 50,000 lines and is not an unlimited full server log. |
| [server_log_capture.json](logs/server_log_capture.json) | Original server-log capture status and limits. |
| [logs/manifest.json](logs/manifest.json) | Source run identity, log hashes, recording coverage, and termination. |

[Scenario description and replay](../README.md) · [Collection log guide](../../../docs/logs.md)
