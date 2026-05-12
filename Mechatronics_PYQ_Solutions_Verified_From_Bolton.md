# Mechatronics PYQ Solutions - Verified From Reference Book

Question source: `D:/Downloads/Mechatronics_PYQ_Final_Verified.docx`  
Reference used: `D:/Downloads/TY sem 2/Mechatronix/mechatronics-electronic-control-systems-in-mechanical-and-electrical-engineering.pdf`

## Reference Verification Anchors

- Closed-loop control: comparison element produces `error = reference - measured value`; negative feedback is required for control. Verified from reference text around lines 860-876.
- Room thermostat block: thermostatic element compares required temperature and controls switching of heater. Verified around lines 932-955.
- Bath temperature block diagram: differential amplifier, relay, heater, measurement feedback. Verified from book answer around lines 30419-30428.
- Measurement system elements: sensor, signal conditioner, display/data presentation. Verified around lines 7074-7079.
- First-order step response and time constant: `x = SSV(1 - e^(-t/tau))`, `tau = a1/a0`, 63 percent response. Verified around lines 22860-22980.
- Thermocouple example `30 x 10^-6/(10s+1)`: step, ramp, impulse solution method. Verified around lines 23973-24037.
- Second-order response performance: overshoot, damping, settling time. Verified around lines 23480-23525 and 23645-23688.
- PLC ladder, latching, sequencing, timers: verified around lines 17840-18430 and PYQ-style PLC problems around lines 18895-18931.
- MEMS definition and airbag example: verified around lines 1497-1528.

Important correction notes:
- The reference book answer key for rolled-sheet thickness sensor gives: **LVDT displacement sensor**. Use this for exam. Non-contact eddy-current sensors are also industrially valid, but not the Bolton answer key.
- Bolton's second-order rise-time convention in this chapter is `tr = pi/(2 omega_d)`. Some control books use `tr = (pi - acos(zeta))/omega_d`. For this paper, use Bolton's convention unless teacher says otherwise.
- Thermocouple impulse: the book prints `V(t)=3 x 10^-4 e^(-0.1t)`. For `t=2 s`, this evaluates to `2.46 x 10^-4 V`. The printed/book-slide value `1.8 x 10^-4 V` is not consistent with the equation for 2 s.

---

# QUESTION 1 - Control Systems, Sensors, Block Diagrams

## 1A. Bath temperature control system

Required answer:

```text
Reference voltage/set value
        |
        v
  (+) Comparator / differential amplifier (-) <--- Measurement feedback voltage
        |
        v
     Relay / controller
        |
        v
  Heater power control
        |
        v
 Liquid bath / process
        |
        v
 Temperature sensor + measurement system
        |
        +-------------------- feedback voltage
```

Explanation:
- Reference voltage represents required bath temperature.
- Measurement system senses actual bath temperature and converts it to feedback voltage.
- Differential amplifier compares both voltages.
- Error signal:

```text
e = reference voltage - feedback voltage
```

- If actual temperature is below set value, error drives relay to switch heater ON.
- When actual temperature reaches set value, error becomes small/zero and relay switches heater OFF.

Book-verified endpoint: comparison element gives error signal; feedback is negative.

## 1B. Room thermostat block diagram

```text
Required temperature -> thermostat/comparator -> switch/controller -> heater -> room temperature
       ^                                                                  |
       |                                                                  |
       +---------------- measured room temperature ------------------------+
```

Key points:
- Thermostat combines comparison and switching action.
- It switches ON when temperature falls below set value.
- It switches OFF when temperature reaches set value.
- This is an ON/OFF closed-loop control system.

## 1C. Sensor, signal conditioner, display elements

### Mercury-in-glass thermometer

| Element | Answer |
|---|---|
| Sensor | Mercury bulb |
| Signal conditioner | Expansion of mercury in capillary / calibrated bore |
| Display | Graduated glass scale |

### Bourdon pressure gauge

| Element | Answer |
|---|---|
| Sensor | Bourdon tube |
| Signal conditioner | Linkage, sector gear, pinion mechanism |
| Display | Pointer and dial |

## 1D. Rolled sheet thickness measurement

