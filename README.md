# Digital System Design — FPGA Lab Sessions

[![Deploy MkDocs to GitHub Pages](https://github.com/srn-research-hub/fpga-lab/actions/workflows/deploy.yml/badge.svg)](https://github.com/srn-research-hub/fpga-lab/actions/workflows/deploy.yml)
[![Target FPGA](https://img.shields.io/badge/FPGA-Artix--7%20XC7A35T-FFC904?logo=amd&logoColor=black)](https://digilent.com/reference/programmable-logic/basys-3/reference-manual)
[![EDA Toolchain](https://img.shields.io/badge/EDA-AMD%20Vivado%20ML-black?logo=xilinx&logoColor=FFC904)](https://www.xilinx.com/products/design-tools/vivado.html)
[![Documentation](https://img.shields.io/badge/Docs-MkDocs%20Material-blue)](https://srn-research-hub.github.io/fpga-lab/)

A comprehensive, interactive course website and laboratory curriculum for **Digital System Design** on the **Digilent Basys 3 FPGA** using **AMD Vivado ML**.

---

## Curriculum Structure

- **[Getting Started](https://srn-research-hub.github.io/fpga-lab/getting-started/)**: Vivado installation, cable drivers, Basys 3 hardware manual, master XDC pin constraints.
- **[Lab 1: Combinational Logic & Vivado Workflow](https://srn-research-hub.github.io/fpga-lab/labs/lab1/)**: RTL modeling, simulation testbenches, synthesis, implementation, and bitstream programming.
- **[Lab 2: Sequential Logic & Clock Dividers](https://srn-research-hub.github.io/fpga-lab/labs/lab2/)**: Synchronous registers, integer clock division (100 MHz to 1 Hz), and binary counters.
- **[Lab 3: Finite State Machines & Debouncing](https://srn-research-hub.github.io/fpga-lab/labs/lab3/)**: 3-block FSM methodology, mechanical button contact debouncers, and traffic light controller.
- **[Lab 4: Memory & 7-Segment Displays](https://srn-research-hub.github.io/fpga-lab/labs/lab4/)**: BRAM / Distributed RAM and time-multiplexed 4-digit 7-segment display controller.
- **[Lab 5: UART Serial Communication](https://srn-research-hub.github.io/fpga-lab/labs/lab5/)**: Asynchronous serial 8N1 communication, baud rate generation, and PC-to-FPGA terminal I/O.
- **[Final Capstone Project](https://srn-research-hub.github.io/fpga-lab/project/)**: Specifications, timeline, scaffolds, and rubrics for collaborative digital system design.
- **[References & Cheatsheets](https://srn-research-hub.github.io/fpga-lab/references/)**: Synthesizable Verilog cheat sheet, Vivado simulation tips, and common FPGA troubleshooting.

---

## Local Development & Preview

The site is built with **MkDocs** and **Material for MkDocs**.

### 1. Prerequisites
Ensure Python 3.10+ and [`uv`](https://github.com/astral-sh/uv) (or standard `pip`) are installed:

```bash
# Using uv (recommended)
uv venv .venv
uv pip install -r requirements.txt
```

### 2. Live Development Server
Start the hot-reloading preview server:

```bash
.venv/bin/mkdocs serve
```

Open [http://127.0.0.1:8000](http://127.0.0.1:8000) in your web browser.

### 3. Production Build
```bash
.venv/bin/mkdocs build --strict
```

---

## Automated Deployment

Pushing changes to the `main` branch automatically triggers the GitHub Actions workflow in [`.github/workflows/deploy.yml`](.github/workflows/deploy.yml), which builds and deploys the static documentation to **GitHub Pages**.

To enable GitHub Pages in your repository:
1. Go to your repository **Settings** -> **Pages**.
2. Under **Build and deployment** -> **Source**, choose **Deploy from a branch**.
3. Select branch **`gh-pages`** and folder **`/ (root)`**, then click **Save**.
