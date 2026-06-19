# Builder Quickstart — ARYA Quadruped Prototype (60% Scale)
**Phase 7 — Mechanical Lead: Arya**

If you're picking this up cold, start here.

## What This Is
A 60%-scale, 4-leg printable/buildable version of the ARYA quadruped, built single-leg-first to de-risk actuator and structural choices before committing to a full build. Full reasoning in `prototype_strategy_decision.md`.

## Before You Start
- FDM printer (PETG-capable) — personal or lab access
- Basic tools: screwdriver set, wire strippers, soldering iron, multimeter, small lever/deadweight setup for load tests
- Budget: ≈₹14,300–21,800 — see `bill_of_materials_v1.md` and `procurement_sheet.csv`

## Read in This Order
1. `prototype_strategy_decision.md` — why this scale, why this build order
2. `printable_parts_manifest.md`, `printing_package.md`, `stl_export_checklist.md` — what to print and how
3. `prototype_actuator_package.md`, `motor_mount_reference.md`, `procurement_list.md` — actuator choice and mounting
4. `telemetry_mounting_plan.md`, `observability_map_v2.md`, `prototype_fault_detection_plan.md` — sensors and what they're watching for
5. `assembly_sequence_v1.md` — the actual build steps, in order
6. `prototype_test_plan.md`, `acceptance_criteria.md`, `failure_log_template.md` — how to test what you built, and how to log it when something breaks
7. `bill_of_materials_v1.md`, `procurement_sheet.csv` — full parts list and ordering sheet

## Two Open Dependencies (Not Yet Resolved)
- **Manya's leg workspace report (Phase 4)** hasn't been produced yet. Tests 3–4 use a placeholder ROM (hip ±25°, knee 10–100°) until it is. Swap it in before trusting Test 4 results.
- **Electronics/driver stack** is a placeholder cost pending Dhruv and Suraj's confirmation.

## The One Rule That Matters
Do not print Batch 2 (the remaining 3 legs + body) until Tests 1–4 pass on the first leg. That gate is the entire point of this build order — it's what keeps a structural or actuator mistake from being repeated four times before anyone notices.

## Success Criteria
Anyone on the team — not just Arya — can pick up this folder and build a working leg without asking a clarifying question first.
