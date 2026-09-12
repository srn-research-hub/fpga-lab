# Digilent Basys 3 Hardware Reference

The **Digilent Basys 3** is a complete, ready-to-use digital circuit development platform built around the **AMD/Xilinx Artix-7 FPGA** (part number `xc7a35tcpg236-1`).

---

## Hardware Specifications

| Subsystem | Specification |
| :--- | :--- |
| **FPGA Part** | AMD Artix-7 XC7A35T-1CPG236C |
| **Logic Cells** | 33,280 (5,200 Slices) |
| **Block RAM** | 1,800 Kbits (50 blocks of 36Kb each) |
| **DSP Slices** | 90 slices (25 × 18 multipliers) |
| **Clock Source** | 100 MHz on-board CMOS crystal oscillator |
| **I/O Standard** | `LVCMOS33` (3.3V Logic Levels) |
| **Programming** | On-board Digilent USB-JTAG port (Micro-USB) |

---

## On-Board Peripheral Reference

```
+-------------------------------------------------------------+
| [USB-JTAG/UART]                                             |
|                                         [VGA Port 12-bit]   |
|   [Pmod JA]      [Pmod JB]     [Pmod JC]      [Pmod JXADC]  |
|                                                             |
|                   +------------------+                      |
|                   |  AMD / XILINX    |                      |
|                   |  ARTIX-7 FPGA    |                      |
|                   +------------------+                      |
|                                                             |
|       [ 4-Digit Multiplexed 7-Segment Display ]             |
|                                                             |
|                      [BTNU]                                 |
|             [BTNL]   [BTNC]   [BTNR]                        |
|                      [BTND]                                 |
|                                                             |
| [LD15 .. LD0]  (16 Individual Green LEDs)                   |
| [SW15 .. SW0]  (16 Slide Switches)                          |
+-------------------------------------------------------------+
```

---

### 1. Clock Source
The board includes a primary 100 MHz oscillator wired to FPGA pin **`W5`**.
- Voltage standard: `LVCMOS33`
- Period: $T = 10\text{ ns}$

### 2. Slide Switches & LEDs
- **16 Slide Switches (`SW0` – `SW15`)**: Provide logic high (`1`) when slid upward towards the 7-segment display, and logic low (`0`) when slid downward towards the board edge.
- **16 User LEDs (`LD0` – `LD15`)**: Driven active high (`1` illuminates the LED).

### 3. Pushbuttons
- 5 momentary tactile pushbuttons arranged in a directional pad:
  - `BTNC` (Center)
  - `BTNU` (Up)
  - `BTNL` (Left)
  - `BTNR` (Right)
  - `BTND` (Down)
- Buttons are **active high** (`1` when pressed). They generate contact bounce when pressed and must be synchronized/debounced in sequential designs.

### 4. 4-Digit 7-Segment Display
- **Common Anode**: Anode pins (`AN3..AN0`) are active-low (`0` enables the digit).
- **Cathodes (`CA` through `CG`, `DP`)**: Active-low (`0` illuminates the segment).
- All 4 digits share the same 7 cathode lines; displaying distinct numbers requires **time-division multiplexing** at ~1 kHz.

### 5. USB-UART Bridge
- A shared FTDI chip connects the FPGA directly to your host PC as a virtual COM port.
- **`RsRx` (FPGA Pin `B18`)**: Data transmitted from PC to FPGA.
- **`RsTx` (FPGA Pin `A18`)**: Data transmitted from FPGA to PC.

### 6. 12-Bit VGA Output
- Resistor ladder DAC with 4 bits per color channel: Red (`VGA_R[3:0]`), Green (`VGA_G[3:0]`), Blue (`VGA_B[3:0]`).
- Synchronization signals: `Hsync` (Horizontal) and `Vsync` (Vertical).
