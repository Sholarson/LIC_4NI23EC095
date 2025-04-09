# 📡 CURRENT MIRROR
## 🎯 Aim

Design and analyze a current mirror circuit used as an active load in an amplifier configuration.

1. **Design Specifications:**
   - Voltage Gain \( A_v > -10 \, \text{V/V} \)
   - Supply Voltage \( V_{DD} = 1.8 \, \text{V} \)
   - Power Consumption \( P \leq 1 \, \text{mW} \)

2. **Tasks:**
   - Design a differential amplifier incorporating a current mirror load as per **Experiment 3**.
   - Perform the following analyses:
     - **DC Analysis**
     - **Transient Analysis**
     - **AC Analysis**


## Theory
**What is Current Mirror?**

The current mirror is an analog circuit that senses the reference current and generates the copy or number of copies of the reference current, with the same characteristics. The replicated current is as stable as the reference current source. The replicated current could be the same as the reference current (Icopy = IREF), or it could be either multiple or fraction of the reference current. (Icopy = N*Iref or Icopy = (1/N)*IREF).

![Alt Text](image/basic.png) 

**MOSFET- Current Mirror**

Fig.3 shows a current mirror circuit using the NMOS transistor. The reference current is converted to the voltage using diode connected transistor and the same is applied between the gate and the source of the another MOSFET.

![Alt Text](image/nmos.png)

The relation between the ID1 and IREF can be given by the following expression.

![Alt Text](image/rel_nmos.png)

By changing the W/L ratio of the two transistors, the current which is fraction or multiple of the reference current can be generated. The only thing which needs to be ensured is that, the MOSFET should operate in the saturation region

**PMOS Current Mirror**

Fig. 6 shows the implementation of current mirror using the PMOS transistors. In PMOS current mirror, the source terminals for both transistors are connected to Supply voltage Vdd.

![Alt Text](image/pmos.png)

The relation between the ID1 and IREF can be given by the same expression.

![Alt Text](image/rel_pmos.png)


## Design

To find total current:

**I<sub>total</sub> = P / V<sub>DD</sub> = 1 mW / 1.8 V = 0.555 mA**

---

### Current Division:

We know:

**I<sub>total</sub> = I<sub>ref</sub> + I<sub>X</sub>**, where **I<sub>X</sub> = I<sub>D</sub>**

- For (W/L) = 1:1 →  
  **I<sub>ref</sub> + I<sub>X</sub> = I<sub>total</sub> / 2 = 0.277 mA**

- For (W/L) = 1:2 →  
  **I<sub>X</sub> = I<sub>total</sub> / 3**

---

### Voltage Gain & Output Resistance:

We use the gain equation:

**A<sub>V</sub> = -g<sub>m</sub> · R<sub>out</sub> = -g<sub>m</sub> · (r<sub>o1</sub> || r<sub>o2</sub>)**

Where:

- **r<sub>o1</sub> = 1 / (λ₁ · I<sub>D</sub>)**  
- **r<sub>o2</sub> = 1 / (λ₂ · I<sub>D</sub>)**

Given:

- λ₁ = 1.382  
- λ₂ = 1.329  
- I<sub>D</sub> = 0.277 mA

Then:

**R<sub>out</sub> = 1 / (I<sub>D</sub> · (λ₁ + λ₂)) = 1331.65 Ω ≈ 1.331 kΩ**

---

### Transconductance:

We use:

**g<sub>m</sub> = 2I<sub>D</sub> / V<sub>OV</sub>**

So:

**A<sub>V</sub> = (2I<sub>D</sub> / V<sub>OV</sub>) · R<sub>out</sub>**

Given gain ≥ 10 V/V, we calculate:

**V<sub>OV</sub> = 0.0737 V**  
**V<sub>GS</sub> = V<sub>OV</sub> + V<sub>t</sub> = 0.0737 + 0.496 = 0.569 V**

So, **required input voltage = 0.569 V**

---

### MOSFET Dimensions

| Transistor | Type | Width (W) | Length (L) |
|------------|------|-----------|------------|
| M1, M2     | PMOS | 10 µm     | 180 nm     |
| M3         | NMOS | 31.23 µm  | 180 nm     |

---

> λ-values were taken from the TSMC 180 nm technology `.lib` file (`PCLM` parameter).  
> These calculations ensure the amplifier operates with **A<sub>V</sub> ≥ 10 V/V** and **V<sub>GS</sub> = 0.569 V**.

## Circuit Diagram ##

<img src="image/image3.png"
style="width:6.26806in;height:3.95208in" />


## 1. DC Analysis

<img src="image/image4.png" width="600"/>

The simulated currents through NMOS (M3) and PMOS (M1, M2) closely match our calculated values, confirming that the design adheres to power specifications.

**Power Consumption:**  
P = I<sub>total</sub> × V<sub>DD</sub> = 0.55401 mA × 1.8 V = **0.9972 mW**  
This falls within our 1 mW power budget.

