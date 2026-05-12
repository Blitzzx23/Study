# Full Comprehensive Revision Notes - Mechatronics / Control Systems PYQ

Source set used: PYQ paper images, Unit I-V slides, Unit II modelling PDF, PLC slides, and W. Bolton reference for standard control/mechatronics forms.

Priority key:
- HIGH: repeated in 3 or more papers, high marks, fast scoring.
- MEDIUM: repeated 1-2 times or supports HIGH numericals.
- LOW: theory support, short answer, or rarely asked.

## PYQ Priority Snapshot

| Unit | HIGH priority | MEDIUM priority | LOW priority |
|---|---|---|---|
| 1 | Block reduction, thermostat/control system block diagram, sensor selection | Open vs closed loop, sensor elements in measuring systems | General examples |
| 2 | Standard first/second order forms, RLC/RC/hydraulic modelling, damping identification | Thermal, mechanical/rotational analogies | Energy storage explanation |
| 3 | First-order response, thermocouple step/ramp/impulse, second-order performance, controller comparison | Partial fractions, inverse Laplace | General response definitions |
| 4 | MEMS, LIGA, ADC, DAS, sampling/quantization | Substrate preparation, deposition, ADC vs DAC | Micro joining details |
| 5 | Embedded systems, IoT, Raspberry Pi, predictive maintenance | Physical layer IoT protocols, sensors in IoT | Classification details |
| 6 | PLC latching, timers, washing machine, pneumatic cylinder, grinder/conveyor | AND/OR rungs, 10 s timing output | PLC hardware intro |

---

# UNIT 1 - Control System Basics, Block Diagrams, Sensors

## A. Core Concepts

### Open-loop vs closed-loop
- Open-loop: control action does not depend on output. Example: timer based heater. Simple and cheap, but cannot correct disturbance.
- Closed-loop: output is measured and fed back; controller acts on error. Example: thermostat heater. Accurate, disturbance rejection, but cost and stability issues.
- Error signal: `e(t) = r(t) - b(t)`, where `r` is reference and `b` is feedback signal.
- Negative feedback is normally used because it reduces error and improves stability. Positive feedback can destabilize unless deliberately used.

### Thermostat / temperature control system
Standard block answer:
`Set temperature/reference -> comparator -> controller/relay -> heater -> room/bath/liquid -> sensor/thermostat -> feedback to comparator`.

For liquid bath PYQ:
- Reference voltage enters differential amplifier.
- Measurement system converts actual temperature into feedback voltage.
- Error voltage = reference voltage - feedback voltage.
- Differential amplifier output drives relay.
- Relay switches heater power ON/OFF.
- Physical meaning: heater adds thermal energy until measured temperature approaches set value.

### Sensor basics
- Sensor: detects physical variable.
- Transducer: converts physical variable into electrical/mechanical signal.
- Signal conditioner: amplifies, filters, linearizes, isolates.
- Display/processor: shows or uses the value.

Measurement chain:
`Measurand -> sensor/transducer -> signal conditioning -> ADC/controller/display -> actuator/decision`.

Sensor classification:
- Displacement/position/proximity: potentiometer, LVDT, capacitive, eddy-current, inductive, optical encoder, Hall.
- Temperature: thermocouple, RTD, thermistor, bimetallic strip.
- Force/pressure: strain gauge load cell, diaphragm, Bourdon tube, piezoelectric.
- Motion: tachogenerator, encoder, accelerometer.

Rolled sheet thickness sensor:
- Best exam answer for moving metal sheet: non-contact eddy-current thickness measurement, often using two opposed eddy-current displacement sensors.
- If gap between sensors is fixed `D`, and measured clearances are `d1` and `d2`, thickness `t = D - d1 - d2`.
- Why suitable: fast, non-contact, works on moving metallic sheet, gives electrical output for control.
- Common mistake: suggesting contact sensor for fast rolling sheet. Contact methods wear out and lag.

### Block diagram reduction
Basic rules:
- Series blocks: `G_eq = G1 G2`.
- Parallel blocks: `G_eq = G1 + G2` with sign as drawn.
- Negative feedback: `G_cl = G/(1 + GH)`.
- Positive feedback: `G_cl = G/(1 - GH)`.

Correction rules while shifting blocks:
- Move summing point from before `G` to after `G`: multiply the side input by `G`.
- Move summing point from after `G` to before `G`: divide the side input by `G`.
- Move takeoff point from before `G` to after `G`: insert `1/G` in the takeoff branch.
- Move takeoff point from after `G` to before `G`: insert `G` in the takeoff branch.

Common mistakes:
- Changing summing point position without multiplying/dividing the side branch.
- Losing the sign at summing junction.
- Treating positive feedback as negative feedback.
- Reducing non-adjacent loops before moving takeoff points correctly.

## B. PYQ Patterns

| PYQ type | Years asked | Marks |
|---|---:|---:|
| Thermostat/temperature bath control block diagram and error signal | Dec 2022, May 2023, May 2024, Nov 2025 | 2 to 5 |
| Block diagram reduction | May 2023, Nov 2023, May 2024, Nov 2024 | 6 to 8 |
| Sensor for rolled sheet thickness | Dec 2022, Nov 2025 | 5 |
| Identify sensor, conditioner, display elements in thermometer/Bourdon gauge | May 2023, Nov 2024 | 2 |
| Elements in thermostatically controlled electric heater | Nov 2023 | 4 |

