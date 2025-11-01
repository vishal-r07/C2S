# IEEE MAPCON Problem 3: Technical Specifications & Design Equations
## Rectangular 2×1 Patch Array Rectenna

---

## PART 1: ANTENNA DESIGN CALCULATIONS

### Single Element Rectangular Patch (2.4 GHz, FR4 substrate)

**Given Parameters:**
- Operating Frequency: f₀ = 2.4 GHz
- Substrate: FR4 (εᵣ = 4.4, loss tangent = 0.02)
- Substrate Thickness: h = 1.6 mm
- Free space constant: c = 3×10⁸ m/s

**Step 1: Calculate Patch Width (W)**

```
W = (c / 2f₀) × √(2 / (εᵣ + 1))
W = (3×10⁸ / 2 × 2.4×10⁹) × √(2 / 5.4)
W = 62.5 × √0.370
W ≈ 38 mm
```

**Step 2: Calculate Effective Dielectric Constant (εᵣ_eff)**

```
εᵣ_eff = [(εᵣ + 1) / 2] + [(εᵣ - 1) / 2] × [1 / √(1 + 12h/W)]
εᵣ_eff = 2.7 + 1.7 × [1 / √(1 + 12×1.6/38)]
εᵣ_eff = 2.7 + 1.7 × [1 / √1.505]
εᵣ_eff ≈ 2.7 + 1.7 × 0.815
εᵣ_eff ≈ 3.68
```

**Step 3: Calculate Length Extension (ΔL) due to Fringing Effect**

```
ΔL = 0.412h × [(εᵣ_eff + 0.3)(W/h + 0.264)] / [(εᵣ_eff - 0.258)(W/h + 0.8)]
ΔL = 0.412 × 1.6 × [(3.98)(24.75 + 0.264)] / [(3.42)(24.75 + 0.8)]
ΔL ≈ 0.412 × 1.6 × [3.98 × 25.01] / [3.42 × 25.55]
ΔL ≈ 0.66 mm
```

**Step 4: Calculate Patch Length (L)**

```
L = (c / 2f₀√εᵣ_eff) - 2ΔL
L = (3×10⁸ / 2 × 2.4×10⁹ × √3.68) - 2×0.66
L = (62.5 / 1.92) - 1.32
L ≈ 32.55 - 1.32
L ≈ 31.2 mm (then increase to ~38-40 mm and tune in simulation)
```

**OPTIMIZED RECTANGULAR PATCH DIMENSIONS:**
- **Length (L): 38-40 mm**
- **Width (W): 38 mm**
- **Ground Plane: 60 × 50 mm (minimum)**
- **Substrate: FR4, 1.6 mm thick**

---

### Inset Feed Position Calculation (50Ω Impedance)

**Objective:** Achieve 50Ω input impedance without external matching network

**Method:** Adjust feed inset distance from patch center

**Initial Feed Position:**
```
Offset from center = W/6 to W/4 (start at ~9-10 mm from center)
```

**Impedance at feed point varies as:**
```
Z_in ≈ Z₀ × √(1 - (Y_offset / (W/2))²)
```

**Optimization:** Simulate and sweep offset from 2-5 mm to achieve:
- Input impedance: 50Ω ± 5Ω
- Return loss: < -15 dB
- Bandwidth: > 50 MHz

**Typical Final Offset: 3-4 mm from patch center**

---

### 2×1 Array Design

**Array Configuration: Series-Fed Linear Array**

**Element Spacing (Center-to-Center):**
```
Spacing = λ/2 = c / (2 × f₀ × √εᵣ_eff)
λ/2 = 3×10⁸ / (2 × 2.4×10⁹ × √3.68)
λ/2 ≈ 62.5 mm
```

**Use spacing = 62 mm** (accounting for substrate effects)

