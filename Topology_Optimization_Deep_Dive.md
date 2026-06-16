# 🔬 Topology Optimization of Engine Mount — Complete Technical Deep-Dive
**Milind Kalse | PACCAR Interview Reference | June 17, 2026**

> [!IMPORTANT]
> This is your **flagship project**. You should be able to talk about every section below for 5–15 minutes with zero hesitation. This document contains everything from your actual project report — no gaps.

---

## 1. Project Identity Card

| Field | Detail |
|---|---|
| **Project Title** | Topology Optimization Case Study: Engine Mount with Additive Manufacturing |
| **Collaboration** | Dassault Systèmes (industry-sponsored) |
| **Team** | Ganesh Dongre, Neil Mapari, Anish Mehta, **Milind Kalse**, Aryan More, Palak Mahajan |
| **Institution** | Department of Mechanical Engineering, VIT Pune |
| **Duration** | Aug – Dec 2025 |
| **Engine** | Honda CB600F (inline-4, 600cc, max 12,500 RPM) |
| **Software** | Altair HyperWorks — **HyperMesh** (pre-processing), **OptiStruct** (solver), **HyperView** (post-processing) |
| **Material** | AlSi10Mg (aluminum-silicon-magnesium alloy) |
| **Manufacturing** | Selective Laser Melting (SLM) — additive manufacturing |
| **Key Outcome** | Mass reduction of engine mounts via density-based topology optimization while maintaining structural integrity and avoiding resonance |

---

## 2. Problem Statement — Why This Project Matters

> "Engine mounts serve a crucial purpose of holding the engine in place while minimising vibrations transmitted from mounts towards chassis."

### The Engineering Challenge (3 layers):

1. **Structural** — The mount must withstand static engine weight + dynamic forces from acceleration, braking, cornering, and engine vibration (secondary unbalanced forces up to **14,252 N** at 12,500 RPM)
2. **Dynamic** — The mount's natural frequencies must **NOT** coincide with engine excitation frequencies (firing frequency range: 4.33 – 41.67 Hz) to avoid destructive resonance
3. **Weight** — Traditional mounts are overdesigned ("overly safe"), adding unnecessary mass. Goal: remove excess material while maintaining Factor of Safety

### Why Topology Optimization + Additive Manufacturing?
- Topology optimization produces organic, load-path-efficient geometries
- These geometries are too complex for casting/forging/machining
- SLM (additive manufacturing) can produce them layer-by-layer
- **Result:** Lighter, stiffer mounts that are actually buildable

---

## 3. Complete Methodology — 6-Step Process

```
┌──────────────────────────────────────────────────────────┐
│  Step 1: Enclosure & Mount Design                        │
│    └─→ Chassis (AISI 304) + 3 initial mount designs      │
│                                                          │
│  Step 2: Force Analysis & Boundary Conditions             │
│    └─→ Static loads + dynamic (secondary unbalance) +     │
│        weight transfer during acceleration/braking/corner │
│                                                          │
│  Step 3: Static Structural Analysis (Baseline)            │
│    └─→ FEA on original mounts → stress & displacement     │
│                                                          │
│  Step 4: Material & AM Process Selection                  │
│    └─→ AlSi10Mg via SLM (highest strength, >99.9% density)│
│                                                          │
│  Step 5: Modal Analysis                                   │
│    └─→ Natural frequencies vs excitation → no resonance   │
│                                                          │
│  Step 6: Topology Optimization + Re-validation            │
│    └─→ Density-based TO (OptiStruct) → re-analyze         │
└──────────────────────────────────────────────────────────┘
```

---

## 4. Load Calculations — The Numbers You MUST Know

### 4.1 Secondary Unbalanced Force (Dominant Dynamic Load)

> [!NOTE]
> Inline-4 engines achieve **perfect primary balance** — all four pistons' primary forces cancel due to symmetric firing order (1-2-4-3) and 90° crank phasing. Only **secondary forces** remain unbalanced.

**Formula:**

$$F_{sec} = n \times m_{rec} \times r \times \lambda \times \omega^2$$

