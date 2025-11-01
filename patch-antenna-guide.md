# IEEE MAPCON Problem 3: Patch Antenna Types for Rectenna Design
## Comprehensive Comparison & Winning Strategy

---

## Executive Summary: Best Choice for Winning

**Recommended: Rectangular Patch Antenna Array (2×1 or 2×2 configuration)**

**Why it wins:**
- Superior return loss and impedance matching (critical for rectifier integration)
- Better bandwidth control for 30 MHz operational requirement
- Excellent gain scalability through arrays
- Proven performance with SMS7630 Schottky diodes
- Easy fabrication tolerances on FR4 substrate
- Scoring advantage: Simulation Accuracy (20 pts) + Output Voltage (10 pts) + Gain Pattern (10 pts)

---

## Complete Patch Antenna Type Analysis

### 1. **RECTANGULAR PATCH ANTENNA** ✓ RECOMMENDED

**Geometry:** Simple rectangle (length L × width W)

**Advantages:**
- **Impedance Matching Excellence:** Rectangular patches achieve near-50Ω impedance with proper feed point adjustment. Feed offset from center (inset feed) provides tunable impedance matching, essential for rectifier circuit integration [1][2]
- **Return Loss Control:** Can achieve -19 to -37 dB return loss at 2.4 GHz with proper tuning [1][51]
- **Bandwidth:** 70-100 MHz achievable with FR4 substrate [51], exceeds 30 MHz requirement
- **Gain:** Single element: 2-4 dBi; 2×1 array: 5-6 dBi; 2×2 array: 8-9 dBi [1][3][17]
- **Beamwidth:** E-plane ~80-100°, H-plane ~60-80° (exceeds >40° requirement easily) [22][28]
- **Fabrication:** Standard PCB etching, tight tolerances possible (±0.1mm)
- **Feed Options:** Both microstrip line feed AND coaxial probe feed compatible [21][27]
- **Rectenna Integration:** Direct conjugate matching possible between antenna impedance and Schottky diode; minimal matching network required [32][36]

**Disadvantages:**
- Narrow inherent bandwidth (needs optimization for 30 MHz)
- Slightly lower gain than circular for same size

**Design Specifications for 2.4 GHz (FR4 substrate, εr=4.4, h=1.6mm):**
- Patch Length: ~38-40 mm
- Patch Width: ~29-30 mm
- Ground plane: ≥60×50 mm
- Inset feed distance from center: 2-4 mm (controls matching)

**Best for scoring:** Design Architecture (15), Simulation Accuracy (20), Efficiency (10), Gain Pattern (10)

---

### 2. **CIRCULAR PATCH ANTENNA** ✓ GOOD ALTERNATIVE

**Geometry:** Perfect circle (diameter D)

**Advantages:**
- **Better Gain/Directivity:** Circular patches provide 5-10% higher directivity than rectangular [2][5]
- **Circular Polarization:** Can achieve circular polarization with dual-fed configuration [25]
- **Fabrication Simplicity:** Circle geometry easier to achieve consistent tolerances across multiple patches
- **Gain:** Single element: 3-4 dBi; 2×2 array: 8.5+ dBi [14]
- **Beamwidth:** Slightly narrower, maintains >40° requirement

**Disadvantages:**
- **Impedance Matching Complexity:** Circular patches have more pronounced impedance variation with feed position [2]
- **Rectenna Integration Challenge:** More difficult conjugate matching with Schottky diodes due to impedance characteristics [32]
- **Return Loss:** Typically 13-14 dB (inferior to rectangular 19+ dB) [2][8]
- **Feed Accuracy:** Feed point adjustment more critical and less intuitive

**When to use:** If circular polarization is needed or if fabrication precision is primary concern; NOT recommended for efficiency-focused rectenna design

---

### 3. **SLOTTED PATCH ANTENNA** ✓ ADVANCED OPTIMIZATION

**Geometry:** Rectangular or circular patch with carefully designed slot(s)

**Types:**
- **Single slot:** Bandwidth enhancement
- **Multi-slot (star-shaped, inverted-U):** Multi-band operation
- **Jerusalem cross slots:** Better impedance matching [18][15]

**Advantages:**
- **Bandwidth Expansion:** Achieve 200-300% bandwidth improvement (can reach 200+ MHz) [12][15][18]
- **Gain Enhancement:** 9-10 dBi with single element [12]
- **Impedance Optimization:** Slots can fine-tune antenna impedance for specific rectifier matching [18]
- **Multiband Capability:** Design for 2.4 GHz + harmonics

