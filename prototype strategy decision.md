# Phase 1 — Quantified Stability Engineering

## Objective

The objective of this phase was to quantify the stability of the ARYA quadruped using measurable engineering parameters instead of descriptive analysis. 
The following parameters were evaluated:

- Support polygon margin
- Stability margin percentage
- Tipping threshold angle
- Center of mass position

## System Specifications Used

| Parameter | Value |
|---|---:|
| Total Mass | 15.26 kg |
| Total Weight | 149.7 N |
| Body Length | 250 mm |
| Body Width | 150 mm |
| Body Height | 165 mm |
| CoM Height (Z) | 58.57 mm |
| CoM Lateral Offset (Y) | 24.45 mm |
| CoM Longitudinal Position (X) | 272.60 mm |

## 1. Support Polygon Margin

**Calculation**

Half body width:
```
150 / 2 = 75 mm
```

CoM lateral offset:
```
24.45 mm
```

Support polygon margin:
```
75 − 24.45 = 50.55 mm
```

**Result**

Support polygon margin = **50.55 mm**

This indicates that the projected center of mass remains safely inside the support polygon formed by the four feet.

## 2. Stability Margin Percentage

**Formula**

```
Stability Margin % = Margin / Half Width × 100
                    = 50.55 / 75 × 100
                    = 67.4%
```

**Stability Classification**

| Stability Margin | Condition |
|---|---|
| Above 50% | Safe |
| 25–50% | Near-Critical |
| Below 25% | Critical |

**Result**

Current Stability Margin = **67.4%**
Current Condition = **SAFE**

## 3. Tipping Threshold Study

**Formula**

```
θ = tan⁻¹(Margin / CoM Height)
  = tan⁻¹(50.55 / 58.57)
  = 40.8°
```

**Result**

Maximum theoretical tipping threshold = **40.8°**

This means instability begins when body tilt causes the CoM projection to move outside the support polygon.

## Phase 1 Engineering Conclusion

The quadruped currently demonstrates stable static support behavior because the projected CoM remains well inside the support polygon, with a 67.4% stability
margin and a theoretical tipping threshold of 40.8°. However, increasing payload, terrain irregularity, or dynamic motion (walking, turning, recovery from
disturbance) will reduce the effective support polygon margin and can rapidly increase instability risk. This static result should be treated as a best-case
baseline, not a guarantee of dynamic stability.
