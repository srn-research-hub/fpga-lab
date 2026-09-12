# Lab 1: Combinational Logic & Vivado Design Flow

<p class="subtitle">Digital System Design · Lab 01</p>

## Objectives
- Learn the end-to-end AMD Vivado RTL design workflow: HDL entry, simulation, synthesis, implementation, and bitstream generation.
- Design synthesizable combinational logic modules (multiplexers and decoders) using continuous assignments (`assign`) and behavioral constructs (`always @*`).
- Construct a behavioral testbench with stimulus vectors and verify functionality in Vivado Simulator (`xsim`).
- Constrain physical FPGA pins using the Basys 3 Master XDC file and verify hardware behavior using slide switches and LEDs.

---

## Pre-Lab Preparation

1. Review the differences between continuous assignment (`assign out = sel ? b : a;`) and procedural assignment (`always @(*) begin ... end`).
2. Construct the truth table for a 4-to-1 Multiplexer with an active-high Enable signal.
3. Write behavioral Verilog module declarations and testbench templates before entering the laboratory.

---

## Design Specification

You will design and implement a **Parameterized 4-to-1 Multiplexer** and a **3-to-8 Binary Decoder** with active-low enable.

```
       +------------------+
d0 --->|                  |
d1 --->|      4-to-1      |---> mux_out
d2 --->|       MUX        |
d3 --->|                  |
       +--------+---------+
                ^
             sel[1:0]
```

### Module Interface: `mux4_1.v`
```verilog
module mux4_1 #(
    parameter WIDTH = 1
)(
    input  wire [WIDTH-1:0] in0,
    input  wire [WIDTH-1:0] in1,
    input  wire [WIDTH-1:0] in2,
    input  wire [WIDTH-1:0] in3,
    input  wire [1:0]       sel,
    output reg  [WIDTH-1:0] out
);

    always @(*) begin
        case (sel)
            2'b00:   out = in0;
            2'b01:   out = in1;
            2'b10:   out = in2;
            2'b11:   out = in3;
            default: out = {WIDTH{1'b0}};
        endcase
    end

endmodule
```

---

## Behavioral Simulation Testbench

Before running synthesis, write a self-checking testbench to verify all input combinations:

```verilog
`timescale 1ns / 1ps

module tb_mux4_1();
    reg  [3:0] in0, in1, in2, in3;
    reg  [1:0] sel;
    wire [3:0] out;

    // Instantiate Unit Under Test (UUT)
    mux4_1 #(.WIDTH(4)) uut (
        .in0(in0), .in1(in1), .in2(in2), .in3(in3),
        .sel(sel), .out(out)
    );

    initial begin
        in0 = 4'hA; in1 = 4'hB; in2 = 4'hC; in3 = 4'hD;
        
        sel = 2'b00; #10;
        if (out !== 4'hA) $error("Test 0 failed!");
        
        sel = 2'b01; #10;
        if (out !== 4'hB) $error("Test 1 failed!");
        
        sel = 2'b10; #10;
        if (out !== 4'hC) $error("Test 2 failed!");
        
        sel = 2'b11; #10;
        if (out !== 4'hD) $error("Test 3 failed!");
        
        $display("ALL TESTS PASSED SUCCESSFULLY!");
        $finish;
    end
endmodule
```

---

## Hardware Pin Mapping (XDC)

Connect the inputs and outputs to Basys 3 physical peripherals:

| Signal | Board Peripheral | FPGA Pin |
| :--- | :--- | :--- |
| `in0[0]`, `in0[1]` | Slide Switches `SW0`, `SW1` | `V17`, `V16` |
| `in1[0]`, `in1[1]` | Slide Switches `SW2`, `SW3` | `W16`, `W17` |
| `sel[0]`, `sel[1]` | Slide Switches `SW14`, `SW15`| `T1`, `R2` |
| `out[0]`, `out[1]` | User LEDs `LD0`, `LD1` | `U16`, `E19` |

---

## Checkoff Rubric

| Item | Points | Description |
| :--- | :---: | :--- |
| **Pre-lab & Schematic** | 20 | Complete truth table and RTL module declarations |
| **Simulation Verification** | 30 | Error-free testbench run in Vivado Simulator with waveforms |
| **Hardware Demonstration** | 50 | Bitstream loaded on Basys 3; switches correctly steer to LEDs |
| **Total** | **100** | |
