# 📈 Unit III — Dynamic Response of Systems

---

## 🔷 Types of System Responses

| Response Type | Description |
|---|---|
| **Natural Response** | System behavior with no external input — decays on its own |
| **Forced Response** | Response produced by a sustained external input |
| **Transient Response** | Initial part of response before the system settles |
| **Steady-State Response** | Final settled output value after transient dies out |

**Standard test inputs used in analysis:**

| Input Type | Shape | Laplace Transform |
|---|---|---|
| **Impulse** | Instantaneous spike | `1` |
| **Step** | Sudden jump to constant value | `1/s` |
| **Ramp** | Linearly increasing | `1/s²` |

---

## 🔷 First-Order Systems

> [!NOTE]
> A first-order system has **one energy storage element** and is governed by a first-order differential equation.

### Time Constant (τ)

> [!IMPORTANT]
> **τ is the time at which the output reaches 63% of its steady-state value.**
> `τ = a₁/a₀`

| Time | % of Steady-State Value Reached |
|---|---|
| t = τ | **63%** |
| t = 2τ | 86% |
| t = 3τ | **95%** ← practical settling point |
| t = 5τ | ~99% |

**Standard first-order equation:**
```
τ·(dy/dt) + y = Gss · u
```

**Transfer Function (1st order):**
```
G(s) = Gss / (τs + 1)
```

**Step response:**
```
y(t) = Gss · (1 – e^(–t/τ))
```

---

## 🔷 Second-Order Systems

> [!NOTE]
> Second-order systems are analogous to a **spring-mass-damper** system. The response character depends on the **damping factor ζ (zeta)**.

### Damping Conditions

| Condition | ζ Value | Response |
|---|---|---|
| **Undamped** | ζ = 0 | Oscillates indefinitely |
| **Underdamped** | 0 < ζ < 1 | Oscillates, then settles |
| **Critically Damped** | ζ = 1 | Fastest settle, no oscillation |
| **Overdamped** | ζ > 1 | Slow, no oscillation |

**Key formulas:**

```
Natural frequency:    ωn = √(a₀/a₂)
Damping factor:       ζ  = √(a₁² / 4·a₀·a₂)
Damped frequency:     ω  = ωn · √(1 – ζ²)
```

### Performance Measures

| Measure | Formula |
|---|---|
| **Rise Time (tr)** | `π / 2ω` |
| **Peak Time (tp)** | `π / ω` |
| **% Overshoot** | `e^(–ζπ/√(1–ζ²)) × 100%` |
| **Settling Time (2%)** | `4 / (ζ·ωn)` |
| **Settling Time (5%)** | `3 / (ζ·ωn)` |

> [!TIP]
> **Exam Example (RLC circuit):** R = 100Ω, L = 2H, C = 20µF
> → ωn = 158 rad/s · ζ = 0.16 → **Underdamped** · ω = 156 rad/s

---

## 🔷 Transfer Function Method

> [!NOTE]
> The **transfer function G(s)** = Laplace Transform of Output / Laplace Transform of Input (at zero initial conditions).

### Procedure

```
Step 1 → Take L.T. of system differential equation
Step 2 → Output(s) = G(s) × Input(s)
Step 3 → Match with standard inverse L.T. table
Step 4 → Take Inverse L.T. → get y(t)
```

**Standard TF forms:**

```
1st order:   G(s) = Gss / (τs + 1)

2nd order:   G(s) = ωn² / (s² + 2ζωns + ωn²)
```

### Systems in Series & Feedback

| Configuration | Formula |
|---|---|
| **Systems in Series** | `G_total = G1 · G2 · G3` |
| **Closed-Loop (with feedback H)** | `G_cl = G(s) / [1 + G(s)·H(s)]` |

---

## 🔷 Bode Plots & Frequency Response

> [!NOTE]
> The **frequency transfer function** G(jω) = output phasor / input phasor, where a phasor has magnitude, frequency, and phase.

A **Bode plot** consists of two graphs plotted on a **logarithmic frequency scale**:

| Graph | What is Plotted | Unit |
|---|---|---|
| **Magnitude plot** | \|G(jω)\| vs ω | dB |
| **Phase plot** | Phase angle φ vs ω | Degrees |

**Magnitude in decibels:**

| dB Value | Actual Magnitude | Meaning |
|---|---|---|
| 0 dB | 1× | Output = Input |
| 20 dB | 10× | Output is 10× input |
| 40 dB | 100× | Output is 100× input |

**Break-point (corner) frequency:**

| System Order | Break-Point Frequency |
|---|---|
| 1st order | `ω = 1/τ` |
| 2nd order | `ω = ωn` |

---

## 🔷 Closed-Loop Controllers

| System | Description |
|---|---|
| **Open-loop** | Input does NOT depend on output — no feedback |
| **Closed-loop** | Feedback compares actual output with desired; controller corrects the error |

**Disturbance** = unwanted signal affecting output. Its effect is **reduced by feedback**.

### Control Modes

| Mode | Correcting Signal | Key Property |
|---|---|---|
| **ON/OFF (Two-step)** | Binary — fully ON or OFF based on error | Simple; causes oscillation around setpoint |
| **Proportional (P)** | Proportional to **current error** | Fast; leaves a permanent **steady-state offset** |
| **Derivative (D)** | Proportional to **rate of change of error** | Anticipatory; reduces overshoot; cannot work alone |
| **Integral (I)** | Proportional to **accumulated (integral of) error** | Eliminates steady-state offset; slower response |
| **PD** | P + D | Faster response, reduced overshoot |
| **PI** | P + I | Eliminates steady-state error |
| **PID** | P + I + D | Best overall performance |

> [!IMPORTANT]
> - **P** → acts on the **present** error
> - **I** → acts on the **past** (accumulated) error
> - **D** → acts on the **future** (predicted) error