## C. Solving Approach

Block reduction scoring method:
1. Label each intermediate variable near every summing junction.
2. Reduce local feedback loops first.
3. Combine parallel feed-forward branches.
4. For non-standard feedback, write node equations instead of forcing a shortcut.
5. Substitute backward and express `C(s)/R(s)` or `Y(s)/R(s)`.

Thermostat block diagram scoring method:
1. Draw set point and feedback entering comparator.
2. Show controller/relay switching heater.
3. Show plant: room/bath/liquid.
4. Show sensor/measurement feedback.
5. Write `error = reference - measured feedback`.

Sensor selection scoring method:
1. State selected sensor.
2. Justify on physical requirement: non-contact, fast, electrical output.
3. Draw or describe measurement arrangement.
4. Give output relation.

## D. Final Verified Answers

### Repeated block diagram: `G1, G2, G3` with feedbacks `H1, H2, H3`
For the PYQ diagram where `H1` feeds back from after `G2` to the first summing junction, `H2` is local feedback around `G2`, and `H3` is feedback around `G3`:

`C(s)/R(s) = G1 G2 G3 / [(1 + G3 H3)(1 + G2 H2 + G1 G2 H1)]`

Use this only when signs match the shown negative feedback loops.

### Repeated block diagram: `G1 G2`, parallel `G3 + G4`, `G5`, feedbacks `H1, H2, H3`
For the PYQ diagram with:
- negative `H1` around `G1G2`,
- negative `H3` from output around `(G3 + G4)G5`,
- positive `H2` feeding back from before `G5` to the first summer,

`Y(s)/R(s) = [G1 G2 G5 (G3 + G4)] / [(1 + G1 G2 H1)(1 + G5 H3 (G3 + G4)) - G1 G2 H2 (G3 + G4)]`

If the `H2` sign is drawn negative in a variant, replace the minus before `G1G2H2(G3+G4)` by plus.

### Measuring system element identification
- Mercury-in-glass thermometer: sensor/transducer = mercury bulb and capillary, signal conditioning = thermal expansion/calibrated capillary, display = graduated scale.
- Bourdon pressure gauge: sensor = Bourdon tube, signal conditioning = linkage/gears, display = pointer and dial.

## E. Important Shortcuts

- Feedback shortcut: denominator sign is opposite of feedback sign. Negative feedback gives `1 + GH`.
- For thickness of moving metal sheet, write: "Two eddy-current sensors, non-contact, fast electrical output, `t = D - d1 - d2`."
- For thermostat: always show comparator. Without comparator/error, answer loses marks.

---

# UNIT 2 - System Modelling and Standard Forms

## A. Core Concepts

### Standard first-order form
`G(s) = K/(tau s + 1)`

Differential form:
`tau dy/dt + y = K x`

Identification:
- If denominator is `a1 s + a0`, then `tau = a1/a0`, `K = numerator/a0`.
- Time constant `tau`: time to reach 63.2 percent of final value for step input.
- Approximate settling: 95 percent at `3 tau`, 98 percent at `4 tau`.

### Standard second-order form
`G(s) = K omega_n^2 / (s^2 + 2 zeta omega_n s + omega_n^2)`

For equation:
`a2 d2x/dt2 + a1 dx/dt + a0 x = input`

Identify:
- `omega_n = sqrt(a0/a2)`
- `zeta = a1/(2 sqrt(a0 a2))`
- `omega_d = omega_n sqrt(1 - zeta^2)` for `0 < zeta < 1`

Damping cases:
- `zeta = 0`: undamped, continuous oscillation.
- `0 < zeta < 1`: underdamped, oscillatory decay.
- `zeta = 1`: critically damped, fastest non-oscillatory response.
- `zeta > 1`: overdamped, slow non-oscillatory response.

### Standard test signals
- Step: sudden change. Tests set-point tracking.
- Ramp: steadily changing input. Tests tracking of changing command.
- Impulse: sudden shock. Tests natural dynamics.

### Modelling building blocks
Mechanical translational:
- Spring: `F = kx`
- Damper: `F = c dx/dt`
- Mass: `F = m d2x/dt2`

Rotational:
- Torsional spring: `T = K theta`
- Rotary damper: `T = B dtheta/dt`
- Inertia: `T = J d2theta/dt2`

Electrical:
- Resistor: `v = R i`
- Inductor: `v = L di/dt`
- Capacitor: `i = C dv/dt`

Hydraulic:
- Resistance: `p1 - p2 = R q`
- Capacitance: `q_in - q_out = A dh/dt`
- Inertance neglected in most PYQs unless explicitly included.

Thermal:
- Heat flow through resistance: `q = (T1 - T2)/R_th`
- Thermal capacitance: `C_th dT/dt = heat in - heat out`

Analogies:
- Force-voltage analogy: force <-> voltage, velocity <-> current, mass <-> inductance, damper <-> resistance, spring <-> inverse capacitance.
- Force-current analogy: force <-> current, velocity <-> voltage, mass <-> capacitance, damper <-> conductance/resistance inverse, spring <-> inductance inverse depending convention.

## B. PYQ Patterns