**Array Gain Prediction:**
```
Gain_array = Gain_element + 10 log₁₀(N) + Coupling_factor
Gain_array = 3.5 dBi + 10 log₁₀(2) - 0.5 dB
Gain_array ≈ 3.5 + 3 - 0.5 = 6 dBi
```

**Power Divider (T-Junction):**
- Design for 50Ω input → 25Ω per element
- Each element fed with 50Ω characteristic line
- Use quarter-wave transformer or stepped impedance lines

**Physical Dimensions (2×1 Array):**
- Total length: 38 mm + 62 mm + margin = ~115-120 mm
- Width: 38 mm
- Beamwidth (E-plane): ~82°
- Beamwidth (H-plane): ~50° (directional in linear direction)

---

## PART 2: RECTIFIER CIRCUIT DESIGN

### Schottky Diode: SMS7630-079LF Specifications

**Key Parameters at 2.4 GHz:**
- Typical Diode Impedance @ -12 dBm: Z_diode = 8 + j13.5 Ω
- Turn-on voltage (V_f): ~0.3 V
- Package: SOD523 (small surface-mount)
- Nonlinear SPICE model: Available from Skyworks

**Rectifier Topologies:**

**Option 1: Single Diode (Simplest)**
```
RF Input → Series Diode → DC Load
Advantages: Minimal components, small size
Disadvantages: Low output voltage @ low power
Output voltage: V_out ≈ 0.3V @ -20 dBm (barely meets requirement)
```

**Option 2: Series-Shunt Configuration (RECOMMENDED)**
```
RF Input → Series Diode → Low-pass Filter → DC Output
            ↓
         Shunt Capacitor
Advantages: Better voltage regulation, output smoothing
Output voltage: V_out ≈ 0.4-0.5V @ -12 dBm, >1V @ 0 dBm
```

**Option 3: Voltage Doubler (if space/power available)**
```
Two diodes + two capacitors in doubler configuration
Output voltage: V_out ≈ 2 × rectified voltage
Tradeoff: More complex, uses more board space
```

### Impedance Matching Network

**Design Objective:** Match 50Ω antenna to ~8+j13.5Ω diode impedance

**Solution 1: Direct Conjugate Match (Preferred for Efficiency)**
```
Match to Z_match = 8 - j13.5 Ω (conjugate of diode)
Design L-Network:
- Series Inductor: L₁ (provides reactance +j13.5Ω at 2.4 GHz)
- Shunt Capacitor: C₁ (transforms to 50Ω)

Calculate:
X_L1 = 13.5 Ω at 2.4 GHz
L₁ = X_L1 / (2πf) = 13.5 / (2π × 2.4×10⁹) ≈ 0.89 nH

Q = (50 - 8) / 13.5 = 3.1
B₁ = √[(50/8 - 1) × (50/8 + 1)] / 50 = 0.0085 S
C₁ = B₁ / (2πf) ≈ 0.56 pF
```

**Solution 2: T-Network or π-Network (Broader Bandwidth)**
```
Better for > 30 MHz bandwidth requirement
Use circuit design software (ADS) for optimization
Typical component values:
- Series L: 0.8-1.2 nH
- Shunt C: 0.5-2 pF
- Series C (if needed): 2-5 pF
```

**Recommendation:** Simulate both in ADS harmonic balance with actual SMS7630 model

### DC Output Filter

**Low-Pass Filter Design (Remove 2f₀ harmonics):**
```
Cutoff frequency: f_c = 1 / (2π√LC) ≈ 100 MHz
(Need to block at 4.8 GHz while passing DC)

Component Values:
- Series Inductor (RF Choke): L_choke ≈ 10-47 nH
  (impedance >> 50Ω at 2.4 GHz)
- Shunt Capacitor: C_filter = 10-100 pF (for DC smoothing)
```

**Output Voltage Calculation:**
```
V_DC(RL) = V_diode × η × √(2) × P_in^0.5
Where:
- η = rectification efficiency (0.4-0.75 typical)
- P_in = input power (in watts)
- Typical: V_DC ≈ 0.15V @ -20 dBm, 0.4V @ -12 dBm
```