Reference-book answer: **LVDT displacement sensor**.

Solution arrangement:
- Use an LVDT-based displacement measuring probe/roller arrangement.
- Sheet passes between rollers or reference surface and sensing probe.
- Displacement of probe varies with sheet thickness.
- LVDT converts displacement into an AC electrical signal.
- Signal is demodulated/conditioned and used for thickness control.

If using two displacement sensors:

```text
Thickness t = fixed gap D - measured clearance d
```

or for two opposed sensors:

```text
t = D - d1 - d2
```

Exam words:
- Fast response.
- Continuous measurement.
- Electrical output.
- Suitable for automatic feedback control.

## 1E. Block diagram reduction rules

Core formulas:

```text
Series:    Geq = G1 G2
Parallel:  Geq = G1 + G2
Negative feedback: Geq = G/(1 + GH)
Positive feedback: Geq = G/(1 - GH)
```

Block shifting corrections:

| Operation | Correction |
|---|---|
| Move summing point before block G to after G | multiply side branch by G |
| Move summing point after block G to before G | divide side branch by G |
| Move takeoff point before block G to after G | insert 1/G in takeoff branch |
| Move takeoff point after block G to before G | insert G in takeoff branch |

### Repeated block diagram final expression - type 1

For repeated diagram with `G1`, `G2`, `G3`, and feedbacks `H1`, `H2`, `H3`:

```text
C(s)/R(s) = G1 G2 G3 / [(1 + G3 H3)(1 + G2 H2 + G1 G2 H1)]
```

### Repeated block diagram final expression - type 2

For diagram with `G1G2`, parallel block `(G3 + G4)`, block `G5`, feedbacks `H1`, `H2`, `H3`:

```text
Y(s)/R(s) =
G1 G2 G5 (G3 + G4)
-------------------------------------------------------------
(1 + G1 G2 H1)(1 + G5 H3(G3 + G4)) - G1 G2 H2(G3 + G4)
```

If the `H2` branch is negative in the given diagram, change the minus term to plus.

---

# QUESTION 2 - System Modelling

## 2A. Hydraulic system: relation between `h2` and time

Assume:
- constant head/source height = `h1`
- output tank head = `h2`
- hydraulic resistance = `R`
- tank cross-sectional area = `A`
- inertance neglected

Flow through resistance:

```text
q = (h1 - h2)/R
```

Continuity:

```text
A dh2/dt = q
```

Therefore:

```text
R A dh2/dt + h2 = h1
```

For `h2(0)=0`:

```text
h2(t) = h1[1 - e^(-t/(RA))]
```

Time constant:

```text
tau = R A
```

Final answer: first-order rise of `h2` to `h1`.

## 2B. RLC system numerical

Given:

```text
R = 100 ohm
L = 2 H
C = 20 uF
d2i/dt2 + (R/L) di/dt + (1/LC)i = V/(LC)
```

Substitute:

```text
R/L = 100/2 = 50
1/(LC) = 1/(2 x 20 x 10^-6) = 25000
```

Standard second-order form:

```text
d2i/dt2 + 2 zeta omega_n di/dt + omega_n^2 i = omega_n^2 V
```

Thus:

```text
omega_n = sqrt(25000) = 158.1 rad/s
2 zeta omega_n = 50
zeta = 50/(2 x 158.1) = 0.158
```

State of damping:

```text
0 < zeta < 1, so system is underdamped
```

Damped angular frequency:

```text
omega_d = omega_n sqrt(1 - zeta^2)
omega_d = 158.1 sqrt(1 - 0.158^2)
omega_d = 156.1 rad/s
```

Response for step input `V`:

```text
i(t) = V[1 - e^(-25t){cos(156.1t) + 0.160 sin(156.1t)}]
```

## 2C. RC circuit: output across capacitor

For series `R-L-C` output across capacitor:

```text
Vi = Ri + L di/dt + Vc
i = C dVc/dt
```

Therefore:

```text
LC d2Vc/dt2 + RC dVc/dt + Vc = Vi
```

Transfer function:

```text
Vc(s)/Vi(s) = 1/(LCs^2 + RCs + 1)
```