| PYQ type | Years asked | Marks |
|---|---:|---:|
| RLC modelling and damping calculation | Dec 2022, Nov 2024, Nov 2025 | 5 to 8 |
| RC network transfer function | May 2024, Nov 2024 | 5 to 6 |
| Hydraulic height-time relation | Dec 2022, Nov 2025 | 5 to 8 |
| Thermal two-compartment equations | May 2023 | 6 |
| Mechanical/electrical analogous networks | May 2023 | 4 |
| Rotational flywheel equations | Nov 2024 | 5 |
| Second-order damping response cases | May 2024 | 4 |
| Accelerometer overshoot/rise time | Nov 2023 | 4 |

## C. Solving Approach

For modelling numericals:
1. Choose the output variable first.
2. Write element equations.
3. Apply KCL/KVL/Newton/torque/heat balance.
4. Take Laplace transform with zero initial conditions.
5. Rearrange as `output/input`.
6. Compare denominator with standard form.

For damping identification:
1. Normalize coefficient of `s^2` to 1.
2. Compare with `s^2 + 2 zeta omega_n s + omega_n^2`.
3. Compute `omega_n`, `zeta`, then `omega_d`.
4. State damping category.

## D. Final Verified Answers

### RLC repeated numerical: `R = 100 ohm, L = 2 H, C = 20 uF`
Given model:
`d2i/dt2 + (R/L) di/dt + (1/LC) i = V/(LC)`

Substitution:
- `R/L = 100/2 = 50`
- `1/(LC) = 1/(2 x 20 x 10^-6) = 25000`
- `omega_n = sqrt(25000) = 158.1 rad/s`
- `2 zeta omega_n = 50`
- `zeta = 50/(2 x 158.1) = 0.158`
- `omega_d = 158.1 sqrt(1 - 0.158^2) = 156.1 rad/s`
- State of damping: underdamped.

Step response for forcing value `V`:
`i(t) = V [1 - e^(-25t){cos(156.1t) + 0.160 sin(156.1t)}]`

### RC shunt network repeated numerical
Circuit: input `V` through `R1`; node has `R2` and `C` in parallel; output across `C`.

`Z_parallel = R2/(1 + s R2 C)`

`Vc(s)/V(s) = R2 / [R1 + R2 + s R1 R2 C]`

Standard form:
`Vc/V = [R2/(R1 + R2)] / [s (R1 R2 C/(R1 + R2)) + 1]`

So:
- Gain `K = R2/(R1 + R2)`
- Time constant `tau = R1 R2 C/(R1 + R2)`

### Series RLC output across capacitor
`Vi = Ri + L di/dt + Vc`, and `i = C dVc/dt`

`LC d2Vc/dt2 + RC dVc/dt + Vc = Vi`

`Vc(s)/Vi(s) = 1/(LC s^2 + RC s + 1)`

### Hydraulic height-time relation
For a tank of cross-sectional area `A`, upstream constant head `h1`, tank head `h2`, hydraulic resistance `R`, and inertance neglected:

`q = (h1 - h2)/R`

`A dh2/dt = q`

`R A dh2/dt + h2 = h1`

For `h2(0) = 0`:
`h2(t) = h1 [1 - e^(-t/(R A))]`

Time constant:
`tau = R A`

### Thermal two-compartment PYQ
With heater input `q`, equal thermal capacitance `C`, equal wall resistance `R`, compartment temperatures `T1`, `T2`, surroundings `T3`:

`C dT1/dt = q - (T1 - T3)/R - (T1 - T2)/R`

`C dT2/dt = (T1 - T2)/R - (T2 - T3)/R`

### Rotational two-flywheel PYQ
Flywheel `J1` connected to ground by torsional spring `Kp`; damping/friction `B12` between flywheels; flywheel `J2` has ground friction `B2`; torque input `Ta` on `J1`.

`J1 theta1'' = Ta - Kp theta1 - B12(theta1' - theta2')`

`J2 theta2'' = B12(theta1' - theta2') - B2 theta2'`

### Second-order equation PYQ
Given:
`d2x/dt2 + 5 dx/dt + 16x = 16y`

Compare with:
`s^2 + 2 zeta omega_n s + omega_n^2`

Final:
- `omega_n = 4 rad/s`
- `zeta = 5/(2 x 4) = 0.625`
- State: underdamped
- `omega_d = 4 sqrt(1 - 0.625^2) = 3.122 rad/s`
- `tr = (pi - acos(0.625))/3.122 = 0.719 s`

### Accelerometer PYQ
Given `f_n = 100 Hz`, `zeta = 0.6`.

Use `omega_n = 2 pi f_n = 628.3 rad/s`.

Percent overshoot:
`Mp = e^[-pi zeta/sqrt(1-zeta^2)] x 100 = 9.48 percent`

Rise time:
`omega_d = 628.3 sqrt(1 - 0.6^2) = 502.7 rad/s`

`tr = (pi - acos(0.6))/omega_d = 0.00441 s = 4.41 ms`

If the examiner treats "100 Hz" as `omega_n = 100 rad/s`, then `tr = 0.0277 s`; but physically correct conversion is `2 pi f`.

## E. Important Shortcuts

