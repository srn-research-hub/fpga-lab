# Synthesizable Verilog HDL Cheat Sheet

A concise reference guide to standard, synthesizable Verilog HDL constructs for FPGA design.

---

## 1. Golden Rules of Verilog Assignments

| Circuit Type | Sensitivity List | Assignment Operator | Target Data Type |
| :--- | :--- | :---: | :---: |
| **Continuous Combinational** | Outside always block (`assign`) | `=` | `wire` |
| **Procedural Combinational** | `always @(*)` | `=` *(Blocking)* | `reg` |
| **Sequential (Flip-Flop/Register)** | `always @(posedge clk)` | `<=` *(Non-blocking)* | `reg` |

> [!CAUTION]
> **Never mix `=` and `<=` inside the same `always` block.**
> Never drive the same `reg` or `wire` from multiple always blocks or continuous assignments!

---

## 2. Inferred Latch Prevention

If a combinational `always @(*)` block fails to specify an output value for every possible execution branch, synthesis tools **infer an asynchronous transparent latch** to hold the previous value.

Latches cause timing hazards, race conditions, and unpredictable bugs in FPGAs.

### Bad (Infers a Latch!):
```verilog
always @(*) begin
    if (sel == 2'b01)
        out = a;
    // Bug: What if sel != 2'b01? out holds state!
end
```

### Good (Pure Combinational):
```verilog
always @(*) begin
    out = 1'b0; // Default assignment prevents all latches!
    if (sel == 2'b01)
        out = a;
end
```

---

## 3. Operators Summary

### Bitwise vs. Logical
- **Bitwise** (evaluates bit-by-bit): `&` (AND), `|` (OR), `^` (XOR), `~` (NOT), `~^` (XNOR).
- **Logical** (evaluates to single-bit `1'b0` or `1'b1`): `&&`, `||`, `!`.
- **Reduction** (reduces bus to 1 bit):
  - `&bus` : 1 if all bits are 1
  - `|bus` : 1 if any bit is 1
  - `^bus` : Parity of bus (1 if odd number of 1s)

### Concatenation and Replication
- Concatenate: `{a, b, c[1:0]}`
- Replication: `{4{1'b0}}` yields `4'b0000`. `{2{a, b}}` yields `{a, b, a, b}`.

---

## 4. Module Parameterization & Instantiation

```verilog
// 1. Definition with parameters
module shift_reg #(
    parameter WIDTH = 8,
    parameter DEPTH = 4
)(
    input  wire             clk,
    input  wire             rst,
    input  wire [WIDTH-1:0] d_in,
    output wire [WIDTH-1:0] d_out
);
    // Internal registers and logic...
endmodule

// 2. Named Port Instantiation
shift_reg #(
    .WIDTH(16),
    .DEPTH(8)
) u_shift_inst (
    .clk   (clk_100mhz),
    .rst   (reset_btn),
    .d_in  (sensor_data),
    .d_out (filtered_data)
);
```
