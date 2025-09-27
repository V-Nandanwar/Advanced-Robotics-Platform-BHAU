# "BHAU" - Hardware Architecture for a 3-MCU Distributed Robotics Platform

This repository documents the hardware architecture for the "BHAU" advanced robotics platform, an omnidirectional robot designed for complex navigation and manipulation tasks. My primary role on this project was leading the end-to-end hardware design, system architecture, and power electronics.

*(Note: The control software for this platform was a collaborative team effort. The focus of this repository is to document the hardware architecture, for which I was the lead.)*

---

## System Architecture

To handle the complex and time-sensitive tasks of locomotion, actuation, and communication simultaneously, I architected a distributed control system. This modular approach delegated specific responsibilities to three specialized microcontrollers, which dramatically improved real-time performance and simplified software development.

*   **STM32-F072RB (Primary Controller):** Dedicated to the most critical task: real-time locomotion. It handled processing optical encoder feedback and running the primary motor control loops.
*   **Arduino Mega 2560 (Actuator Controller):** Managed all secondary, multi-axis actuation, including the stepper motor for head rotation and the four servo motors for the gripper arm.
*   **ESP32 (Wireless & Command Interface):** Served as the communications hub, receiving commands wirelessly and delegating tasks to the other two controllers via UART.

*(A detailed data and control flow diagram will be added shortly.)*

---

## Power Distribution System

A key challenge for this multi-MCU platform was designing a robust power distribution system to deliver stable, isolated power to both high-current motors and sensitive microcontrollers from two separate LiPo batteries.

I engineered a custom, multi-stage power architecture to solve this. The system utilizes two primary power domains to prevent motor noise from affecting the control logic: a 24V domain for the high-torque drive motors and a 12V domain for all logic and auxiliary actuators. High-efficiency buck converters were used to create multiple stable voltage rails, with custom Power Distribution Boards (PDBs) providing fused, protected outputs for each subsystem.

The complete power architecture is detailed in the diagram below:

![BHAU Power Distribution Architecture](Power_System_Architecture.png)
