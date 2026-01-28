# Closed-Loop Motor Control System

A closed-loop motor position control system implemented on an Arduino-based platform with P, PD, and PID controllers.

**Author:** Anusha Chatterjee  
**ASUID:** 1234397790

## 🌐 Live Website

Visit the project website: [https://sleepingbomb.github.io/motor-control-system](https://sleepingbomb.github.io/Mechatronics_project/)

## 📁 Repository Structure

```
├── index.html      # Main website file
├── report.pdf      # Full project report
└── README.md       # This file
```

## 🎬 Demo Video

[Watch the demo video on Google Drive](https://drive.google.com/file/d/1rqqiYZKDZaguEpFDiF7OSoR5UjCef8WX/view)

## 🚀 Deployment Instructions

1. **Upload all files** to your GitHub repository:
   - `index.html`
   - `report.pdf`
   - `README.md`

2. **Enable GitHub Pages:**
   - Go to your repository **Settings**
   - Navigate to **Pages** (under "Code and automation")
   - Under "Source", select **Deploy from a branch**
   - Choose **main** branch and **/ (root)** folder
   - Click **Save**

3. Your site will be live at `https://yourusername.github.io/repository-name/` within a few minutes.

## 📋 Project Overview

This project develops and validates a closed-loop motor position control system that can accurately track a desired reference signal. The system uses:

- **Hardware:** Arduino Uno, DC Motor, Quadrature Encoder
- **Software:** MATLAB/Simulink
- **Control Schemes:** P, PD, and PID controllers

### Key Findings

| Controller | Steady-State Error | Overshoot | Stability |
|------------|-------------------|-----------|-----------|
| P          | High              | Moderate  | Good      |
| PD         | Moderate          | Low       | Better    |
| PID        | Near Zero         | Tunable   | Best      |

## 🛠️ Technologies Used

- MATLAB & Simulink
- Arduino Uno
- DC Motor with Quadrature Encoder
- PWM Control

## 📄 License

This project is for academic purposes.

---

© 2024 Anusha Chatterjee
