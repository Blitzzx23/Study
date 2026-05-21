# 🔬 Unit IV — Micro Mechatronic Systems & Data Acquisition

---

## 🔷 Micro Mechatronics

> [!NOTE]
> **Micro Mechatronics** is the synergetic integration of mechanical and electronic systems based on **scaling effects at the microscale (µm range)**. It is a key enabler in areas like electronic automotive technology and medical devices.

---

## 🔷 MEMS vs. Microelectronics

| Feature | Microelectronics (ME) | MEMS |
|---|---|---|
| **Materials** | Silicon, metals | Silicon, metals, polymers, glass |
| **Functions** | Electrical only | Electrical + Mechanical + Optical + Chemical + Biological |
| **Structures** | Stationary, 2D, isolated | Stationary & movable, 3D, interfaces with surrounding medium |
| **Maturity** | Mature, standardised | No fixed standards; distinct techniques |

### Advantages of Microsystem Products

- ✅ Less material usage
- ✅ Lower power requirements
- ✅ Greater functionality per unit space
- ✅ Access to regions forbidden to larger devices
- ✅ Lower cost at scale

### Industrial Applications of MEMS

| Application Area | Examples |
|---|---|
| **Printing** | Ink-jet printing heads |
| **Data storage** | Thin-film magnetic heads, compact disks |
| **Automotive** | Airbag sensors, pressure sensors |
| **Medical** | Blood pressure sensors, lab-on-chip |
| **Chemical/Environmental** | Gas sensors, flow meters |

---

## 🔷 Microfabrication Techniques

### 1. Bulk Micromachining

> [!NOTE]
> Deep **wet etching** of a single-crystal silicon substrate to create 3D structures.

- Uses **KOH (Potassium Hydroxide)** — has very low etch rate in the crystal face direction → sharp, precise edges.
- **p+ Etch-Stop Technique:** Silicon substrate is doped with **Boron**, which resists etching. Epitaxial silicon deposition follows the same crystal structure. This controls etch depth precisely and creates **thin membranes**.

**Surface Micromachining** — Shallower version; planar structuring of the substrate surface.

---

### 2. LIGA Process

> [!IMPORTANT]
> **LIGA** stands for three German words — also representing the 3 process steps:

| Letter | German Word | English Meaning | Step |
|---|---|---|---|
| **L** | Lithographie | X-ray Lithography | Pattern creation using X-rays |
| **I** | Galvanoformung | Electrodeposition / Electroforming | Fill pattern with metal using current |
| **G** | Abformtechnik | Plastic Molding | Use metal mold to mass-produce polymer parts |

**Advantages:**
- Versatile — produces parts by multiple methods
- Very high aspect ratios (large height-to-width ratio)
- Part sizes range from **micrometers to centimeters**
- Close tolerances

> [!CAUTION]
> **Disadvantage:** LIGA is a **very expensive process**. Large production quantities are required to justify its use.

---

### 3. Ultra-High Precision Machining

- Uses **single-crystal diamond cutting tools**
- Position control resolution as fine as **0.01 µm**

**Applications:**

| Product | Use |
|---|---|
| Computer hard discs | Precision surface finishing |
| Photocopier drums | Smooth cylindrical surfaces |
| Compact disk reader head molds | Sub-micron accuracy |
| HD-TV projection lenses | Optical surface quality |

---

### 4. Microstereolithography (MSTL)

> [!NOTE]
> A microscale **3D fabrication process** using a focused laser to cure photosensitive or powder materials layer by layer.

| Parameter | Conventional STL | MSTL |
|---|---|---|
| **Layer thickness** | 75 – 500 µm | **10 – 20 µm** |
| **Laser spot diameter** | ~250 µm | **1 – 2 µm** |
| **Materials** | Photosensitive polymer only | Polymer, **ceramic, metallic** (powder-based) |

---

### 5. Nanofabrication

> [!WARNING]
> **UV photolithography cannot be used at nanoscale** — long wavelengths cause diffraction and blur the pattern.

- Solution: **High-resolution Electron Beam Lithography**
- Shorter wavelength → virtually eliminates diffraction during exposure → nanoscale precision

---

## 🔷 Data Acquisition System (DAQ / DAS)

> [!NOTE]
> A DAQ system **acquires analog signals from the real world** and converts them to digital form that a computer can process and act upon.

### Signal Flow Through a DAQ System

```
Real World
    ↓
[1] Transducer / Sensor          → converts physical quantity to electrical signal
    ↓
[2] Analog Multiplexer           → selects one of multiple input channels
    ↓
[3] Signal Conditioning          → amplification + filtering (removes noise)
    ↓
[4] Sample & Hold Circuit        → captures and holds signal steady during conversion
    ↓
[5] ADC (Analog-to-Digital)      → converts analog voltage to digital number
    ↓
[6] Microcomputer System         → processes, stores, or transmits data
    ↓
[7] DAC (Digital-to-Analog)      → converts processed data back to analog
    ↓
[8] Actuator                     → performs physical action
```

---

## 🔷 Analog-to-Digital Conversion (ADC)

> [!NOTE]
> ADC and DAC allow digital computers to interact with real-world signals — voltage, current, temperature, pressure, acceleration, etc.

**Digital information differs from analog in two key ways:**

| Property | Description |
|---|---|
| **Sampled** | Measurements taken at discrete time intervals — not continuous |
| **Quantized** | Amplitude rounded to the nearest discrete digital level |

**Quantization Error** — The rounding error introduced during quantization. It is an inherent limitation of all ADC systems.

---

## 🔷 Nyquist Sampling Theorem

> [!IMPORTANT]
> **"An analog signal can be perfectly reconstructed from its digital samples if the sampling rate is at least TWICE the highest frequency present in the original signal."**
>
> `Sampling Rate ≥ 2W samples/second`
> where **W** = highest frequency in the signal.

| Condition | Result |
|---|---|
| Sampling rate ≥ 2W | Perfect reconstruction ✅ |
| Sampling rate < 2W | **Aliasing** — distorted/incorrect reconstruction ❌ |
