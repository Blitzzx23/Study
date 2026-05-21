# ⚙️ Unit I — Introduction, Sensors & Actuators

---

## 🔷 What is Mechatronics?

> [!NOTE]
> Mechatronics is the **synergistic integration** of mechanical engineering, electronics, and control systems to design intelligent products and processes.

Three core ideas:
- Adding **electronic control** to a mechanical system
- **Enhancing** existing mechanical designs with intelligent control
- **Replacing** mechanical components with electronic solutions

**Key concept:** Energy conversion and transfer between interconnected subsystems.

**Sub-disciplines involved:**

| Mechanical | Electrical | Control |
|---|---|---|
| Thermodynamics | Electronics | Instrumentation |
| Fluid Mechanics | Electrical Machinery | PLC / Logic |
| Hydraulics & Pneumatics | Microelectronics | Software Programming |

**Real examples:** CNC machines · Washing machines · Centre lathes · Automated assembly cells

---

## 🔷 Design of Mechatronic Systems

| Stage | Description |
|---|---|
| **1. Modeling & Simulation** | Physical system is represented as a mathematical/computational model and analysed via simulation before building |
| **2. Prototyping** | Actual hardware (sensors, actuators) is interfaced with partial models and synchronised to validate the design |
| **3. Deployment** | Final product — software deployment, manufacturing, and lifecycle testing |

---

## 🔷 Measurement System

> [!NOTE]
> A **measurement system** measures a required physical parameter.
> **Input** = quantity being measured | **Output** = measured value in usable form

**Example:** Digital Tachometer
- Input → shaft rotation
- Output → speed displayed on LED

---

## 🔷 Control Systems

### Open-Loop vs Closed-Loop

| Feature | Open-Loop | Closed-Loop |
|---|---|---|
| **Feedback** | ❌ None | ✅ Present |
| **Self-correction** | No | Yes |
| **Effect of disturbance** | Large | Reduced |
| **Example** | Timer-controlled boiler | Thermostat-controlled heater |

> [!IMPORTANT]
> **Feedback** = adjusting future actions based on information about past performance.
> **Disturbance** = unwanted signal affecting output — its effect is reduced by feedback.

### Real-World Control Examples

| System | Sensor | Actuator | Controller |
|---|---|---|---|
| Toilet tank | Floater | Pin valve | Lever arm |
| Robot arm | Potentiometer | DC motor | Op-amp circuit |
| Air pressure vessel | Pressure sensor | Control valve | Electronic controller |

---

## 🔷 Static Characteristics of Measurement Systems

> [!TIP]
> Static characteristics describe **steady-state performance** — how well the instrument measures when nothing is changing.

| Characteristic | Definition |
|---|---|
| **Accuracy** | Closeness of reading to the true value |
| **Sensitivity** | Smallest detectable change; = ΔOutput / ΔInput |
| **Linearity** | Output increases proportionally and symmetrically with input |
| **Reproducibility** | Consistency of readings over an extended time period |
| **Repeatability** | Variation of readings in a single session (random nature) |
| **Resolution** | Smallest input increment that produces a detectable output change |
| **Threshold** | Minimum input below which no output change is detected |
| **Drift** | Slow unintended change in output without any change in input |
| **Stability** | Ability to maintain performance over its operating life |
| **Tolerance** | Maximum allowable measurement error |
| **Range / Span** | Minimum to maximum measurable values |

---

## 🔷 Dynamic Characteristics of Measurement Systems

> [!TIP]
> Dynamic characteristics describe how the instrument **behaves when the measurand is changing with time**.

| Characteristic | Definition |
|---|---|
| **Speed of Response** | Rapidity with which the system reacts to measurand changes |
| **Measuring Lag** | Delay before the system begins to respond |
| **Fidelity** | Degree to which the system follows changes without dynamic error |
| **Dynamic Error** | Difference between the true changing value and the indicated value |

---

## 🔷 Sensors & Transducers

> [!NOTE]
> A **sensor / transducer** is a device that provides a usable **electrical output** in response to a specified **physical measurand** (quantity, property, or condition).

---

### 📍 Displacement, Position & Proximity Sensors

| Sensor | Working Principle | Applications |
|---|---|---|
| **Potentiometer** | Moving wiper changes resistance → proportional voltage output. Resolution: ±0.01% (wire-wound), ~0.1 µm (conductive plastic) | Machine-tool controls, elevators, throttle controls |
| **LVDT** | Linear Variable Differential Transformer — uses electromagnetic induction to measure linear displacement | High-precision displacement measurement |
| **Eddy Current** | AC magnetic field induces eddy currents in conductive material; disturbance is measured | Precision automation, machine tool monitoring, vibration measurement |
| **Hall Effect** | Magnetic field produces a transverse voltage across a current-carrying conductor. Operates at 100 kHz, non-contact | Fluid level, displacement & position detection in industrial automation |
| **Pneumatic** | Air pressure used to detect proximity or position | General proximity sensing |

---

### 🌡️ Temperature Sensors

| Sensor | Principle | Key Formula / Detail |
|---|---|---|
| **Bimetallic Strip** | Two bonded metals with different expansion coefficients — strip bends when heated | Used in simple thermostats |
| **RTD** | Resistance of metal **increases** with temperature | `Rt = R₀(1 + αT)` where α = temp. coefficient |
| **Thermistor (NTC)** | Semiconductor resistance **decreases** with temperature; nonlinear response | Bead size: 0.5–5 mm; used in engines, thermostats, 3D printers |
| **Thermocouple** | Seebeck Effect (1821): dissimilar metal junction heated → EMF produced | `ΔVAB = α · ΔT` where α = Seebeck coefficient |

> [!IMPORTANT]
> **RTD** → resistance goes **UP** with temperature.
> **Thermistor (NTC)** → resistance goes **DOWN** with temperature.

---

### 💪 Force, Pressure & Flow Sensors

| Sensor | Principle |
|---|---|
| **Strain Gauge** | Deformation changes electrical resistance of a bonded conductor — used in load cells |
| **Piezoelectric Sensor** | Mechanical stress on certain crystals produces an electric charge |
| **Diaphragm / Capsule** | Fluid pressure deflects a flexible membrane — deflection is measured |
| **Orifice Plate** | Flow measured via pressure drop across a constriction |
| **Turbine Meter** | Flow rate proportional to turbine rotation speed |

---

## 🔷 Actuators

> [!NOTE]
> An **actuator** receives a low-energy control signal and converts its primary energy source into **mechanical motion**.

| Type | Principle | Key Details |
|---|---|---|
| **Mechanical** | Converts rotary → linear motion via gears, pulleys, chains, springs | Example: chain block hoist |
| **Pneumatic** | Compressed air drives a piston in a cylinder | Produces linear or rotary motion; faster start/stop; safer & cheaper |
| **Hydraulic** | High-pressure fluid drives a cylinder or fluid motor | Liquid is incompressible → higher force; used for heavy loads |
| **Electrical** | EMF produces mechanical torque via electromagnetic effect | Cleanest type; examples: electric motor, solenoid valve |
| **Hybrid** | Combination of any two types above | Example: thermo-hydraulic electronic valve actuator |

### Hydraulic Cylinder — Single vs Double Acting

| Type | How it Works |
|---|---|
| **Single Acting** | Fluid pressure on **one side only**; spring provides the return stroke |
| **Double Acting** | Fluid pressure on **both sides**; side with higher pressure determines direction |

> [!TIP]
> **Hydraulic vs Pneumatic:** Hydraulic uses liquid → higher force, incompressible. Pneumatic uses air → faster, safer, cheaper but lower force.
