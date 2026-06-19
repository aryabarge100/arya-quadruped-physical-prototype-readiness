# Prototype Fault Detection Plan — ARYA Quadruped (60% Scale)
**Phase 5 — Mechanical/Telemetry Collaboration: Arya × Dhruv**

Every threshold below is **rescaled for the 60%-scale prototype**, not copied from the full-scale analysis. Two kinds of metrics behave differently under scaling:
- **Scale-invariant** (carry over unchanged): stability margin %, tipping angle, slip risk index — these are ratios, so geometric scaling cancels out.
- **Scale-dependent** (must be recalculated): absolute support-polygon margin in mm, absolute leg load in N — these depend on the robot's actual size and weight, which dropped substantially at 60% scale.

## Mechanical Failure Modes → Observable Signal

| Failure Mode | Observable Signal | Sensor | Prototype Threshold | Schema State | Response |
|---|---|---|---|---|---|
| Foot slip | Slip Risk Index = required friction / available friction | Foot contact sensor + IMU (derived) | >0.5 = moderate risk, >1.0 = slip occurring (unchanged from full-scale — ratio-based) | `terrain_state.traction_state`: SLIPPING / TOTAL_LOSS | Gait slowdown, stance widening |
| Leg overload | Per-leg reaction force | Hip current-sense (derived torque/force) | Safe <10 N, Near-critical 10–15 N, Critical >15 N (rescaled from 50 N/75 N full-scale, using the ≈0.20 mass ratio between 60%-scale prototype and full-scale robot) | `actuation_state.driver_status`: CURRENT_LIMITED at near-critical, THERMAL_FAULT risk at critical | Torque limiting, recovery posture |
| Support polygon collapse / tipping | Stability margin % | Computed from IMU + foot positions | Safe >50%, Near-critical 25–50%, Critical <25% (use the **percentage** form, not the full-scale 40 mm/15 mm absolute values — those were calibrated to a 150 mm half-width body, not this prototype's 90 mm) | `locomotion_state.support_polygon_state`: DYNAMIC_TRI → UNSTABLE_DIAG → COLLAPSED | Recovery posture, emergency halt |
| Tipping threshold exceeded | Body tilt angle | IMU | 40.8° theoretical max (unchanged — margin/CoM-height ratio is scale-invariant); recommended safe operating tilt below 15°, same as full-scale | `health_status`: UNSTABLE above 15°, EMERGENCY_STOP approaching 40.8° | Self-righting, static stand |
| Actuator thermal fault | Winding/case temperature | Thermistor at hip servo | Safe <45°C, Warning 45–55°C, Critical >55°C for DS3225 (DS3225 is rated lower than the GoBilda-class actuators referenced in the dashboard mockup — do not reuse the 38–40°C "nominal" baseline shown there without checking it against DS3225's own datasheet limits) | `actuation_state.thermal_state[4]`, `driver_status`: THERMAL_FAULT | Throttle to CURRENT_LIMITED, halt if sustained |
| Communication/bus timeout | Bus health heartbeat | Driver board (software-side) | Per Dhruv's existing fault matrix: TIMEOUT_CRITICAL triggers SAFE_FALLBACK control mode + RECOVERY_PULSE gait | `system_health.watchdog_status`, `actuation_state.bus_health` | Matches Dhruv's `ACTUATOR_BUS_TIMEOUT` entry in `fault_propagation_matrix.md` directly — no mechanical change needed, just confirm the mechanical recovery posture (legs tucked, low CoM) is physically achievable within the joint range of motion |
| Joint/link structural failure | Indirect — no direct strain sensor planned at prototype stage | Inferred from sudden angle/torque mismatch (commanded vs. measured, if encoders are added per the mounting plan) | Mismatch beyond expected backlash tolerance | `system_health.schema_status`: MISMATCH_WARNING (repurposed) | Halt, visual inspection — this is the one failure mode without a clean direct sensor; flagged as a gap below |

## Known Gap
Structural failure (link bending, joint pin stress, body plate flex) has no direct sensor in this plan — it's inferred indirectly through angle/torque mismatch, which only works if the recommended AS5600 encoders are installed. Without them, a cracked or bent link could go undetected until visible. If the encoder addition isn't done before Tests 5–7, add a manual visual-inspection checkpoint between each test in `prototype_test_plan.md` (Phase 6) as a stand-in.

## Success Criteria
Every critical failure mode identified in the project's prior stability/terrain analysis (foot slip, overload, tipping, thermal fault, bus timeout) has at least one observable signal, correctly rescaled for the 60%-scale prototype rather than inherited from the full-scale numbers.
