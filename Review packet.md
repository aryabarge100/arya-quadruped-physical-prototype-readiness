# REVIEW PACKET — ARYA Quadruped Prototype Readiness Sprint
**Mechanical Lead: Arya (Roll No. ME1102) | Phases 1–3, 5–7**

## Objective
Converge on a single buildable, testable prototype rather than continuing to refine a full-scale design that can't be printed, bought, or tested yet.

## Decision
**Option B — 60% linear scale, full 4-leg quadruped, single-leg-first build order.** Full reasoning in `prototype_strategy_decision.md`.

Full-scale Option A required the already-decided GoBilda 5202 + belt actuators (8× at ₹4,500–7,500 each — ₹40,000+ before anything is printed) and was ruled out as a *first* prototype on cost alone. Option C (leg rig only) was folded into the build *order* of Option B rather than treated as a separate path, since it can't satisfy the full stand/weight/crawl test sequence on its own.

## Baseline Data (from SolidWorks export + review packets)
| Parameter | Full-scale | 60%-scale prototype (estimated) |
|---|---|---|
| Mass | 15.261 kg | ≈2.5–3.5 kg |
| Body (L×W×H) | 250×150×165 mm | ≈150×90×99 mm |
| Leg reach | 80+100 mm | ≈48+60 mm |
| Static leg load | 37.4 N | ≈7.4 N |
| Worst-case leg load | 74.85 N | ≈14.8 N |
| Stability margin | 67.4% (scale-invariant) | 67.4% |
| Tipping threshold | 40.8° (scale-invariant) | 40.8° |

## Actuators (Phase 3)
**DS3225** (≈25 kg·cm) across all 8 joints — clears the rescaled torque target (≈16.3 kg·cm worst-case with 1.5× safety factor) at low cost and full India availability. GoBilda 5202+belt remains correct for the final full-scale robot, not this prototype.

## Telemetry (Phase 5, in collaboration with Dhruv)
Sensors mapped against Dhruv's Canonical Telemetry Contract v2: IMU (body-centered), per-leg hip thermistor and current-sense (driving `thermal_state`/`joint_torque`), foot contact FSRs, and recommended AS5600 encoders for genuine `hip_angles`/`knee_angles` feedback (without them, those fields would only echo commanded position). Full mapping in `observability_map_v2.md`.

**Flagged to Dhruv:** the 350-frame reliability report shows only 14.9% compliance against the 4 ms loop-latency target — the telemetry pipeline shouldn't be treated as the primary safety net during live load testing (Tests 5–7) until that's resolved.

## Test Plan (Phase 6)
Seven tests, gated in two groups. Tests 1–4 (link strength, hip bracket load, single-leg assembly, actuator motion) must pass before Batch 2 is printed. Tests 5–7 (static stand, weight support, slow crawl) validate the complete robot. Numeric pass/fail lines in `acceptance_criteria.md`; failures logged via `failure_log_template.md`.

## Build Kit (Phase 7)
Full BOM (`bill_of_materials_v1.md`, `procurement_sheet.csv`), step-by-step `assembly_sequence_v1.md`, and `builder_quickstart.md` so any team member — not just Arya — can execute the build.

**Total estimated cost:** ≈₹14,300–21,800, within the assumed ₹15,000–30,000 budget.

## Open Items (Not Yet Resolved)
1. Manya's leg workspace report (Phase 4) — test ROM values are a placeholder until this lands.
2. Electronics/driver stack cost — placeholder pending Dhruv/Suraj.
3. AS5600 encoder addition — recommended, not yet committed; affects whether Test 4's angle-deviation check is meaningful.
4. Dhruv's telemetry loop latency — 14.9% deadline compliance needs resolution before Tests 5–7 are run with the dashboard as the live safety monitor.

## Closing
A single tested leg module is the next concrete checkpoint — not another report. Everything above points at one part on a desk, printed, wired, and load-tested before the remaining three legs are committed to.
