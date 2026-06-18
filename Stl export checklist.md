# STL Export Checklist — ARYA Quadruped Prototype
**Phase 2 — Mechanical Lead: Arya**

Run through this before any part leaves SolidWorks. Check each box per part, not once for the whole assembly.

- [ ] Units confirmed as millimeters in SolidWorks export dialog
- [ ] 60% uniform scale applied to the part (or confirmed already modeled at scaled dimensions) — do not rely on the slicer to scale
- [ ] Export resolution set to "Fine" (deviation tolerance ≤0.01 mm) — coarse default will visibly facet the hip bracket and foot curves at this small size
- [ ] Exported as an individual part STL, not the full assembly — assemblies export as a single fused mesh and break per-part slicer settings
- [ ] Minimum wall thickness checked ≥1.2 mm anywhere on the part (PETG at 0.4 mm nozzle struggles below this) — check hip bracket walls and foot dome specifically, they scale down the most
- [ ] No non-manifold geometry or open surfaces (SolidWorks Mesh Prep Wizard or a quick Netfabb check before slicing)
- [ ] Orientation in the STL matches the planned print orientation from `printable_parts_manifest.md` — don't rely on "auto-orient" in the slicer for load-bearing parts, the grain direction matters for strength
- [ ] File named per convention: `ARYA_<part>_60pct_v1.stl`
- [ ] Version tag matches the corresponding GitHub commit/tag in `aryabarge100/Quadruped-productization-layer-and-stability-`
- [ ] Mass properties re-run on the scaled part in SolidWorks and logged — replaces the estimated masses in `printable_parts_manifest.md` once available

## Success Criteria
Every Batch 1 part (hip bracket, upper link, lower link, foot) clears every box above before it is sent to the slicer.