- First order: denominator `tau s + 1`. The coefficient of `s` is the time constant after normalizing constant term to 1.
- Second order: the constant term is `omega_n^2`.
- Hydraulic tank: area behaves like capacitance, resistance gives lag, so answer is almost always first order.
- RC with `R2 || C`: final gain is voltage-divider gain `R2/(R1+R2)`.

---

# UNIT 3 - Dynamic Response, Laplace, Controllers

## A. Core Concepts

### Physical meaning of responses
- Step response: output due to sudden constant input. It shows speed, overshoot, damping, final value.
- Ramp response: output due to linearly increasing input. It shows tracking ability and lag.
- Impulse response: output due to sudden shock. It reveals natural modes.

### First-order response formulas
For `G(s) = K/(tau s + 1)`.

Step input `A`:
`y(t) = K A [1 - e^(-t/tau)]`

Ramp input `a t`:
`y(t) = K a [t - tau + tau e^(-t/tau)]`

Impulse input of area `A`:
`y(t) = (K A/tau) e^(-t/tau)`

### Second-order performance measures
For underdamped system:

`omega_d = omega_n sqrt(1 - zeta^2)`

`t_p = pi/omega_d`

`M_p = e^[-pi zeta/sqrt(1-zeta^2)] x 100`

`t_s(2 percent) = 4/(zeta omega_n)`

`t_s(5 percent) = 3/(zeta omega_n)`

`t_r = (pi - acos(zeta))/omega_d`

### Controllers
Control actions:
- P: `u = Kp e`
- I: `u = Ki integral(e dt)`
- D: `u = Kd de/dt`
- PI: `u = Kp e + Ki integral(e dt)`
- PD: `u = Kp e + Kd de/dt`
- PID: `u = Kp e + Ki integral(e dt) + Kd de/dt`

Controller comparison:

| Controller | Rise time | Overshoot | Settling | Steady-state error | Notes |
|---|---|---|---|---|---|
| P | Decreases | Increases | Small change | Reduces but not zero | Simple, may destabilize at high gain |
| I | Decreases slowly | Increases | Increases | Eliminates | Can make system sluggish/oscillatory |
| D | Little change | Decreases | Decreases | No direct effect | Improves damping, noise sensitive |
| PI | Decreases | Increases | Increases | Eliminates | Very common for process control |
| PD | Decreases | Decreases | Decreases | Not eliminated | Useful for damping |
| PID | Decreases | Controlled | Decreases | Eliminates | Best general industrial controller if tuned |

## B. PYQ Patterns

| PYQ type | Years asked | Marks |
|---|---:|---:|
| Thermocouple first-order step/ramp/impulse | Dec 2022, Nov 2024 | 5 |
| Transfer function output for step/ramp, `G=2/(s+2)` | May 2023 | 2 |
| Transfer function output for step/ramp, `G=2/((s+3)(s+4))` | Nov 2023 | 4 |
| Performance measures of second-order system | Dec 2022 | 5 |
| Damping values for second-order step response | May 2024 | 4 |
| P, PI, PD, PID comparison | Dec 2022, May 2023, Nov 2023, May 2024, Nov 2024, Nov 2025 | 2 to 5 |

## C. Solving Approach

For response problems:
1. Write input transform: step `A/s`, ramp `a/s^2`, impulse `A`.
2. Multiply by `G(s)`.
3. Use partial fractions.
4. Inverse Laplace.
5. Substitute time value only after obtaining `y(t)`.

For second-order performance:
1. Find `omega_n`, `zeta`.
2. Check damping category.
3. If underdamped, compute `omega_d`.
4. Use direct formulas for `tr`, `tp`, `Mp`, `ts`.

## D. Final Verified Answers

### Thermocouple repeated PYQ
Given:
`G(s) = 30 x 10^-6 / (10s + 1) V/deg C`

So `K = 30 x 10^-6 V/deg C`, `tau = 10 s`.

Step input `100 deg C`:
`V(t) = 3 x 10^-3 [1 - e^(-t/10)] V`

Time to reach 95 percent:
`0.95 = 1 - e^(-t/10)`

`t = -10 ln(0.05) = 29.96 s approx 30 s`

Ramp input `5t deg C`:
`V(t) = 150 x 10^-6 [t - 10 + 10 e^(-t/10)] V`

At `t = 12 s`:
`V(12) = 7.52 x 10^-4 V approx 0.752 mV`

Impulse input of area `100 deg C`:
`V(t) = 3 x 10^-4 e^(-t/10) V`

At `t = 2 s`:
`V(2) = 2.46 x 10^-4 V approx 0.246 mV`

Corrected note: the impulse value must include the `1/tau` factor from inverse Laplace of `1/(tau s + 1)`.

### `G(s) = 2/(s+2)`
Unit step:
`Y(s) = 2/[s(s+2)]`

`y(t) = 1 - e^(-2t)`

Unit ramp:
`Y(s) = 2/[s^2(s+2)]`

`y(t) = t - 1/2 + (1/2)e^(-2t)`

### `G(s) = 2/[(s+3)(s+4)]`
Unit step:
`Y(s) = 2/[s(s+3)(s+4)]`

`y(t) = 1/6 - (2/3)e^(-3t) + (1/2)e^(-4t)`

Unit ramp:
`Y(s) = 2/[s^2(s+3)(s+4)]`

