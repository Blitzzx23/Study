# 🔧 Mechatronics & Control Systems — Viva Notes
> All technical terms kept. Sentences written to be clear and easy to understand.

---

## UNIT I — Introduction to Mechatronics, Sensors & Actuators

### What is Mechatronics?
Mechatronics is the integration of electronics and control into mechanical systems. The goal is to either enhance an existing mechanical design with intelligent control, or replace purely mechanical components with electronic solutions. The key concept is energy conversion — different subsystems convert and transfer energy to achieve the desired function.

Sub-fields that come together in mechatronics: Thermodynamics, Fluid Mechanics (Hydraulics & Pneumatics), Electronics, Electrical Machinery, Microelectronics, Logic Functions, PLC, Software Programming, and Instrumentation & Control.

**Examples of mechatronic systems:** CNC machines, washing machines, centre lathes, automated assembly cells, automated packaging systems.

---

### Design of Mechatronic Systems — 3 Concepts

**1. Modeling and Simulation**
Physical systems are represented using mathematical or computational models. The model is analysed through numerical simulation, which guides the design process before anything is physically built.

**2. Prototyping**
Partial mathematical models are combined with actual hardware (sensors, actuators). The real hardware is interfaced with input/output signals and synchronized with the model to validate the design.

**3. Deployment**
This is the final stage — the product is manufactured, software is deployed, and the system is tested for real-world use.

---

### Measurement System
A measurement system is used to measure a required parameter. The **input** is the quantity being measured, and the **output** is the measured value presented in a usable form.

**Example:** A digital tachometer — Input is the rotation of a shaft; Output is the speed shown on an LED display.

---

### Control System
A control system is a group of physical components connected to command, direct, or regulate itself or another system. The components can be electrical, mechanical, hydraulic, pneumatic, thermal, or chemical in nature.

**Open-loop control system:** The control action is independent of the actual process output. There is no feedback. For example, a boiler controlled only by a timer runs for a fixed duration regardless of the actual building temperature.

**Closed-loop control system:** The control action depends on comparing the desired output with the actual output. A thermostat, for example, monitors the building temperature and feeds that information back so the controller can adjust the heating to maintain the setpoint. This is why closed-loop systems are also called **feedback control systems**.

**Feedback** is the process of adjusting future actions based on information about past performance.

**Disturbance** is any unwanted signal that affects the system output. Feedback reduces the effect of disturbances.

**Real-world examples:**
- Toilet tank water level: floater = sensor, pin valve = actuator, lever arm = controller.
- Single-link robot arm: potentiometer = sensor, DC motor = actuator, op-amp circuit = controller.

---

### Static Characteristics of Measurement Systems

These characteristics describe the **steady-state performance** of a measurement system — how well it measures when things aren't changing.

| Term | What it means |
|---|---|
| **Accuracy** | How close the measured reading is to the true value of the quantity |
| **Sensitivity** | The smallest change in the measurand that the instrument can detect; defined as ΔOutput / ΔInput |
| **Linearity** | The ability of the instrument to reproduce input characteristics in a symmetrical, linear manner |
| **Reproducibility** | How consistently the same value is obtained when measured repeatedly over time |
| **Repeatability** | The variation in readings taken in a single session; this variation is random in nature |
| **Resolution** | The smallest increment in input that produces a detectable change in output |
| **Threshold** | The minimum input value below which no output change can be detected at all |
| **Drift** | A slow, unintended change in output reading even though the input hasn't changed |
| **Stability** | The ability of the instrument to maintain its performance throughout its specified operating life |
| **Tolerance** | The maximum allowable error permitted in a measurement |
| **Range / Span** | The minimum and maximum values of the quantity that the instrument is designed to measure |

---

### Dynamic Characteristics of Measurement Systems

These characteristics describe how a measurement system **behaves when the measurand is changing with time**.

