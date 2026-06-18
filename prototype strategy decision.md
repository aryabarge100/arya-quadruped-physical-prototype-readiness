# Prototype Strategy Decision — ARYA Quadruped
Phase 1 — Mechanical Lead: Arya

## Assumptions Used
No printer access, budget, or deadline was confirmed before this decision was drafted. The following defaults were assumed — flag any that are wrong and the cost/build estimates below get revised:
- Printer access: personal or college-lab FDM printer (PETG-capable)
- Budget: ₹15,000–30,000 for prototype actuators + hardware (excludes printer/filament you may already own)
- Timeline: 2–3 weeks to first tested leg module

## Baseline Data (from SolidWorks mass properties + review packets)
| Parameter | Value |
|---|---|
| Total mass (full-scale CAD) | 15.261 kg |
| Total weight | 149.7 N |
| Body (L×W×H) | 250 × 150 × 165 mm |
| CoM | X=272.60, Y=24.45, Z=58.57 mm |
| Support polygon margin | 50.55 mm (67.4% stability margin, SAFE) |
| Static leg load | 37.4 N/leg |
| Crawl-gait support load | 49.9 N/leg |
| Worst-case loaded leg | 74.85 N (unbalanced terrain) |
| Hip+knee torque, current full-scale geometry | up to ~3 Nm/joint (50 mm lever assumption); higher (~6–7 Nm) at the revised 80+100 mm link reach — this is why hobby servos were already ruled out for the final robot and GoBilda 5202 + 3:1 belt was selected |

## Option Evaluation

**Option A — 100% scale, current geometry, current mass**
Reuses all existing CAD and stability analysis directly. But it requires the already-selected GoBilda 5202 + belt actuators (8 units, ₹5,000–8,000 each → ₹40,000–64,000), large-format prints of a 250×150 mm aluminum-spec body in plastic, and a full actuator/electronics stack before anything can be tested. Too much capital and time committed before a single physical fact is confirmed.

**Option B — 50–60% scale, reduced mass, reduced actuator demand**
At 60% linear scale: body ≈150×90×99 mm, link reach ≈108 mm (48+60 mm), estimated build mass ≈2.5–3.5 kg (structure converts from 6061 aluminum to PETG, which alone cuts structural mass by roughly half, combined with the volume reduction). Per-leg static load drops to ≈7.4 N, and worst-case joint torque drops to ≈0.8–1.2 Nm (≈8–13 kg·cm) — within range of mid-tier hobby servos. Printable on any standard FDM bed. Still a complete 4-legged robot, so it can run the *entire* Phase 6 test sequence (static stand, weight support, crawl), not just a subset.

**Option C — Single-leg validation rig (one hip, one knee)**
Fastest and cheapest first part on a desk, and structurally it's the right way to de-risk link strength and actuator torque before committing to 4 legs. But it cannot satisfy Phase 6 Tests 5–7 (static stand, weight support test, slow crawl test), which need a complete standing robot. Used alone, it stalls the sprint at "one leg works" with no path to a walking prototype.

## Recommended Path
**Option B (60% scale, full 4-leg quadruped) — selected.**

Sequencing borrows Option C's logic instead of treating it as a separate path: print and load-test **one** leg module (hip bracket, upper link, lower link, foot) first, validate it against Phase 6 Tests 1–4, and only then print the remaining three legs. This gives you Option C's fast/cheap/low-risk first checkpoint *and* a real walking prototype at the end, with one scale decision and no parallel indecision.

## Engineering Rationale
- Option A's actuator cost alone (₹40k–64k) exceeds the stated prototype budget bracket before any printing or testing begins — not viable as a *first* prototype.
- Option B's reduced lever arms and mass bring joint torque down from the ~6–7 Nm regime (which forced the GoBilda decision for the final robot) into the 0.8–1.2 Nm regime, where DS3225-class servos have real margin (see `prototype_actuator_package.md`).
- Option C alone never produces a standing or walking robot, so two of the seven required physical tests (Test 6, Test 7) can never be closed.
- The single-leg-first build order inside Option B captures Option C's risk-reduction value without sacrificing the end goal.

## Cost Estimate
| Bucket | Estimate |
|---|---|
| Actuators (8× DS3225-class servo) | ₹9,600–14,400 |
| Bearings, fasteners, wiring | ₹1,500–2,000 |
| Filament (PETG, ~1.5 kg total) | ₹1,400–1,800 |
| Battery + misc electronics mounts | ₹600–900 |
| **Total** | **≈ ₹13,000–19,000** (within assumed budget) |

## Build Estimate
| Stage | Duration |
|---|---|
| Finalize 60% scale CAD + export | 2–3 days |
| Print + assemble single leg module | 2–3 days |
| Run Tests 1–4 on single leg | 1–2 days |
| Print + assemble remaining 3 legs + body | 4–5 days |
| Run Tests 5–7 (stand, weight, crawl) | 2–3 days |
| **Total** | **≈ 2–2.5 weeks** |

## Risk Estimate
| Risk | Level | Mitigation |
|---|---|---|
| Servo torque margin insufficient under dynamic load | Medium | DS3225 chosen with ~1.5–2× margin over static calc; see Phase 3 |
| Printed joint wear (spline-only mounting) | Medium | Add support bearing at knee — see `motor_mount_reference.md` |
| Mass estimate inaccurate until real CAD export | Medium | Re-run SolidWorks mass properties at 60% scale before finalizing BOM |
| Schedule slip | Low | Single-leg gate catches structural/actuator problems before 4× part cost is committed |

## Success Criteria — Confirmed
One path selected: **Option B, 60% scale, single-leg-first build order.** No parallel paths remain open.




