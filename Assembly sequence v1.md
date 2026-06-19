# Assembly Sequence v1 — ARYA Quadruped Prototype (60% Scale)
**Phase 7 — Mechanical Lead: Arya**

Follows the single-leg-first build order locked in `prototype_strategy_decision.md`. Do not skip the Step 4 gate.

## Step 1 — Print Batch 1
Print hip bracket, upper link, lower link, foot (1 each) per `printing_package.md`. Run every part through `stl_export_checklist.md` before slicing.

## Step 2 — Assemble Single Leg
Mount DS3225 (hip) into the hip bracket per `motor_mount_reference.md`. Attach upper link to hip horn. Mount knee bearing + DS3225 (knee) at the upper-lower link joint. Attach foot to lower link.

## Step 3 — Wire Single Leg
Install hip thermistor, hip current-sense tap, foot contact sensor (FSR), and AS5600 encoders if using them, per `telemetry_mounting_plan.md`. Route all leads to a temporary test setup (full electronics mount integration happens in Step 7).

## Step 4 — GATE: Run Tests 1–4
Execute `prototype_test_plan.md` Tests 1–4 in order. Log any failure in `failure_log_template.md`. **Do not proceed to Step 5 until all four tests pass per `acceptance_criteria.md`.**

## Step 5 — Print Batch 2
Print the remaining 3× of each leg part, plus the body/chassis plate, battery mount, and electronics mount.

## Step 6 — Assemble Remaining Legs
Repeat Step 2 for the other three legs (FR, RL, RR), identically to the validated FL leg.

## Step 7 — Mount Body & Central Electronics
Bolt the body/chassis plate to all 4 hip brackets. Mount the battery mount and electronics mount to the body plate. Install the IMU on its boss, centered near the body's CoM projection. Install the battery and driver/microcontroller stack.

## Step 8 — Full Wiring Integration
Route all leg sensor leads (thermistor, current-sense, foot contact, encoders) and the IMU to the electronics mount, following the wiring convention in `telemetry_mounting_plan.md`. Connect battery voltage sense at the battery mount.

## Step 9 — Power-On Check
Before any commanded motion: power on, confirm every field in `observability_map_v2.md` is reporting a live value through Dhruv's telemetry pipeline. Do not proceed to Step 10 with any sensor silent or reporting a stale value.

## Step 10 — GATE: Run Tests 5–7
Execute `prototype_test_plan.md` Tests 5–7 (static stand, weight support, slow crawl). Log every result in `failure_log_template.md` against `acceptance_criteria.md`.

## Step 11 — Sign-Off
Compile results into `/review_packets/REVIEW_PACKET.md`.

## Success Criteria
A builder can follow Steps 1–11 in order without needing to consult anyone — every step references the exact document that has the detail they need.
