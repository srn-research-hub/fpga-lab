# Laboratory Sessions Overview

The laboratory component consists of **5 hands-on lab sessions** designed to take you from basic digital logic building blocks to complex memory-mapped and communication subsystems.

---

## Laboratory Schedule & Roadmap

| Lab | Topic | Primary Concepts | Hardware Utilized |
| :---: | :--- | :--- | :--- |
| **[Lab 1](lab1.md)** | **Combinational Logic & Flow** | Muxes, Decoders, Vivado RTL-to-Bitstream Flow | Switches (`SW0..SW7`), LEDs (`LD0..LD3`) |
| **[Lab 2](lab2.md)** | **Sequential Logic & Clocks** | D-Flip-Flops, Registers, 100MHz Clock Division | 100MHz Osc, Counter LEDs |
| **[Lab 3](lab3.md)** | **FSMs & Debouncing** | Mealy/Moore State Machines, Switch Debouncers | Pushbuttons (`BTNC..BTNR`), LEDs |
| **[Lab 4](lab4.md)** | **Memory & 7-Segment** | Block RAM (BRAM), Anode/Cathode Time-Multiplexing | 4-Digit 7-Segment Display, Switches |
| **[Lab 5](lab5.md)** | **UART Serial I/O** | Asynchronous Serial Protocol, Baud Rate Gen, FIFOs | USB-UART Bridge (`RsRx`/`RsTx`) |

---

## Lab Deliverables & Grading Policy

Each laboratory assignment is evaluated on three components:

1. **Pre-Lab Preparation (20%)**: Complete module interface declarations, truth tables, state transition diagrams, or preliminary behavioral testbenches prior to attending your lab section.
2. **In-Lab Checkoff & Hardware Demo (50%)**: Demonstrate fully functional synthesis, bitstream programming, and correct real-time behavior on the physical Basys 3 board to the Teaching Assistant.
3. **Post-Lab Technical Report (30%)**: Submit a clean, professional PDF containing:
   - System block diagram and architectural description.
   - Annotated simulation waveforms verifying corner cases.
   - Resource utilization summary (LUTs, FFs, BRAM) from Vivado implementation.
   - Well-commented Verilog source code and testbenches.
