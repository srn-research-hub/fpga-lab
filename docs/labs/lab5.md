# Lab 5: UART Serial Communication

<p class="subtitle">Digital System Design · Lab 05</p>

## Objectives
- Understand the fundamentals of **asynchronous serial communication (RS-232 / UART)**.
- Implement an accurate baud rate generator yielding standard communication speeds (**115200 baud**).
- Design a UART Transmitter (`uart_tx`) and a 16× oversampling UART Receiver (`uart_rx`) using finite state machines.
- Establish bidirectional communication between the Basys 3 FPGA and a host computer serial terminal via the on-board FTDI USB bridge.

---

## The UART 8N1 Protocol

UART is an asynchronous protocol (no shared clock line). Lines idle at **logic high** (`1`).

```
Idle (1) -> [Start: 0] -> [D0] [D1] [D2] [D3] [D4] [D5] [D6] [D7] -> [Stop: 1] -> Idle
```

At **$115,200\text{ baud}$**, each bit duration is:

$$T_{\text{bit}} = \frac{1}{115,200} \approx 8.68\ \mu\text{s}$$

On a $100\text{ MHz}$ FPGA clock:

$$\text{Clocks per bit} = \frac{100 \times 10^6}{115,200} \approx 868\text{ clock cycles}$$

---

## UART Transmitter Module (`uart_tx.v`)

```verilog
module uart_tx #(
    parameter CLKS_PER_BIT = 868 // 100MHz / 115200 baud
)(
    input  wire       clk,
    input  wire       rst,
    input  wire       tx_start,
    input  wire [7:0] tx_data,
    output reg        tx_active,
    output reg        tx_serial,
    output reg        tx_done
);

    localparam S_IDLE  = 2'b00;
    localparam S_START = 2'b01;
    localparam S_DATA  = 2'b10;
    localparam S_STOP  = 2'b11;

    reg [1:0]  state;
    reg [15:0] clk_count;
    reg [2:0]  bit_index;
    reg [7:0]  data_reg;

    always @(posedge clk or posedge rst) begin
        if (rst) begin
            state     <= S_IDLE;
            tx_serial <= 1'b1;
            tx_active <= 1'b0;
            tx_done   <= 1'b0;
            clk_count <= 0;
            bit_index <= 0;
        end else begin
            case (state)
                S_IDLE: begin
                    tx_serial <= 1'b1;
                    tx_active <= 1'b0;
                    tx_done   <= 1'b0;
                    clk_count <= 0;
                    bit_index <= 0;
                    if (tx_start) begin
                        data_reg  <= tx_data;
                        tx_active <= 1'b1;
                        state     <= S_START;
                    end
                end

                S_START: begin
                    tx_serial <= 1'b0; // Start bit
                    if (clk_count < CLKS_PER_BIT - 1) begin
                        clk_count <= clk_count + 1'b1;
                    end else begin
                        clk_count <= 0;
                        state     <= S_DATA;
                    end
                end

                S_DATA: begin
                    tx_serial <= data_reg[bit_index];
                    if (clk_count < CLKS_PER_BIT - 1) begin
                        clk_count <= clk_count + 1'b1;
                    end else begin
                        clk_count <= 0;
                        if (bit_index < 7) begin
                            bit_index <= bit_index + 1'b1;
                        end else begin
                            bit_index <= 0;
                            state     <= S_STOP;
                        end
                    end
                end

                S_STOP: begin
                    tx_serial <= 1'b1; // Stop bit
                    if (clk_count < CLKS_PER_BIT - 1) begin
                        clk_count <= clk_count + 1'b1;
                    end else begin
                        tx_done   <= 1'b1;
                        clk_count <= 0;
                        state     <= S_IDLE;
                    end
                end
            endcase
        end
    end

endmodule
```

---

## Host Serial Terminal Setup

You can interact with your FPGA design using any serial terminal on your host machine:

- **Windows**: PuTTY or TeraTerm (Set Speed: `115200`, Data bits: `8`, Parity: `None`, Stop bits: `1`).
- **macOS / Linux**:
  ```bash
  # Check connected USB-Serial device
  ls /dev/tty.usbserial-*
  
  # Connect via screen
  screen /dev/tty.usbserial-* 115200
  ```

---

## Checkoff Rubric

| Item | Points | Description |
| :--- | :---: | :--- |
| **Baud Rate Calculation** | 20 | Detailed derivation and tolerance analysis for 115200 baud |
| **UART Loopback Simulation** | 30 | Simulation showing byte transmission and reception with framing verification |
| **Hardware Demo** | 50 | Bidirectional communication: keystrokes typed in terminal echo and display on LEDs |
| **Total** | **100** | |
