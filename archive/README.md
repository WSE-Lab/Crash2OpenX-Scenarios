# Archive and provenance

This directory retains the collection's selection history and original source snapshots. For normal use, start with the [scenario catalog](../scenarios/README.md) or [replay guide](../docs/usage.md).

## Selection history

`selection/` contains the original package-level records:

| File | Contents |
| --- | --- |
| `inventory_42.json` | Metadata for the 42-case inventory from which the delivered ten cases were selected. |
| `selection.json`, `all_attempts_review.json` | Selected configurations, review records, and screened attempts. |
| `case_index.csv` | Original case index with historical paths and Chinese descriptions. Use [scenarios/index.csv](../scenarios/index.csv) for current paths and English descriptions. |
| `selection_notes.md`, `report.md` | Original selection rationale and results summary. |
| `REPRODUCE.md` | Original reproduction notes; use [docs/usage.md](../docs/usage.md) for current paths. |
| `tests.log` | Archived test output from preparation of the original package. |
| `START_HERE.html.txt` | Original gallery source, preserved as text. The active gallery is [preview/index.html](../preview/index.html). |

Only ten scenario directories are delivered. Inventory entries and rejected attempts are metadata, not additional runnable scenarios. Historical paths are retained in these records to preserve the original evidence.

## Implementation snapshot

`implementation_snapshot/` contains partial first-party tools, runner modules, schemas, tests, and dependency metadata. See the [subdirectory reference](../docs/structure.md#archived-implementation). Use the full [Crash2OpenX toolchain](https://github.com/WSE-Lab/Crash2OpenX) to execute a scenario.

## Provenance

| File | Contents |
| --- | --- |
| [provenance/original_manifest.json](provenance/original_manifest.json) | Untouched original manifest: 742 file hashes using original ZIP-relative paths. The manifest itself was the 743rd file. |
| [provenance/import_20260925.json](provenance/import_20260925.json) | Original import record and source ZIP SHA-256. Its layout description refers to the first import. |
| [provenance/layout.json](provenance/layout.json) | Mapping of all 743 original files to their current repository paths, with their original SHA-256 hashes. |

The directory reorganization preserves all original file contents. Current English documentation, the current CSV index, and the gallery with updated links are maintained separately. The original Chinese case notes are preserved in each scenario's `source/README.zh-CN.md`.

Use the [verification command](../docs/usage.md#verify-the-original-files) to check the original files at their current paths.
