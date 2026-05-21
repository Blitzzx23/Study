# 🏭 PLC — Programmable Logic Controller
### Mechatronics Viva Notes

---

## 🔷 What is a PLC?

> [!NOTE]
> A **Programmable Logic Controller (PLC)** is a special-purpose industrial digital computer designed to control manufacturing processes or machinery. It continuously monitors inputs from sensors and switches, executes a stored control program, and drives outputs (actuators, motors, valves) accordingly.

**Origin:** Developed in the late 1960s to replace **relay-based control panels** in automotive manufacturing. The first commercial PLC was the Modicon 084 (1969).

**Why PLC over relays?**

| Feature | Relay Panel | PLC |
|---|---|---|
| **Modification** | Rewiring required (time-consuming) | Just change the program |
| **Reliability** | Mechanical contacts wear out | No moving parts in logic |
| **Diagnostics** | Difficult to troubleshoot | Built-in fault indicators |
| **Space** | Large panels | Compact unit |
| **Cost (large systems)** | Higher | Lower |

---

## 🔷 Basic Structure of a PLC

```
┌─────────────────────────────────────────────┐
│                    PLC                      │
│                                             │
│  ┌──────────┐    ┌─────────┐    ┌────────┐ │
│  │  Input   │    │  CPU    │    │ Output │ │
│  │  Module  │───▶│(Processor│──▶│ Module │ │
│  │          │    │+Memory) │    │        │ │
│  └──────────┘    └─────────┘    └────────┘ │
│       ▲                               │     │
│  Sensors,                        Actuators, │
│  Switches,                       Motors,    │
│  Encoders                        Valves     │
│                                             │
│         ┌──────────────┐                   │
│         │ Power Supply │                   │
│         └──────────────┘                   │
└─────────────────────────────────────────────┘
```

### Main Components

| Component | Function |
|---|---|
| **CPU (Central Processing Unit)** | Executes the control program; performs logic, timing, counting operations |
| **Memory** | Stores the user program and data (RAM for program, ROM for OS) |
| **Input Module** | Interfaces physical input devices (sensors, switches) to the CPU |
| **Output Module** | Interfaces CPU commands to physical output devices (actuators, motors, valves) |
| **Power Supply** | Converts AC mains to DC voltages required by PLC modules |
| **Programming Device** | Laptop or dedicated terminal used to write and upload the program |
| **Communication Module** | Allows PLC to communicate with other PLCs, SCADA, or HMI systems |

---

## 🔷 Input & Output (I/O) Modules

### Input Module
Accepts signals from field devices and converts them to a level the CPU can process.

| Input Device Type | Example |
|---|---|
| **Digital (Discrete) Input** | Push buttons, limit switches, proximity sensors, photoelectric sensors |
| **Analog Input** | Temperature sensors (RTD, thermocouple), pressure transducers, flow meters |

### Output Module
Receives commands from CPU and drives field devices.

| Output Device Type | Example |
|---|---|
| **Digital (Discrete) Output** | Relay coils, solenoid valves, indicator lamps, motor starters |
| **Analog Output** | Variable-speed drives, proportional control valves |

> [!TIP]
> **Discrete I/O** = ON/OFF signals (0 or 1).
> **Analog I/O** = Continuous range of values (e.g., 4–20 mA or 0–10 V).

---

## 🔷 PLC Scan Cycle

> [!IMPORTANT]
> A PLC does NOT execute its program once and stop. It continuously repeats a **scan cycle** as long as it is in RUN mode.

```
Scan Cycle (repeated continuously):

  ┌─────────────────────────────────────────────────┐
  │                                                 │
  ▼                                                 │
[1] READ INPUTS
    → Snapshot of all input states stored in memory
        ↓
[2] EXECUTE PROGRAM
    → CPU runs through the entire ladder program
      using the input snapshot from step 1
        ↓
[3] UPDATE OUTPUTS
    → Results of program execution written to
      all physical output devices
        ↓
[4] HOUSEKEEPING / DIAGNOSTICS
    → Internal checks, communication tasks, timer updates
        ↓
    ──────────────────────────────────────── (repeat) ┘
```

**Scan Time** = Time taken to complete one full scan cycle (typically **1 ms to 100 ms** depending on program size and PLC speed).

> [!WARNING]
> If scan time is too long relative to the process speed, the PLC may miss fast-changing inputs. Fast processes require PLCs with short scan times.

---

## 🔷 PLC Memory Types