`y(t) = t/6 - 7/72 + (2/9)e^(-3t) - (1/8)e^(-4t)`

## E. Important Shortcuts

- First-order step reaches 95 percent in about `3 tau`.
- For ramp response of first order, memorize: `K a [t - tau + tau e^(-t/tau)]`.
- For impulse response, area input `A` gives `K A/tau e^(-t/tau)`.
- In controller comparison, write effect on steady-state error first. That scores quickly.

---

# UNIT 4 - MEMS, LIGA, ADC, DAS

## A. Core Concepts

### MEMS and micro-mechatronics
MEMS: micro-electro-mechanical systems that integrate mechanical microstructures, sensors, actuators, and electronics on a small substrate.

Micro-mechatronics: integration of mechanical and electronic systems at micro scale.

Functional relationship in a microsensor:
`Measurand -> micro sensing element -> transduction -> signal conditioning -> processing -> output/display/control`

For a microsystem with actuation:
`Sensor -> electronics/controller -> microactuator -> mechanical output -> feedback`.

Applications:
- Automotive: accelerometers, pressure sensors, airbag sensors.
- Medical: micro pumps, lab-on-chip, pressure sensors.
- Manufacturing: micro grippers, precision sensing.
- Consumer: microphones, inkjet print heads.

### MEMS fabrication techniques
- Bulk micromachining: removes material from substrate depth; makes cavities, membranes, high aspect structures.
- Surface micromachining: deposits and patterns thin layers on surface; sacrificial layer is removed to free moving structures.
- Lithography: pattern transfer using mask and radiation.
- Etching: wet or dry removal of selected material.
- Deposition: CVD, PVD/sputtering, evaporation, electroplating.
- Substrate preparation: cleaning, oxidation, photoresist coating, baking, alignment.

### LIGA
LIGA stands for:
- Lithographie: X-ray lithography.
- Galvanoformung: electroforming/electrodeposition.
- Abformung: molding/replication.

Process:
1. Prepare substrate and apply thick PMMA photoresist.
2. Expose with deep X-rays through mask.
3. Develop exposed regions.
4. Electroplate metal into developed cavities.
5. Remove resist to obtain metal microstructure or use it as mold insert.
6. Replicate parts by molding if required.

Advantages:
- Very high aspect ratio.
- Excellent accuracy and vertical sidewalls.
- Micro to centimeter height range.
- Good for mass replication after mold is made.

Disadvantages:
- Expensive synchrotron X-ray source.
- High setup cost.
- Economical mainly for large quantity or high precision parts.

### ADC and DAC
ADC converts analog signal to digital number.

ADC steps:
1. Signal conditioning and anti-alias filtering.
2. Sampling.
3. Sample and hold.
4. Quantization.
5. Binary encoding.

Key formulas:
- Nyquist condition: `fs >= 2 fmax`.
- Resolution for `n` bits: number of levels `= 2^n`.
- Quantization step: `Delta = VFS/2^n`.
- Quantization error: `+/- Delta/2`.

DAC converts digital number to analog output using resistor networks, weighted currents, or R-2R ladder.

### Data acquisition system (DAS)
General block:
`Sensors -> signal conditioning -> multiplexer -> sample and hold -> ADC -> microprocessor/computer -> display/storage/control -> DAC -> actuator`

Purpose:
- Acquire real-world analog signals.
- Convert to digital form.
- Process, display, store, or use for control.

## B. PYQ Patterns

| PYQ type | Years asked | Marks |
|---|---:|---:|
| LIGA process | Dec 2022, May 2023, Nov 2023, Nov 2024, Nov 2025 | 5 |
| MEMS/microsensor functional relationship | Dec 2022, May 2023, May 2024 | 5 |
| ADC process, ADC performance, sampling/quantization | May 2023, May 2024, Nov 2025 | 5 |
| ADC vs DAC | May 2023 | 5 |
| DAS and examples | Nov 2023, May 2024, Nov 2025 | 5 |
| Substrate preparation and film deposition | May 2024 | 5 |

## C. Solving Approach

For LIGA:
1. Expand the abbreviation.
2. Draw/write the three-stage flow: lithography, electroforming, molding.
3. Add two advantages and one disadvantage.
4. Add one application.

For ADC:
1. Start from analog signal.
2. Mention anti-alias filter before sampling.
3. Define sampling and quantization.
4. Give `fs >= 2fmax`, `Delta = VFS/2^n`, error `+/-Delta/2`.

For DAS:
1. Draw complete block diagram.
2. Explain each block in one line.
3. Add application example: automobile monitoring/process control.

## D. Final Verified Answers

### ADC performance factors
- Resolution: more bits gives smaller `Delta`.
- Sampling rate: must satisfy Nyquist.
- Conversion time: determines maximum signal speed.
- Quantization error/noise: limited to `+/-Delta/2`.
- Linearity: DNL/INL affects accuracy.
- Signal conditioning quality: noise and aliasing dominate if ignored.

### ADC vs DAC
| Point | ADC | DAC |
|---|---|---|
| Direction | Analog to digital | Digital to analog |
| Input | Continuous signal | Binary number |
| Output | Binary code | Analog voltage/current |
| Key stages | Sampling, quantization, encoding | Decoding, reconstruction/filtering |
| Use | Sensor data to controller | Controller output to actuator |

