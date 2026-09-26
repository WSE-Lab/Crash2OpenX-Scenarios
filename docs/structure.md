# Directory reference

Every scenario has the same structure. The four directories correspond to running the test, viewing it, tracing its source, and examining its recorded execution.

## Scenario layout

```text
scenarios/<case_id>/
├── README.md
├── simulation/
│   ├── scenario.xosc
│   ├── map.xodr
│   └── scene_seed.json
├── preview/
│   ├── interaction.mp4
│   ├── contact_sheet.jpg
│   ├── map.html
│   ├── map_overview.png
│   └── map_and_response.png
├── source/
│   ├── report.pdf
│   ├── source_text.txt
│   ├── source_extraction.json
│   ├── road_seed.json
│   ├── scene_seed.json
│   ├── road_generation.json
│   └── README.zh-CN.md
└── evidence/
    ├── README.md
    ├── logs/
    │   ├── openscenario_full.log
    │   ├── rgb_recorder.log
    │   ├── paper_recorder.log       (only where captured)
    │   ├── carla_server.log.gz
    │   ├── server_log_capture.json
    │   └── manifest.json
    ├── manifest.json
    ├── quality_review.json
    ├── clip_provenance.json
    ├── carla_rgb.mp4
    ├── sim_trace_raw.jsonl
    ├── frame_states.jsonl
    ├── events.jsonl
    ├── summary.json
    ├── behavior_check.json
    ├── roadgraph_selfcheck.json
    ├── remote_run.json
    ├── scenario.runtime.xosc
    ├── demo.log
    ├── runner.log
    ├── run_scene_wrapper.log
    ├── ads_review/
    ├── rgb_frames/
    ├── runtime_manifest.json
    └── runtime_code/
```

## simulation

| File | Purpose |
| --- | --- |
| `scenario.xosc` | OpenSCENARIO 1.0 entry point for the delivered test. Its relative map reference is `map.xodr`. |
| `map.xodr` | OpenDRIVE 1.5 road network used by the scenario. Keep it beside `scenario.xosc`. |
| `scene_seed.json` | Derived scene parameters for this experimental ADS test. |

Use this directory's scenario/map pair for a new run. [Replay commands](usage.md#run-one-case) also pass the derived scene seed and the original road seed from `source/`.

## preview

| File | Purpose |
| --- | --- |
| `interaction.mp4` | Selected interaction video for quick review. |
| `contact_sheet.jpg` | Sampled frames from the reviewed interaction. |
| `map.html`, `map_overview.png` | Interactive/static views of the generated road. |
| `map_and_response.png` | Road geometry and measured trajectory/response plot. |

These assets summarize the test. The full recorded RGB episode and clip hashes live in `evidence/`.

## source

| File | Purpose |
| --- | --- |
| `report.pdf`, `source_text.txt` | Original crash report and extracted text. |
| `source_extraction.json` | Report extraction metadata. |
| `road_seed.json`, `scene_seed.json` | Original road/scene seeds. The scene seed here precedes the experimental modifications in `simulation/scene_seed.json`. |
| `road_generation.json` | Road-generation metadata. |
| `README.zh-CN.md` | Original Chinese case note, preserved for provenance. Its path descriptions refer to the original package layout. |

## evidence

**Start with `evidence/logs/openscenario_full.log` for the full recorded execution console**, or read the case's `evidence/README.md` for its captured interval and termination. The [log guide](logs.md) links directly to all ten full logs.