For circuit with input through `R1`, and output node containing `R2 || C`:

```text
Vc(s)/V(s) = R2 / [R1 + R2 + s R1 R2 C]
```

Standard first-order form:

```text
Vc/V = [R2/(R1 + R2)] / [s(R1R2C/(R1 + R2)) + 1]
```

Final:

```text
Gain K = R2/(R1 + R2)
tau = R1R2C/(R1 + R2)
```

## 2D. Thermal two-compartment system

Assume:
- heater input = `q`
- compartment temperatures = `T1`, `T2`
- surrounding temperature = `T3`
- each wall resistance = `R`
- each compartment thermal capacitance = `C`

Heat balance for compartment 1:

```text
C dT1/dt = q - (T1 - T3)/R - (T1 - T2)/R
```

Heat balance for compartment 2:

```text
C dT2/dt = (T1 - T2)/R - (T2 - T3)/R
```

## 2E. Accelerometer overshoot and rise time

Given:

```text
zeta = 0.6
omega_n = 100 rad/s  (Bolton convention, even when question writes Hz)
```

Maximum percentage overshoot:

```text
Mp = exp[-pi zeta/sqrt(1-zeta^2)] x 100
Mp = exp[-pi(0.6)/sqrt(1-0.36)] x 100
Mp = 9.5 %
```

Damped angular frequency:

```text
omega_d = 100 sqrt(1 - 0.6^2) = 80 rad/s
```

Using Bolton rise-time convention:

```text
tr = pi/(2 omega_d) = pi/(160) = 0.0196 s
```

Final:

```text
Percentage overshoot = 9.5 %
Rise time = 0.020 s
```

## 2F. Second-order step response for damping factor

| Damping factor | Response form |
|---|---|
| `zeta = 0` | undamped, continuous oscillation |
| `0 < zeta < 1`, e.g. `0.5` | underdamped, oscillatory decay, overshoot |
| `zeta = 1` | critically damped, fastest non-oscillatory response |
| `zeta > 1`, e.g. `1.5` | overdamped, slow non-oscillatory response |

## 2G. Rotational flywheel equations

Let:
- `J1`, `J2` = flywheel inertias
- `Kf` = flexible shaft stiffness to ground
- `Br1` = friction/damping between flywheels
- `Br2` = friction of second flywheel to ground
- input torque = `Ta`
- angular displacements = `theta1`, `theta2`

Equations:

```text
J1 theta1'' = Ta - Kf theta1 - Br1(theta1' - theta2')
```

```text
J2 theta2'' = Br1(theta1' - theta2') - Br2 theta2'
```

---

# QUESTION 3 - Dynamic Response and Controllers

## 3A. Thermocouple response

Given:

```text
G(s) = 30 x 10^-6/(10s + 1) V/deg C
K = 30 x 10^-6
tau = 10 s
```

### Step input of 100 deg C

Input:

```text
Theta(s) = 100/s
```

Output:

```text
V(s) = [30 x 10^-6/(10s+1)] [100/s]
```

Time response:

```text
V(t) = 3 x 10^-3 [1 - e^(-t/10)] V
```

Steady-state value:

```text
Vss = 3 x 10^-3 V
```

Time for 95 percent:

```text
0.95 = 1 - e^(-t/10)
e^(-t/10) = 0.05
t = -10 ln(0.05) = 29.96 s
```

Final:

```text
t95 = 30 s
```

### Ramp input `5t deg C/s`

Input transform:

```text
Theta(s) = 5/s^2
```

Output:

```text
V(t) = 150 x 10^-6 [t - 10 + 10 e^(-t/10)] V
```

At `t = 12 s`:

```text
V(12) = 150 x 10^-6 [12 - 10 + 10e^-1.2]
V(12) = 7.52 x 10^-4 V
```

Reference-book rounded value:

```text
V(12) approx 7.5 x 10^-4 V
```

### Impulse input of area `100 deg C`

Input transform:

```text
Theta(s) = 100
```

Output transform:

```text
V(s) = 30 x 10^-6 x 100/(10s+1)
     = 3 x 10^-4/(s+0.1)
```

