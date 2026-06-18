# Printing Package — ARYA Quadruped Prototype (60% Scale)
**Phase 2 — Mechanical Lead: Arya**

## Material Decision
**PETG**, not PLA, for every load-bearing part (hip bracket, upper link, lower link, foot). PLA is brittle under the repeated bending/impact loads in the crawl and weight-support tests, and softens at temperatures a servo body or motor casing can realistically reach during a sustained test. PLA is acceptable only for the electronics mount, which carries no mechanical load.

## Slicer Settings
| Setting | Load-bearing parts (hip, links, foot) | Body / mounts |
|---|---|---|
| Layer height | 0.16–0.2 mm | 0.2 mm |
| Wall count | 4 | 3 |
| Infill | 35–40% (gyroid) | 15–20% (grid) |
| Infill (foot only) | 60% — small part, full strength worth the time cost | — |
| Top/bottom layers | 5 | 4 |
| Print speed | 40–50 mm/s | 50–60 mm/s |
| Bed temp | 80–85°C | 80–85°C |
| Nozzle temp | 235–245°C | 235–245°C |
| Supports | None planned for Batch 1; check hip bracket servo-pocket overhang once exported and add tree supports only there if needed | None |

## Print Batching
1. **Batch 1 — single leg module:** hip bracket, upper link, lower link, foot (1 each). Print together on one plate; combined plate time ≈1.8–2.3 hr per the parts manifest.
2. **Gate:** run Phase 6 Tests 1–4 on this module before touching Batch 2.
3. **Batch 2 — remaining structure:** 3× each leg part, plus body plate, battery mount, electronics mount.

## Assembly Hardware (not printed)
- M3×8 screws and nuts — hip bracket-to-body, link pivots
- 5 mm ID flanged bearings — knee joint (see `motor_mount_reference.md`)
- Heat-set threaded inserts (M3) recommended for any bracket reused across multiple print/test cycles, to avoid stripped plastic threads

## File Naming & Packaging
Follow the GitHub repo convention already in use (`aryabarge100/Quadruped-productization-layer-and-stability-`):
`ARYA_<part>_<scale>_v<version>.stl` — e.g. `ARYA_hipbracket_60pct_v1.stl`. Keep Batch 1 and Batch 2 STLs in separate folders so the single-leg gate is visually obvious to anyone opening the repo.

## Success Criteria
A builder can load these settings into the slicer and start printing without needing to make a single material or setting decision themselves.