| Term | What it means |
|---|---|
| **Speed of Response** | How rapidly the system responds to changes in the measurand |
| **Measuring Lag** | The delay (retardation) between the actual change and the system's response to it |
| **Fidelity** | The degree to which the system follows changes in the measurand without dynamic error |
| **Dynamic Error** | The difference between the true changing value and the value indicated by the system |

---

### Sensors & Transducers

A **sensor (transducer)** is a device that provides a usable output — usually an electrical signal — in response to a specified measurand (a physical quantity, property, or condition).

Sensors are essential in manufacturing for automatic production and process monitoring. They reduce the need for skilled labor, minimize system downtime, and enable ultra-precision in product quality.

---

#### Classification of Sensors

**A. Displacement, Position & Proximity Sensors**

**Potentiometer:** Uses a wire-wound or conductive plastic track. As the object moves, the wiper changes resistance, which produces a proportional output voltage. Resolution of wire-wound type is ±0.01%; conductive plastic type is ~0.1 µm. Applications: machine-tool controls, elevators, liquid-level assemblies, automobile throttle controls.

**LVDT (Linear Variable Differential Transformer):** Measures linear displacement using electromagnetic induction. Very high accuracy and resolution.

**Eddy Current Sensor:** Generates an alternating magnetic field that induces eddy currents in any nearby conductive (but non-magnetic) material. The change in these currents is used to detect proximity or displacement. Applications: precision automation, machine tool monitoring, vibration measurement. Works even in oily or dirty environments.

**Hall Effect Sensor:** Detects the presence and strength of a magnetic field and converts it to an electrical signal. Operates at 100 kHz; non-contact in nature; excellent immunity to environmental contaminants. Applications: fluid level measurement, displacement detection, position detection in industrial automation.

**Pneumatic Sensor:** Uses air pressure to detect proximity or position.

---

**B. Temperature Sensors**

**Bimetallic Strip:** Consists of two metals bonded together. Since different metals have different coefficients of thermal expansion, the strip bends when heated. Used in simple thermostats and temperature-activated switches.

**RTD (Resistance Temperature Detector):** Based on the principle that the electrical resistance of a metal increases with temperature. The governing equation is:

**Rt = R₀ (1 + αT)**

where Rt = resistance at temperature T, R₀ = resistance at 0°C, α = temperature coefficient of resistance.

Applications: food processing, HVAC, petrochemical processing, micro-electronics.

**Thermistor:** A semiconductor device (typically sintered metal oxide or doped polycrystalline ceramic) whose resistance **decreases** with increasing temperature (NTC — Negative Temperature Coefficient). Exhibits nonlinear response. The bead dimension is 0.5 mm to 5 mm, coated in ceramic or glass, and enclosed in a stainless steel tube. Applications: engine coolant temperature monitoring, digital thermostats, 3D printer hot-ends, battery pack temperature monitoring.

**Thermocouple:** Based on the **Seebeck Effect (1821)** — when two wires of dissimilar metals are joined at both ends and one junction is heated, a continuous EMF is produced in the circuit. The open-circuit voltage is:

**ΔVAB = α · ΔT**

where α is the Seebeck coefficient.

---

**C. Force & Pressure Sensors**

**Strain Gauge (Force Sensor):** A thin electrical conductor whose resistance changes when mechanically deformed. Bonded to a load cell structure, it measures force indirectly through deformation.

**Piezoelectric Sensor:** Certain crystals produce an electric charge when subjected to mechanical stress. Used for dynamic force and pressure measurements.

---

**D. Flow & Level Sensors**
- Liquid flow: Orifice plate, Turbine meter
- Liquid level: Floats, Differential pressure sensors

---

**E. Light Sensors**
- Photodiodes, Photo resistors, Photo transistors

---

### Actuators

An **actuator** is a component that receives a control signal and converts it into mechanical motion. It requires both a control signal (low-energy input — electrical, pneumatic, or hydraulic) and a primary energy source. When the control signal is received, the actuator converts the energy into the required mechanical motion.