Time response:

```text
V(t) = 3 x 10^-4 e^(-0.1t) V
```

At `t = 2 s`:

```text
V(2) = 3 x 10^-4 e^-0.2
V(2) = 2.46 x 10^-4 V
```

Book discrepancy:
- The reference text prints `1.8 x 10^-4 V`, but its own equation gives `2.46 x 10^-4 V` for 2 s.
- In exam, show the equation and substitution. If your teacher follows the printed slide value, mention `1.8 x 10^-4 V` as printed-book value.

## 3B. Transfer function `G(s)=2/(s+2)`

### Unit step input

```text
Y(s) = G(s) x 1/s = 2/[s(s+2)]
```

Partial fraction:

```text
2/[s(s+2)] = 1/s - 1/(s+2)
```

Final:

```text
y(t) = 1 - e^(-2t)
```

### Unit ramp input

```text
Y(s) = 2/[s^2(s+2)]
```

Final:

```text
y(t) = t - 1/2 + (1/2)e^(-2t)
```

## 3C. Transfer function `G(s)=2/[(s+3)(s+4)]`

### Unit step input

```text
Y(s) = 2/[s(s+3)(s+4)]
```

Partial fraction:

```text
Y(s) = 1/(6s) - 2/[3(s+3)] + 1/[2(s+4)]
```

Final:

```text
y(t) = 1/6 - (2/3)e^(-3t) + (1/2)e^(-4t)
```

### Unit ramp input

```text
Y(s) = 2/[s^2(s+3)(s+4)]
```

Partial fraction:

```text
Y(s) = -7/(72s) + 1/(6s^2) + 2/[9(s+3)] - 1/[8(s+4)]
```

Final:

```text
y(t) = t/6 - 7/72 + (2/9)e^(-3t) - (1/8)e^(-4t)
```

## 3D. Second-order equation

Given:

```text
d2x/dt2 + 5 dx/dt + 16x = 16y
```

Compare with:

```text
d2x/dt2 + 2 zeta omega_n dx/dt + omega_n^2 x = omega_n^2 y
```

Therefore:

```text
omega_n^2 = 16
omega_n = 4 rad/s
```

```text
2 zeta omega_n = 5
zeta = 5/(2 x 4) = 0.625
```

Damping:

```text
0 < zeta < 1, so underdamped
```

Damped frequency:

```text
omega_d = omega_n sqrt(1 - zeta^2)
omega_d = 4 sqrt(1 - 0.625^2)
omega_d = 3.12 rad/s
```

Rise time by Bolton convention:

```text
tr = pi/(2 omega_d)
tr = pi/(2 x 3.12)
tr = 0.503 s
```

Final:

```text
omega_n = 4 rad/s
zeta = 0.625
omega_d = 3.12 rad/s
tr = 0.50 s
```

## 3E. Performance measures for second-order system

For underdamped response:

```text
omega_d = omega_n sqrt(1 - zeta^2)
tp = pi/omega_d
tr = pi/(2 omega_d)     [Bolton convention]
Mp = exp[-pi zeta/sqrt(1-zeta^2)] x 100
ts(2%) = 4/(zeta omega_n)
ts(5%) = 3/(zeta omega_n)
```

Meaning:
- Rise time: speed of response.
- Peak time: time to first maximum.
- Overshoot: maximum crossing above steady value.
- Settling time: time to remain close to final value.
- Damping ratio: controls oscillation and overshoot.

## 3F. Controller comparison

| Controller | Effect on steady-state error | Effect on stability/response | Exam line |
|---|---|---|---|
| P | Reduces but does not eliminate | Faster response, high gain may cause oscillation | Simple but offset remains |
| PI | Eliminates steady-state error | More overshoot, longer settling if poorly tuned | Used in process control |
| PD | Little/no direct effect on steady-state error | Adds damping, improves transient response | Noise sensitive |
| PID | Eliminates error and improves transient response | Best if tuned properly | Most complete industrial action |

PI control:

```text
u(t) = Kp e(t) + Ki integral e(t) dt
```

PID control:

