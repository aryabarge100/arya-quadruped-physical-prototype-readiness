# Bill of Materials v1 — ARYA Quadruped Prototype (60% Scale)
**Phase 7 — Mechanical Lead: Arya**

Consolidates `procurement_list.md` (Phase 3) plus the telemetry additions from Phase 5 into one master BOM.

## Structural (Printed)
| Item | Qty | Material | Source |
|---|---|---|---|
| Hip bracket | 4 | PETG | Printed in-house — see `printable_parts_manifest.md` |
| Upper link | 4 | PETG | Printed in-house |
| Lower link | 4 | PETG | Printed in-house |
| Foot | 4 | PETG + TPU pad | Printed in-house |
| Body/chassis plate | 1 | PETG | Printed in-house |
| Battery mount | 1 | PETG | Printed in-house |
| Electronics mount | 1 | PETG | Printed in-house |
| PETG filament | 1–2 kg | — | Local 3D-print store / Amazon India |

## Actuators & Mechanical Hardware
| Item | Qty | Est. Unit (₹) | Est. Total (₹) |
|---|---|---|---|
| DS3225 servo | 8 | 1,200–1,800 | 9,600–14,400 |
| 5 mm ID flanged ball bearing | 8 | 40–60 | 320–480 |
| M3 screws + nuts (assorted) | 1 set | 150–250 | 150–250 |
| M3 heat-set threaded inserts | 20 | 8–12 | 160–240 |
| Servo extension leads | 8 | 15–20 | 120–160 |
| Rubber/TPU foot pads | 4 | 25 | 100 |

## Telemetry & Sensing (Phase 5 additions)
| Item | Qty | Est. Unit (₹) | Est. Total (₹) |
|---|---|---|---|
| AS5600 magnetic encoder (recommended, joint angle feedback) | 8 | 150–250 | 1,200–2,000 |
| Thermistor (hip joint temp) | 4 | 40–80 | 160–320 |
| FSR foot contact sensor | 4 | 80–150 | 320–600 |
| IMU (e.g. MPU6050/MPU9250 class) | 1 | 150–400 | 150–400 |

## Power & Electronics
| Item | Qty | Est. Unit (₹) | Est. Total (₹) |
|---|---|---|---|
| 2S LiPo battery | 1 | 600–900 | 600–900 |
| Driver/microcontroller stack (e.g. ESP32 + PCA9685, placeholder pending Dhruv/Suraj's stack decision) | 1 set | 650–1,000 | 650–1,000 |

## Total Estimate
**≈ ₹14,300–21,800** (mid-estimate ≈ ₹18,000), within the originally assumed ₹15,000–30,000 budget bracket. This is higher than the Phase 3 actuator-only estimate because it now includes the telemetry sensors added in Phase 5.

## Open Items
- Driver/microcontroller cost is a placeholder until Dhruv and Suraj confirm the electronics stack.
- AS5600 encoders are recommended, not yet confirmed — see `telemetry_mounting_plan.md` for the tradeoff if skipped.

## Success Criteria
Every part needed to build and instrument the prototype is on one list, with no item left as "figure it out later" except the two explicitly flagged open items above.
