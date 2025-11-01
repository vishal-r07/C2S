# Quick Decision Guide: Patch Antenna Selection for IEEE MAPCON Problem 3

---

## WINNING ANTENNA TYPE: Rectangular 2×1 Array

### Why This Configuration Wins (80/80 Points Potential)

| Scoring Criteria | How Rectangular 2×1 Array Excels |
|------------------|-----------------------------------|
| **Design Architecture (15 pts)** | Novel 2×1 configuration + matched feed design shows understanding. Simple rectangular geometry = clear documentation. |
| **Simulation Accuracy (20 pts)** | Easy to model precisely in CST. Array coupling well-understood. Can achieve tight tolerance match between simulation and measurement. |
| **Output Voltage (10 pts)** | 6 dBi gain = 4× power at antenna output. Enables >200 mV easily at -10 dBm. |
| **Antenna Gain Pattern (10 pts)** | Textbook array pattern. Clear radiation pattern visible. Demonstrates beamforming. |
| **Rectenna Demo (10 pts)** | Highest efficiency (70-75%) = impressive demo voltage/current. Best metrics to showcase. |
| **Report Clarity (10 pts)** | Simple geometry = easy to explain. Can show clear before/after (single vs array). |
| **Application Relevance (5 pts)** | Arrays critical for wireless power systems. Shows scalability thinking. |
| **Total Projected Score** | **70-80 points** |

---

## ANTENNA TYPE DECISION MATRIX

**Answer These Questions to Confirm Your Choice:**

### Question 1: Do you have access to CST or HFSS?
- ✓ YES → Choose **Rectangular Single or Array** (simulation-dependent)
- ✗ NO → Choose **Circular Single** (simpler analysis, hand calculations possible)

### Question 2: What is your priority?
- **Maximize Efficiency** → **Rectangular 2×1 Array** (best match + gain)
- **Simplest Fabrication** → **Circular Single** (one patch, easier tolerances)
- **Show Advanced Design** → **Slotted 2×1 Array** (impressive but risky)
- **Maximize DC Output Voltage** → **Rectangular 2×2 Array** (but larger)

### Question 3: Fabrication capabilities?
- Professional PCB house available → **Rectangular 2×1 (or Slotted)**
- DIY etching only → **Circular Single** (forgiving tolerances)
- Limited space on board → **Rectangular Single** (no array)

### Question 4: Time available?
- 4 weeks (full time) → **Rectangular 2×1 or Slotted Single**
- 2-3 weeks → **Rectangular Single**
- <2 weeks → **Circular Single**

---

## ANTENNA COMPARISON: ONE-PAGE SUMMARY

### RECTANGULAR PATCH ANTENNA ⭐⭐⭐⭐⭐

**Best For:** Winning the contest, maximum efficiency, rectenna integration

**Pros:**
- Excellent return loss (-25 to -37 dB achievable)
- Perfect impedance matching possible (50Ω direct)
- 3-4 dBi gain easily achievable
- Professional appearance
- Proven rectenna integration

**Cons:**
- Requires CST/HFSS for optimization
- Inset feed tuning critical
- Narrow bandwidth (need optimization)

**Fabrication Ease:** ⭐⭐⭐⭐⭐ Easy
**Efficiency:** ⭐⭐⭐⭐⭐ Excellent (70%+)
**Cost:** $ 5-10 (2-layer PCB, minimal components)

**When to Choose:**
- If you want to WIN and have 3+ weeks
- If you have access to simulation software
- If fabrication quality is good

---

### CIRCULAR PATCH ANTENNA ⭐⭐⭐⭐

**Best For:** Circular polarization, beginner students, DIY fabrication

**Pros:**
- Slightly higher gain/directivity (3.5-4.5 dBi)
- Easier to fabricate (circle tolerances forgiving)
- Hand analysis possible
- Circular polarization option

**Cons:**
- Impedance matching harder (Z varies more with position)
- Return loss typically -13 to -15 dB (worse than rectangular)
- Less efficient rectenna integration
- Feed point optimization tedious

**Fabrication Ease:** ⭐⭐⭐⭐ Very Easy
**Efficiency:** ⭐⭐⭐ Medium (50-65%)
**Cost:** $ 5-10 (similar to rectangular)

**When to Choose:**
- If you DON'T have simulation software
- If DIY etching is your only option
- If you want faster design process

---

### SLOTTED PATCH ANTENNA ⭐⭐⭐⭐

**Best For:** Advanced students, impressing judges, high efficiency requirement

**Pros:**
- Excellent impedance matching capability
- High gain (4-9 dBi for slotted designs)
- Very high efficiency (70-80%)
- Shows advanced design knowledge

**Cons:**
- Complex design (6-8 weeks normally)
- Requires extensive HFSS optimization
- Fabrication tolerances VERY tight
- Risky for competition (small design errors ruin performance)

**Fabrication Ease:** ⭐⭐ Difficult (requires precision)
**Efficiency:** ⭐⭐⭐⭐⭐ Exceptional (75%+)
**Cost:** $ 10-15 (needs professional PCB house)

**When to Choose:**
- If you're VERY confident in simulation skills
- If you want to "show off" advanced design
- NOT recommended for first attempt at rectenna

---

### SINGLE ELEMENT vs. ARRAY

