# Observability Map v2 — ARYA Quadruped Prototype
**Phase 5 — Mechanical/Telemetry Collaboration: Arya × Dhruv**
Aligned to Dhruv's `canonical_telemetry_v2.json` (Canonical Telemetry Contract v2).

This maps every required field in the schema to its physical source and the owner responsible for it, so nothing in the contract is left without a real-world origin.

## control_state
| Field | Physical Source | Owner |
|---|---|---|
| `gait_mode` | Commanded by control software, no mechanical sensor | Control (Suraj) |
| `target_velocity` | Commanded by control software | Control (Suraj) |
| `control_mode` | Software state | Control (Suraj) |
| `recovery_state` | Software state, triggered by stability metrics below | Control (Suraj) |

## locomotion_state
| Field | Physical Source | Owner |
|---|---|---|
| `hip_angles[4]` | AS5600 encoder per hip (recommended) or commanded PWM angle (interim proxy) | Mechanical (Arya) → Telemetry (Dhruv) |
| `knee_angles[4]` | AS5600 encoder per knee (recommended) or commanded PWM angle (interim proxy) | Mechanical (Arya) → Telemetry (Dhruv) |
| `foot_positions[4][3]` | Computed (not directly sensed) from hip/knee angles + known link lengths (48 mm upper, 60 mm lower at 60% scale) via forward kinematics | Control (Suraj) using Mechanical's geometry |
| `support_polygon_state` | Computed from foot positions + ground contact state | Control (Suraj) |
| `stability_margin` | Computed from CoM projection vs support polygon — see `prototype_fault_detection_plan.md` for the rescaled thresholds | Mechanical (Arya) provides the math, Control (Suraj) computes it live |

## terrain_state
| Field | Physical Source | Owner |
|---|---|---|
| `terrain_type` | Not directly sensed at prototype stage — would need a terrain classifier (camera/IMU pattern) out of scope for this sprint | Telemetry (Dhruv) — flagged as a gap |
| `slip_probability` | Derived from required vs. available friction (see fault detection plan) | Mechanical (Arya) provides the formula |
| `traction_state` | Derived from foot contact sensor + slip_probability | Mechanical (Arya) sensor, Control (Suraj) logic |
| `incline_estimate` | IMU orientation reading | Telemetry (Dhruv), sensor mounted per `telemetry_mounting_plan.md` |

## actuation_state
| Field | Physical Source | Owner |
|---|---|---|
| `joint_torque[4]` | Derived from hip current-sense reading + DS3225 torque-current curve (one representative value per leg, not per joint — matches schema's 4-element array) | Mechanical (Arya) sensor placement, Telemetry (Dhruv) conversion |
| `driver_status` | Motor driver board state | Telemetry (Dhruv) |
| `bus_health` | Communication bus state | Telemetry (Dhruv) |
| `thermal_state[4]` | Thermistor at each leg's hip servo case | Mechanical (Arya) sensor placement, Telemetry (Dhruv) readout |

## system_health
| Field | Physical Source | Owner |
|---|---|---|
| `watchdog_status` | Software heartbeat | Telemetry (Dhruv) |
| `timing_status` | Software loop timing — current 350-frame report shows only 14.9% compliance against the 4.0 ms target, flagged below | Telemetry (Dhruv) |
| `schema_status` | Software validation | Telemetry (Dhruv) |
| `replay_status` | Software replay engine | Telemetry (Dhruv) |

## Coordination Flag for Dhruv
The 350-frame reliability report shows `average_loop_latency_ms: 4.47` against a `target_deadline_ms: 4.0`, with deadline compliance at only **14.9%**. Mechanically, this matters because the fault detection plan below assumes the telemetry loop can catch a fault fast enough to matter during Tests 5–7 (live weight-bearing and crawl tests). If the loop is missing its deadline 85% of the time, a real mechanical fault (overload, slip, joint stall) could occur and clear before it's even logged. Recommend resolving this before relying on the pipeline as the safety net during physical load testing — until then, treat the dashboard as observational only, not as the primary fault-catch mechanism.

## Success Criteria
Every field in the Canonical Telemetry Contract v2 has a named physical or computational source and an owner. No field is left unaccounted for.
