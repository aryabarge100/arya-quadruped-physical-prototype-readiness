# Failure Log Template — ARYA Quadruped Prototype
**Phase 6 — Mechanical Lead: Arya**

Copy this block for every failure observed during Tests 1–7. One entry per failure event, even if multiple occur in the same test run.

---

### Entry Template

**Test ID:** (e.g. Test 6 — Weight Support)
**Date/Time:**
**Tester:**

**Observed Failure:**
(plain description — what happened, what you saw/heard)

**Sensor Readings at Failure:**
| Field | Value |
|---|---|
| `health_status` | |
| `support_polygon_state` / stability margin | |
| Per-leg load (N) — FL / FR / RL / RR | |
| Joint thermistor (°C) — FL / FR / RL / RR | |
| `driver_status` / `bus_health` | |
| Slip risk index | |
| Body tilt angle | |

**Threshold Crossed:**
(reference the specific line from `acceptance_criteria.md` that was violated)

**Root Cause Hypothesis:**
(your best mechanical/electrical guess — confirm or revise after inspection)

**Corrective Action Taken:**

**Re-test Result:**
(Pass / Fail / Not yet re-tested)

---

## Success Criteria
Every failure during the test sequence has a logged entry with sensor evidence, not just a verbal "it didn't work" — this is what makes the next design iteration evidence-based instead of guesswork.