| Aspect | Single Element | 2×1 Array | 2×2 Array |
|--------|---|---|---|
| **Gain** | 3-4 dBi | 6-7 dBi | 8-10 dBi |
| **Output Voltage** | ~0.15V @ -10dBm | ~0.35V | ~0.5V |
| **Beamwidth** | Wide (~90°) | ~82° | ~60° |
| **Size** | 50×50mm | 120×50mm | 80×80mm |
| **Complexity** | Simple | Medium | Hard |
| **Efficiency** | 50-60% | 70-75% | 72-76% |
| **Matching Network** | Simple | Moderate | Complex |
| **Fabrication Time** | 1-2 days | 2-3 days | 3-4 days |

**RECOMMENDATION:** Use **2×1 Array**
- Sweet spot between complexity and performance
- Gain improvement obvious (6 dB boost vs single element)
- Fits on standard student contest board
- Array design shows advanced skills without excessive risk

---

## DESIGN SPECIFICATIONS: COPY-PASTE FOR YOUR CST MODEL

### Rectangular Single Element (2.4 GHz, FR4)
```
Patch Length: 38-40 mm
Patch Width: 38 mm
Substrate thickness: 1.6 mm
Ground plane: 60 × 50 mm
Feed position: 3 mm inset from center
Feed line width: 2.8 mm
Dielectric constant: 4.4
Loss tangent: 0.02
```

### 2×1 Array
```
Element 1 center: (0, 0)
Element 2 center: (62, 0)
Spacing: 62 mm (λ/2)
Power divider: T-junction at midpoint
Input port impedance: 50Ω
Expected gain: 6-7 dBi
Expected beamwidth: 82° E-plane
```

---

## RECTENNA MATCHING NETWORK SELECTION

Based on antenna choice:

### If Using Rectangular Patch:
```
Option A (Best): Direct conjugate match
- Series L ≈ 0.9 nH
- Shunt C ≈ 0.6 pF
- Efficiency: 75%+
- Complexity: Very Low

Option B: L-Network matching
- More flexible
- Better bandwidth
- Efficiency: 70%+
```

### If Using Circular Patch:
```
Requires T or π network (more components)
Series L: 1-2 nH
Shunt C: 1-3 pF
Series C: 2-5 pF
Efficiency: 60-70%
```

### If Using Slotted Patch:
```
Direct conjugate match often works
Similar to rectangular approach
Efficiency: 75-80%
```

---

## FABRICATION CHECKLIST

Before sending PCB to fab:

- [ ] **Patch dimensions verified** in simulation
- [ ] **Feed position optimized** (S11 < -15 dB)
- [ ] **Ground plane size confirmed** (min 60×50 mm)
- [ ] **Microstrip line width calculated** (50Ω: ~2.8 mm on FR4)
- [ ] **Via placement planned** (under feeds)
- [ ] **Component placement marked** (matching L, C, diode, filter)
- [ ] **DC output pads sized** for multimeter probes
- [ ] **Soldermask applied** (except pads, traces)
- [ ] **Silkscreen labels** (helpful for assembly)
- [ ] **DXF/Gerber files reviewed** by instructor
- [ ] **PCB house tolerance** confirmed (±0.1 mm achievable)

---

## SIMULATION SOFTWARE WORKFLOW

### CST Microwave Studio (RECOMMENDED)
1. Create rectangular patch (L, W, h)
2. Add ground plane (60×50 mm)
3. Draw microstrip feed line
4. Set inset feed position
5. Define FR4 material (εr=4.4, tan δ=0.02)
6. Mesh with wavelength refinement
7. Run frequency domain solver
8. Extract S-parameters, impedance, gain, pattern
9. Optimize inset position to achieve Z = 50Ω

**Expected Simulation Time:**
- Single element: 30-45 min
- Array: 60-90 min
- Optimization loop: 2-4 hours

### ADS (For Rectifier Integration)
1. Import antenna S-parameters from CST
2. Model SMS7630 with SPICE model
3. Design matching network
4. Run harmonic balance
5. Optimize for max efficiency
6. Extract output voltage vs input power

---

## FINAL RECOMMENDATION TABLE

| Situation | Antenna Type | Array? | Expected Points | Risk Level |
|-----------|---|---|---|---|
| **First time, 3+ weeks, CST access** | Rectangular | 2×1 | 75-80 | ⭐ Low |
| **Expert student, 4+ weeks** | Rectangular | 2×2 | 78-80 | ⭐ Low |
| **No simulation software** | Circular | Single | 60-70 | ⭐⭐ Medium |
| **Show-off design, lots of time** | Slotted | 2×1 | 75-80 | ⭐⭐⭐ High |
| **Rushed, <2 weeks** | Circular | Single | 55-65 | ⭐⭐⭐⭐ Very High |

---

## KEY SUCCESS FACTORS

✓ **Simulation Before Fabrication** (saves $, time, embarrassment)
✓ **Impedance Matching Critical** (more important than antenna gain)
✓ **Array Configuration** (doubles efficiency over single element)
✓ **Tight Fabrication Tolerances** (±0.1 mm, professional PCB)
✓ **Measurement Documentation** (photos, plots, data spreadsheet)
✓ **Report Quality** (presentation > raw specs)

---

## SCORING HACK: How to Get Extra Points

1. **Design Architecture:** Show trade-offs analysis (why rectangular vs circular?)
2. **Simulation Accuracy:** Include Smith chart plots of impedance vs frequency
3. **Gain Pattern:** Measure actual antenna pattern, not just simulated
4. **Application Relevance:** Position as IoT/satellite power harvesting system
5. **Innovation:** Add passive power combiner for scalability explanation