| Type | Principle | Key Details |
|---|---|---|
| **Mechanical** | Converts rotary motion to linear motion | Uses gears, rails, pulleys, chains, springs |
| **Pneumatic** | Compressed air drives a piston in a cylinder | Produces linear or rotary motion; safer, cheaper, reliable; ideal for quick start/stop |
| **Hydraulic** | High-pressure hydraulic fluid drives a cylinder or fluid motor | Liquid is incompressible → generates higher force than pneumatic; used for heavy loads |
| **Electrical** | Electromagnetic force (EMF) produces mechanical torque | Cleanest actuator type; examples: electric motor, solenoid valve |
| **Hybrid** | Combination of any two of the above types | Example: thermo-hydraulic electronic actuator in hot water valve systems |

**Hydraulic Cylinder — Single vs Double Acting:**
- **Single acting:** Fluid pressure is applied to only one side of the piston. A spring provides the return stroke.
- **Double acting:** Fluid pressure is applied to both sides of the piston. The side with higher pressure determines the direction of motion.

---

## UNIT II — System Models (From PDF)

### Why Model a System?
Modeling means representing a real physical system through a suitable alternative form — most commonly a **mathematical model**. Other forms include graphical models, prototype models, FEA models, and CAD models.

The purpose of modeling is to understand and predict system behavior, study the effect of various parameters, and support research, optimization, and design — without needing to build the actual system first.

Important considerations: all models involve **assumptions and simplifications**. The model uses **lumped parameter building blocks**, with mathematical equations and energy considerations for each block.

---

### 1. Mechanical System (Translational)
**Input:** Force (F) | **Output:** Displacement (x)

| Building Block | Equation | Energy Behaviour |
|---|---|---|
| **Spring** (stiffness) | F = kx | Stores energy: E = ½kx² |
| **Dashpot / Damper** | F = c(dx/dt) | Dissipates energy: E = cv² |
| **Mass** (inertia) | F = m(d²x/dt²) | Stores energy: E = ½mv² |

Applications: machine mounted on ground, automobile suspension, passenger-in-car model.

---

### 2. Rotational System
**Input:** Torque (T) | **Output:** Angular Displacement (θ)

| Building Block | Role |
|---|---|
| **Torsional Spring** | Stiffness of the rotational system |
| **Rotary Damper** | Torque opposing rotational motion |
| **Moment of Inertia** | Resistance to angular acceleration |

---

### 3. Electrical System
**Input:** Supply voltage (V) or current (i) | **Output:** Voltage across a component

| Component | Governing Equation | Energy Behaviour |
|---|---|---|
| **Inductance (L)** | v = L(di/dt) | Stores energy: E = ½Li² |
| **Capacitance (C)** | i = C(dv/dt) ; q = ∫i·dt | Stores energy: E = ½Cv² |
| **Resistance (R)** | v = R·i | Dissipates energy: P = v²/R |

Kirchhoff's Laws are used to formulate the system equations: **KCL** (sum of currents at a junction = 0) and **KVL** (sum of voltages around a loop = 0).

#### Electrical ↔ Mechanical Analogy

| Electrical System | Mechanical System |
|---|---|
| Resistor (dissipates P = v²/R) | Dashpot (dissipates P = cv²) |
| Inductance | Mass |
| Capacitance | Spring |
| Voltage (V) | Force (F) |
| Current (I) | Velocity (v) |

---

### 4. Hydraulic System
**Input:** Liquid inflow (q) | **Output:** Liquid height (h) in container

| Building Block | Equation |
|---|---|
| **Hydraulic Resistance (R)** | P₁ – P₂ = R·q |
| **Hydraulic Capacitance (C = A/ρg)** | q₁ – q₂ = C·(dp/dt) |
| **Hydraulic Inertance (I = Lρ/A)** | P₁ – P₂ = I·(dq/dt) |

The PDF also covers Pneumatic and Thermal systems, and combinational systems (e.g., electrical-mechanical, hydraulic-mechanical).

