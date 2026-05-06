# Design & Implementation of an SoC-Based Flight Controller for UAVs

![Status](https://img.shields.io/badge/Status-Completed-success)
![Platform](https://img.shields.io/badge/Platform-Xilinx_Zynq--7000-orange)
![Tech](https://img.shields.io/badge/Tech-VHDL%20|%20Embedded%20C%20|%20Control%20Theory-blue)

## 📖 Overview
This project focuses on the development of a custom flight controller for a quadrotor drone using a **Hardware/Software (HW/SW) co-design** approach on the **Xilinx Zynq-7010 (Zybo)** System-on-Chip. 

By partitioning the system, we leverage the FPGA's parallelism for time-critical sensor data acquisition and motor actuation, while utilizing the ARM Cortex-A9 processor for complex navigation and control algorithms. The result is a high-performance system capable of real-time stability and deterministic response.

## 🏗 System Architecture
The system is divided into two main domains to ensure maximum flight reliability:

### 🟦 Programmable Logic (PL - FPGA)
* **Custom AXI PWM IP:** High-resolution hardware cores for jitter-free motor control.
* **I2C Controller:** Hardware-level interfacing with the **MPU6050** (IMU) to offload bit-level communication from the CPU.
* **Telemetry Buffer:** Dedicated BRAM-backed FIFO for the **ESP-01S Wi-Fi** module to ensure zero data loss during high-speed telemetry transmission.

### 🟩 Processing System (PS - ARM Cortex-A9)
* **State Estimation:** Implementation of a discrete-time **Kalman Filter** (100 Hz) for fusing accelerometer and gyroscope data.
* **Control Loops:** Nested **PID control** architecture for precise attitude (pitch, roll, yaw) and altitude stabilization.
* **Data Processing:** Real-time conversion of raw sensor data into Euler angles.

## 🛠 Tech Stack
* **Hardware:** Zybo (Zynq-7000), MPU6050 IMU, HMC5883L Magnetometer, SimonK 30A ESCs.
* **Languages:** VHDL (Hardware Description), Embedded C (Firmware).
* **Tools:** Xilinx Vivado Design Suite, Vivado SDK, MATLAB/Simulink (6-DOF Modeling).

## 🚀 Key Features
* **HW/SW Co-Design:** Efficient partitioning that reduces CPU load by offloading I/O tasks to the FPGA.
* **Hardware-in-the-Loop (HIL):** Validation of control laws using a real-time simulation plant in MATLAB/Simulink.
* **Ultra-Low Latency:** Microsecond-level accuracy in PWM signal generation for immediate motor response.
* **Power Efficiency:** The hardware peripheral logic consumes less than **25 mW**.

## 📊 Results
* **Stability:** Achieved robust attitude stabilization and vibration rejection during test flights.
* **Precision:** The Kalman Filter successfully mitigated sensor drift, providing a stable 100 Hz attitude estimate.
* **Payload Capacity:** Validated for a quadrotor mass of approximately **1.2 kg**.

## 📂 Repository Structure
```text
├── hardware/             # Vivado Project: Block Designs, and VHDL Source
├── firmware/             # C/C++ Source Code
├── simulation/           # MATLAB/Simulink Models & HIL Configurations
└── docs/                 # Full Technical Report