```text
u(t) = Kp e(t) + Ki integral e(t) dt + Kd de/dt
```

---

# QUESTION 4 - MEMS, LIGA, ADC, DAS

## 4A. MEMS and microsensor functional relationship

Reference-book MEMS definition:
- MEMS are mechanical devices built onto semiconductor chips.
- They include microsensors, microactuators, and microprocessor/electronics.
- They sense, control, and actuate mechanical processes at micro scale.

Functional relationship:

```text
Measurand
   -> microsensing element
   -> transduction
   -> signal conditioning
   -> processing/controller
   -> output/display/control signal
```

With actuation:

```text
Sensor -> signal conditioning -> controller -> microactuator -> mechanical output
```

Applications:
- Airbag accelerometer.
- Inkjet printer head.
- Pressure sensors.
- Micro pumps.
- Medical diagnostic devices.
- Micro grippers.

## 4B. LIGA process

Note: the extracted reference PDF verifies MEMS but does not expose LIGA details clearly; LIGA sequence is verified from the provided Unit IV PPT/course notes.

LIGA full form:

```text
Lithographie  -> X-ray lithography
Galvanoformung -> electroforming/electrodeposition
Abformung -> molding/replication
```

Process:
1. Prepare substrate.
2. Coat thick PMMA/photoresist.
3. Expose through X-ray mask.
4. Develop exposed resist.
5. Electroform metal into developed cavities.
6. Strip resist.
7. Use metal microstructure directly or as mold insert for replication.

Advantages:
- High aspect ratio.
- Very accurate vertical sidewalls.
- Good surface finish.
- Suitable for mass replication.

Disadvantages:
- Expensive.
- Needs X-ray/synchrotron setup.
- Not economical for small quantity.

Comparison with other MEMS fabrication:

| Method | Main idea | Best for | Limitation |
|---|---|---|---|
| Bulk micromachining | Etch into silicon bulk | cavities, membranes | substrate-dependent |
| Surface micromachining | deposit/sacrifice thin layers | small movable parts | lower height |
| LIGA | X-ray lithography + electroforming + molding | high-aspect-ratio parts | expensive |

## 4C. ADC and DAC comparison

| Point | ADC | DAC |
|---|---|---|
| Conversion | Analog to digital | Digital to analog |
| Input | Voltage/current from sensor | Binary data |
| Output | Binary word | Analog voltage/current |
| Main stages | sampling, quantization, encoding | decoding, reconstruction |
| Use | sensor to computer/PLC | controller to actuator |

ADC steps:

```text
Analog signal -> anti-alias filter -> sample and hold -> quantizer -> encoder -> digital output
```

Important formulas:

```text
Sampling condition: fs >= 2 fmax
Number of levels = 2^n
Resolution step = full-scale range / 2^n
Quantization error = +/- half LSB
```

Factors affecting ADC performance:
- Resolution.
- Sampling rate.
- Conversion time.
- Quantization error.
- Linearity.
- Noise.
- Input signal conditioning.

## 4D. Data acquisition system

Book-verified flow:

```text
Sensors
 -> signal conditioning
 -> multiplexer
 -> amplifier
 -> ADC
 -> data/control register
 -> computer/processor
 -> display/storage/control
 -> DAC if actuator output is analog
 -> actuator
```

Explanation:
- Sensor converts physical variable to electrical signal.
- Signal conditioner amplifies/filters/linearizes.
- Multiplexer selects one of many channels.
- ADC converts analog signal into digital data.
- Computer processes and stores data.
- Control output may be sent through DAC/driver to actuator.

Automobile DAS example:
- Sensors: temperature, speed, pressure, vibration, acceleration, fuel level.
- ECU/DAQ reads and processes values.
- System performs monitoring, fault detection, warning, safety control, driver assistance.

---

# QUESTION 5 - Embedded Systems, Raspberry Pi, IoT

## 5A. Embedded systems

Definition:

```text
An embedded system is a dedicated computer-based system built into a larger device to monitor, control, or perform a specific function.
```

Architecture:

```text
Sensors -> input interface/ADC -> microcontroller/processor -> memory/software -> output driver -> actuator/display
```