### DAS for automobile monitoring
Sensors measure speed, temperature, pressure, vibration, braking, acceleration.
Signal conditioning filters/amplifies.
ADC converts to digital.
Processor detects faults, logs data, warns driver, and can trigger safety action.

## E. Important Shortcuts

- LIGA answer must include German words plus process sequence.
- ADC answer must include both sampling and quantization.
- DAS block diagram is high scoring; draw it even if theory is asked.

---

# UNIT 5 - Embedded Systems, Raspberry Pi, IoT, Smart Systems

## A. Core Concepts

### Embedded systems
Embedded system: application-specific computing system built into a larger product to monitor and control it.

Core architecture:
`Sensors -> input interface/ADC -> processor or MCU -> memory/software -> output driver -> actuator/display/communication`

Components:
- Processor/MCU/SoC.
- RAM, ROM/Flash.
- GPIO, ADC/DAC, timers.
- Communication: UART, SPI, I2C, CAN, Ethernet, Wi-Fi, Bluetooth.
- Power supply.
- Real-time software/RTOS if needed.

Purpose:
- Data collection.
- Monitoring.
- Control.
- Communication.
- User interface.

### Multitasking in embedded systems
Multitasking means multiple tasks appear to run together by scheduling.

Example washing machine tasks:
- Read water level, door lock, temperature.
- Control inlet pump, heater, drain pump, motor.
- Update display/buzzer.
- Monitor faults and timeout.

RTOS/exam keywords:
- Task.
- Priority.
- Scheduler.
- Interrupt.
- Semaphore.
- Timer.

### Raspberry Pi
Raspberry Pi is a single-board computer.

Main components:
- SoC with CPU/GPU.
- RAM.
- GPIO header.
- USB, HDMI, Ethernet/Wi-Fi/Bluetooth.
- CSI camera and DSI display connectors.
- MicroSD storage.
- Power input.

Working:
1. Bootloader loads OS from microSD.
2. Linux OS runs application.
3. GPIO/sensors provide inputs.
4. Program processes data.
5. Outputs drive LEDs, relays, motors, camera, network, or cloud.

### IoT architecture
`Sensors/actuators -> edge device/MCU -> communication network -> gateway/cloud -> analytics/storage -> dashboard/user interface -> control action`

Physical layer/network technologies:
- Wi-Fi: high data rate, higher power.
- Bluetooth/BLE: short range, low power.
- ZigBee/IEEE 802.15.4: mesh, low power.
- LoRaWAN: long range, low data rate.
- Cellular/NB-IoT/LTE-M: wide area.
- Ethernet: reliable wired.
- RFID/NFC: identification/short range.

IoT risks:
- Security attacks.
- Privacy leakage.
- Interoperability issues.
- Power/battery constraints.
- Network latency.
- Data quality and false alarms.
- Maintenance and firmware update difficulty.

### Predictive maintenance
Uses IoT sensors and analytics to predict failure before breakdown.

Flow:
`Vibration/temp/current/acoustic sensors -> DAQ/edge processor -> feature extraction -> cloud/ML rule -> fault prediction -> alert/work order`

Benefits:
- Less unplanned downtime.
- Better equipment reliability.
- Planned maintenance.
- Lower spare part and labor cost.
- Better safety.

## B. PYQ Patterns

| PYQ type | Years asked | Marks |
|---|---:|---:|
| Embedded systems and multitasking case study | Dec 2022, Nov 2024 | 5 |
| Raspberry Pi components/working/application | May 2023, Nov 2023 | 5 |
| IoT physical layer/network technologies | Dec 2022, Nov 2024 | 5 |
| IoT devices, protocols, UI example | May 2024 | 5 |
| IoT risks and sensor types | Nov 2023 | 4 |
| Predictive maintenance/reliability | Nov 2025 | 5 |

## C. Solving Approach

For embedded system answers:
1. Define embedded system.
2. Draw architecture.
3. Explain input, processing, output.
4. Give one application/case study.

For Raspberry Pi:
1. Define as single-board computer.
2. List components.
3. Explain working using one example.

For IoT:
1. Draw layered architecture.
2. Mention sensors, connectivity, cloud, application.
3. Add protocols and UI/dashboard.
4. For predictive maintenance, include analytics and alerts.

## D. Final Verified Answers

### Embedded multitasking case study: washing machine
Tasks:
- `T1`: monitor door lock/water level.
- `T2`: control fill, heat, wash, drain timers.
- `T3`: read temperature and safety limits.
- `T4`: update display/buzzer.
- `T5`: fault handling.

Answer endpoint:
The scheduler gives repeated CPU time to each task; high priority safety tasks interrupt normal cycle tasks.

### Raspberry Pi application: IoT temperature monitor
Sensor connects to GPIO/I2C.
Python program reads sensor.
Data is timestamped and sent via Wi-Fi to server/cloud.
Dashboard displays temperature.
Relay/fan can be actuated if limit is crossed.

### Predictive maintenance answer
Sensors: vibration accelerometer, temperature, current, pressure, acoustic.
Edge/cloud analytics detects trends such as increasing vibration RMS or bearing temperature.
System issues alarm before failure.
Maintenance is scheduled based on condition, not fixed time.

## E. Important Shortcuts

