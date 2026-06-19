# Telemetry Mounting Plan — ARYA Quadruped Prototype (60% Scale)
**Phase 5 — Mechanical/Telemetry Collaboration: Arya × Dhruv**

This plan places physical sensors on the mechanical structure already defined in `printable_parts_manifest.md` / `motor_mount_reference.md`, sized to satisfy Dhruv's Canonical Telemetry Contract v2 (4-element per-leg arrays: FL, FR, RL, RR — matching the Mission Control dashboard layout).

## Sensor Placement

| Sensor | Qty | Location | Mounting Method | Wires To |
|---|---|---|---|---|
| IMU | 1 | Body/chassis plate, centered as close to the body's CoM XY-projection as the plate allows | Bolted to a small printed boss on the chassis plate (added to Batch 2 body part) — rigid mount, no foam/damping, orientation must match the robot's body frame exactly | Electronics mount |
| Joint thermal sensor (per leg) | 4 | At the **hip** servo case of each leg (FL, FR, RL, RR) — hip carries the larger continuous load and is representative of leg thermal state | Small thermistor/NTC bonded or clipped to the DS3225 case, routed through the wire channel already specified in the hip bracket | Electronics mount |
| Motor current sense (per leg) | 4 | Inline with each leg's hip servo power lead | Current-sense resistor or hall-effect sensor on the driver board, not on the leg itself — no new mechanical mount needed beyond existing wire channel | Electronics mount |
| Joint angle feedback | 0 (baseline) or 8 (recommended) | Hip + knee pivot of each leg | **Baseline:** none — schema's `hip_angles`/`knee_angles` would mirror the *commanded* PWM angle, not a measured one. **Recommended:** AS5600 magnetic encoder at each pivot (₹150–250 each, ~₹1,200–2,000 for 8) bolted to the joint axis opposite the servo horn, reading a small magnet pressed into the link | Electronics mount |
| Battery voltage sense | 1 | At the battery mount, inline with main power feed | Voltage divider tap at the mount's power connector — no separate physical sensor body | Electronics mount |
| Foot contact sensor | 4 | Underside of each printed foot | FSR (force-sensitive resistor) or microswitch seated in a shallow pocket molded into the foot's flat base, under the rubber/TPU pad | Routed up through lower link wire channel to electronics mount |

## Important Call-Out: Joint Angle Feedback
Dhruv's schema lists `hip_angles` and `knee_angles` as **required** fields, not optional. A standard PWM servo like the DS3225 doesn't report measured position — it only accepts a commanded one. If no encoder is added, those telemetry fields will report what the robot was *told* to do, not what it's actually doing, which defeats the point of "observable from day one." Recommend adding the 8 AS5600 encoders to the procurement list before Test 5–7 (the tests where real angle deviation under load actually matters). If time/budget doesn't allow it before the single-leg gate, using commanded angle as an interim proxy is acceptable for Tests 1–4 only — flag it as a known gap, not a silent assumption.

## Wiring Convention
All sensor leads route to the **electronics mount** (Phase 2 part) as the single junction point. Hip brackets and upper/lower links each have a wire channel already specified in `printing_package.md` — no separate sensor wiring channel needs to be added to the CAD, but route sensor leads alongside the existing servo signal/power leads rather than as a second pass-through.

## Success Criteria
Every sensor required to populate Dhruv's Canonical Telemetry Contract v2 has a defined physical location and mounting method on the existing mechanical structure.