---

## PART 3: SIMULATION STRATEGY (CST/HFSS)

### Step 1: Antenna Simulation (CST Microwave Studio)

**Model Setup:**
1. Create rectangular patch on FR4 substrate
2. Add ground plane (60×50 mm minimum)
3. Define microstrip feed line (width ≈ 2.8 mm for 50Ω)
4. Inset feed point at 3 mm from center

**Mesh Settings:**
- Mesh density: Fine near patch, coarse far field
- Min wavelength elements: 10-15 per wavelength
- Frequency range: 2.3-2.5 GHz

**Simulation Results to Extract:**
- S-parameters (S11, S21)
- Input impedance vs frequency
- Radiation pattern (E-plane, H-plane)
- Realized gain
- Beamwidth (-3 dB)

**Pass Criteria:**
- S11 < -10 dB at 2.4 GHz
- Gain > 3 dBi
- Beamwidth > 40°
- Bandwidth > 30 MHz (-6 dB level)

### Step 2: Array Simulation

1. Design T-junction power divider
2. Create 2-element array in CST
3. Simulate coupled array behavior
4. Extract array impedance at feed port
5. Verify gain improvement (~3 dB from 2 elements)

**Target Array Performance:**
- Gain: 5.5-6.5 dBi
- Beamwidth: Similar to single element
- Coupling: -15 dB or better isolation

### Step 3: Rectifier Harmonic Balance Simulation (ADS)

1. Import antenna as port with measured impedance
2. Model SMS7630 using SPICE model from Skyworks
3. Design matching network (L and C values)
4. Run harmonic balance analysis:
   - Frequency: 2.4 GHz
   - Power sweep: -20 to 0 dBm
   - Optimization goal: Maximize efficiency

**Output Metrics:**
- RF-to-DC efficiency vs input power
- Output voltage vs input power
- Load resistance variation

### Step 4: Integration & Optimization

1. Combine antenna + matching + rectifier in single ADS schematic
2. Simulate end-to-end rectenna system
3. Optimize for:
   - Efficiency > 50% @ -10 dBm
   - Output voltage > 200 mV
   - Bandwidth > 30 MHz

---

## PART 4: FABRICATION SPECIFICATIONS

### PCB Layout Rules

**Material Specification:**
```
Layer 1 (Top): Patch + feed line (1 oz copper)
Layer 2 (Bottom): Ground plane (continuous)
Substrate: FR4, εᵣ = 4.4, h = 1.6 mm
Copper thickness: 35 μm (1 oz standard)
```

**Microstrip Line Width (50Ω on FR4, 1.6mm):**
```
Width = 2.8-3.0 mm (use PCB trace calculator to confirm)
```

**Via Placement:**
- Ground vias under feed line (3-4 per inch)
- Via diameter: 0.3 mm minimum
- Via spacing: 5 mm maximum

**Patch Dimensions (Final - tune in sim, then fabricate):**
```
Patch: 38.5 × 38.5 mm (square optimal for fabrication)
OR Rectangular: 40 × 29 mm
Ground plane: 60 × 50 mm
Feed line width: 2.8 mm, length: ~10 mm to feed point
```

**Component Placement (2×1 Array with Rectifier):**
```
Position 1 (Element 1): Patch at (0, 0)
Position 2 (Element 2): Patch at (62, 0)
Power divider: Between patches, centered
Matching L: At combined feed point
Matching C: In series with diode
Diode: At rectifier input (keep leads < 2 mm)
Choke L: Series after diode
Filter C: Shunt to ground
DC output: Via 2 pads with 2mm spacing (for multimeter probes)
```

---

## PART 5: MEASUREMENT & TESTING PROTOCOL

### Pre-fabrication Verification (Simulation)