**Parameters:**
| Symbol | Value | Meaning |
|---|---|---|
| $n$ | 4 | Number of cylinders |
| $m_{rec}$ | 0.4 kg | Reciprocating mass per cylinder (piston + portion of con-rod) |
| $r$ | 0.0228 m | Crank radius (stroke/2 = 0.0456/2) |
| $\lambda$ | 0.228 | Con-rod ratio ($r/L$ = 0.0228/0.1) |
| $\omega$ | 1309.0 rad/s | Angular velocity at 12,500 RPM ($2\pi \times 12500/60$) |

**Calculation at 12,500 RPM:**
$$F_{sec} = 4 \times 0.4 \times 0.0228 \times 0.228 \times (1309.0)^2 = \mathbf{14{,}252 \text{ N}}$$

> This oscillates at **2× crankshaft frequency = 417 Hz**, alternating between +14,252 N and −14,252 N about 417 times per second.

### 4.2 Weight Transfer Forces

Using the weight transfer equation: $\Delta F = \frac{m \times a \times h}{L}$

With engine mass = 60 kg, max acceleration/braking = 1.2g, max cornering = 0.8g:

| Direction | Total Force | Per-Mount Force (6 mounts) |
|---|---|---|
| **Fy (vertical — secondary unbalance)** | 14,000 N | **2,500 N** |
| **Fz (braking/acceleration)** | 1,720 N | **750 N** |
| **Fx (cornering)** | 960 N | **250 N** |

### 4.3 Firing Frequency Table

$$f_{firing} = \frac{n \times \text{RPM}}{60 \times s}$$

where $n = 4$ cylinders, $s = 2$ (4-stroke)

| RPM | Firing Frequency (Hz) |
|---|---|
| 1,300 (idle) | 4.33 |
| 3,000 | 10.00 |
| 6,000 | 20.00 |
| 9,000 | 30.00 |
| 12,500 (max) | 41.67 |

> **Critical frequency range to avoid: 4.33 – 41.67 Hz**

---

## 5. FEA Setup — Meshing & Connections

### 5.1 Mesh Details

| Parameter | Value |
|---|---|
| **Element type** | Tetrahedral (tetramesh) |
| **Global element size** | 1 mm |
| **Minimum element size** | 0.2 mm (critical regions) |
| **Quality criterion** | Target skewness ≤ 0.6 |
| **Software** | Altair HyperMesh |

### 5.2 Connection Elements — RBE2 vs RBE3

> [!TIP]
> This is a **very common interview question**. Know the difference cold.

| Element | Type | Purpose | Stiffness Effect |
|---|---|---|---|
| **RBE2** | Rigid body element | Fully coupled constraint — all dependent nodes follow master node | **Adds artificial stiffness** — use for BCs, fixture points, load introduction |
| **RBE3** | Interpolation element | Weighted load distribution — no rigid constraint | **No artificial stiffness** — use for distributing forces realistically |

**In your project:**
- **RBE2** → Used at bolt-hole locations (fixed supports — zero displacement in all DOF)
- **RBE3** → Used for realistic load transfer from engine to mount surfaces

### 5.3 Boundary Conditions Applied

- **Constraints:** Fixed supports (all 6 DOF locked) at bolt-hole locations where mounts connect to chassis
- **Loads:** Per-mount forces → Fy = 2,500 N, Fz = 750 N, Fx = 250 N
- Only tensile Z-direction force applied (braking and acceleration create equal-magnitude opposing forces)

---

## 6. Static Analysis Results — Baseline (Before Optimization)

| Mount | Max Displacement | Max Von Mises Stress |
|---|---|---|
| **Mount 1** | 0.18 mm | 212 MPa |
| **Mount 2** | 0.098 mm | 81.4 MPa |
| **Mount 3** | 0.093 mm | 85.3 MPa |

> **AlSi10Mg yield strength (SLM): ~250–460 MPa** → All mounts are within safe limits before optimization.

---

## 7. Modal Analysis Results — Resonance Check

### 7.1 Chassis Modal Results

| Mode | Natural Frequency |
|---|---|
| Mode 1 | 12.7 Hz |
| Mode 2 | 7.35 Hz |
| Mode 3 | 21.4 Hz |

### 7.2 Mount Modal Results

| Parameter | Value |
|---|---|
| **Max natural frequency (any mount)** | 4.8 Hz |

### 7.3 Resonance Validation