---

## UNIT III — Dynamic Response of Systems

### Types of Responses
- **Natural response:** The system's behavior without any external forcing input — it decays naturally.
- **Forced response:** The response due to a sustained external input signal.
- **Transient response:** The initial part of the response before the system reaches steady state.
- **Steady-state response:** The final settled value of the output after the transient has died out.

**Standard test inputs used in analysis:** Step, Ramp, Impulse.

---

### First-Order Systems

A first-order system is governed by a first-order differential equation with one energy storage element.

**Time Constant (τ):** The time at which the output reaches **63% of its steady-state value**. Mathematically, τ = a₁/a₀.

**Standard first-order equation:** τ(dy/dt) + y = Gss · u

**Transfer function (1st order):** G(s) = Gss / (τs + 1)

**Step response:** y(t) = Gss · (1 – e^(–t/τ))

- At t = τ → output = 63% of SSV
- At t = 3τ → output ≈ 95% of SSV (used as practical settling criterion)

---

### Second-Order Systems

Second-order systems are analogous to a **spring-mass-damper** system. Their response depends on the amount of damping.

**Damping Factor (ζ)** determines the type of response:

| Condition | Response Type | Description |
|---|---|---|
| ζ > 1 | **Overdamped** | Slow return to equilibrium, no oscillation |
| ζ = 1 | **Critically damped** | Fastest return without oscillating |
| ζ < 1 | **Underdamped** | Oscillates before settling at the final value |
| ζ = 0 | **Undamped** | Oscillates indefinitely |

**Natural angular frequency:** ωn = √(a₀/a₂)

**Damped frequency:** ω = ωn · √(1 – ζ²)

#### Performance Measures for 2nd Order Systems

| Measure | Formula |
|---|---|
| **Rise time (tr)** | π / 2ω |
| **Peak time (tp)** | π / ω |
| **Percentage Overshoot** | e^(–ζπ/√(1–ζ²)) × 100% |
| **Settling time (2% criterion)** | 4 / (ζωn) |
| **Settling time (5% criterion)** | 3 / (ζωn) |

**RLC Example:** R = 100Ω, L = 2H, C = 20µF → ωn = 158 rad/s, ζ = 0.16 → **underdamped**, ω = 156 rad/s.

---

### Transfer Function Method

The **transfer function G(s)** is defined as the Laplace Transform of the output divided by the Laplace Transform of the input, assuming zero initial conditions.

**Procedure:**
1. Take the Laplace Transform of the system's differential equation.
2. Output(s) = G(s) × Input(s)
3. Match the expression with a standard inverse Laplace table entry.
4. Take the Inverse Laplace Transform to get the output as a time-domain expression y(t).

**Standard Laplace Transforms of inputs:**
- Step → 1/s | Ramp → 1/s² | Impulse → 1

**Standard 2nd order transfer function:**
G(s) = ωn² / (s² + 2ζωns + ωn²)

**Systems in series:** G_total(s) = G1(s) · G2(s) · G3(s)

**Closed-loop with feedback:** G_cl(s) = G(s) / [1 + G(s)·H(s)]

---

### Bode Plots & Frequency Transfer Functions

The **frequency transfer function** G(jω) = output phasor / input phasor, where a phasor is a quantity with magnitude, frequency, and phase.

A **Bode plot** consists of two graphs plotted against angular frequency ω on a logarithmic scale:
1. Magnitude |G(jω)| expressed in decibels (dB)
2. Phase angle φ

**Magnitude in dB:** 20 dB means magnitude = 10 (output amplitude is 10× input); 40 dB means magnitude = 100.

**Break-point frequency:**
- 1st order system: ω = 1/τ
- 2nd order system: ω = ωn

---

### Closed-Loop Controllers

**Open-loop system:** The input signal does not depend on the actual process output — no feedback.

**Closed-loop system:** Feedback from the output modifies the input, so the system continuously works to maintain the required output.

