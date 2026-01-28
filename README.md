<div align="center">

# 🔧 Closed-Loop Motor Control System

[![GitHub Pages](https://img.shields.io/badge/Live%20Demo-GitHub%20Pages-2ea44f?style=for-the-badge&logo=github)](https://sleepingbomb.github.io/Mechatronics_project/)
[![MATLAB](https://img.shields.io/badge/MATLAB-Simulink-0076A8?style=for-the-badge&logo=mathworks)](https://www.mathworks.com/)
[![Arduino](https://img.shields.io/badge/Arduino-Uno-00979D?style=for-the-badge&logo=arduino)](https://www.arduino.cc/)
[![License](https://img.shields.io/badge/License-Academic-yellow?style=for-the-badge)](#)

**A comprehensive implementation and comparative analysis of P, PD, and PID controllers for DC motor position tracking on an Arduino-based platform.**

[View Live Demo](https://sleepingbomb.github.io/Mechatronics_project/) · [Watch Video](https://drive.google.com/file/d/1rqqiYZKDZaguEpFDiF7OSoR5UjCef8WX/view) · [Read Report](https://github.com/sleepingbomb/Mechatronics_project/blob/main/anushaFinal.pdf)

</div>

---

## 📖 About The Project

This project develops and validates a **closed-loop motor position control system** capable of accurately tracking a desired reference signal. Using MATLAB/Simulink models deployed on an Arduino Uno, the system implements three control strategies—**Proportional (P)**, **Proportional-Derivative (PD)**, and **Proportional-Integral-Derivative (PID)**—to systematically compare their performance in terms of stability, steady-state error, and dynamic response.

### 🎯 Project Objectives

- Design and implement a closed-loop position control system using Arduino and Simulink
- Compare P, PD, and PID control schemes through systematic tuning
- Analyze performance metrics: rise time, overshoot, settling time, and steady-state error
- Demonstrate how derivative and integral actions improve tracking performance

---

## 🏗️ System Architecture

The control system consists of six main functional blocks:

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                         CLOSED-LOOP CONTROL SYSTEM                          │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   ┌──────────────┐      ┌─────────┐      ┌────────────┐      ┌──────────┐  │
│   │  Reference   │      │  Error  │      │    PID     │      │   PWM    │  │
│   │  Generator   │─────▶│ Compute │─────▶│ Controller │─────▶│  Output  │  │
│   │  (Sine Wave) │      │  e(t)   │      │            │      │ (Pin 9)  │  │
│   └──────────────┘      └─────────┘      └────────────┘      └────┬─────┘  │
│          │                   ▲                                     │        │
│          │                   │                                     ▼        │
│          │              ┌─────────┐                          ┌──────────┐  │
│          │              │Encoder  │◀─────────────────────────│ DC Motor │  │
│          │              │Feedback │                          │ + Driver │  │
│          │              │(Pin 2,3)│                          └──────────┘  │
│          │              └─────────┘                                ▲        │
│          │                                                         │        │
│          │              ┌─────────────┐                           │        │
│          └─────────────▶│  Direction  │───────────────────────────┘        │
│                         │   Control   │                                     │
│                         │ (Pin 4 & 5) │                                     │
│                         └─────────────┘                                     │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

| Block | Function | Arduino Pins |
|-------|----------|--------------|
| **Direction Control** | Sets motor rotation (CW/CCW) via complementary logic | Digital 4, 5 |
| **Encoder Feedback** | Reads quadrature encoder for position measurement | Digital 2, 3 |
| **Error Computation** | Calculates tracking error: e(t) = θ_des - θ_act | — |
| **PID Controller** | Generates control effort based on error | — |
| **Reference Generator** | Produces sinusoidal position reference | — |
| **PWM Output** | Converts control signal to motor voltage | PWM 9 |

---

## 📊 Control Strategies

### Proportional (P) Control
```
u(t) = Kp · e(t)
```
Simple and responsive, but inherently produces steady-state error for constant references.

### Proportional-Derivative (PD) Control
```
u(t) = Kp · e(t) + Kd · de(t)/dt
```
Adds predictive damping to reduce overshoot and oscillations, improving transient response.

### Proportional-Integral-Derivative (PID) Control
```
u(t) = Kp · e(t) + Ki · ∫e(t)dt + Kd · de(t)/dt
```
Combines all three actions to eliminate steady-state error while maintaining stability.

---

## 📈 Results & Performance Comparison

<div align="center">

| Controller | Steady-State Error | Overshoot | Rise Time | Stability |
|:----------:|:------------------:|:---------:|:---------:|:---------:|
| **P** | ⚠️ High | ⚠️ Moderate | ✅ Fast | ✅ Good |
| **PD** | ⚠️ Moderate | ✅ Low | ✅ Fast | ✅ Better |
| **PID** | ✅ Near Zero | ✅ Tunable | ✅ Fast | ✅ Best |

</div>

### Sample Results

| P Control | PD Control | PID Control |
|:---------:|:----------:|:-----------:|
| Kp = 3-4 | Kp = 5-9, Kd = 1-1.5 | Kp = 3, Kd = 1.5-2, Ki = 0.5-1 |
| Noticeable phase lag | Reduced overshoot | Best tracking accuracy |
| Steady-state error present | Improved damping | Near-zero steady-state error |

> **Legend:** 🔴 Dashed line = Reference Signal | 🔵 Solid line = Actual Motor Position

---

## 🛠️ Hardware & Software

### Hardware Components
| Component | Specification |
|-----------|---------------|
| **Microcontroller** | Arduino Uno (ATmega328P) |
| **Actuator** | DC Motor with H-Bridge Driver |
| **Sensor** | Quadrature Encoder (Channels A & B) |
| **Power** | External motor power supply |

### Software Tools
- **MATLAB R2023a+** with Simulink
- **Simulink Support Package for Arduino Hardware**
- **Arduino IDE** (for initial board setup)

---

## 📁 Repository Structure

```
Mechatronics_project/
│
├── 📄 index.html           # Project website (GitHub Pages)
├── 📄 anushaFinal.pdf      # Complete project report with results
├── 📄 README.md            # Project documentation (this file)
│
└── 📁 images/              # Result plots and diagrams
    ├── p_control_*.png     # P controller response plots
    ├── pd_control_*.png    # PD controller response plots
    └── pid_control_*.png   # PID controller response plots
```

---

## 🚀 Quick Start

### Prerequisites
- MATLAB/Simulink with Arduino Hardware Support Package
- Arduino Uno with motor driver circuit
- DC motor with quadrature encoder

### Running the Project
1. **Clone this repository**
   ```bash
   git clone https://github.com/sleepingbomb/Mechatronics_project.git
   cd Mechatronics_project
   ```

2. **Open Simulink Model** in MATLAB

3. **Configure Hardware Settings**
   - Go to **Hardware** tab → **Hardware Settings**
   - Select **Arduino Uno** as target board
   - Configure COM port

4. **Adjust Controller Gains**
   - Double-click PID Controller block
   - Set Kp, Ki, Kd values

5. **Deploy to Hardware**
   - Click **Build, Deploy & Start**
   - Observe motor tracking response

---

## 🎬 Demo Video

<div align="center">

[![Watch Demo Video](https://img.shields.io/badge/▶_Watch_Demo-Google_Drive-EA4335?style=for-the-badge&logo=googledrive&logoColor=white)](https://drive.google.com/file/d/1rqqiYZKDZaguEpFDiF7OSoR5UjCef8WX/view)

*Click above to watch the motor control system in action*

</div>

---

## 📝 Key Findings

<table>
<tr>
<td width="60">🔴</td>
<td><strong>P Control</strong> achieves basic tracking but cannot eliminate steady-state error. Increasing Kp speeds up response but causes oscillations.</td>
</tr>
<tr>
<td>🟠</td>
<td><strong>PD Control</strong> dramatically improves transient response through derivative damping, reducing overshoot while maintaining responsiveness.</td>
</tr>
<tr>
<td>🟢</td>
<td><strong>PID Control</strong> provides optimal performance by driving steady-state error to zero through integral action, achieving the best overall tracking.</td>
</tr>
</table>

> **Conclusion:** *"The systematic addition of derivative and integral terms to a proportional controller significantly enhances tracking accuracy and robustness in practical motor control systems."*

---

## 📚 References

- Franklin, G.F., Powell, J.D., & Emami-Naeini, A. (2019). *Feedback Control of Dynamic Systems*
- MathWorks Documentation: [Simulink Support Package for Arduino](https://www.mathworks.com/hardware-support/arduino-simulink.html)
- Arduino Reference: [Encoder Library](https://www.arduino.cc/reference/en/libraries/encoder/)

---

## 👤 Author

<div align="center">

**Anusha Chatterjee**  
Arizona State University  
ASUID: 1234397790

[![GitHub](https://img.shields.io/badge/GitHub-sleepingbomb-181717?style=flat-square&logo=github)](https://github.com/sleepingbomb)

</div>

---

## 📜 License

This project is developed for **academic purposes** as part of a Mechatronics course curriculum.

---

<div align="center">

### ⭐ Found this helpful? Give it a star!

[View Live Website](https://sleepingbomb.github.io/Mechatronics_project/) · [Report Bug](https://github.com/sleepingbomb/Mechatronics_project/issues) · [View Report](https://github.com/sleepingbomb/Mechatronics_project/blob/main/anushaFinal.pdf)

---

*© 2024 Anusha Chatterjee — Mechatronics Project*

</div>