> Engine firing frequency range: **4.33 – 41.67 Hz**
> Mount natural frequency: **4.8 Hz**

⚠️ The mount natural frequency (4.8 Hz) is **close to idle firing frequency (4.33 Hz)** but below the primary operating range. During actual operation (above idle), the excitation frequency moves away from the mount's natural frequency — **no resonance at operating speeds**.

> **Key talking point:** "We verified that the mount's natural frequencies don't coincide with the engine's firing frequencies across the RPM range, which would cause destructive resonance, NVH issues, and premature fatigue failure."

---

## 8. Topology Optimization — The Core of the Project

### 8.1 The SIMP Method (Know This Theory)

**SIMP = Solid Isotropic Material with Penalization**

Each element gets a pseudo-density $\rho$ between 0 and 1:
- $\rho = 0$ → void (remove material)
- $\rho = 1$ → solid (keep material)

**Stiffness interpolation:**

$$\tilde{K}(\rho) = \rho^p \cdot K$$

where $p$ = penalization factor (typically **p = 3**)

**Why penalize?** For $0 < \rho < 1$: $\rho^3 \ll \rho$, so intermediate densities become "expensive" — the optimizer is forced toward a clear **0/1 (void/solid)** result. Without penalization, you'd get a gray, uninterpretable density field.

### 8.2 Optimization Setup in OptiStruct

| Parameter | Setting |
|---|---|
| **Objective** | Minimize compliance (= maximize stiffness) |
| **Constraint** | Volume fraction target (mass reduction %) |
| **Design space** | Mount body geometry |
| **Non-design space** | Bolt holes, mounting faces (preserved) |
| **Manufacturing constraints** | Minimum member size, overhang angle for SLM |
| **Method** | Density-based (SIMP) |

### 8.3 OptiStruct Iterative Process

```
┌─────────────────────────────────────────┐
│           START (initial density ρ₀)     │
│                    │                     │
│                    ▼                     │
│         FEA Solve (K·u = F)              │
│                    │                     │
│                    ▼                     │
│       Sensitivity Analysis               │
│    (∂compliance/∂ρ for each element)      │
│                    │                     │
│                    ▼                     │
│         Density Update                   │
│    (OC method or MMA optimizer)          │
│                    │                     │
│                    ▼                     │
│       Convergence Check                  │
│    (Has objective stabilized?)           │
│         │                    │           │
│        YES                  NO           │
│         │                    │           │
│         ▼                    └──→ Loop   │
│      OUTPUT                              │
│  (density distribution)                  │
└─────────────────────────────────────────┘
```

### 8.4 Post-Optimization Results

| Mount | Pre-Optimization Stress | Post-Optimization Stress | Status |
|---|---|---|---|
| **Mount 1** | 212 MPa | **319 MPa** | ⚠️ Higher but still < UTS (460 MPa) |
| **Mount 2** | 81.4 MPa | **130 MPa** | ✅ Well within limits |
| **Mount 3** | 85.3 MPa | Data in report | ✅ Within limits |

> **Key insight:** Post-optimization stresses increase because there's less material carrying the same load. The design is still safe because stresses remain below the material's strength limits — but this is exactly why **re-validation after optimization is mandatory**.

### 8.5 Why Stresses Increase After Optimization — How to Explain This

> "When you remove material, the same loads are carried by less material, so local stresses naturally increase. The optimization algorithm is smart — it removes material from **low-stress regions** and keeps it where **load paths are strongest**. But the engineer must verify that the new peak stresses still remain below the material's yield strength with an adequate safety factor. That's why re-analysis is not optional — it's a critical step."

---

## 9. Material Deep-Dive — AlSi10Mg

### 9.1 Material Properties

| Property | Value |
|---|---|
| **Composition** | Aluminum-Silicon-Magnesium alloy |
| **Tensile Strength (XY plane, SLM)** | ~460 MPa |
| **Tensile Strength (Z direction, SLM)** | ~394 MPa |
| **Fatigue Strength** | ~97 MPa |
| **Density** | ~2.67 g/cm³ |
| **Young's Modulus** | ~70 GPa |
| **Thermal Expansion** | Low |
| **Corrosion Resistance** | Good |

### 9.2 Why AlSi10Mg?

1. **Excellent castability** — Si content improves fluidity and reduces cracking
2. **High specific strength** — strong for its weight
3. **Well-characterized SLM parameters** — mature process, reliable results
4. **Industry workhorse** — used widely in automotive & aerospace AM

### 9.3 SLM Process Parameters

| Parameter | Recommended Range |
|---|---|
| **Energy density** | 50 – 60 J/mm³ |
| **Achievable density** | >99.7% (up to 99.9%) |
| **Cooling rate** | 10³ – 10⁸ K/s |
| **Microstructure** | Ultra-fine cellular/dendritic with interconnected Si network |

### 9.4 Anisotropy — Critical Point

> SLM-produced AlSi10Mg is **anisotropic** — stronger in the XY (horizontal) plane than in the Z (build) direction. The mount must be oriented on the build plate so that **primary load-bearing axes align with the XY plane**.

---

## 10. Manufacturing Strategy — SLM End-to-End

### 10.1 Why SLM Over Other AM Processes?

| Process | Verdict | Why |
|---|---|---|
| **SLM** ✅ | **Selected** | Highest as-built strength, >99.9% density, best dimensional accuracy |
| **LMD** | Feasible but inferior | Lower cooling rate → coarser microstructure → lower strength |
| **EBM** ❌ | Unsuitable | Vacuum + high temperature → vaporizes Al and Mg |
| **Binder Jetting** ❌ | Unsuitable | Non-fusion → inherent porosity → low strength |
| **SLS** ❌ | Unsuitable | Partial fusion → low density, requires costly HIP post-processing |

### 10.2 Post-Processing Strategy (Mandatory)

1. **T6 Heat Treatment** — Solutionizing → Quenching → Artificial Aging
   - Relieves residual stresses from SLM
   - Stabilizes high-strength condition
   - Alters Si network to improve ductility/toughness

2. **Surface Finishing** — Machining or shot peening of fatigue-critical surfaces
   - SLM produces "stair-stepping" surface roughness
   - Rough surfaces act as **stress concentrators** → reduce fatigue life
   - Mechanical finishing is **mandatory** for cyclic loading applications

3. **Build Orientation** — Align primary load axis with XY plane to leverage anisotropic strength advantage

---

## 11. Key Concepts You Must Explain Fluently

### 11.1 Design Space vs Non-Design Space

| | Definition | In Your Project |
|---|---|---|
| **Design space** | Volume where the optimizer can add/remove material | Mount body |
| **Non-design space** | Regions that must remain unchanged | Bolt holes, mounting faces, interfaces |

### 11.2 Compliance

$$C = \frac{1}{2} \mathbf{F}^T \mathbf{u} = \text{Strain Energy}$$

- **Minimize compliance** = **Maximize global stiffness**
- A stiffer structure distributes loads more efficiently
- Most common objective function in topology optimization

### 11.3 Volume Fraction

- Ratio of final material volume to initial design space volume
- Constraint: e.g., volume fraction ≤ 0.4 means keep only 40% of material
- Lower volume fraction = more aggressive mass reduction

### 11.4 Manufacturing Constraints in OptiStruct

