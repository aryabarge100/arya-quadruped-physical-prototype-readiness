# Prototype Test Plan — ARYA Quadruped (60% Scale)
**Phase 6 — Mechanical Lead: Arya**

Tests are sequenced so the single-leg gate (Tests 1–4) must pass before Batch 2 printing/assembly begins, per the build order locked in `prototype_strategy_decision.md`.

**Open dependency:** Tests 3–4 reference leg range-of-motion (ROM). Manya's `leg_workspace_report.md` (Phase 4) hasn't been produced yet in this sprint. Until it is, the ROM bounds below are a conservative placeholder (hip ±25°, knee 10–100°) — replace with Manya's confirmed values before running Test 4 for real.

## Test 1 — Single Printed Link Strength
**Setup:** Clamp the upper link (then separately the lower link) at its mounting boss. Apply a static transverse load at the free end via deadweight or a luggage scale.
**Procedure:** Apply 30 N (≈2× the worst-case computed leg force of 14.8 N at this scale, per `prototype_fault_detection_plan.md`). Hold 60 seconds.
**Pass:** No visible cracking, no layer separation, permanent deflection <1 mm after load removal.
**Fail:** Any crack, delamination along print layers, or deflection >1 mm.

## Test 2 — Hip Bracket Load Test
**Setup:** Mount the hip bracket to a rigid test fixture exactly as it will sit on the body plate.
**Procedure:** Apply a torque load at the bracket's servo-mount boss equivalent to 2× worst-case joint torque (≈3.2 Nm), via a calibrated lever arm and deadweight.
**Pass:** No crack at mounting bosses, no screw pull-through, no visible deformation.
**Fail:** Crack, stripped insert, or bracket flex >0.5 mm under load.

## Test 3 — Single Leg Assembly
**Setup:** Fully assemble one leg: hip bracket + DS3225 (hip) + upper link + knee bearing + DS3225 (knee) + lower link + foot.
**Procedure:** Manually cycle the leg through the placeholder ROM (hip ±25°, knee 10–100°). Check for binding, uneven gaps, or interference between links.
**Pass:** Smooth motion through full ROM, no binding, bearing seats correctly, no visible misalignment at any joint.
**Fail:** Binding, grinding, visible gap >0.3 mm at any pivot, or interference between upper/lower link at ROM limits.

## Test 4 — Actuator Motion Test
**Setup:** Power the assembled single leg with no external load on the foot.
**Procedure:** Command both joints through the full placeholder ROM at slow speed. Monitor current draw and (if AS5600 encoders are installed per `telemetry_mounting_plan.md`) compare measured vs. commanded angle.
**Pass:** No audible skipping/clicking, current draw stays below DS3225 stall current, measured-vs-commanded angle deviation <3° if encoders are present.
**Fail:** Skipping, stalling, current spikes at no load, or deviation >3°.

**GATE: Do not proceed to Batch 2 printing until Tests 1–4 all pass.**

## Test 5 — Static Stand
**Setup:** Full 4-leg assembly, all sensors wired per `telemetry_mounting_plan.md`, on a flat, level, dry surface.
**Procedure:** Power on, command STAND gait, hold for 2 minutes.
**Pass:** Stability margin >50%, no leg exceeds 10 N static load, no actuator current limiting triggered, IMU tilt <5°.
**Fail:** Stability margin <25%, any leg >15 N, current-limited or thermal-fault state on any joint.

## Test 6 — Weight Support Test
**Setup:** Robot standing and stable per Test 5.
**Procedure:** Add known payload in 0.5 kg increments to the body plate. Log per-leg load (derived from hip current sense) after each increment.
**Pass:** Record the payload increment at which any leg first crosses 10 N (near-critical) — this is the prototype's measured safe payload limit. Continuing past 15 N on any leg is a hard stop.
**Fail:** Any leg exceeds 15 N, or visible structural flex/creak in links or body plate at any point.

## Test 7 — Slow Crawl Test
**Setup:** Robot standing and stable, payload at or below the Test 6 safe limit.
**Procedure:** Command a slow crawl gait (3-leg support cycle) for 5–10 minutes continuous. Monitor stability margin, slip risk index (via foot contact sensors), and joint thermistor readings throughout.
**Pass:** Stability margin stays >25% throughout the gait cycle, slip index stays <1.0, no joint thermistor exceeds 45°C over the run.
**Fail:** Stability margin drops <25% at any point, slip index >1.0, or any joint exceeds 45°C.

## Success Criteria
Testing becomes deterministic — every test has a defined setup, procedure, and numeric pass/fail line, not a subjective "looks okay" call.