**Disadvantages:**
- **Design Complexity:** Requires optimization; not straightforward calculation
- **Fabrication Precision:** Slots demand tight tolerances; small errors cause frequency shift
- **Simulation Dependency:** Must use HFSS/CST extensively for accuracy
- **Rectenna Complexity:** May require more sophisticated matching network

**Best when:** Pursuing excellence in "Simulation Accuracy" and "Maximum Efficiency" scoring sections

---

### 4. **MICROSTRIP LINE FED vs. COAXIAL PROBE FED**

These are feeding mechanisms, not patch types, but critical for performance:

**Microstrip Line Feed (Inset Feed):**
- **Advantages:** Planar, easy integration, impedance tuning via inset position
- **Best for:** Rectangular patches, student fabrication
- **Impedance range:** 20-100Ω easily achievable by adjusting inset length
- **Coupling:** Direct electrical contact with patch

**Coaxial Probe Feed:**
- **Advantages:** Low loss, excellent impedance matching range (0-100Ω), widely used in industry
- **Best for:** Maximum efficiency demonstration, professional appearance
- **Disadvantage:** Requires drilling through substrate (more fabrication steps)
- **Better for:** Scoring Demo/Measurement (10 pts) - judges expect coaxial feed

**Recommendation for Contest:** Use inset microstrip feed for simplicity; upgrade to coaxial probe if fabrication resources available

---

### 5. **PATCH ANTENNA ARRAYS**

**Why Arrays Win Contests:**

Single element: ~3 dBi gain → Meets minimum >3 dBi barely
Array configuration: 5-9 dBi gain → Significant efficiency improvement

**Best Array Configuration: 2×1 Series-Fed Array**

**Advantages:**
- Gain increase: 3-4 dB over single element [3][11]
- Beamwidth maintained >40°
- Series feeding maintains single feed point (simpler fabrication)
- Element spacing: λ/2 ≈ 62mm at 2.4 GHz (tight coupling managed well)
- Increased directivity → Better RF-to-DC conversion [3]

**2×1 Array Performance:**
- Gain: 5-6 dBi (doubles output power)
- Return loss: -10 to -20 dB
- Fabrication size: ~120mm × 60mm (fits contest board easily)

**Alternative: 2×2 Array**
- Gain: 8-10 dBi (4x power!)
- Directivity: Excellent
- Trade-off: Larger size, more complex fabrication

---

## Comparative Performance Table

| Parameter | Rectangular | Circular | Slotted | Single vs Array |
|-----------|-------------|----------|---------|-----------------|
| **Return Loss (dB)** | -19 to -37 | -13 to -15 | -15 to -25 | Single -10 to -15 |
| **Gain (dBi)** | 3-4 single | 3.5-4 single | 9+ single | 2×1: +5-6 dBi |
| **Beamwidth** | 80-100° | 60-80° | Variable | Similar to element |
| **Impedance Match** | Excellent | Good | Excellent | Better with array |
| **Fabrication Ease** | Very Easy | Easy | Moderate | Easy (repetition) |
| **Rectenna Efficiency** | 50-75% | 45-65% | 60-80% | +30-50% (array) |
| **Bandwidth** | 70-100 MHz | 50-80 MHz | 200+ MHz | Similar scaling |
| **Design Simplicity** | Simple | Simple | Complex | Moderate |
| **Simulation Time** | ~2-4 hrs | ~2-4 hrs | ~6-8 hrs | ~3-5 hrs |

---

## Winning Design Architecture

### **RECOMMENDED SOLUTION: Rectangular 2×1 Array with Slotted Elements**

**Why This Wins:**
1. **Exceptional Gain:** 6-8 dBi (vs >3 dBi requirement) = Better efficiency, DC output voltage
2. **Superior Matching:** Rectangular patches + slot optimization = Conjugate match with SMS7630
3. **Design Architecture Score:** Novel array + slotted design = 13-15 points
4. **Simulation Accuracy:** CST/HFSS verification of both patch AND array = 18-20 points
5. **Efficiency:** Slotted impedance control + 2×1 gain = >60% RF-to-DC = 9-10 points
6. **Gain Pattern:** Clear array pattern, demonstrable beamwidth = 9-10 points
7. **Fabrication:** Standard PCB process, single board, repeatable = 9-10 points

