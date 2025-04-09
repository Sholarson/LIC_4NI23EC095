# 📡 CURRENT MIRROR
## 🎯 Aim
Design and analyze current mirror circuit as active load in amplifier circuit

The analysis includes:


✅ DC Analysis


✅ Transient Analysis


✅ AC Analysis

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

<img src="./media/image3.png"
style="width:6.26806in;height:3.95208in" />

## Circuit

![Alt Text](image/circuit.png)

## Design part
Total Current = I = 10^(-3)/1.8 A = 0.555 mA

a) Current ratio = 1:1

  I = Iref + Ix

  Iref = Ix = 0.277 mA

b) Current ratio = 1:2

  I = Iref + Ix

  2 * Iref = Ix = 0.3703 mA, Iref = 0.1851 mA
    
## CASE 1: When Length = 1um

## 🔍 DC Analysis

![Alt Text](image/dc.png)

## 🔍 Transient Analysis.

![Alt Text](image/transient.png)

## 🔍 AC Analysis.

![Alt Text](image/ac.png)

## CASE 2: When Length = 180um

## 🔍 DC Analysis

![Alt Text](image/.png)

## 🔍 Transient Analysis.

![Alt Text](image/.png)

## 🔍 AC Analysis.

![Alt Text](image/.png)

## CASE 3: When Length = 500um

## 🔍 DC Analysis

![Alt Text](image/.png)

## 🔍 Transient Analysis.

![Alt Text](image/.png)

## 🔍 AC Analysis.

![Alt Text](image/.png)


## 📊 Results

1. When length = 1um

   a. width = 6.4719825um

2. 
1. DC Operating Point:

2. Transient Analysis:

3. AC Analysis:

## 📉Inference:


## ⚡ Conclusion:
