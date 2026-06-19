# Acceptance Criteria — ARYA Quadruped Prototype (60% Scale)
**Phase 6 — Mechanical Lead: Arya**

Consolidated pass/fail thresholds referenced by `prototype_test_plan.md`, cross-referenced to Dhruv's schema states from `observability_map_v2.md` where applicable.

| Metric | Safe | Near-Critical | Critical | Schema State (if applicable) |
|---|---|---|---|---|
| Per-leg static load | <10 N | 10–15 N | >15 N | `driver_status`: OPERATIONAL → CURRENT_LIMITED → THERMAL_FAULT risk |
| Stability margin | >50% | 25–50% | <25% | `support_polygon_state`: DYNAMIC_TRI → UNSTABLE_DIAG → COLLAPSED |
| Body tilt angle | <15° | 15–25° | approaching 40.8° | `health_status`: NOMINAL → UNSTABLE → EMERGENCY_STOP |
| Slip risk index | <0.5 | 0.5–1.0 | >1.0 | `traction_state`: OPTIMAL → SLIPPING → TOTAL_LOSS |
| Joint thermal (DS3225) | <45°C | 45–55°C | >55°C | `thermal_state`, `driver_status`: THERMAL_FAULT |
| Commanded-vs-measured angle deviation (if encoders installed) | <3° | 3–6° | >6° | none defined — mechanical-only check |
| Link/bracket permanent deflection under test load | <1 mm | 1–2 mm | >2 mm | none defined — mechanical-only check |

## Per-Test Pass Line
| Test | Pass Condition |
|---|---|
| Test 1 — Link strength | Holds 30 N, <1 mm permanent deflection, no crack |
| Test 2 — Hip bracket load | Holds 3.2 Nm equivalent, no crack, no insert pull-through |
| Test 3 — Single leg assembly | Smooth motion through placeholder ROM, no binding |
| Test 4 — Actuator motion | No skip/stall, current under stall limit, <3° deviation if encoders present |
| Test 5 — Static stand | Stability margin >50%, all legs <10 N, no current-limit trigger |
| Test 6 — Weight support | Documents the real payload limit where a leg first crosses 10 N; hard stop at 15 N |
| Test 7 — Slow crawl | Stability margin stays >25% throughout, slip index <1.0, all joints <45°C |

## Success Criteria
No test result requires a judgment call — every pass/fail line maps to a number already defined in this document or in `prototype_fault_detection_plan.md`.
