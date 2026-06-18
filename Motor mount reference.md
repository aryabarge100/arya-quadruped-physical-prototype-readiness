# Motor Mount Reference — DS3225 Servo
**Phase 3 — Mechanical Lead: Arya**

## Servo Envelope
- Case dimensions: ≈40 × 20 × 40.5 mm (standard size, same footprint as MG996R/DS3218MG)
- Output: 25T spline horn, standard servo arm/disc compatible
- Mounting: 4× tab holes through the servo flange, typically M3 clearance

## Hip Joint Mounting
- Hip bracket pocket sized to servo case with +0.2 mm clearance per side for a snug, non-press-fit seat (servo should be removable for swaps between Tests 1–4 and 5–7 if you reuse MG996R for early checks)
- 4× M3 bolts through bracket tabs into printed bracket — use heat-set threaded inserts if this bracket will be assembled/disassembled more than 2–3 times
- Horn bolts directly to the upper link mounting boss; torque the horn screw to spec, do not over-torque into PETG

## Knee Joint Mounting — Add a Support Bearing
The spline horn alone is not meant to carry continuous radial load from the lower link's weight and ground reaction force. Add a **5 mm ID flanged ball bearing** on the opposite side of the knee joint from the servo, so the lower link is supported at two points (servo spline + bearing) rather than cantilevered off the spline alone. This significantly reduces spline wear and slop over repeated test cycles.

## Wiring
- Route servo signal/power cable through a channel molded into the hip bracket and upper link (no exposed wire across the moving joint)
- Use servo extension leads rather than splicing, so any servo can be swapped without rewiring

## Success Criteria
Mounting interface fully specified — a builder can bolt a DS3225 into the printed hip bracket and knee joint without guessing tolerances or needing a redesign.
