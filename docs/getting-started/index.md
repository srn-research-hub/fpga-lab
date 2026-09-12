# Getting Started

This section walks you through setting up your software development environment, configuring your hardware platform, and understanding the physical FPGA constraints required to target the **Digilent Basys 3**.

---

## Preparation Checklist

Before attending your first lab session, complete the following items:

- [ ] **Install AMD Vivado ML Edition (Standard)** — Follow the [Vivado Installation Guide](vivado-setup.md).
- [ ] **Install Digilent Board Files & Cable Drivers** — Ensure your computer detects the on-board FTDI USB JTAG programmer.
- [ ] **Review the Basys 3 Hardware Architecture** — Study the [Basys 3 Hardware Guide](basys3-guide.md) to understand clocking, pin mappings, and I/O characteristics.
- [ ] **Download the Master XDC File** — Familiarize yourself with the [Master XDC Constraints](xdc-master.md).

---

## Lab Kit Contents

Each lab station or individual kit includes:

| Item | Description |
| :--- | :--- |
| **Digilent Basys 3 Board** | Featuring the AMD/Xilinx Artix-7 XC7A35T-1CPG236C FPGA |
| **Micro-USB Cable** | Provides power and unified JTAG programming / UART serial communication |
| **Pmod Modules** (as required) | Peripheral modules such as rotary encoders, buzzers, or sensors |

---

## Lab Policies & Safety

> [!WARNING]
> **Electrostatic Discharge (ESD) Precaution**
> FPGAs are sensitive CMOS devices. Ground yourself by touching a grounded metal chassis before handling the Basys 3 board, and hold the board by its corners. Never plug or unplug Pmod peripherals while the board power switch is turned **ON**.
