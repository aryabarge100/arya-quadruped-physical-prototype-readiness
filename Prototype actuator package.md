# Prototype Actuator Package — ARYA Quadruped (60% Scale)
**Phase 3 — Mechanical Lead: Arya**

This is the prototype-only actuator decision. It is allowed to differ from the final-robot recommendation (GoBilda 5202 + 3:1 belt reduction), which was sized for
the full-scale 80+100 mm link geometry at 15.26 kg and remains correct for that build.

## Required Torque at 60% Scale
| Condition | Per-leg force | Lever arm | Torque | kg·cm equivalent |
|---|---|---|---|---|
| Static stand | ≈7.4 N | 0.108 m | ≈0.80 Nm | ≈8.1 kg·cm |
| Crawl gait (3-leg support) | ≈9.9 N | 0.108 m | ≈1.07 Nm | ≈10.9 kg·cm |
| Worst-case unbalanced terrain | ≈14.8 N | 0.108 m | ≈1.60 Nm | ≈16.3 kg·cm |

Target with safety factor (1.5×): **≈24 kg·cm** sustained capability per joint.

## Comparison
| Actuator | Rated torque | Cost (India) | Availability | Mounting impact | Verdict |
|---|---|---|---|---|---|
| MG996R | ~10–11 kg·cm stall | ₹250–400 | Very high (every robotics seller) | Standard servo tab mount, 25T spline horn | Thin margin against worst-case torque — usable for Tests 1–4 (motion-only, no body weight) but not safe for Tests 5–7 |
| DS3225 | ~25 kg·cm stall, metal gear, waterproof | ₹1,200–1,800 | High (Robu.in, Robokits, Amazon India) | Same tab-mount footprint as MG996R, larger case (~40×20×40.5 mm) | Clears the 24 kg·cm target with margin — recommended for all 7 tests |
| GoBilda 5202 + 3:1 belt | Far exceeds requirement at this scale | ₹4,500–7,500 per unit | Limited India stock, often import lead time | Requires belt/pulley mounting, not a drop-in servo tab | Overkill and overpriced for the 60% prototype — reserve for the final full-scale robot |
| DS3218MG (India-stocked alternative) | ~20 kg·cm | ₹900–1,300 | High | Same footprint as DS3225 | Acceptable fallback if DS3225 stock is an issue; slightly less margin |

## Recommendation
**DS3225 for all 8 joints (4 hips + 4 knees).** It's the only option in this list that clears the safety-factored torque target while staying in a low-cost, India-stocked, drop-in servo form factor. MG996R is acceptable only as a throwaway set for early no-load kinematic checks if you want to save the DS3225 units for the real load tests — it should not be used for Tests 5–7.

## Success Criteria
Prototype actuator selected (DS3225), available through normal India suppliers, procurement can start immediately — see `procurement_list.md`.
