# Crash2OpenX Scenarios

Ten crash-inspired ADS tests with the inputs needed to rerun them, an original report, and a compact record of each observed result. Runtime code is supplied by the separate [Crash2OpenX project](https://github.com/WSE-Lab/Crash2OpenX).

**[Replay instructions](REPRODUCE.md)** · **[Case 013 full execution log](scenarios/013_Zoox_February_19_2025/openscenario_full.log)**

## Layout

```text
crash2openx-scenarios/
├── README.md
├── REPRODUCE.md          Fixed runtime version and replay commands
├── manifest.json         Input/result checksums and runtime reference
└── scenarios/
    └── <case_id>/
        ├── README.md                Description, result, and replay command
        ├── scenario.xosc            Runnable OpenSCENARIO
        ├── map.xodr                 Matching OpenDRIVE map
        ├── scene_seed.json          Scene parameters
        ├── road_seed.json           Road parameters
        ├── report.pdf               Original crash report
        ├── preview.mp4              Full recorded video
        ├── openscenario_full.log    Full recorded execution console
        └── summary.json             Result and termination
```

Each scenario directory contains **nine files**. Open its README to see the outcome, limitations, and exact replay command. The full console log always has the same name: **`openscenario_full.log`**.

## Scenarios

| ID | Scenario | Files | Full execution log |
| --- | --- | --- | --- |
| 013 | Adjacent cut-in with a cyclist ahead | [Open](scenarios/013_Zoox_February_19_2025/README.md) | [Log](scenarios/013_Zoox_February_19_2025/openscenario_full.log) |
| 035 | ADS left turn with crossing traffic | [Open](scenarios/035_Zoox_January_26_2025/README.md) | [Log](scenarios/035_Zoox_January_26_2025/openscenario_full.log) |
| 038 | Partial encroachment beside an ADS-controlled truck | [Open](scenarios/038_Waymo_December_17_2024/README.md) | [Log](scenarios/038_Waymo_December_17_2024/openscenario_full.log) |
| 055 | Cross-traffic vehicle turning right into the ADS path | [Open](scenarios/055_Waymo_November_3_2024_%281%29/README.md) | [Log](scenarios/055_Waymo_November_3_2024_%281%29/openscenario_full.log) |
| 097 | Roadside vehicle merging into the ADS lane | [Open](scenarios/097_Zoox_May_30_2024/README.md) | [Log](scenarios/097_Zoox_May_30_2024/openscenario_full.log) |
| 120 | Large turning vehicle at an intersection | [Open](scenarios/120_Zoox_February_22_2024_%281%29/README.md) | [Log](scenarios/120_Zoox_February_22_2024_%281%29/openscenario_full.log) |
| 135 | Three-vehicle intersection conflict | [Open](scenarios/135_Zoox_January_1_2024_%28A%29/README.md) | [Log](scenarios/135_Zoox_January_1_2024_%28A%29/openscenario_full.log) |
| 144 | Cyclist cut-in during an ADS turn | [Open](scenarios/144_Waymo_October_17_2023/README.md) | [Log](scenarios/144_Waymo_October_17_2023/openscenario_full.log) |
| 262 | Lead-vehicle slowdown and ADS following response | [Open](scenarios/262_Zoox_February_11_2023/README.md) | [Log](scenarios/262_Zoox_February_11_2023/openscenario_full.log) |
| 293 | Oncoming left-turn onset conflict | [Open](scenarios/293_Zoox_October_14_2022/README.md) | [Log](scenarios/293_Zoox_October_14_2022/openscenario_full.log) |

## Use the collection

Clone the current version, then open any case's video, report, or log:

```sh
git clone --depth 1 https://github.com/WSE-Lab/Crash2OpenX-Scenarios.git crash2openx-scenarios
```

To rerun a case, follow [REPRODUCE.md](REPRODUCE.md). It pins the external toolchain revision and requires CARLA **0.9.16**, the project's patched ScenarioRunner, and InterFuser (`if_if`) with its weights. Execution uses a configured Linux NVIDIA GPU host. Viewing the supplied results needs no simulator.

Each supplied result is one recorded run of an experimental test variant. Full logs cover the actual recorded attempt, including collision exits and timeouts. Case **038** ended on timeout; case **262** uses a lead-vehicle slowdown rather than a complete stop. Refer to each case README for its specific limits. New runs can produce different trajectories; these records do not establish exact crash reconstruction or failure rates.