Components:
- Processor or microcontroller.
- RAM and ROM/Flash.
- Input/output ports.
- Timers.
- ADC/DAC.
- Communication interfaces.
- Power supply.
- Embedded software/RTOS.

Multitasking case study: washing machine

Tasks:
- Read water level.
- Read temperature.
- Control inlet pump.
- Control heater.
- Control drain pump.
- Update display/buzzer.
- Monitor safety faults.

Conclusion:
- Scheduler or cyclic program gives time to each task.
- Safety tasks get higher priority.

## 5B. Raspberry Pi

Definition:

```text
Raspberry Pi is a small single-board computer with CPU, memory, GPIO, storage interface, display/audio/video ports, and communication interfaces.
```

Main components:
- SoC with CPU/GPU.
- RAM.
- GPIO pins.
- microSD card.
- USB.
- HDMI.
- Ethernet/Wi-Fi/Bluetooth.
- Camera/display connectors.
- Power input.

Working example: temperature monitoring
1. Temperature sensor connected to GPIO/I2C.
2. Raspberry Pi reads data using program.
3. Data is processed and displayed/stored.
4. If limit exceeds, relay/fan is switched.
5. Data can be sent to cloud/dashboard.

## 5C. IoT physical layer network technologies

| Technology | Use | Advantage | Limitation |
|---|---|---|---|
| Wi-Fi | home/industrial gateway | high data rate | higher power |
| BLE | wearable/short range | low power | short range |
| ZigBee | sensor mesh | low power mesh | lower data rate |
| LoRaWAN | long-range sensor network | long range | very low data rate |
| Cellular/NB-IoT | wide-area IoT | wide coverage | cost/SIM dependence |
| Ethernet | industrial wired | reliable | wired only |
| RFID/NFC | identification | simple, low power | very short range |

IoT architecture:

```text
Sensors/actuators -> edge controller -> network/gateway -> cloud/server -> analytics -> user interface -> control action
```

Risks:
- Security attacks.
- Privacy issues.
- Network failure.
- Interoperability.
- Power consumption.
- Data accuracy problems.

## 5D. Predictive maintenance

Process:

```text
Sensors -> DAQ/edge device -> cloud/analytics -> fault prediction -> alert/work order
```

Sensors:
- Vibration.
- Temperature.
- Current.
- Pressure.
- Acoustic emission.

How reliability improves:
- Early fault detection.
- Less unplanned downtime.
- Maintenance scheduled before failure.
- Better spare planning.
- Improved safety.

## 5E. Sampling and quantization in ADC

Sampling:
- Converts continuous-time signal into discrete-time values.
- Must follow Nyquist:

```text
fs >= 2 fmax
```

Quantization:
- Converts each sampled amplitude into nearest digital level.
- For `n` bits:

```text
levels = 2^n
step size = full-scale range / 2^n
error = +/- step/2
```

---

# QUESTION 6 - PLC Verified Solutions

## PLC reference basics

PLC scan:

```text
Read inputs -> execute ladder program -> update outputs -> repeat
```

Ladder rules:
- Inputs/contacts are placed before output coil.
- Series contacts = AND.
- Parallel contacts = OR.
- Output latch uses output contact in parallel with start contact.
- Timers behave like relays whose contacts change after preset delay.

## 6A. Basic AND rung

Question: two NO switches both must be closed for motor to operate.

```text
X1 --| |-- X2 --| |----------------( Y )
```

Logic:

```text
Y = X1 AND X2
```

## 6B. Basic OR rung

Question: either of two NO switches can energize coil.

```text
X1 --| |--+------------------------( Y )
          |
X2 --| |--+
```

Logic:

```text
Y = X1 OR X2
```

## 6C. Motor start-stop latch

Inputs:

```text
START = NO pushbutton
STOP_OK = NC stop input healthy/true when not pressed
MOTOR = output
```

Ladder:

```text
STOP_OK --| |--+-- START --| |--+----( MOTOR )
              |              |
              +-- MOTOR --| |-+
```

Logic:

```text
MOTOR = STOP_OK AND (START OR MOTOR)
```