**Disturbance** is an unwanted signal that affects the output. In a closed-loop system, feedback reduces the effect of disturbances.

#### Control Modes

| Mode | Principle | Characteristic |
|---|---|---|
| **Two-step / ON-OFF** | Switch operates based on the error signal | Simple; causes oscillation around setpoint |
| **Proportional (P)** | Correcting signal is proportional to error | Fast; leaves a permanent steady-state error (offset) |
| **Derivative (D)** | Correcting signal is proportional to rate of change of error | Anticipatory; prevents overshoot; cannot be used alone |
| **Integral (I)** | Correcting signal is proportional to the integral of error over time | Eliminates steady-state offset; slower response |
| **PD** | P + D combined | Faster response with reduced overshoot |
| **PI** | P + I combined | Eliminates steady-state error |
| **PID** | All three combined | Best overall control performance |

---

## UNIT IV — Micro Mechatronic Systems & Data Acquisition

### Micro Mechatronics
Micro Mechatronics is the integration of mechanical and electronic systems at the **microscale**, exploiting the scaling effects that occur in the micro world. It is expected to be a key component in areas like electronic automotive technology.

---

### MEMS vs. Microelectronics

| Feature | Microelectronics (ME) | MEMS |
|---|---|---|
| **Materials** | Silicon, metals | Silicon, metals, polymers, glass, etc. |
| **Functions** | Electrical only | Electrical, mechanical, optical, chemical, biological |
| **Structures** | Stationary, 2D, isolated from environment | Stationary and movable, 3D, interfaces with the surrounding medium |
| **Maturity** | Mature, standardized | No fixed methodology or standards yet |

**Advantages of microsystem products:** Less material, lower power consumption, greater functionality per unit space, accessibility to regions forbidden to larger devices, and typically lower cost.

**Industrial applications:** Ink-jet printing heads, thin-film magnetic heads, compact disks, automotive components, medical devices, chemical/environmental sensors.

---

### Microfabrication Techniques

**Bulk Micromachining**
This involves deep wet etching of a single-crystal silicon substrate. A solution like KOH (potassium hydroxide) has a very low etch rate in the direction of the crystal face, which allows precise geometric structures with sharp edges to be formed when the lattice is correctly oriented.

The **p+ etch-stop technique** uses Boron doping to create an etch-resistant layer. Epitaxial deposition then applies an upper silicon layer that follows the same crystal structure. This controls etch depth and creates thin membranes.

**Surface Micromachining**
Planar structuring of the substrate surface using shallow etching — unlike bulk micromachining which goes deep.

**LIGA Process** (developed in Germany, early 1980s)
LIGA stands for the German words:
- **L** = Lithographie (X-ray Lithography)
- **I** = Galvanoformung (Electrodeposition / Electroforming)
- **G** = Abformtechnik (Plastic Molding)

These also represent the three steps in the LIGA process sequence.

*Advantages:* Versatile; high aspect ratios possible; part sizes from micrometers to centimeters; close tolerances.
*Disadvantage:* Very expensive — large production quantities are needed to justify its use.

**Ultra-High Precision Machining**
Uses single-crystal diamond cutting tools and position control systems with resolutions as fine as **0.01 µm**. Applications: computer hard discs, photocopier drums, mold inserts for compact disk reader heads, HD-TV projection lenses, VCR scanning heads.

**Microstereolithography (MSTL)**
A microscale 3D fabrication process. Conventional STL uses layer thicknesses of 75–500 µm; MSTL achieves **10–20 µm** per layer. Conventional laser spot diameter is ~250 µm; MSTL reduces this to **1–2 µm**. Work material is not limited to photosensitive polymer — ceramic and metallic materials (in powder form) can also be used.

**Nanofabrication**
At nanoscale, UV photolithography cannot be used effectively because its long wavelength causes diffraction. Instead, **high-resolution electron beam lithography** is used — its shorter wavelength virtually eliminates diffraction during exposure.

