# Crash2OpenX Scenarios

Ten selected crash-inspired autonomous-driving-system (ADS) test scenarios generated with [Crash2OpenX](https://github.com/WSE-Lab/Crash2OpenX). Each case includes a portable OpenSCENARIO/OpenDRIVE pair, its source report and seeds, and recorded CARLA/InterFuser execution evidence.

This initial collection comes from `ads_showcase_10_20260919.zip`, selected from a 42-case inventory. Each case represents one recorded run at one experimental parameter setting. The collection supports scenario inspection and replay; it does not establish exact crash reconstruction or statistical failure rates.

## Quick start

```sh
git clone https://github.com/WSE-Lab/Crash2OpenX-Scenarios.git crash2openx-scenarios
cd crash2openx-scenarios
python3 -m http.server 8000 --bind 127.0.0.1
```

Open **http://localhost:8000/START_HERE.html** to browse the original gallery and play the videos. Viewing the collection needs only a browser and Python 3; CARLA and model weights are needed only for a new simulation. Repository access requires a GitHub account with permission to this private repository. GitHub displays the README but does not run the HTML gallery.

For an English overview, use the case table below. The original gallery and archived notes retain their original language. To rerun a case, follow [the English reproduction guide](REPRODUCE.en.md).

## Selected cases

Each link opens an English case guide inside the corresponding directory under `cases/`.

| Case directory | Test interaction | Recorded outcome |
| --- | --- | --- |
| [013_Zoox_February_19_2025](cases/013_Zoox_February_19_2025/README.en.md) | Adjacent vehicle cuts in with a cyclist ahead. | ADS brakes; contact with the cutting-in vehicle. |
| [035_Zoox_January_26_2025](cases/035_Zoox_January_26_2025/README.en.md) | ADS left turn conflicts with cross traffic. | Contact and brief ADS lane departure. |
| [038_Waymo_December_17_2024](cases/038_Waymo_December_17_2024/README.en.md) | Adjacent vehicle partially encroaches toward an ADS-controlled truck. | Braking; approximately 3.73 m minimum clearance, no contact. Only the interaction window was accepted; the full run timed out. |
| [055_Waymo_November_3_2024_(1)](cases/055_Waymo_November_3_2024_%281%29/README.en.md) | Cross-traffic vehicle turns right into the ADS path. | Contact after the NPC's right turn. |
| [097_Zoox_May_30_2024](cases/097_Zoox_May_30_2024/README.en.md) | Roadside vehicle merges into the ADS lane. | ADS brakes; contact with the merging vehicle. |
| [120_Zoox_February_22_2024_(1)](cases/120_Zoox_February_22_2024_%281%29/README.en.md) | Large turning vehicle crosses the ADS path at an intersection. | Contact with the turning vehicle. |
| [135_Zoox_January_1_2024_(A)](cases/135_Zoox_January_1_2024_%28A%29/README.en.md) | Three-vehicle intersection conflict with cross traffic and a stationary vehicle. | Contact with a crossing SUV; ADS lane departure later in the episode. |
| [144_Waymo_October_17_2023](cases/144_Waymo_October_17_2023/README.en.md) | Cyclist cuts in while the ADS turns. | Braking and lane departure; approximately 1.84 m minimum clearance, no contact. |
| [262_Zoox_February_11_2023](cases/262_Zoox_February_11_2023/README.en.md) | Lead SUV slows down in front of a following ADS vehicle. | ADS braking and stop-and-go motion; approximately 1.19 m minimum clearance, no contact. |
| [293_Zoox_October_14_2022](cases/293_Zoox_October_14_2022/README.en.md) | Oncoming vehicle starts a left turn across the ADS path. | Contact early in the turn; ADS brakes to a stop. |

Reported clearances describe the reviewed interaction window. Some clips include later contact beyond that window; consult the per-case quality review and collision events together.

## Repository layout

```text
crash2openx-scenarios/
├── README.md                      English entry point and directory guide
├── REPRODUCE.en.md                 Environment setup and replay commands
├── START_HERE.html                 Original browsable gallery
├── showcase.mp4                    Combined showcase video
├── case_index.csv                  Original case index, metrics, and artifact paths
├── selection.json                  Selected configurations and review records
├── inventory_42.json               Metadata for the original 42-case inventory
├── all_attempts_review.json        Screening records, including rejected attempts
├── MANIFEST.json                   Original package file hashes
├── IMPORT_PROVENANCE.json          Archive identity and import verification
├── REPRODUCE.md                    Original reproduction notes (Chinese)
├── report.md                       Original results summary (Chinese)
├── selection_notes.md              Original selection rationale
├── tests.log                       Archived test output from package preparation
├── cases/                         The 10 selected scenario directories
└── implementation_snapshot/        Archived generation/review implementation
```

`inventory_42.json` and the attempt records describe the selection process; only the ten case directories contain delivered scenarios. The archived test log records the original packaging run, not a new execution of the simulations.

### Inside each case directory

| File or directory | Contents and how to use it |
| --- | --- |
| `README.en.md` | English interaction description, observed outcome, limitations, and artifact links. |
| `README.md` | Original Chinese case note, preserved with the source package. |
| `scenario.xosc` | OpenSCENARIO 1.0 test entry point. Pass this file to the Crash2OpenX runner. Its map reference is the relative path `map.xodr`. |
| `map.xodr` | OpenDRIVE 1.5 road network used by this scenario. Keep it next to `scenario.xosc`. |
| `scene_seed.json` | Derived scene parameters for the delivered ADS test. |
| `manifest.json` | Source identifiers and hashes, original/derived scene parameters, calibration, and scope of the test. Compare `source_scene` and `derived_scene` here. |
| `quality_review.json` | Measured interactions, native-map checks, termination, contact evidence, and limitations. |
| `map.html`, `map_overview.png` | Interactive/static views of the generated road geometry. |
| `map_and_response.png` | Road and measured trajectory/response visualization. |
| `interaction.mp4`, `contact_sheet.jpg` | Selected interaction video and sampled frames for quick review. |
| `clip_provenance.json` | Clip timing and hashes linking the excerpt to the recorded videos. |
| `source/` | Original report PDF, extracted text, extraction metadata, original road/scene seeds, and road-generation metadata. Start with `report.pdf` or `source_text.txt` to inspect the source; use `road_seed.json` when replaying. |
| `evidence/` | Recorded simulation videos, traces, events, logs, runtime input, and execution provenance. See the breakdown below. |

### Inside `evidence/`

| File or directory | Contents and how to use it |
| --- | --- |
| `carla_rgb.mp4` | Full recorded RGB video for the episode. |
| `sim_trace_raw.jsonl`, `frame_states.jsonl` | Recorded actor motion and frame/state data for offline analysis. JSONL files contain one JSON object per line. |
| `events.jsonl` | Recorded events, including collision-sensor evidence. |
| `summary.json`, `behavior_check.json` | Episode summary and behavior checks. Read alongside `quality_review.json`. |
| `roadgraph_selfcheck.json` | Agreement checks between generated road geometry and CARLA's native road sampling. |
| `remote_run.json` | Execution metadata and hashes of the uploaded scenario/map. Historical machine paths are provenance, not paths to use on your machine. |
| `scenario.runtime.xosc` | Archived runtime input, which may contain server-specific absolute paths. Use the case-level `scenario.xosc` to launch a new run. |
| `demo.log`, `runner.log`, `run_scene_wrapper.log` | Logs for diagnosing the recorded run and its termination. |
| `ads_review/` | Review video, selected frames, and `review.json` used to inspect the ADS interaction. |
| `rgb_frames/` | Camera metadata and frame timestamps. Individual raw RGB frames are not included in this directory. |
| `runtime_manifest.json` | Hashes identifying the execution code captured for that case. |
| `runtime_code/src/` | First-party scenario execution, recording, geometry, and condition modules. |
| `runtime_code/scripts/` | Headless execution/recording wrapper. |
| `runtime_code/scenario_runner/` | ScenarioRunner modules used by that episode, including the project-specific extensions. |
| `runtime_code/PCLA/` | InterFuser integration/configuration and device-selection provenance. Model weights are not included. |

### Inside `implementation_snapshot/`

| Directory or file | Purpose |
| --- | --- |
| `tools/` | Archived scene expansion, timing/trigger logic, plotting, review, packaging, and validation tools. |
| `runner/src/` | Runner modules captured during preparation of the collection. |
| `runner/runtime_overrides/` | NPC vehicle-control override from that implementation. |
| `schemas/` | SceneSeed schema documentation. |
| `tests/` | Archived regression checks for spacing, junction timing, waiting, and generated routes. |
| `pyproject.toml`, `uv.lock` | Dependency metadata from the source project. |

This snapshot is a partial source archive. Use the full [Crash2OpenX repository](https://github.com/WSE-Lab/Crash2OpenX) and its supported runtime to run the scenarios. The per-case `evidence/runtime_code/` records what was actually used for that episode; versions can differ between cases.

## Integrity and interpretation

All 743 files from the original ZIP are preserved byte-for-byte. `MANIFEST.json` covers 742 original files, excluding itself; newly added English documentation and repository metadata are outside that original manifest. See [IMPORT_PROVENANCE.json](IMPORT_PROVENANCE.json) for the archive SHA-256 and import record, and [REPRODUCE.en.md](REPRODUCE.en.md#verify-the-original-files) for a hash check.

Scenario acceptance means the documented test interaction was usable. ADS collisions and lane departures remain observed outcomes. Signal compliance, exact impact locations, and complete accident chains were not accepted as reconstructed. Case 262 uses a lead-vehicle slowdown from 3.8 to 2.4 m/s rather than a full stop, and maps the ADS to the original report's following vehicle; case 038 maps the ADS to the truck and has a full-episode timeout. Each case guide records its specific limits.