- Raspberry Pi answer: write "SoC, RAM, GPIO, microSD, USB, HDMI, Wi-Fi/Ethernet, OS".
- IoT answer: never stop at sensors; include communication, cloud, analytics, UI.
- Predictive maintenance: "sense -> transmit -> analyze -> predict -> alert" is the full marks flow.

---

# UNIT 6 - PLC, Ladder Logic, Timers, Sequencing

## A. Core Concepts

### PLC basics
PLC scans repeatedly:
1. Read inputs.
2. Execute ladder logic.
3. Update outputs.
4. Diagnostics/communication.

Common ladder symbols:
- NO contact: `--| |--`
- NC contact: `--|/|--`
- Coil/output: `--( )`
- Timer ON delay: `TON T1 preset`
- Timer done bit: `T1.DN`

### Correct seal-in logic
Industrial motor latch:

`STOP_OK --+-- START --+----( MOTOR )`

`         |           |`

`         +-- MOTOR --+`

Where `STOP_OK` is true when stop circuit is healthy. If physical stop pushbutton is NC, PLC input is normally true; use an NO contact named `STOP_OK` in the rung.

Common mistake:
- Using stop as NO physical logic without considering PLC input state.
- Forgetting motor seal-in contact.

### Timer interlocking
For output ON for 10 s then OFF:
- Start a cycle bit.
- Output = cycle bit AND NC `T1.DN`.
- Timer runs while cycle bit is ON.
- When `T1.DN` becomes true, output turns OFF and cycle can reset.

Common mistake:
- Driving output by `T1.DN`; that turns it ON after 10 s, not during first 10 s.

### Sequential logic
Use step bits:
- `S1`: Fill
- `S2`: Heat
- `S3`: Drain

Only one step output should be active at a time. Use timer done bits and NC timer contacts to avoid overlap.

## B. PYQ Patterns

| PYQ type | Years asked | Marks |
|---|---:|---:|
| Washing machine sequence with pump/heater/drain | Dec 2022, May 2023, Nov 2023, May 2024, Nov 2025 | 8 to 10 |
| Pneumatic cylinder with 4/2 solenoid valve | Dec 2022, Nov 2023, May 2024, Nov 2025 | 8 to 10 |
| Motor start-stop seal-in | Nov 2023 | 3 |
| Grinder two-hand safety with opposite output | Nov 2024 | 8 |
| Conveyor stop for 100 s at photo sensor | Nov 2024 | 8 |
| AND/OR ladder rungs | May 2023, Nov 2024 | 2 |
| 10 s timing output | May 2024, Nov 2025 | 2 |

## C. Solving Approach

For PLC PYQs:
1. Assign input/output addresses first.
2. Write the required sequence in words.
3. Use a master RUN latch if start/stop exists.
4. Use step bits for multi-stage sequence.
5. Use TON timers with NC done contacts for dwell timing.
6. Cross-interlock mutually exclusive outputs.
7. Add reset/done logic.

Scoring method:
- 1 mark: address table.
- 2 marks: start/stop or enable logic.
- 3 marks: correct timers/sequence.
- 2 marks: output logic.
- 1 mark: interlocks/reset.

## D. Final Verified Answers

### Simple AND/OR rungs
AND: both NO switches must close.

`X1 --| |-- X2 --| |----------------( Y )`

OR: either switch can close.

`X1 --| |--+------------------------( Y )`

`          |`

`X2 --| |--+`

### Motor seal-in / latching
Inputs:
- `START`: NO momentary.
- `STOP_OK`: true when NC stop is not pressed.
- `MOTOR`: output.

Rung:
`STOP_OK --| |--+-- START --| |--+----( MOTOR )`

`              |              |`

`              +-- MOTOR --| |-+`

### 10 s timing output
Goal: output ON immediately for 10 s, then OFF.

Address:
- `START`
- `CYCLE`
- `T10`
- `Y`

Logic:
1. `START` latches `CYCLE`.
2. `TON T10` runs when `CYCLE = 1`, preset `10 s`.
3. `Y = CYCLE AND NOT T10.DN`.
4. `T10.DN` resets `CYCLE`.

This is the corrected output-on-during-timing logic.

### Washing machine sequence
Variant 1: Fill 100 s, heat 50 s, drain 100 s.

Inputs/outputs:
- `START`, `STOP_OK`
- `RUN`
- `T_FILL = 100 s`, `T_HEAT = 50 s`, `T_DRAIN = 100 s`
- `PUMP_IN`, `HEATER`, `PUMP_OUT`

Correct industrial-standard sequence:
1. `RUN` seal-in: `STOP_OK AND (START OR RUN)`.
2. Fill stage: `RUN AND NOT T_FILL.DN` -> `PUMP_IN`, run `T_FILL`.
3. Heat stage: `RUN AND T_FILL.DN AND NOT T_HEAT.DN` -> `HEATER`, run `T_HEAT`.
4. Drain stage: `RUN AND T_HEAT.DN AND NOT T_DRAIN.DN` -> `PUMP_OUT`, run `T_DRAIN`.
5. Done/reset: `T_DRAIN.DN` resets `RUN` or cycle bits.

Mutual exclusion:
- `PUMP_IN` only before `T_FILL.DN`.
- `HEATER` only after fill and before heat done.
- `PUMP_OUT` only after heat and before drain done.