| Memory Type | Content | Volatile? |
|---|---|---|
| **ROM (Read-Only Memory)** | PLC operating system / firmware | Non-volatile |
| **RAM (Random Access Memory)** | User program, I/O image table, data registers | Volatile (battery-backed) |
| **EEPROM / Flash** | Backup of user program | Non-volatile |

---

## 🔷 PLC Programming Languages

> [!NOTE]
> IEC 61131-3 is the international standard defining **5 PLC programming languages**. All are used in industry.

| Language | Type | Visual? | Best Used For |
|---|---|---|---|
| **Ladder Diagram (LD)** | Graphical | ✅ Yes | General logic; resembles relay ladder diagrams |
| **Function Block Diagram (FBD)** | Graphical | ✅ Yes | Complex signal processing; analog control |
| **Sequential Function Chart (SFC)** | Graphical | ✅ Yes | Sequential/step-based processes (e.g., washing machine) |
| **Instruction List (IL)** | Text | ❌ No | Low-level; similar to assembly language |
| **Structured Text (ST)** | Text | ❌ No | High-level; similar to Pascal; for complex math/algorithms |

---

## 🔷 Ladder Diagram (Most Important for Viva)

> [!NOTE]
> **Ladder Diagram (LD)** is the most widely used PLC programming language. It is a **graphical language** that resembles the wiring diagram of a relay-based control panel.

### Ladder Diagram Structure

```
Left Rail          Rungs           Right Rail
   │                                   │
   ├──[ ]──[ ]──────────────( )────────┤  ← Rung 1
   │  NO    NO               Coil      │
   │                                   │
   ├──[/]──────────────────( )─────────┤  ← Rung 2
   │  NC                   Coil        │
   │                                   │
   ├──[ ]──┬──[ ]──────────( )─────────┤  ← Rung 3 (parallel)
   │       └──[ ]──────────            │
```

### Basic Ladder Symbols

| Symbol | Name | Meaning |
|---|---|---|
| `──[ ]──` | **Normally Open (NO) Contact** | Passes current when input is ON (1) |
| `──[/]──` | **Normally Closed (NC) Contact** | Passes current when input is OFF (0) |
| `──( )──` | **Output Coil** | Turns ON when rung has continuity |
| `──(/)──` | **Negated Output Coil** | Turns OFF when rung has continuity |
| `──[SET]──` | **Set (Latch) Coil** | Latches ON; stays ON even when input removed |
| `──[RST]──` | **Reset (Unlatch) Coil** | Resets a latched coil to OFF |

### Logic Gates in Ladder Diagram

| Logic Gate | Ladder Implementation |
|---|---|
| **AND** | Two NO contacts in **series** |
| **OR** | Two NO contacts in **parallel** |
| **NOT** | One NC contact |
| **NAND** | Two NO contacts in series → output through NC coil |
| **NOR** | Two NC contacts in series |

---

## 🔷 Latching (Seal-In Circuit)

> [!IMPORTANT]
> **Latching** allows an output to remain ON even after the input that triggered it is released.

```
Ladder Rung:

  ──[ Start ]──┬──[/Stop]──( Motor )──
               │
  ──[ Motor ]──┘

```
- When **Start** button is pressed → Motor turns ON.
- **Motor contact** (seal-in contact) in parallel with Start → keeps the circuit energised after Start is released.
- Only **Stop** (NC contact) can de-energise the output.

> [!NOTE]
> This is equivalent to a **self-holding relay circuit** in conventional control panels.

---

## 🔷 Timers in PLC

A **timer** in a PLC measures time and activates an output after a preset delay.

| Timer Type | Behaviour |
|---|---|
| **TON — Timer ON Delay** | Output turns ON after a set delay once input is activated |
| **TOF — Timer OFF Delay** | Output turns OFF after a set delay once input is de-activated |
| **TP — Pulse Timer** | Output remains ON for a fixed preset time regardless of input duration |

**Timer Parameters:**

| Parameter | Symbol | Meaning |
|---|---|---|
| Enable input | IN | Starts the timer |
| Preset value | PT | Target time value |
| Elapsed time | ET | Current time count |
| Output | Q | ON when ET ≥ PT |

---

## 🔷 Counters in PLC

A **counter** counts events (pulses) and activates an output when a preset count is reached.

| Counter Type | Behaviour |
|---|---|
| **CTU — Count Up** | Counts upward from 0; output ON when count ≥ preset |
| **CTD — Count Down** | Counts downward from preset; output ON when count ≤ 0 |
| **CTUD — Count Up/Down** | Counts in both directions |