**Total Expected Score: 75-80/80 points**

---

## Design Process Roadmap

### Phase 1: Single Element Optimization (Week 1)
1. Start with rectangular patch calculator
   - Length: L = (c/2f_0)√(1/εr_eff) × adjustment factor
   - Width: W = (c/2f_0)√(2/(εr+1))
   
2. Simulate in CST/HFSS:
   - Rectangular patch first
   - Achieve -15 dB return loss at 2.4 GHz
   - Optimize inset feed: start at 2.5mm from center, sweep 1-4mm
   - Target: 50Ω impedance ± 10Ω

3. Optional: Add single centered slot for impedance fine-tuning

### Phase 2: Array Design (Week 1-2)
1. Design 2×1 series-fed array
   - Element spacing: 62-65mm (λ/2 at 2.4 GHz)
   - T-junction power divider for equal power distribution
   - Port impedance: 50Ω

2. Simulate combined array
   - Target: 5-6 dB gain improvement
   - Verify beamwidth >40°
   - Check mutual coupling effects

### Phase 3: Rectenna Integration (Week 2)
1. Model SMS7630 Schottky diode in harmonic balance simulator
   - Typical impedance @ -12 dBm: Z_diode = 8 + j13.5 Ω
   
2. Design matching network:
   - **Option A (Simple):** Direct conjugate match to antenna
   - **Option B (Robust):** L-network or π-network matching
   - **Target:** -20 dBm input → >50% efficiency

3. Add DC filtering:
   - Choke inductor (L_choke >> 2f_0)
   - Low-pass filter capacitor for output voltage smoothing

### Phase 4: Fabrication & Testing (Week 3)
1. PCB layout in KiCad or Altium:
   - FR4 substrate 1.6mm thickness
   - Microstrip feed lines (50Ω)
   - Schottky diode placement near antenna feed
   - Through-hole connectors for DC measurement

2. Etching + assembly
3. Measurement: Return loss, gain pattern, RF-to-DC efficiency

---

## Contest Scoring Strategy

| Category | Strategy | Expected Points |
|----------|----------|-----------------|
| **Design Architecture (15)** | 2×1 slotted array + novel matching topology | 14-15 |
| **Simulation Accuracy (20)** | CST full-wave + harmonic balance verification | 18-20 |
| **Output Voltage (10)** | >200mV @ -12 dBm (2×1 array gain advantage) | 9-10 |
| **Antenna Gain Pattern (10)** | CST radiation pattern proof + beamwidth documentation | 9-10 |
| **Rectenna Demo (10)** | Live measurement of voltage, efficiency, current | 8-10 |
| **Report Clarity (10)** | Professional presentation, design rationale, equations | 9-10 |
| **Application Relevance (5)** | IoT/wireless power harvesting use case | 4-5 |
| **TOTAL** | | **75-80/80** |

---

## Critical Fabrication Tips

1. **FR4 Substrate:** Use high-quality microwave-grade FR4 (not standard PCB FR4)
   - εr = 4.4 ± 0.05 (tight tolerance)
   - Thickness: 1.6mm standard
   - Loss tangent: tan(δ) ≤ 0.02

2. **Copper Etching Tolerance:** ±0.1mm is critical
   - Larger tolerances shift resonance by ±50-100 MHz
   - Use professional PCB house, NOT DIY etching

3. **Coaxial Connector Placement:** Mount SMA connector away from patch
   - Keep high-impedance feed line 50Ω (width calculation needed)
   - Use ground plane vias to reduce loop area

4. **SMS7630 Diode Mounting:** 
   - SOD523 package (small surface-mount)
   - Place at antenna feed point or via matching network
   - Keep leads SHORT (inductance critical!)

---

## Software Recommendations

- **Antenna Simulation:** CST Microwave Studio (better for arrays) or HFSS
- **Rectifier Design:** ADS (Advanced Design System) for harmonic balance
- **PCB Layout:** KiCad (free, professional quality)
- **Measurement:** Network Analyzer (borrow from lab) for S-parameters

---

## References for Further Reading

Key papers to cite in your report:
- Rectangular patch efficiency at 2.4 GHz
- Arrays for gain improvement
- Schottky diode rectenna matching techniques
- CST simulation best practices for arrays