- [ ] Single element: S11 < -15 dB at 2.4 GHz
- [ ] Single element: Gain > 3 dBi
- [ ] Array: Gain > 5.5 dBi
- [ ] Rectifier efficiency > 50% @ -10 dBm

### Post-fabrication Measurements

**Antenna Measurements (Network Analyzer):**
```
1. S11 parameter vs frequency (2.3-2.5 GHz)
   - Should see dip < -10 dB at 2.4 GHz
   
2. Impedance vs frequency (Smith chart plot)
   - Should approach 50Ω at 2.4 GHz
   
3. Antenna gain (using reference horn antenna or pattern measurements)
   - Should measure 5-7 dBi for 2×1 array
```

**Rectenna Measurements (Function Generator + Multimeter):**
```
1. Input: CW 2.4 GHz signal at calibrated power levels
   - Power range: -20 dBm to 0 dBm (in 2 dBm steps)
   
2. Measure DC output voltage across known load resistor
   - Load options: 1 kΩ, 10 kΩ, 50 kΩ
   
3. Calculate efficiency:
   η = (P_dc) / (P_rf_in) = (V_dc²/R_L) / (10^(P_dBm/10) × 10^-3)
   
4. Record at minimum 3 power levels
```

**Scoring Documentation:**
```
- Photos of fabricated antenna
- Radiation pattern plots (simulated + measured if possible)
- S-parameter measurements
- Efficiency curves (plotted)
- Output voltage vs input power graph
- Beamwidth measurements
```

---

## PART 6: QUICK REFERENCE DESIGN TABLE

| Parameter | Specification | Status |
|-----------|---------------|--------|
| **Antenna Type** | Rectangular 2×1 Array | ✓ Recommended |
| **Operating Frequency** | 2.4 GHz | ✓ Fixed |
| **Substrate** | FR4, εᵣ=4.4, h=1.6mm | ✓ Use quality PCB |
| **Patch (Single)** | 38×38 mm (rect: 40×29) | ✓ Verify in CST |
| **Array Spacing** | 62 mm (center-to-center) | ✓ Calculate λ/2 |
| **Antenna Gain** | 6-7 dBi (2×1 array) | ✓ Exceeds >3 dBi |
| **Beamwidth** | 80° E-plane, 50° H-plane | ✓ Exceeds >40° |
| **Rectifier Diode** | SMS7630-079LF | ✓ Discrete Schottky |
| **Matching Network** | L + C (conjugate match) | ✓ 2 components typical |
| **Output Filter** | Choke + Capacitor | ✓ DC smoothing |
| **Target Efficiency** | >50% @ -10 to 0 dBm | ✓ Critical spec |
| **Output Voltage** | >200 mV @ -10 dBm | ✓ Must meet |
| **Bandwidth** | 30 MHz operational | ✓ S11 < -6 dB |
| **PCB Size** | ~150 × 80 mm | ✓ Student-friendly |
| **Fabrication** | Standard PCB etching | ✓ No special tools |

---

## PART 7: TIMELINE FOR 4-WEEK PROJECT

**Week 1:**
- Mon-Tue: Single patch design, CST modeling
- Wed-Thu: Feed optimization, target S11 < -10 dB
- Fri: Design review, documentation

**Week 2:**
- Mon: Design 2×1 array, power divider
- Tue-Wed: Array simulation, verify gain improvement
- Thu: Rectifier matching network design (ADS)
- Fri: Integration simulation

**Week 3:**
- Mon-Tue: PCB layout, design review, send to fab
- Wed: Receiving PCB
- Thu-Fri: Assembly, soldering (Schottky diode, passive components)

**Week 4:**
- Mon-Tue: Network analyzer measurements (S-parameters)
- Wed: Rectenna efficiency testing
- Thu: Data collection, report writing
- Fri: Final report, presentation preparation

**Critical Path:** PCB fabrication time (allow 7-10 days)