## 6D. Timing circuit: output ON for 10 s then OFF

Industrial-correct solution:

```text
START latches CYCLE
TON T1 runs while CYCLE is ON
Y = CYCLE AND NOT T1.DN
T1.DN resets CYCLE
```

Rung form:

```text
START --| |------------------------( SET CYCLE )

CYCLE --| |------------------------( TON T1, 10 s )

CYCLE --| |-- T1.DN --|/|----------( Y )

T1.DN --| |------------------------( RESET CYCLE )
```

Important: using `T1.DN` directly to energize output would switch the output ON after 10 s, which is wrong.

## 6E. Washing machine sequence

Required:
1. Fill pump ON for 100 s.
2. Fill pump OFF, heater ON for 50 s.
3. Heater OFF, drain pump ON for 100 s.
4. Stop/reset.

Addresses:

| Symbol | Meaning |
|---|---|
| `START` | start pushbutton |
| `STOP_OK` | stop/safety healthy |
| `RUN` | cycle latch |
| `T_FILL` | 100 s fill timer |
| `T_HEAT` | 50 s heat timer |
| `T_DRAIN` | 100 s drain timer |
| `PUMP_IN` | inlet pump |
| `HEATER` | heater |
| `PUMP_OUT` | drain pump |

Correct ladder logic:

```text
STOP_OK --| |--+-- START --| |--+----( RUN )
              |              |
              +-- RUN ----| |-+

RUN --| |-- T_FILL.DN --|/|----------( PUMP_IN )
RUN --| |-- T_FILL.DN --|/|----------( TON T_FILL, 100 s )

RUN --| |-- T_FILL.DN --| |-- T_HEAT.DN --|/|----( HEATER )
RUN --| |-- T_FILL.DN --| |-- T_HEAT.DN --|/|----( TON T_HEAT, 50 s )

RUN --| |-- T_HEAT.DN --| |-- T_DRAIN.DN --|/|---( PUMP_OUT )
RUN --| |-- T_HEAT.DN --| |-- T_DRAIN.DN --|/|---( TON T_DRAIN, 100 s )

T_DRAIN.DN --| |--------------------( RESET RUN )
```

Key verification:
- Only one output is ON in each stage.
- Timer done bit of previous stage enables next stage.
- NC timer done contact stops current output.
- Final drain done resets the cycle.

## 6F. Pneumatic cylinder using 4/2 solenoid valve: proximity sensor version

Inputs:

```text
LS_RET = sensor at retracted end
LS_EXT = sensor at extended end
RUN = system enable
```

Outputs:

```text
Y_EXT = extend solenoid
Y_RET = retract solenoid
```

Logic:

```text
Y_EXT = RUN AND LS_RET AND NOT LS_EXT AND NOT Y_RET
Y_RET = RUN AND LS_EXT AND NOT LS_RET AND NOT Y_EXT
```

Ladder:

```text
RUN --| |-- LS_RET --| |-- LS_EXT --|/|-- Y_RET --|/|----( Y_EXT )

RUN --| |-- LS_EXT --| |-- LS_RET --|/|-- Y_EXT --|/|----( Y_RET )
```

Important:
- `Y_EXT` and `Y_RET` must be mutually exclusive.
- Cross-interlock solenoids using NC contacts.

## 6G. Pneumatic cylinder: momentary pushbutton version

Inputs:

```text
PB_EXT = extend pushbutton
PB_RET = retract pushbutton
LS_EXT = extended limit
LS_RET = retracted limit
STOP_OK = safety/stop healthy
```

Internal latches:

```text
EXT_REQ
RET_REQ
```

Logic:

```text
EXT_REQ sets by PB_EXT
EXT_REQ resets by LS_EXT or PB_RET

RET_REQ sets by PB_RET
RET_REQ resets by LS_RET or PB_EXT

Y_EXT = STOP_OK AND EXT_REQ AND NOT Y_RET
Y_RET = STOP_OK AND RET_REQ AND NOT Y_EXT
```

## 6H. Grinder two-hand safety logic

Inputs:

```text
X1, X2 = NO momentary two-hand buttons
X3 = NC stop pushbutton
STOP_OK = true when X3 is not pressed
```

Outputs:

```text
Y1 = grinder motor coil
Y2 = opposite of Y1
```

Correct logic:

```text
Y1 = STOP_OK AND [(X1 AND X2) OR Y1]
Y2 = NOT Y1
```

Ladder:

```text
STOP_OK --| |--+-- X1 --| |-- X2 --| |--+----( Y1 )
              |                         |
              +-- Y1 --| |--------------+

Y1 --|/|--------------------------------( Y2 )
```

Explanation:
- Both hands required to start.
- Seal-in keeps motor ON after buttons release.
- Pressing NC stop breaks `STOP_OK`, dropping `Y1`.
- `Y2` is exactly opposite of `Y1`.

## 6I. Conveyor dwell for 100 s at workstation

Inputs:

```text
START = NO start
STOP_OK = NC stop healthy
PHOTO = item detected at station
```

Outputs/internal:

```text
MOTOR = conveyor motor
RUN = conveyor enabled
DWELL = item stopped for operation
T_DWELL = 100 s timer
```

Correct sequence:

```text
STOP_OK AND (START OR RUN) -> RUN
RUN AND PHOTO -> SET DWELL
DWELL -> TON T_DWELL, 100 s
MOTOR = RUN AND NOT DWELL
T_DWELL.DN -> RESET DWELL
STOP not OK -> RESET RUN and DWELL
```

Ladder:

```text
STOP_OK --| |--+-- START --| |--+----( RUN )
              |              |
              +-- RUN ----| |-+

RUN --| |-- PHOTO --| |----------------( SET DWELL )

DWELL --| |----------------------------( TON T_DWELL, 100 s )

RUN --| |-- DWELL --|/|----------------( MOTOR )

T_DWELL.DN --| |-----------------------( RESET DWELL )
```

Key point:
- Motor stops only during the 100 s dwell.
- Motor restarts automatically after `T_DWELL.DN`.

---

# Final High-Probability Answer Sheet

| Topic | Final verified answer |
|---|---|
| Bath control error | `e = reference voltage - measured feedback voltage` |
| Thermostat | closed-loop ON/OFF control; thermostat acts as comparator + switch |
| Rolled sheet sensor | LVDT displacement sensor, per reference answer key |
| Measurement system elements | sensor + signal conditioner + display/data presentation |
| Hydraulic tank | `RA dh2/dt + h2 = h1`; `h2 = h1(1-e^(-t/RA))` |
| RLC numerical | `omega_n=158.1 rad/s`, `zeta=0.158`, `omega_d=156.1 rad/s`, underdamped |
| Accelerometer | overshoot `9.5%`, rise time `0.020 s` by Bolton convention |
| `x''+5x'+16x=16y` | `omega_n=4`, `zeta=0.625`, `omega_d=3.12`, `tr=0.50 s` |
| Thermocouple step | `V=3e-3(1-e^-t/10)`, `t95=30 s` |
| Thermocouple ramp | `V=150e-6[t-10+10e^-t/10]`, `V(12)=7.5e-4 V` |
| Thermocouple impulse | `V=3e-4e^-0.1t`, mathematically `V(2)=2.46e-4 V` |
| `G=2/(s+2)` step | `y=1-e^-2t` |
| `G=2/(s+2)` ramp | `y=t-1/2+(1/2)e^-2t` |
| `G=2/((s+3)(s+4))` step | `y=1/6-(2/3)e^-3t+(1/2)e^-4t` |
| `G=2/((s+3)(s+4))` ramp | `y=t/6-7/72+(2/9)e^-3t-(1/8)e^-4t` |
| ADC Nyquist | `fs >= 2 fmax` |
| ADC quantization | levels `2^n`, error `+/- half LSB` |
| PLC latch | `Output = STOP_OK AND (START OR Output)` |
| PLC 10 s output | `Y = CYCLE AND NOT T1.DN` |
| Cylinder outputs | cross-interlock `Y_EXT` and `Y_RET` |
| Washing machine | fill 100 s, heat 50 s, drain 100 s with NC timer done interlocks |

