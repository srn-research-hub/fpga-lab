# Common Pitfalls & Troubleshooting Guide

A curated guide to resolving the most frequent synthesis errors, implementation DRC violations, and hardware issues encountered in FPGA labs.

---

## 1. Synthesis & Implementation DRC Errors

### Error: `[DRC NSTD-1] Unspecified I/O Standard`
- **Cause**: One or more top-level module ports were not assigned an I/O standard in your `.xdc` file.
- **Fix**: Open your XDC file and verify that every port has an accompanying `set_property IOSTANDARD LVCMOS33 [get_ports <port_name>]` line.

### Error: `[DRC UCIO-1] Unconstrained Logical Port`
- **Cause**: A top-level port is missing a physical FPGA pin assignment (`PACKAGE_PIN`).
- **Fix**: Check port names in your Verilog `module top (...)` declaration against the exact case-sensitive port names inside `constraints.xdc`.

### Error: `[Synth 8-3352] multi-driven net to pin`
- **Cause**: A `reg` or `wire` is being assigned in two separate `always` blocks or by both an `assign` statement and an `always` block.
- **Fix**: Combine the assignments into a single `always` block using multiplexer logic or conditional `if/else` statements.

---

## 2. Hardware & Programmer Issues

### Issue: Hardware Manager reports "No targets found"
1. Verify the board power switch is **ON** (look for the illuminated green LED near the switch).
2. Ensure you are using a **data-capable** micro-USB cable (many cheap cables are power-only charging cables).
3. Try plugging into a different USB port directly on your PC (avoid unpowered USB hubs).
4. On Linux, ensure `udev` rules for Digilent JTAG cables are installed:
   ```bash
   cd /tools/Xilinx/Vivado/<version>/data/xicom/cable_drivers/lin64/install_script/install_drivers/
   sudo ./install_drivers
   ```

### Issue: Outputs glitch or button presses trigger multiple times
- **Cause**: Mechanical contact bounce.
- **Fix**: Pass the raw pushbutton input through a synchronous debouncer module (see [Lab 3: FSMs & Debouncing](../labs/lab3.md)) before using it as an FSM transition condition or clock enable.

### Issue: Inferred Latches / Unexpected Circuit Behavior
- **Cause**: Incomplete `if-else` or `case` statements in combinational `always @(*)` blocks.
- **Fix**: Provide default assignments at the very top of your combinational always blocks:
  ```verilog
  always @(*) begin
      // Assign default values to ALL outputs first
      next_state = state;
      led_output = 1'b0;
      
      // Conditional overrides
      case (state)
          // ...
      endcase
  end
  ```
