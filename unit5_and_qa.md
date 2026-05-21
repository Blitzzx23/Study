# 💻 Unit V — Microcontrollers & Embedded Systems

---

## 🔷 Microcontroller (MCU)

> [!NOTE]
> A **microcontroller** is a small computer fabricated as a single **MOS (Metal-Oxide-Semiconductor) Integrated Circuit** chip, integrating a CPU, memory, and programmable I/O peripherals — all in one package.

- Also called an **embedded controller** — built into the device it controls
- Manufactured using **VLSI fabrication**
- Program memory types: **NOR Flash, Ferroelectric RAM, OTP ROM**

---

## 🔷 Microprocessor vs. Microcontroller

| Feature | Microprocessor | Microcontroller |
|---|---|---|
| **Contains** | CPU only | CPU + RAM + ROM + I/O (all on one chip) |
| **Used in** | Personal computers | Embedded systems |
| **External chips needed** | Yes — separate RAM, ROM, I/O | No — fully integrated |
| **Cost** | Higher system cost | Lower system cost |
| **Examples** | Intel x86 series | Intel 8051, PIC, ATmega |

> [!IMPORTANT]
> A **microprocessor** is just the brain.
> A **microcontroller** is the brain + memory + senses — all in one chip.

### Common Microcontrollers

| Bit Width | Examples |
|---|---|
| **8-bit** | Intel 8031/8051, PIC1x, Motorola MC68HC11 |
| **16-bit** | Higher precision and performance than 8-bit |
| **Arduino (8-bit AVR)** | ATmega8, ATmega168, ATmega328, ATmega1280, ATmega2560 |
| **Arduino Due (32-bit)** | Atmel SAM3X8E — introduced in 2012 |

---

## 🔷 Embedded Systems

> [!NOTE]
> An **embedded system** is a microcontroller-based computing system designed to perform a **specific dedicated function** within a larger mechanical or electrical product.

### Embedded System vs. General Computer

| Feature | General Computer | Embedded System |
|---|---|---|
| **Purpose** | General-purpose (runs any software) | Fixed, dedicated function |
| **OS** | Windows / Linux | Custom firmware or RTOS |
| **User interface** | Keyboard, mouse, screen | May have none at all |
| **Real-time constraints** | Usually none | Often required |
| **Resources** | Large (GBs RAM, TBs storage) | Limited (KBs to MBs) |

---

## 🔷 Classification of Embedded Systems

### 1. Based on Generation
First Generation → Second → Third → **Fourth Generation**

### 2. Based on Complexity & Performance

| Type | Description |
|---|---|
| **Small-Scale** | Simple, 8-bit, minimal resources (e.g., timer circuit) |
| **Medium-Scale** | Moderate complexity (e.g., microwave oven controller) |
| **Large-Scale / Complex** | High performance, multi-processor (e.g., aircraft flight control) |

### 3. Based on Deterministic Behavior
- **Deterministic** — same input always produces the same output and response time
- **Non-deterministic** — response time may vary

### 4. Based on Triggering
- **Time-triggered** — actions occur at fixed time intervals
- **Event-triggered** — actions occur in response to external events

---

## 🔷 Purpose of Embedded Systems

| # | Purpose |
|---|---|
| 1 | Data collection, storage, and representation |
| 2 | Data communication |
| 3 | Data (signal) processing |
| 4 | Monitoring |
| 5 | Control |
| 6 | Application-specific user interface |

---

## 🔷 Application Areas of Embedded Systems

| Domain | Examples |
|---|---|
| **Consumer Electronics** | Digital cameras, camcorders |
| **Household Appliances** | Washing machine, microwave oven, fridge, TV, DVD players |
| **Home Automation & Security** | Air conditioners, sprinklers, intruder alarms, CCTV, fire alarms |
| **Automotive** | ABS (Anti-lock Braking), engine control, ignition, GPS navigation |

---

## 🔷 Core of an Embedded System

| Component Type | Examples |
|---|---|
| **General Purpose Processors** | Microprocessors, Microcontrollers, DSPs |
| **ASICs** | Application-Specific Integrated Circuits — custom chips for one job |
| **PLDs** | Programmable Logic Devices — reconfigurable logic |
| **COTS** | Commercial Off-The-Shelf Components — standard ready-made parts |

---

## 🔷 Serial vs. Parallel Communication

| Feature | Serial Communication | Parallel Communication |
|---|---|---|
| **Data transmission** | One bit at a time on a single line | Multiple bits simultaneously on multiple lines |
| **Wiring** | Simple — fewer wires | Complex — more wires |
| **Speed** | Moderate (though modern serial is very fast) | Faster for short distances |
| **Distance** | Suitable for longer distances | Prone to noise over longer distances |
| **Examples** | UART, SPI, I2C, USB | Memory bus, old printer port |

---

---

# 🎯 Master Viva Q&A Cheat Sheet
### All 5 Units — Quick Reference

| Question | Answer |
|---|---|
| What is Mechatronics? | Integration of electronics and control systems into mechanical systems to achieve intelligent operation |
| What is a transducer/sensor? | A device that provides a usable electrical output in response to a specified physical measurand |
| What is an LVDT? | Linear Variable Differential Transformer — measures linear displacement using electromagnetic induction |
| What is the Seebeck Effect? | When two dissimilar metal junctions are held at different temperatures, an EMF proportional to the temperature difference is produced |
| RTD vs Thermistor? | RTD: resistance **increases** with temperature. Thermistor (NTC): resistance **decreases** with temperature |
| What is Time Constant (τ)? | Time taken for a first-order system output to reach 63% of its steady-state value |
| What is Damping Factor (ζ)? | A dimensionless parameter determining whether a 2nd order system is overdamped (>1), critically damped (=1), or underdamped (<1) |
| What is a Transfer Function? | Ratio of Laplace Transform of output to Laplace Transform of input, assuming zero initial conditions |
| What is a Bode Plot? | Two graphs — magnitude (dB) vs frequency and phase angle vs frequency — both on log scale |
| What does a PID controller do? | P corrects present error; I corrects accumulated past error; D anticipates future error from rate of change |
| Open-loop vs Closed-loop? | Open-loop has no feedback; closed-loop uses feedback to compare actual vs desired output and self-correct |
| What is MEMS? | Micro Electro Mechanical Systems — microscale devices integrating electrical and mechanical functions using semiconductor fabrication |
| What is the LIGA process? | Microfabrication using X-ray Lithography (L) + Electroforming (I) + Plastic Molding (G) |
| What is the Nyquist Theorem? | Sampling rate must be ≥ 2× highest signal frequency for perfect reconstruction |
| What is Quantization Error? | Error introduced when a continuous analog value is rounded to the nearest discrete digital level in an ADC |
| Microprocessor vs Microcontroller? | Microprocessor = CPU only; Microcontroller = CPU + RAM + ROM + I/O all integrated on one chip |
| What is an Embedded System? | A dedicated microcontroller-based system designed for a specific function within a larger product |
| What is Bulk Micromachining? | Deep wet etching of a silicon substrate (using KOH) to create precise 3D microstructures |
| Electrical-Mechanical Analogy? | Resistor ↔ Dashpot · Inductor ↔ Mass · Capacitor ↔ Spring · Voltage ↔ Force · Current ↔ Velocity |
| What is Signal Conditioning? | Amplification and filtering of a raw sensor signal to prepare it for ADC input |
| What is Aliasing? | Distortion that occurs when a signal is sampled below the Nyquist rate |
| What is the p+ etch-stop technique? | Boron doping of silicon creates an etch-resistant layer, allowing precise membrane thickness in bulk micromachining |
