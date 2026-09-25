# Adjacent cut-in with a cyclist ahead

Case ID: `013_Zoox_February_19_2025`

Tests the ADS response when an adjacent vehicle cuts into its lane while a cyclist remains ahead of that vehicle.

## Recorded outcome

The ADS braked but made contact with the cutting-in vehicle.

## Scope and limitations

The cyclist remains ahead of the cutting-in vehicle. Speeds and spacing were adjusted experimentally; the exact impact locations in the source report were not reconstructed.

This is a crash-inspired ADS test variant with one recorded episode at the delivered parameter setting. Experimental onset, speed, and spacing may differ from the report. Read [manifest.json](manifest.json) for the source/derived parameters and [quality_review.json](quality_review.json) for the measured window and checks.

## Files and directories

| Entry | Purpose |
| --- | --- |
| [scenario.xosc](scenario.xosc) and [map.xodr](map.xodr) | Portable test and generated road; keep both files together. |
| [scene_seed.json](scene_seed.json) | Derived scene parameters used for this test. |
| [source/](source/) | Original [report](source/report.pdf), extracted text, original seeds, and generation metadata. |
| [evidence/](evidence/) | Recorded RGB video, traces, collision events, logs, runtime input, and code provenance. |
| [interaction.mp4](interaction.mp4) | Selected interaction clip. |
| [evidence/carla_rgb.mp4](evidence/carla_rgb.mp4) | Full recorded RGB episode. |
| [map.html](map.html) and [map_overview.png](map_overview.png) | Generated road views. |
| [map_and_response.png](map_and_response.png) | Road geometry and measured response visualization. |
| [contact_sheet.jpg](contact_sheet.jpg) and [clip_provenance.json](clip_provenance.json) | Sampled frames and excerpt provenance. |

The [root README](../../README.md#inside-evidence) explains the subdirectories under `evidence/`, including `ads_review/`, `rgb_frames/`, and `runtime_code/`.

## Use this case

View the clip and road images locally, or serve the collection with `python3 -m http.server 8000 --bind 127.0.0.1` from the repository root and open the gallery. For a new simulation, complete the [runtime setup](../../REPRODUCE.en.md#prepare-the-execution-environment), then run this from the full Crash2OpenX toolchain directory:

```sh
CASE_DIR="/absolute/path/to/crash2openx-scenarios/cases/013_Zoox_February_19_2025"
uv run python tools/carla_remote.py run \
  --xodr "$CASE_DIR/map.xodr" --xosc "$CASE_DIR/scenario.xosc" \
  --pcla-agent if_if --sut-actor hero --rgb-actor-role hero --max-seconds 600 \
  --scene-seed "$CASE_DIR/scene_seed.json" --road-seed "$CASE_DIR/source/road_seed.json"
```

For a configured local Linux GPU host, use `tools/carla_local.py` with the same arguments. Replays may produce different trajectories. The original Chinese case note is preserved in [README.md](README.md).