Variant 2: only heat 50 s then drain 100 s:
1. `RUN` seal-in.
2. `RUN AND NOT T_HEAT.DN` -> `HEATER`.
3. `RUN AND T_HEAT.DN AND NOT T_DRAIN.DN` -> `PUMP_OUT`.
4. `T_DRAIN.DN` resets cycle.

Common verification errors corrected:
- Pump and heater must not energize together.
- Use NC timer done contacts to stop each stage.
- Timer done bit should start the next stage, not directly energize previous output.
- Add final reset; otherwise last timer remains latched forever.

### Pneumatic cylinder with 4/2 solenoid valve
Case A: automatic reciprocation by end proximity sensors.

Inputs:
- `LS_RET`: piston at retracted end.
- `LS_EXT`: piston at extended end.
- `RUN`

Outputs:
- `Y_EXT`: solenoid to extend.
- `Y_RET`: solenoid to retract.

Correct logic:
- `Y_EXT = RUN AND LS_RET AND NOT LS_EXT AND NOT Y_RET`
- `Y_RET = RUN AND LS_EXT AND NOT LS_RET AND NOT Y_EXT`

If using internal step bits:
- `EXT_STEP` sets when `LS_RET` is true; resets when `LS_EXT` is true.
- `RET_STEP` sets when `LS_EXT` is true; resets when `LS_RET` is true.
- Outputs are cross-interlocked.

Case B: momentary pushbutton for either direction.

Inputs:
- `PB_EXT`, `PB_RET`, `LS_EXT`, `LS_RET`, `STOP_OK`

Logic:
- `EXT_REQ` latches by `PB_EXT`, resets by `LS_EXT` or `PB_RET`.
- `RET_REQ` latches by `PB_RET`, resets by `LS_RET` or `PB_EXT`.
- `Y_EXT = STOP_OK AND EXT_REQ AND NOT Y_RET`
- `Y_RET = STOP_OK AND RET_REQ AND NOT Y_EXT`

Common mistake:
- Energizing both solenoids at once. Always cross-interlock.

### Grinder two-hand safety PYQ
Inputs:
- `X1`, `X2`: NO momentary two-hand start buttons.
- `X3`: physical NC stop button. PLC input is true when not pressed, so name it `STOP_OK`.

Outputs:
- `Y1`: grinder motor.
- `Y2`: opposite of `Y1`.

Correct logic:
- `Y1 = STOP_OK AND [(X1 AND X2) OR Y1]`
- `Y2 = NOT Y1`

Ladder idea:
`STOP_OK --| |--+-- X1 --| |-- X2 --| |--+----( Y1 )`

`              |                         |`

`              +-- Y1 --| |--------------+`

`Y1 --|/|------------------------------------( Y2 )`

Safety note:
- Both hands are required only to start.
- Seal-in keeps grinder running.
- Pressing NC stop opens `STOP_OK` and drops `Y1`.

### Conveyor with photo sensor and 100 s dwell
Inputs:
- `START`, `STOP_OK`, `PHOTO`: item detected at station.

Outputs:
- `MOTOR`

Internal:
- `RUN`, `DWELL`, `T_DWELL = 100 s`

Correct sequence:
1. `RUN = STOP_OK AND (START OR RUN)`.
2. When `RUN AND PHOTO`, latch `DWELL`.
3. During dwell, `MOTOR = RUN AND NOT DWELL`.
4. `TON T_DWELL` runs when `DWELL = 1`.
5. When `T_DWELL.DN`, reset `DWELL`, motor restarts.
6. If stop is pressed, reset `RUN` and `DWELL`.

Common mistake:
- Stopping permanently at the sensor without restart after 100 s.

## E. Important Shortcuts

- Latch formula: `Output = Stop_OK AND (Start OR Output)`.
- Timer-output formula: `Output = Enable AND NOT Timer.DN`.
- Sequence formula: previous timer done starts next stage; current timer done stops current stage.
- Mutual exclusion: `Y1` rung includes NC `Y2`; `Y2` rung includes NC `Y1`.
- PLC exams reward clean address tables. Always start ladder answers with inputs/outputs.

---

# Final PYQ Checklist Before Exam

1. Block diagram reduction: practice both repeated diagrams and remember shifting correction rules.
2. Thermostat block diagram: comparator, relay/controller, heater, plant, sensor feedback.
3. RLC numerical: `omega_n = 158.1 rad/s`, `zeta = 0.158`, `omega_d = 156.1 rad/s`, underdamped.
4. Equation `x'' + 5x' + 16x = 16y`: `omega_n = 4`, `zeta = 0.625`, `omega_d = 3.122`, `tr = 0.719 s`.
5. Thermocouple: step 95 percent time `30 s`; ramp at 12 s `7.52 x 10^-4 V`; impulse at 2 s `2.46 x 10^-4 V`.
6. RC network: gain `R2/(R1+R2)`, time constant `R1R2C/(R1+R2)`.
7. LIGA: lithography, electroforming, molding.
8. ADC: sampling, quantization, encoding; `fs >= 2 fmax`; error `+/-Delta/2`.
9. IoT predictive maintenance: sensor, edge/cloud analytics, warning, planned maintenance.
10. PLC: seal-in, NC timer interlocking, mutually exclusive solenoids, final reset.