---

## 2. Transient Analysis

 
<img src="image/image6.png" width="600"/>  
<img src="image/image7.png" width="700"/>

A sinusoidal input with a DC offset of 0.569 V is applied. The peak output voltage is **1.2381 V**, for an input peak of **10 mV**.

**Voltage Gain:**  
A<sub>V</sub> = (V<sub>out</sub> - V<sub>mid</sub>) / V<sub>in</sub>  
= (1.2381 V – 0.96 V) / 10 mV = **-27.81 V/V = 28.88 dB**

> Gain requirement (≥10 V/V) is successfully met.

---

## 3. AC Analysis

<img src="image/image8.png" width="700"/>

**Bandwidth (3 dB point):**  
**629.997 MHz**

**Midband Gain:**  
**29.298 dB** (very close to transient gain: **28.884 dB**)

> The AC response confirms the expected bandwidth and validates the gain accuracy.

---

## Circuit 2: Ratio of 1:2 using L = 180 nm

For ratio of 1:2,  
I<sub>ref</sub> = I<sub>total</sub>/3 = **0.183 mA**

### Circuit Diagram  
<img src="image/image9.png" alt="Circuit Diagram" width="600"/>

### DC Analysis  
<img src="image/image10.png" alt="DC Analysis" width="500"/>

### Transient Analysis  
<img src="image/image11.png" alt="Transient Analysis" width="550"/>

**Gain (V/V)** = (1.26006 - 0.96) / (-10 mV) = **30.006 V/V = 29.544 dB**  
*Input Voltage:* 10 mV peak  
*Frequency:* 1 kHz  
*Waveform:* Sine

Let us perform the frequency response to verify this.

### AC Analysis  
<img src="image/image12.png" alt="AC Analysis" width="600"/>

**Midband Gain:** ≈ **29.325 dB**  
**Calculated Gain:** 29.544 dB → ≈ **29.25 V/V**

---

## Analysis using L = 500 nm

### 1) Ratio of 1:1 using L = 500 nm

**CMOSN (M3):** W = 65.19 µm, L = 500 nm  
**CMOSP (M1, M2):** W = 10 µm, L = 500 nm

<img src="image/image13.png" alt="Circuit Diagram - L = 500nm, 1:1" width="500"/>

#### DC Analysis  
<img src="image/image14.png" alt="DC Analysis" width="500"/>

#### Transient Analysis  
<img src="image/image15.png" alt="Transient Analysis" width="600"/>

#### AC Analysis  
<img src="image/image16.png" alt="AC Analysis" width="600"/>

**Gain:** 37.87023 dB  
**3 dB Bandwidth:** 122.329 MHz

---

### 2) Ratio of 1:2 using L = 500 nm

**CMOSN (M3):** W = 85.243 µm, L = 500 nm  
**CMOSP (M1):** W = 10 µm, L = 500 nm  
**CMOSP (M2):** W = 20 µm, L = 500 nm

#### DC Analysis  
<img src="image/image17.png" alt="DC Analysis" width="550"/>

#### Transient Analysis  
<img src="image/image18.png" alt="Transient Analysis" width="600"/>

**Gain (V/V):** -62.063 V/V = **35.855 dB**

#### AC Analysis  
<img src="image/image19.png" alt="AC Analysis" width="600"/>

**3 dB Bandwidth:** 93.0732 MHz  
**Gain:** 38.015 dB

---

## Analysis using L = 1 µm

### 1) Ratio of 1:1

**CMOSN (M3):** W = 93.35 µm, L = 1 µm  
**CMOSP (M1, M2):** W = 10 µm, L = 1 µm

<img src="image/image20.png" alt="Circuit Diagram" width="550"/>

#### DC Analysis  
<img src="image/image17.png" alt="DC Analysis" width="500"/>

#### Transient Analysis  
<img src="image/image21.png" alt="Transient Analysis" width="580"/>

**Gain (V/V):** -60 V/V = **35.563 dB**

#### AC Analysis  
<img src="image/image22.png" alt="AC Analysis" width="500"/>

**3 dB Bandwidth:** 98.90171 MHz  
**Gain:** 35.481 dB

---

### 2) Ratio of 1:2

**CMOSN (M3):** W = 121.51 µm, L = 1 µm  
**CMOSP (M1):** W = 20 µm, L = 1 µm  
**CMOSP (M2):** W = 10 µm, L = 1 µm

<img src="image/image23.png" alt="Circuit Diagram" width="600"/>

#### DC Analysis  
<img src="image/image24.png" alt="DC Analysis" width="500"/>

#### Transient Analysis  
<img src="image/image25.png" alt="Transient Analysis" width="600"/>

#### AC Analysis  
<img src="image/image26.png" alt="AC Analysis" width="600"/>

**3 dB Bandwidth:** 57.2524 MHz  
**Gain:** 38.69341 dB

---

## Table of Comparisons