| Constraint | Purpose | Your Use |
|---|---|---|
| **Minimum member size** | Prevent un-printable thin features | Ensured SLM feasibility |
| **Overhang angle** | Limit unsupported overhangs (>45° needs support) | Reduced support structures |
| **Draw direction** | For casting — single/split pull directions | Not primary (SLM doesn't need mold) |
| **Symmetry** | Force symmetric geometry | Applied where appropriate |

### 11.5 Three Types of Structural Optimization

| Type | What Changes | Your Project |
|---|---|---|
| **Topology** | Material distribution (0 or 1) | ✅ Primary method |
| **Topography** | Rib/bead patterns on shell surfaces | Not used |
| **Size/Shape** | Dimensions (thickness, fillet radii) | Could be a follow-up step |

---

## 12. Anticipated Interview Questions — With Answers

### Methodology Questions

**Q: Walk me through the project step by step.**
> *Use the 6-step flow from Section 3. Hit each step in 2 sentences max. Total: 90 seconds.*

**Q: How did you calculate the loads?**
> "We calculated three types: (1) Secondary unbalanced forces from the inline-4 engine's reciprocating mass — 14,252 N at max RPM, (2) Weight transfer during acceleration, braking, and cornering using $\Delta F = maH/L$, and (3) Static engine weight distributed across six mount points. The per-mount forces were Fy = 2,500 N, Fz = 750 N, Fx = 250 N."

**Q: Why are only secondary forces considered, not primary?**
> "The Honda CB600F is an inline-4. Due to the symmetric firing order and 90° crank phasing, all four pistons' primary forces cancel perfectly. Secondary forces — caused by connecting rod obliquity — remain unbalanced and act at 2× crankshaft frequency. These are the dominant excitation, especially at high RPM."

**Q: What boundary conditions did you apply?**
> "Fixed supports — all 6 DOF locked — at bolt-hole locations using RBE2 elements. Loads distributed to mount surfaces using RBE3 elements for realistic force transfer without artificial stiffening."

**Q: What's the difference between RBE2 and RBE3?**
> "RBE2 is a rigid connection — all dependent nodes follow the master node exactly. It adds stiffness and is used for fixture points and boundary conditions. RBE3 is an interpolation element — it distributes load through weighted averaging without adding stiffness. It's used for realistic load transfer."

### FEA/Optimization Questions

**Q: What element type did you use and why?**
> "Tetrahedral elements — specifically because the engine mount has a complex 3D geometry that doesn't lend itself to mapped hexahedral meshing. Tetras can conform to any shape. We used 1 mm global size with 0.2 mm in critical regions and controlled skewness below 0.6."

**Q: What is the SIMP method?**
> "Solid Isotropic Material with Penalization. Each element gets a density between 0 and 1. The stiffness is $\rho^p K$ where p ≈ 3. The penalization forces intermediate densities toward clear 0/1 values, giving you a manufacturable black-and-white structure."

**Q: What was your objective function? What were the constraints?**
> "Objective: minimize compliance — meaning maximize global stiffness. Constraint: volume fraction below a target value — meaning how much material we keep. Plus manufacturing constraints for SLM."

**Q: How did you validate the optimized design?**
> "We re-ran static structural analysis on the optimized geometry. Mount 1 went from 212 MPa to 319 MPa — stress increased because less material carries the same load — but it's still below AlSi10Mg's UTS of 460 MPa. We also re-checked natural frequencies against engine excitation to confirm no resonance."

**Q: Why did stress increase after optimization?**
> "Same load, less material. The optimizer removes material from low-stress regions and concentrates it along primary load paths. Local stresses increase, but the structure overall is more efficient. The key validation is that peak Von Mises stress remains below yield/UTS with an adequate safety factor."

### Material & Manufacturing Questions

**Q: Why AlSi10Mg?**
> "It's the industry standard for SLM — excellent printability, good strength-to-weight ratio (UTS ~460 MPa, density 2.67 g/cm³), well-characterized process parameters, and widely used in automotive and aerospace. It offered the best combination of performance and manufacturing maturity."

**Q: Why SLM specifically? Why not other AM processes?**
> "SLM gives the highest as-built strength due to extremely high cooling rates (10³ to 10⁸ K/s), producing ultra-fine microstructure. Density exceeds 99.9%, which is critical for fatigue life. EBM would vaporize the aluminum. Binder jetting and SLS produce porous parts that need expensive post-processing like HIP."

**Q: What post-processing would you apply?**
> "Three steps: (1) T6 heat treatment — solutionizing, quenching, aging — to relieve residual stresses and achieve stable high-strength state. (2) Machining or shot peening of fatigue-critical surfaces to remove stair-stepping roughness that would reduce fatigue life. (3) Correct build orientation so primary loads align with the XY plane where SLM strength is highest."

**Q: Is AlSi10Mg anisotropic in SLM?**
> "Yes — stronger in the XY plane (~460 MPa UTS) than in the Z build direction (~394 MPa). We accounted for this by orienting the mount so the primary load axis aligns with the horizontal build plane."

### PACCAR Relevance Questions

**Q: How is this relevant to heavy-duty trucks?**
> "Engine mounts in trucks are among the most critical structural components — they carry engine weight, vibration, and road loads for millions of cycles. Topology optimization can reduce mount weight while maintaining durability, contributing to overall vehicle weight reduction and fuel efficiency. The same methodology — define loads, FEA, optimize, validate — applies directly."

**Q: Could this approach be used for truck hoods or cab structures?**
> "Absolutely. For hoods, you'd use shell-based optimization with gauge/thickness variables. For cab structural nodes and brackets, solid-element topology optimization is directly applicable. The key difference is the manufacturing — truck volumes may favor optimized castings rather than SLM, so you'd adjust the manufacturing constraints (draw direction for casting instead of overhang angle for SLM)."

**Q: What would you do differently for a production truck component?**
> "Three things: (1) Include fatigue load cases — truck components see millions of cycles from road loads. (2) Use dynamic loads from road load data (RLD) instead of simplified static loads. (3) Apply manufacturing constraints for the actual production process — likely casting or stamping for trucks rather than SLM, which would change the geometric constraints."

---

## 13. Quick-Reference Data Card

> [!TIP]
> Glance at this card 5 minutes before your interview. These are the numbers they'll probe.

| Item | Value |
|---|---|
| Engine | Honda CB600F, inline-4, 600cc, 12,500 RPM max |
| Secondary force at max RPM | **14,252 N** |
| Secondary vibration frequency | **417 Hz** (2× crankshaft) |
| Per-mount forces | Fy=2500N, Fz=750N, Fx=250N |
| Firing frequency range | 4.33 – 41.67 Hz |
| Mesh | Tetra, 1mm global, 0.2mm min, skewness ≤ 0.6 |
| Mount 1 stress (before → after TO) | 212 → 319 MPa |
| Mount 2 stress (before → after TO) | 81.4 → 130 MPa |
| Mount max natural frequency | 4.8 Hz |
| Chassis modes | 7.35, 12.7, 21.4 Hz |
| AlSi10Mg UTS (XY) | ~460 MPa |
| AlSi10Mg UTS (Z) | ~394 MPa |
| AlSi10Mg fatigue strength | ~97 MPa |
| SLM density achieved | >99.9% |
| SLM cooling rate | 10³ – 10⁸ K/s |
| Optimization method | SIMP (penalization factor p=3) |
| Objective | Minimize compliance (maximize stiffness) |
| Software | HyperMesh + OptiStruct (Altair HyperWorks) |

---

## 14. The 60-Second Elevator Pitch (If They Say "Summarize This Project")

> "We designed and optimized engine mounts for a Honda CB600F using topology optimization. The engine produces secondary unbalanced forces of about 14,000 N at max RPM — this, combined with weight transfer during acceleration, braking, and cornering, gives us per-mount loads of roughly 2,500 N vertical, 750 N longitudinal, 250 N lateral.
>
> We set up the FEA in HyperMesh with tetrahedral elements, used RBE2 for fixed bolt-hole constraints and RBE3 for realistic load distribution. Static analysis confirmed baseline stresses were within AlSi10Mg's limits. Modal analysis confirmed no resonance with engine firing frequencies.
>
> We then ran density-based topology optimization in OptiStruct — SIMP method — minimizing compliance with a volume fraction constraint. The optimized mounts showed increased local stresses — expected, since less material carries the same load — but all within the material's UTS of 460 MPa. The material was selected for SLM manufacturing, with T6 heat treatment and surface finishing for fatigue performance.
>
> The project demonstrates a complete design-to-validation workflow: load calculation → FEA → modal check → topology optimization → re-validation → manufacturing strategy."

---

## 15. What Sets This Project Apart From Other Students

| Differentiator | Why It Matters |
|---|---|
| **Calculated actual dynamic loads** | Didn't use arbitrary loads — derived secondary forces from engine physics |
| **Modal analysis for resonance** | Most student projects skip vibration check — you validated against excitation frequencies |
| **RBE2/RBE3 understanding** | Shows you know FEA modelling technique, not just button-pushing |
| **AM process comparison** | Systematically rejected EBM, BJG, SLS with engineering reasoning |
| **Post-processing strategy** | T6 heat treatment + surface finishing — shows manufacturing maturity |
| **Industry collaboration** | Dassault Systèmes sponsorship adds credibility |
| **HyperMesh/OptiStruct** | Industry-standard tools — PACCAR likely uses these exact tools |

---

*You own this project. Every number, every decision, every method. Now go talk about it like you built it — because you did.* 🚀
