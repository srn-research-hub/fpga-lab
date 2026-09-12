# Lab 3: Finite State Machines & Debouncing

<p class="subtitle">Digital System Design · Lab 03</p>

## Objectives
- Master the **3-always-block methodology** for robust, synthesizable Finite State Machines (FSMs).
- Understand mechanical switch contact bounce and implement a hardware debouncing circuit with a synchronous 2-FF synchronizer and counter timer.
- Build a single-cycle edge detector (pulse generator) for reliable user button events.
- Implement an interactive digital FSM application (Traffic Light Controller with Pedestrian Crosswalk).

---

## The Mechanical Contact Bounce Problem

Pushbuttons and toggle switches contain physical metal contacts. When pressed, the contacts mechanically bounce against each other for $5\text{ ms}$ to $20\text{ ms}$ before settling into a steady state.

```
Raw Button:    ____|||||||||||--------------------
Debounced:     ____________________----------------
Single Pulse:  ____________________|‾|_____________
```

Without a debouncer, an FPGA clocked at $100\text{ MHz}$ registers hundreds of false button transitions on every press!

---

## Hardware Debouncer Architecture

```verilog
module debouncer #(
    parameter CLK_FREQ_HZ = 100_000_000,
    parameter DEBOUNCE_MS = 10
)(
    input  wire clk,
    input  wire rst,
    input  wire button_in,
    output reg  button_out,
    output wire button_pulse // 1-clock-cycle pulse on press
);

    localparam THRESHOLD = (CLK_FREQ_HZ / 1000) * DEBOUNCE_MS;

    // 2-stage synchronizer to prevent metastability
    reg sync_0, sync_1;
    always @(posedge clk) begin
        sync_0 <= button_in;
        sync_1 <= sync_0;
    end

    reg [31:0] counter;
    reg button_state;
    reg button_state_prev;

    always @(posedge clk or posedge rst) begin
        if (rst) begin
            counter      <= 0;
            button_state <= 0;
        end else if (sync_1 != button_state) begin
            counter <= counter + 1'b1;
            if (counter >= THRESHOLD) begin
                button_state <= sync_1;
                counter      <= 0;
            end
        end else begin
            counter <= 0;
        end
    end

    // Output registration and edge detection
    always @(posedge clk) begin
        button_out        <= button_state;
        button_state_prev <= button_out;
    end

    assign button_pulse = button_out & ~button_state_prev;

endmodule
```

---

## 3-Block FSM Coding Template

A robust synthesizable FSM decouples sequential state registers from combinational next-state and output logic:

```verilog
module traffic_light_fsm (
    input  wire       clk,
    input  wire       rst,
    input  wire       sensor_pedestrian,
    output reg  [2:0] main_lights, // Red, Yellow, Green
    output reg  [2:0] side_lights
);

    // State Encoding (One-Hot or Gray)
    localparam S_GREEN  = 2'b00;
    localparam S_YELLOW = 2'b01;
    localparam S_RED    = 2'b10;

    reg [1:0] state, next_state;

    // 1. Sequential State Register
    always @(posedge clk or posedge rst) begin
        if (rst)
            state <= S_GREEN;
        else
            state <= next_state;
    end

    // 2. Combinational Next-State Logic
    always @(*) begin
        next_state = state;
        case (state)
            S_GREEN:  if (sensor_pedestrian) next_state = S_YELLOW;
            S_YELLOW: next_state = S_RED;
            S_RED:    next_state = S_GREEN;
            default:  next_state = S_GREEN;
        endcase
    end

    // 3. Output Logic (Registered or Combinational)
    always @(*) begin
        case (state)
            S_GREEN:  begin main_lights = 3'b001; side_lights = 3'b100; end
            S_YELLOW: begin main_lights = 3'b010; side_lights = 3'b100; end
            S_RED:    begin main_lights = 3'b100; side_lights = 3'b001; end
            default:  begin main_lights = 3'b100; side_lights = 3'b100; end
        endcase
    end

endmodule
```

---

## Checkoff Rubric

| Item | Points | Description |
| :--- | :---: | :--- |
| **State Transition Diagram** | 20 | Complete, verified state diagram submitted with pre-lab |
| **Debouncer & Synchronizer** | 30 | Debounce counter correctly filters contact bounce |
| **Hardware Demo** | 50 | FSM transitions accurately on physical button presses with zero glitching |
| **Total** | **100** | |
