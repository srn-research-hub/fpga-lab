# Digital System Design — FPGA Lab Sessions

<p class="subtitle">UCF · College of Engineering & Computer Science · Department of ECE</p>

Welcome to the **FPGA Laboratory Sessions for Digital System Design**. This course provides hands-on experience in RTL design using synthesizable **Verilog HDL**, simulation testbenches, and hardware implementation on the **Digilent Basys 3 FPGA** (AMD/Xilinx Artix-7) using **AMD Vivado ML**.

---

<div class="stat-grid">
  <div class="stat-card">
    <div class="stat-value">5</div>
    <div class="stat-label">Laboratory Sessions</div>
    <div class="stat-sub">From Gates to Serial I/O</div>
  </div>
  <div class="stat-card">
    <div class="stat-value">1</div>
    <div class="stat-label">Capstone Project</div>
    <div class="stat-sub">Team Digital System Design</div>
  </div>
  <div class="stat-card">
    <div class="stat-value">Artix-7</div>
    <div class="stat-label">FPGA Target</div>
    <div class="stat-sub">XC7A35T-1CPG236C</div>
  </div>
  <div class="stat-card">
    <div class="stat-value">Vivado</div>
    <div class="stat-label">EDA Toolchain</div>
    <div class="stat-sub">Synthesis · P&R · ILA</div>
  </div>
</div>

---

## Quick Navigation

<div class="card-grid card-grid--4">
  <div class="nav-card">
    <span class="card-icon">🚀</span>
    <strong>Toolchain Setup</strong>
    <p>Install AMD Vivado ML Edition and configure cable drivers.</p>
    <a class="md-button md-button--primary" href="getting-started/vivado-setup.md">Get Started →</a>
  </div>
  <div class="nav-card">
    <span class="card-icon">🔌</span>
    <strong>Basys 3 Board</strong>
    <p>Pinouts, clocking, switches, LEDs, and 7-segment display specs.</p>
    <a class="md-button md-button--primary" href="getting-started/basys3-guide.md">Hardware Guide →</a>
  </div>
  <div class="nav-card">
    <span class="card-icon">🧪</span>
    <strong>Lab Sessions</strong>
    <p>Complete lab manuals for all 5 progressive FPGA labs.</p>
    <a class="md-button md-button--primary" href="labs/index.md">View Labs →</a>
  </div>
  <div class="nav-card">
    <span class="card-icon">🏆</span>
    <strong>Capstone Project</strong>
    <p>System specifications, project scaffolds, and grading rubrics.</p>
    <a class="md-button md-button--primary" href="project/index.md">Project Specs →</a>
  </div>
</div>

---

## Laboratory Curriculum Arc

The laboratory sessions follow a progressive learning path from basic combinational logic gates to complex interactive digital systems.

<div class="card-grid card-grid--3">
  <a class="day-card" href="labs/lab1.md">
    <div class="day-num">LAB 01</div>
    <div class="day-title">Combinational Logic & Vivado Workflow</div>
    <div class="day-desc">HDL primitives, structural & behavioral modeling, testbenches, synthesis, and programming your first bitstream.</div>
  </a>

  <a class="day-card" href="labs/lab2.md">
    <div class="day-num">LAB 02</div>
    <div class="day-title">Sequential Logic & Clock Dividers</div>
    <div class="day-desc">D Flip-Flops, synchronous registers, binary up/down counters, and dividing the 100 MHz oscillator to human-visible frequencies.</div>
  </a>

  <a class="day-card" href="labs/lab3.md">
    <div class="day-num">LAB 03</div>
    <div class="day-title">Finite State Machines & Debouncing</div>
    <div class="day-desc">Mealy and Moore FSM state diagrams, push-button mechanical contact debouncing, and synchronous edge detection.</div>
  </a>

  <a class="day-card" href="labs/lab4.md">
    <div class="day-num">LAB 04</div>
    <div class="day-title">Memory & 7-Segment Displays</div>
    <div class="day-desc">Distributed and Block RAM (BRAM), time-multiplexed 4-digit 7-segment LED display controller, and hex decoders.</div>
  </a>

  <a class="day-card" href="labs/lab5.md">
    <div class="day-num">LAB 05</div>
    <div class="day-title">UART Serial Communication</div>
    <div class="day-desc">Asynchronous serial transmitter and receiver, baud rate generator, FIFO buffers, and PC-to-FPGA serial interaction.</div>
  </a>

  <a class="day-card" href="project/index.md">
    <div class="day-num">FINAL PROJECT</div>
    <div class="day-title">Capstone Digital System Design</div>
    <div class="day-desc">Collaborative digital system implementation integrating FSMs, memory, peripherals, and external I/O on the Basys 3.</div>
  </a>
</div>

---

## Standard Laboratory Workflow

Every lab follows an industry-standard digital IC design and FPGA verification pipeline:

```mermaid
flowchart LR
    A[Design Spec] --> B[Verilog RTL]
    B --> C[Simulation & TB]
    C -->|Bugs Found| B
    C -->|Tests Pass| D[XDC Constraints]
    D --> E[Vivado Synthesis]
    E --> F[Implementation & Timing]
    F --> G[Generate Bitstream]
    G --> H[Basys 3 Demo]
```

> [!TIP]
> **Simulate Before You Synthesize!**
> Synthesis and Bitstream generation can take several minutes. Writing behavioral testbenches and verifying in Vivado Simulator (`xsim`) saves 80% of your lab debugging time.

---

## Resources & Helpful References

- [Basys 3 Master XDC Constraints](getting-started/xdc-master.md) — Copy and uncomment pins for switches, LEDs, 7-seg, and clock.
- [Synthesizable Verilog HDL Cheat Sheet](references/verilog-cheatsheet.md) — Quick reference for operators, always blocks, and FSM templates.
- [Vivado Simulation & Timing Tips](references/vivado-tips.md) — How to inspect waveforms, fix timing violations, and read synthesis logs.
- [Troubleshooting & Common Traps](references/troubleshooting.md) — How to solve inferred latches, multi-driven nets, and unassigned pins.