| File or directory | Purpose |
| --- | --- |
| `README.md` | Direct log links, captured frame/time interval, and the actual termination of this run. |
| `logs/openscenario_full.log` | Full captured wrapper console output, including the complete scenario subprocess output. An unmodified copy of `run_scene_wrapper.log`. |
| `logs/rgb_recorder.log`, `logs/paper_recorder.log` | Original recorder/video-encoding diagnostics; the paper recorder log is included only where captured. |
| `logs/carla_server.log.gz`, `logs/server_log_capture.json` | Compressed CARLA server diagnostics and original capture settings. Server capture was limited to the last 50,000 lines. |
| `logs/manifest.json` | Added log file hashes, source run identity, coverage counts, and termination. |
| `manifest.json` | Source hashes, calibration, and original/derived parameters. Compare `source_scene` and `derived_scene`. |
| `quality_review.json` | Measured interactions, native-map checks, termination, contacts, and limitations. |
| `clip_provenance.json` | Timing and hashes linking the preview clip to the original videos. |
| `carla_rgb.mp4` | Full recorded RGB episode. |
| `sim_trace_raw.jsonl` | Full recorded per-tick actor states, including motion, controls, bounding boxes, and lane data. Each line is one JSON object. |
| `frame_states.jsonl` | Per-tick ADS ego state and control records. |
| `events.jsonl` | Episode boundaries, recorded OpenSCENARIO storyboard transitions, and sensor events, including collision evidence. |
| `summary.json`, `behavior_check.json` | Episode summary and behavior checks. |
| `roadgraph_selfcheck.json` | Agreement between generated road geometry and native CARLA road sampling. |
| `remote_run.json` | Execution metadata and hashes of the uploaded inputs. Historical machine paths identify the original run. |
| `scenario.runtime.xosc` | Archived runtime input that can contain server-specific absolute paths. For new runs, use `simulation/scenario.xosc`. |
| `demo.log` | Scenario subprocess stdout/stderr, fully included in `logs/openscenario_full.log`. |
| `run_scene_wrapper.log` | Original filename of the full recorded console log, retained for compatibility and provenance. |
| `runner.log` | Short outer-launcher status/result summary; not the full scenario console. |
| `ads_review/` | Review video, selected frames, and `review.json`. |
| `rgb_frames/` | Camera metadata and frame timestamps; raw individual RGB images are not included here. |
| `runtime_manifest.json` | Hashes of the runtime code captured for this case. |
| `runtime_code/src/` | First-party execution, recording, geometry, and condition modules. |
| `runtime_code/scripts/` | Headless execution/recording wrapper. |
| `runtime_code/scenario_runner/` | ScenarioRunner modules and project extensions used for this episode. |
| `runtime_code/PCLA/` | InterFuser integration/configuration and device-selection provenance. Agent weights are not bundled. |

Original JSON records retain historical filenames and paths. For example, a clip record may refer to `interaction.mp4` at the old case root; that file now lives in `preview/`. The [provenance path map](../archive/provenance/layout.json) resolves every original package path to its current location without changing recorded evidence.

## Collection directories

| Directory | Purpose |
| --- | --- |
| [scenarios/](../scenarios/README.md) | Ten case directories, a readable catalog, and `index.csv`. CSV artifact paths are relative to the repository root. |
| [docs/](README.md) | Current English setup, replay, and directory guides. |
| [preview/](../preview/README.md) | Collection gallery (`index.html`) and combined video (`showcase.mp4`). This is separate from each case's individual previews. |
| [archive/](../archive/README.md) | Selection history, a partial implementation snapshot, and provenance. Everyday browsing and replay use the first three directories. |

## Archived implementation

`archive/implementation_snapshot/` captures source files used while preparing the collection. It requires dependencies and missing modules from the full Crash2OpenX project.

| Entry | Contents |
| --- | --- |
| `tools/` | Expansion, timing/trigger logic, plotting, review, packaging, and validation tools. |
| `runner/src/` | Runner modules captured during package preparation. |
| `runner/runtime_overrides/` | NPC vehicle-control override. |
| `schemas/` | SceneSeed schema documentation. |
| `tests/` | Archived checks for approach spacing, junction timing/waiting, and generated routes. |
| `pyproject.toml`, `uv.lock` | Dependency metadata from the source project. |

The per-case `evidence/runtime_code/` identifies what that particular episode actually ran; versions can differ between cases. Use the full toolchain for [supported replay](usage.md).
