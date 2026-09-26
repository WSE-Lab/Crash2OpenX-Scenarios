# Scenario catalog

Choose a scenario below. Every directory uses the same four folders: `simulation/`, `preview/`, `source/`, and `evidence/`. Full IDs preserve the original report identity.

| ID | Scenario | Recorded outcome |
| --- | --- | --- |
| [013](013_Zoox_February_19_2025/README.md) | Adjacent cut-in with a cyclist ahead | The ADS braked but made contact with the cutting-in vehicle. |
| [035](035_Zoox_January_26_2025/README.md) | ADS left turn with crossing traffic | The crossing vehicle contacted the ADS; the ADS also briefly departed its lane during the turn. |
| [038](038_Waymo_December_17_2024/README.md) | Partial encroachment beside an ADS-controlled truck | The truck braked. Minimum reviewed clearance was approximately 3.73 m, with no contact. |
| [055](055_Waymo_November_3_2024_%281%29/README.md) | Cross-traffic vehicle turning right into the ADS path | The NPC contacted the ADS after turning right. |
| [097](097_Zoox_May_30_2024/README.md) | Roadside vehicle merging into the ADS lane | The ADS braked but made contact with the merging vehicle. |
| [120](120_Zoox_February_22_2024_%281%29/README.md) | Large turning vehicle at an intersection | The turning vehicle contacted the ADS. |
| [135](135_Zoox_January_1_2024_%28A%29/README.md) | Three-vehicle intersection conflict | A crossing SUV contacted the ADS; the ADS departed its lane later in the episode. |
| [144](144_Waymo_October_17_2023/README.md) | Cyclist cut-in during an ADS turn | The ADS braked and departed its lane. Minimum reviewed clearance was approximately 1.84 m, with no contact. |
| [262](262_Zoox_February_11_2023/README.md) | Lead-vehicle slowdown and ADS following response | The ADS braked and exhibited stop-and-go motion. Minimum reviewed clearance was approximately 1.19 m, with no contact. |
| [293](293_Zoox_October_14_2022/README.md) | Oncoming left-turn onset conflict | Contact occurred early in the oncoming vehicle's turn; the ADS braked to a stop. |

Clearance and TTC metrics in [index.csv](index.csv) describe the reviewed interaction window. Contacts can occur later in the full episode. One recorded run per configuration does not establish a failure rate.

[Full execution logs](../docs/logs.md) · [Usage guide](../docs/usage.md) · [Full directory reference](../docs/structure.md) · [Video gallery](../preview/index.html)