---

### Data Acquisition System (DAQ / DAS)

The purpose of a data acquisition system is to **acquire analog signals** from the real world and **present them in digital form** that a computer can process.

**Main components of a DAQ system (in order):**

| # | Component | Function |
|---|---|---|
| 1 | **Transducers/Sensors** | Convert physical parameters to electrical signals |
| 2 | **Analog Multiplexer** | Routes one of several analog inputs to the ADC |
| 3 | **Signal Conditioning** | Amplifies weak signals and filters out noise |
| 4 | **Sample and Hold Circuit** | Captures and holds the signal steady during ADC conversion |
| 5 | **ADC (Analog-to-Digital Converter)** | Converts continuous analog signal to discrete digital value |
| 6 | **Microcomputer System** | Processes, stores, or transmits the digital data |
| 7 | **DAC (Digital-to-Analog Converter)** | Converts processed digital data back to analog |
| 8 | **Actuator** | Performs the physical action based on processed output |

---

### Analog-to-Digital Conversion (ADC)

ADC and DAC allow digital computers to interact with real-world signals like voltage, temperature, pressure, velocity, etc.

Digital information differs from analog in two key respects:
1. It is **sampled** — measurements are taken at discrete time intervals, not continuously.
2. It is **quantized** — the continuous amplitude is rounded to the nearest discrete digital level.

**Quantization Error:** The error introduced by rounding the analog value to the nearest digital level. It is an inherent limitation of all digital systems.

---

### Nyquist Sampling Theorem

> An analog signal can be **perfectly reconstructed** from its digital samples if the sampling rate is at least **twice the highest frequency** present in the original signal.

If the highest frequency in the signal is W Hz, the required sampling rate is ≥ 2W samples/second (or sampling interval ≤ 1/2W seconds).

Sampling below this rate causes **aliasing** — the reconstructed signal is distorted and does not represent the original.

---

## UNIT V — Microcontrollers & Embedded Systems

### Microcontroller (MCU)

A **microcontroller** is a small computer fabricated as a single Metal-Oxide-Semiconductor (MOS) Integrated Circuit. It integrates a CPU, memory (RAM, ROM/Flash), and programmable I/O peripherals all on one chip.

Because it is built into the devices it controls, it is also referred to as an **embedded controller**. It is manufactured using **VLSI fabrication**.

**Program memory types used:** Ferroelectric RAM, NOR Flash, OTP ROM.

**Arduino boards** use Atmel 8-bit AVR microcontrollers (ATmega series). The 32-bit Arduino Due is based on the Atmel SAM3X8E (introduced 2012).

---

### Microprocessor vs. Microcontroller

| Feature | Microprocessor | Microcontroller |
|---|---|---|
| **Contains** | CPU only | CPU + Memory + I/O (all on one chip) |
| **Used in** | Personal computers | Embedded systems |
| **External components needed** | Yes — separate RAM, ROM, I/O required | No — everything is integrated |
| **Examples** | Intel x86 series | Intel 8051, PIC, ATmega |

**8-bit microcontroller examples:** Intel 8031/8051, PIC1x, Motorola MC68HC11.
16-bit microcontrollers offer greater precision and performance than 8-bit types.

---

### Embedded Systems

An **embedded system** is a microcontroller-based system designed to perform a dedicated function within a larger mechanical or electrical product.

**Classification of Embedded Systems:**

**1. Based on Generation:** First → Second → Third → Fourth generation.

**2. Based on Complexity and Performance:**
- Small-scale embedded systems
- Medium-scale embedded systems
- Large-scale / Complex embedded systems

**3. Based on Deterministic Behavior**

**4. Based on Triggering** (time-triggered vs event-triggered)

---

### Purpose of Embedded Systems
1. Data collection, storage, and representation
2. Data communication
3. Data (signal) processing
4. Monitoring
5. Control
6. Application-specific user interface

---

### Major Application Areas