| **Parameter**            | **L = 180 nm (1:1)** | **L = 180 nm (1:2)** | **L = 500 nm (1:1)** | **L = 500 nm (1:2)** | **L = 1 µm (1:1)** | **L = 1 µm (1:2)** |
|--------------------------|----------------------|----------------------|----------------------|----------------------|--------------------|--------------------|
| **NMOS Width**           | 31.23 µm             | 41.127 µm            | 65.19 µm             | 85.243 µm            | 93.35 µm           | 121.51 µm          |
| **PMOS Width (M1)**      | 10 µm                | 10 µm                | 10 µm                | 10 µm                | 10 µm              | 20 µm              |
| **PMOS Width (M2)**      | 10 µm                | 20 µm                | 10 µm                | 20 µm                | 10 µm              | 10 µm              |
| **Voltage Gain (V/V)**   | 27.81                | 30.006               | 61.00                | 62.063               | 60                 | 86.03              |
| **Gain (dB)**            | 29.298               | 29.325               | 37.87                | 38.015               | 35.481             | 38.693             |
| **3dB Bandwidth (MHz)**  | 629.997              | 438.012              | 122.329              | 93.073               | 98.902             | 57.252             |


-------------------------------------------------------------------------------------------------------------

# Differential Amplifier Design and Analysis

## Part 2: Differential Amplifier

After understanding the basics of the current mirror, we now move on to designing a **differential amplifier** using the same parameters employed in the differential amplifier simulation.

![Differential Amplifier Schematic](image/image27.png)

### N-Channel MOSFETs (CMOSN)

| Transistor | Width (W) | Length (L) |
|------------|-----------|------------|
| M1         | 108.5 µm  | 180 nm     |
| M2         | 108.5 µm  | 180 nm     |
| M3         | 22.42 µm  | 180 nm     |
| M6         | 10 µm     | 180 nm     |

> **Note**: The (W/L) ratio of **M3** is more than double that of **M6** to ensure that the current flowing through M3 is double that of M6:
> - \( I_{M3} = 1.222 \, \text{mA} \)
> - \( I_{M6} = 0.611 \, \text{mA} \)

This rationale is also applied to **M4** and **M5**, which have equal (W/L) ratios to ensure equal current distribution.

### P-Channel MOSFETs (CMOSP)

| Transistor | Width (W) | Length (L) |
|------------|-----------|------------|
| M4         | 52 µm     | 180 nm     |
| M5         | 52 µm     | 180 nm     |
| M6         | 10 µm     | 180 nm     |

---

## DC Analysis

![DC Analysis](image/image28.png)

As shown in the above DC analysis, the simulation values obtained closely match the required values for the chosen (W/L) ratios.

---

## Transient Analysis

![Transient Analysis](image/image29.png)

A differential input of **10 mV peak**, **1 kHz sine wave** was applied to the gate of **M1**. Since the output of a differential amplifier is the **difference in drain voltages** of M1 and M2, only one side of the differential input was excited.

> **Important Insight**: If a **common-mode input** is applied, the differential amplifier ideally rejects the signal, resulting in negligible gain.

### Voltage Gain Calculation

\[
A_v = \frac{V_{out1} - V_{out2}}{V_{in}} = \frac{1.092 \, \text{V} - 0.95 \, \text{V}}{-10 \, \text{mV}} = -14.2 \, \text{V/V} \approx 23.045 \, \text{dB}
\]

---

## Results and Inferences

### 1. Gain-Bandwidth Trade-off

There is a clear inverse relationship between **gain** and **bandwidth**:

- **180 nm**: Modest gain (~29 dB), High bandwidth (>600 MHz)
- **1 μm**: High gain (~35–39 dB), Reduced bandwidth (<100 MHz)

### 2. Channel Length Effects

Increasing channel length from **180 nm → 500 nm → 1 μm** leads to:

- **Increased Gain**: Due to reduced channel length modulation (λ), resulting in higher output resistance.
- **Decreased Bandwidth**: Caused by increased parasitic capacitances in longer channel devices.
- **Larger Transistor Widths Required**: NMOS widths increased (e.g., 31 µm → 121 µm) to maintain the same current levels.

### 3. W/L Ratio Impact

A **1:2 W/L ratio** consistently yields better gain performance than 1:1 across all channel lengths:

| Channel Length | Gain (1:1 Ratio) | Gain (1:2 Ratio) |
|----------------|------------------|------------------|
| 180 nm         | 29.298 dB        | 29.325 dB        |
| 500 nm         | 37.870 dB        | 38.015 dB        |
| 1 µm           | 35.481 dB        | 38.693 dB        |

---

## Conclusion

The differential amplifier experiment highlights:

- The influence of **channel length** and **W/L ratios** on gain and bandwidth.
- The ability to **customize circuit performance** based on design goals by strategically selecting transistor geometries.
- The trade-offs between **gain**, **bandwidth**, and **silicon area**, which must be considered during analog circuit design.

