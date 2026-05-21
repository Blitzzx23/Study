# 📐 Unit II — System Models

---

## 🔷 Why Do We Model Systems?

> [!NOTE]
> **Modeling** means representing a real physical system using a suitable alternative form so that its behavior can be studied and predicted **without building it first**.

**Types of models:**

| Type | Description |
|---|---|
| Mathematical Model | Governing equations derived from physical laws |
| Graphical Model | Block diagrams, signal flow graphs |
| Prototype Model | Partial physical model for validation |
| FEA Model | Finite Element Analysis — numerical simulation |
| CAD Model | 3D geometry representation |

**Why model?** → Understand & predict behavior · Study parameter effects · Support R&D & optimization

> [!IMPORTANT]
> All models use **lumped parameter building blocks** with appropriate assumptions and simplifications. Analogy between different system types (electrical, mechanical, hydraulic) is a key concept.

---

## 🔷 1. Mechanical System — Translational

**Input:** Force (F) | **Output:** Displacement (x)

| Building Block | Symbol | Governing Equation | Energy Behaviour |
|---|---|---|---|
| **Spring** (stiffness k) | k | `F = k·x` | Stores: `E = ½·k·x²` |
| **Dashpot / Damper** (c) | c | `F = c·(dx/dt)` | Dissipates: `E = c·v²` |
| **Mass** (inertia m) | m | `F = m·(d²x/dt²)` | Stores: `E = ½·m·v²` |

**Applications:** Machine mounted on ground · Automobile suspension · Passenger-in-car model

---

## 🔷 2. Rotational System

**Input:** Torque (T) | **Output:** Angular Displacement (θ)

| Translational Equivalent | Rotational Building Block |
|---|---|
| Spring | **Torsional Spring** — rotational stiffness |
| Dashpot | **Rotary Damper** — torque opposing angular motion |
| Mass | **Moment of Inertia** — resistance to angular acceleration |

---

## 🔷 3. Electrical System

**Input:** Supply voltage (V) or current (i) | **Output:** Voltage across a component

| Component | Governing Equation | Energy Behaviour |
|---|---|---|
| **Resistor (R)** | `v = R·i` | Dissipates: `P = v²/R` |
| **Capacitor (C)** | `i = C·(dv/dt)` ; `q = ∫i·dt` | Stores: `E = ½·C·v²` |
| **Inductor (L)** | `v = L·(di/dt)` | Stores: `E = ½·L·i²` |

> [!TIP]
> **Kirchhoff's Laws:**
> - **KCL (Law 1):** Sum of currents at any junction = 0
> - **KVL (Law 2):** Sum of voltages around any closed loop = 0

---

## 🔷 Electrical ↔ Mechanical Analogy

> [!IMPORTANT]
> Both systems follow the **same mathematical equations**. Knowing one helps you solve the other.

| Electrical System | Mechanical System | Behaviour |
|---|---|---|
| **Resistor** | **Dashpot** | Dissipates energy |
| **Inductor** | **Mass** | Stores kinetic energy |
| **Capacitor** | **Spring** | Stores potential energy |
| **Voltage (V)** | **Force (F)** | Driving quantity |
| **Current (I)** | **Velocity (v)** | Response quantity |

---

## 🔷 4. Hydraulic System

**Input:** Liquid inflow (q) | **Output:** Liquid height (h) in container

| Building Block | Formula | Analogy |
|---|---|---|
| **Hydraulic Resistance (R)** | `P₁ – P₂ = R·q` | Electrical Resistor |
| **Hydraulic Capacitance** `C = A/ρg` | `q₁ – q₂ = C·(dp/dt)` | Electrical Capacitor |
| **Hydraulic Inertance** `I = L·ρ/A` | `P₁ – P₂ = I·(dq/dt)` | Electrical Inductor |

> [!NOTE]
> The PDF also covers **Pneumatic** and **Thermal** systems, and **combinational systems** — e.g., electrical-mechanical, hydraulic-mechanical, and rotational-translational combinations.

---

## 🔷 Summary — System Analogy Table

| Quantity | Mechanical | Rotational | Electrical | Hydraulic |
|---|---|---|---|---|
| **Driving input** | Force (F) | Torque (T) | Voltage (V) | Pressure (P) |
| **Response output** | Displacement (x) | Angle (θ) | Charge (q) | Volume flow (q) |
| **Energy dissipator** | Dashpot | Rotary damper | Resistor | Hydraulic resistance |
| **Energy storage (kinetic)** | Mass | Moment of inertia | Inductor | Hydraulic inertance |
| **Energy storage (potential)** | Spring | Torsional spring | Capacitor | Hydraulic capacitance |