---

## 🔷 PLC vs. Microcontroller

| Feature | PLC | Microcontroller |
|---|---|---|
| **Environment** | Industrial (harsh — dust, vibration, temperature) | Controlled environments |
| **Programming** | Ladder Diagram / IEC 61131-3 languages | C, C++, Assembly, Python |
| **I/O handling** | Built-in robust I/O modules | Requires external interface circuits |
| **Reliability** | Extremely high; designed for 24/7 operation | Moderate |
| **Ease of use** | Easy for electrical engineers (ladder = relay logic) | Requires software programming skills |
| **Cost** | Higher (industrial grade) | Lower |
| **Flexibility** | Less flexible for complex algorithms | Highly flexible |
| **Application** | Industrial automation, process control | Consumer electronics, embedded systems |

---

## 🔷 PLC vs. Relay Control

| Feature | Relay Control | PLC |
|---|---|---|
| **Logic change** | Requires rewiring | Just reprogram |
| **Speed** | Slower (mechanical contacts) | Faster (electronic) |
| **Reliability** | Lower (wear and tear) | Higher (no moving parts in logic) |
| **Diagnostics** | Difficult | Built-in LED indicators, fault logs |
| **Size** | Large panels | Compact |

---

## 🔷 Industrial Applications of PLCs

| Industry | Application |
|---|---|
| **Automotive** | Assembly line control, welding robots, paint shop automation |
| **Food & Beverage** | Bottling lines, mixing processes, conveyor control |
| **Chemical / Petrochemical** | Process control, batch mixing, valve sequencing |
| **Manufacturing** | CNC machine interfacing, material handling |
| **Utilities** | Water treatment plants, power distribution |
| **Building Automation** | HVAC control, elevator control, fire safety systems |

---

## 🔷 Sequential Control — Washing Machine Example

> [!NOTE]
> **Sequential control** means the system moves through a fixed series of steps, one after another. SFC (Sequential Function Chart) or Ladder logic with timers is used.

```
Step 1 → FILL       (Water inlet valve ON until water level sensor trips)
    ↓
Step 2 → WASH       (Drum motor ON for preset time — TON timer)
    ↓
Step 3 → DRAIN      (Drain pump ON until level sensor OFF)
    ↓
Step 4 → RINSE      (Fill + Drum motor ON for preset time)
    ↓
Step 5 → SPIN       (High-speed motor ON for preset time)
    ↓
Step 6 → DONE       (Buzzer ON, all outputs OFF)
```

Each step transitions to the next based on a **sensor condition** or a **timer expiry**.

---

## 🎯 PLC Quick Viva Q&A

| Question | Answer |
|---|---|
| What is a PLC? | An industrial digital computer that monitors inputs, executes a stored control program, and drives outputs to control machinery or processes |
| Why was PLC developed? | To replace relay-based control panels — easier to reprogram, more reliable, compact |
| What is the PLC scan cycle? | Read inputs → Execute program → Update outputs → Housekeeping — repeated continuously |
| What is scan time? | Time taken to complete one full scan cycle; typically 1–100 ms |
| What is Ladder Diagram? | A graphical PLC programming language resembling relay wiring diagrams; uses contacts (inputs) and coils (outputs) |
| What is a NO contact? | Normally Open — passes current (logic 1) only when the associated input is ON |
| What is a NC contact? | Normally Closed — passes current when the associated input is OFF |
| What is latching in PLC? | A seal-in circuit where a parallel contact of the output coil keeps the output ON after the trigger input is released |
| What is TON timer? | Timer ON Delay — output turns ON after a preset delay from when input is activated |
| What is a CTU counter? | Count Up counter — counts rising edges of input; output turns ON when count reaches preset value |
| AND gate in ladder? | Two NO contacts in series |
| OR gate in ladder? | Two NO contacts in parallel |
| What are IEC 61131-3 languages? | Ladder Diagram, Function Block Diagram, Sequential Function Chart, Instruction List, Structured Text |
| PLC vs Microcontroller? | PLC: industrial grade, robust I/O, ladder programming, 24/7 reliability. MCU: flexible programming, lower cost, for embedded/consumer applications |
| What is SFC? | Sequential Function Chart — graphical PLC language used for step-based sequential processes like washing machines |
| What is discrete I/O? | ON/OFF (digital) signals — e.g., push buttons (input), solenoid valves (output) |
| What is analog I/O? | Continuous signal range — e.g., 4–20 mA from a temperature sensor (input), variable-speed drive signal (output) |
