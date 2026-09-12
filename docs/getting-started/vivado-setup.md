# Vivado Installation & Environment Setup

This guide details how to install and configure **AMD Vivado ML Edition (Standard)** for digital system synthesis and FPGA bitstream generation.

---

## 1. Downloading AMD Vivado ML

The free version of Vivado (**Vivado ML Standard / WebPACK**) supports the Artix-7 XC7A35T FPGA on the Basys 3 without requiring a paid license.

1. Navigate to the official [AMD Xilinx Downloads Portal](https://www.xilinx.com/support/download.html).
2. Download the **Vivado ML Edition: All OS Installer Single-File Download** or the **Web Installer**.
3. Create a free AMD/Xilinx account if you do not already have one.

---

## 2. Recommended Installation Options

During the installer wizard:

- **Edition**: Select **Vivado ML Standard**.
- **Devices**: You only need **7-Series Devices (Artix-7)**. You can uncheck Kintex-7, Virtex-7, UltraScale, and Versal to save ~30 GB of disk space.
- **Tools**: Keep **Vivado Design Suite**, **Vivado Simulator (xsim)**, and **Install Cable Drivers** checked.

---

## 3. Installing Digilent Board Files

Installing board files enables Vivado to automatically configure I/O standards, voltage banks, and peripheral constraints for the Basys 3.

```bash
# Clone Digilent vivado-boards repository
git clone https://github.com/Digilent/vivado-boards.git

# Copy board files to your Vivado installation directory:
# On Linux:
cp -r vivado-boards/new/board_files/* /tools/Xilinx/Vivado/<version>/data/boards/board_files/

# On Windows:
# Copy to C:\Xilinx\Vivado\<version>\data\boards\board_files\
```

---

## 4. macOS Users Setup Note

> [!NOTE]
> **Vivado on macOS**
> Vivado is natively supported on **Windows** and **Linux (Ubuntu / RHEL)**.
> If you are on an Apple Silicon or Intel Mac:
> - **Option A (Recommended)**: Use a lightweight virtual machine running Ubuntu 22.04 LTS via **UTM** (free) or **Parallels Desktop**, and enable USB passthrough for the Digilent USB cable.
> - **Option B**: Connect via SSH with X11 forwarding to the department lab server (`vlsi.eecs.ucf.edu`).
> - **Option C**: Use open-source simulation tools (**Icarus Verilog** `iverilog` and **GTKWave**) natively on macOS via Homebrew for simulation testbenches, and synthesize on lab workstations.

---

## 5. Verification Test

Open Vivado and execute the following in the Vivado TCL Console to verify that the Artix-7 target part is installed:

```tcl
get_parts xc7a35tcpg236-1
```

If it returns `xc7a35tcpg236-1`, your environment is ready!