| Domain | Examples |
|---|---|
| **Consumer Electronics** | Camcorders, digital cameras |
| **Household Appliances** | Television, washing machine, microwave oven, refrigerator, DVD players |
| **Home Automation & Security** | Air conditioners, sprinkler systems, intruder detection alarms, CCTV, fire alarms |
| **Automotive** | ABS (Anti-lock Braking Systems), engine control, ignition systems, automatic navigation |

---

### Core of an Embedded System

1. **General Purpose & Domain-Specific Processors**
   - Microprocessors
   - Microcontrollers
   - Digital Signal Processors (DSPs)
2. **Application Specific Integrated Circuits (ASICs)**
3. **Programmable Logic Devices (PLDs)**
4. **Commercial Off-The-Shelf Components (COTS)**

---

### Serial vs. Parallel Communication

**Serial Communication:** Data is transmitted one bit at a time over a single wire or channel. Simpler wiring, suitable for longer distances. Examples: UART, SPI, I2C.

**Parallel Communication:** Multiple bits are transmitted simultaneously over multiple lines. Faster for short distances but uses more wires, making it less practical for long-distance transmission.

---

## 🎯 Quick Viva Q&A

| Question | Answer |
|---|---|
| What is Mechatronics? | The integration of electronics and control systems into mechanical systems to achieve intelligent operation |
| What is a transducer/sensor? | A device that provides a usable electrical output in response to a specified physical measurand |
| What is LVDT? | A Linear Variable Differential Transformer — measures linear displacement using electromagnetic induction |
| What is the Seebeck Effect? | When two dissimilar metals are joined and one junction is heated, an EMF proportional to the temperature difference is produced — basis of the thermocouple |
| RTD vs Thermistor? | RTD: resistance increases with temperature. Thermistor (NTC): resistance decreases with temperature |
| What is Time Constant (τ)? | The time at which the output of a first-order system reaches 63% of its steady-state value |
| What is Damping Factor (ζ)? | A dimensionless parameter that determines whether a second-order system is overdamped (ζ>1), critically damped (ζ=1), or underdamped (ζ<1) |
| What is a Transfer Function? | The ratio of Laplace Transform of output to Laplace Transform of input, assuming zero initial conditions |
| What is a Bode Plot? | A pair of graphs showing the magnitude (in dB) and phase angle of a system's frequency response plotted against frequency on a logarithmic scale |
| What does PID controller do? | P corrects proportional to current error; I corrects accumulated past error (eliminates offset); D anticipates future error from its rate of change |
| Open-loop vs Closed-loop? | Open-loop has no feedback; closed-loop uses feedback to continuously compare actual vs desired output and correct the difference |
| What is MEMS? | Micro Electro Mechanical Systems — microscale devices that integrate electrical and mechanical functionality, fabricated using semiconductor processes |
| What is the LIGA process? | A microfabrication process using X-ray Lithography, Electroforming, and Plastic Molding to create high-aspect-ratio microstructures |
| What is the Nyquist Theorem? | To perfectly reconstruct an analog signal from digital samples, the sampling rate must be at least twice the highest frequency in the signal |
| What is Quantization Error? | The error introduced when a continuous analog value is rounded to the nearest discrete digital level during ADC conversion |
| Microprocessor vs Microcontroller? | A microprocessor contains only the CPU; a microcontroller integrates the CPU, memory, and I/O peripherals on a single chip |
| What is an embedded system? | A microcontroller-based system designed to perform a specific dedicated function within a larger product |
| What is Bulk Micromachining? | A process of deep wet etching (using KOH) into a silicon substrate to create 3D microstructures with controlled geometry |
| Electrical-Mechanical Analogy? | Resistor ↔ Dashpot, Inductor ↔ Mass, Capacitor ↔ Spring, Voltage ↔ Force, Current ↔ Velocity |
| What is Signal Conditioning? | Processing of a raw sensor signal (amplification, filtering) to make it suitable for ADC input |
