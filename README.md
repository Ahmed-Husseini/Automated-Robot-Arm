# Automated-Robot-Arm

An embedded robotic system that classifies and sorts colored objects using a robotic arm controlled by an STM32F103C8T6 microcontroller.

---

## 🎯 Project Overview

The goal of this project is to design, build, and program a robotic arm capable of detecting object color and placing it in the appropriate bin. The robot picks up balls from a central basket, identifies their color using a sensor, and sorts them accordingly.

### 🔄 Operating Logic
1. Arm picks a ball from the central container.
2. A TCS3200 color sensor detects the ball’s color (red or blue).
3. Based on the result:
   - 🔵 Blue → right bin
   - 🔴 Red → left bin
4. The process repeats until the input container is empty.

---

## 🧰 Hardware Components

| Component          | Details                         |
|--------------------|----------------------------------|
| Microcontroller    | STM32F103C8T6 (Blue Pill)        |
| Servo Motors       | 2× MG966R, 2× SG90               |
| Color Sensor       | TCS3200                          |
| Ultrasonic Sensor  | HC-SR04                          |
| Gyroscope          | MPU6050                          |
| I2C Servo Driver   | PCA9685                          |
| LCD (Optional)     | I2C 16x2 LCD Display             |

---

## 🧠 Software Overview

- **FreeRTOS** used for task scheduling.
- **Register-level programming** (bare-metal) without HAL.
- Key modules:
  - Distance measurement using ultrasonic sensor.
  - Color detection task via TCS3200.
  - Servo control using PCA9685 I2C driver.
- Implemented in C with `CMSIS` and STM32 low-level access.

---

## 📐 Control Design

- DC motor and potentiometer were separated from prebuilt servo loop.
- System modeled and linearized with MATLAB:
  - Moment of Inertia: 0.01 kg·m²
  - Transfer function derived and simulated.
- PID controller designed using MATLAB:
  ```math
  C(s) = 50 + 2s + 100/s
