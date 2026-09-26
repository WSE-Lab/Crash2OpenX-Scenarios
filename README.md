# Crash2OpenX Scenarios

Ten selected crash-inspired ADS tests, with executable OpenSCENARIO/OpenDRIVE files, source reports, and recorded CARLA/InterFuser evidence.

**Start here:** [Choose a scenario](scenarios/README.md) · [Full execution logs](docs/logs.md) · [View videos](preview/README.md) · [Run a scenario](docs/usage.md)

## Where is the full OpenSCENARIO log?

Open **`scenarios/<case_id>/evidence/logs/openscenario_full.log`** for the full recorded execution console. For case 013, go directly to the **[full log](scenarios/013_Zoox_February_19_2025/evidence/logs/openscenario_full.log)** or its [evidence file guide](scenarios/013_Zoox_February_19_2025/evidence/README.md).

The per-tick actor trace is `evidence/sim_trace_raw.jsonl`; recorded storyboard transitions and sensor events are in `evidence/events.jsonl`. `runner.log` is only the outer-launcher summary. See [all ten full-log links and their recorded termination](docs/logs.md).

## Where things live

```text
crash2openx-scenarios/
├── README.md
├── scenarios/       10 scenarios, each with the same structure
│   └── <case_id>/
│       ├── README.md       Description, outcome, limits, and replay command
│       ├── simulation/     Run: scenario.xosc, map.xodr, scene_seed.json
│       ├── preview/        View: video clips, maps, response plots
│       ├── source/         Trace: original report, text, and seeds
│       └── evidence/       Inspect: full recordings, traces, reviews, runtime code
│           ├── README.md   Which log to read and what this run captured
│           └── logs/       openscenario_full.log and auxiliary diagnostics
├── docs/            Setup, replay instructions, and detailed directory guide
├── preview/         Collection-wide video gallery and combined video
└── archive/         Selection history, implementation snapshot, and provenance
```

| What you want to do | Open |
| --- | --- |
| Pick one of the 10 scenarios | [Scenario catalog](scenarios/README.md) |
| Load a scenario into the supported runner | `scenarios/<case_id>/simulation/scenario.xosc` and its sibling `map.xodr` |
| Watch an interaction | `scenarios/<case_id>/preview/interaction.mp4` |
| Read the original report | `scenarios/<case_id>/source/report.pdf` |
| Read the full recorded OpenSCENARIO console log | [Full-log index](docs/logs.md): `scenarios/<case_id>/evidence/logs/openscenario_full.log` |
| Check an observed outcome | `scenarios/<case_id>/evidence/quality_review.json` and `events.jsonl` |
| Set up CARLA and replay | [Usage guide](docs/usage.md) |
| Understand every subdirectory | [Directory reference](docs/structure.md) |
| Audit the original package | [Archive guide](archive/README.md) |

## Preview without installing CARLA

From this repository's root:

```sh
python3 -m http.server 8000 --bind 127.0.0.1
```

Open **http://localhost:8000/preview/**. Stop the server with Ctrl+C. The gallery retains the original Chinese descriptions; the README and scenario guides are in English. GitHub displays Markdown but does not execute the HTML gallery.

## Replay requirements

Use [Crash2OpenX](https://github.com/WSE-Lab/Crash2OpenX) with CARLA **0.9.16**, the project's patched ScenarioRunner, PCLA's InterFuser agent (`if_if`), and its pretrained weights. Execution requires a configured Linux NVIDIA GPU host; viewing the archived results needs only a browser. Follow the [replay guide](docs/usage.md) for local and remote commands.

## What the results mean

The collection contains one recorded episode per selected configuration, drawn from a 42-case inventory. Parameters such as speed, spacing, and interaction timing were adjusted to create ADS tests. These are not claims of exact accident reconstruction or statistical failure rates.

Each scenario README records its limits. In particular, case **038** has an accepted interaction window but a full-episode timeout; case **262** uses a moving lead-vehicle slowdown, not a complete stop. Contacts and lane departures are preserved as observed outcomes.

All **743 original package files** retain their original bytes at the new paths. [Provenance records](archive/README.md#provenance) and the [verification command](docs/usage.md#verify-the-original-files) support integrity checks.
