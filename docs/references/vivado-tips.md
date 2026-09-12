# Vivado Workflow & Simulation Tips

Essential productivity techniques, debugging tricks, and command-line tips for **AMD Vivado ML**.

---

## 1. Inspecting Your Design Before Synthesis

### Open Elaborated Design
Under **RTL Analysis** in the Vivado Flow Navigator, click **Open Elaborated Design** -> **Schematic**.
- This parses your raw Verilog and visually renders the inferred gates, registers, and multiplexers.
- **Why this matters**: If you see red or orange latch symbols (`LDCE`) instead of standard D Flip-Flops (`FDRE`), you accidentally introduced an inferred latch!

---

## 2. Vivado Simulator (`xsim`) Power Tips

- **Change Signal Radix**: Right-click any signal or bus in the waveform window -> **Radix** -> Choose **Hexadecimal** or **Unsigned Decimal**.
- **Add Internal Signals**: Expand the hierarchy tree in the **Scope** window, select a submodule, and drag its internal nets directly into the **Waveform** pane. Click **Restart** (Ctrl+Shift+F5) and **Run All** (F3) to capture the new signals.
- **Measuring Signal Delays**: Click the waveform to drop **Cursor 1**. Drag with your mouse to drop **Cursor 2**. Vivado automatically displays the time delta ($\Delta T$) and corresponding frequency ($1/\Delta T$).

---

## 3. Essential TCL Console Commands

Vivado features an interactive TCL console at the bottom of the IDE:

```tcl
# Query resource utilization summary
report_utilization -hierarchical

# Inspect timing slack (Worst Negative Slack)
report_timing_summary -max_paths 10

# Find all physical package pins
get_package_pins -of_objects [get_ports]

# Reset and re-run synthesis from scratch
reset_run synth_1
launch_runs synth_1 -jobs 4
```

---

## 4. Programming the Basys 3

1. Connect the Micro-USB cable to the Basys 3 USB-JTAG port.
2. Toggle the power switch (top left corner) to **ON** (a green power LED will illuminate).
3. In Vivado Flow Navigator -> **Open Hardware Manager** -> **Open Target** -> **Auto Connect**.
4. Right-click the detected `xc7a35t` device -> **Program Device**.
5. Select your `.bit` file located in:
   `<project_name>.runs/impl_1/<top_module>.bit`
6. Click **Program**! The yellow `DONE` LED on the Basys 3 will light up when configuration is complete.
