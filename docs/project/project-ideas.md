# Project Scaffolds & Ideas

Teams can choose one of the following four pre-approved project scaffolds, or submit a custom project proposal to the instructor.

---

## Option 1: Multi-Mode Digital Stopwatch & Precision Lap Timer

```
+-------------------------------------------------------------+
| [MM:SS] on 7-Segment Displays (Minutes and Seconds)         |
| BTNU: Start/Resume   BTND: Stop/Pause   BTNC: Lap/Split     |
| SW[0]: Normal/Lap Mode   SW[1]: Countdown/Countup           |
| Block RAM: Stores up to 16 historical lap times             |
+-------------------------------------------------------------+
```

### Architecture Highlights
- Precision $100\text{ Hz}$ ($10\text{ ms}$) timebase derived from the $100\text{ MHz}$ system clock.
- BCD (Binary Coded Decimal) counters with ripple-carry logic for hundredths of a second, seconds, and minutes.
- Circular Block RAM buffer storing up to 16 lap timestamps with recall mode.
- 4-digit multiplexed 7-segment display with blinking decimal point separator.

---

## Option 2: "Simon Says" Interactive Memory Game

```
+-------------------------------------------------------------+
| 4 Directional Buttons (BTNU, BTND, BTNL, BTNR)              |
| 4 Colored LEDs (or 4 LED groups) indicating sequence        |
| Linear Feedback Shift Register (LFSR) pseudo-random gen     |
| 7-Segment Display showing current score / level             |
+-------------------------------------------------------------+
```

### Architecture Highlights
- **LFSR (Linear Feedback Shift Register)**: Generates random 4-step sequence extensions on each completed level.
- **Game Controller FSM**: States for `IDLE`, `GENERATE_PATTERN`, `DISPLAY_PATTERN`, `USER_INPUT_WAIT`, `EVALUATE`, `GAME_OVER`, and `VICTORY`.
- **Scoreboard Subsystem**: Tracks high scores and renders the level number onto the 7-segment display.
- **Audio Output (Optional Stretch Goal)**: Drive a piezo buzzer via Pmod with unique tone frequencies per button.

---

## Option 3: UART Command Processor & RPN Calculator

```
+-------------------------------------------------------------+
| PC Terminal <---> USB-UART Bridge <---> FPGA Core           |
| Commands: "PUSH 12", "ADD", "SUB", "MUL", "PRINT", "POP"    |
| Internal 16-word Stack Architecture                         |
| Real-time stack depth shown on LEDs; Top-of-Stack on 7-seg  |
+-------------------------------------------------------------+
```

### Architecture Highlights
- Command parser FSM decoding ASCII input strings over the $115,200\text{ baud}$ UART interface.
- 16-bit Hardware ALU supporting Addition, Subtraction, Multiplication, and Bitwise operations.
- LIFO (Last-In-First-Out) hardware stack buffer with overflow/underflow flag protections.
- Immediate terminal response transmitting calculation results back to the PC console.

---

## Option 4: VGA Video Display Engine & Retro Pong Animation

```
+-------------------------------------------------------------+
| 640x480 @ 60Hz Industry-Standard Timing Generator          |
| HSYNC (Pin J19), VSYNC (Pin V20), 12-bit RGB DAC            |
| Ball velocity, paddle physics, wall collision detection     |
| Pushbuttons control Player 1 and Player 2 paddles           |
+-------------------------------------------------------------+
```

### Architecture Highlights
- Pixel clock generator ($25.175\text{ MHz}$) using Artix-7 mixed-mode clock manager (MMCM / Clocking Wizard IP).
- Horizontal and Vertical timing counters generating exact blanking intervals, front porch, and back porch sync pulses.
- BRAM-based tile graphics or on-the-fly combinational coordinate geometry rendering.
- Game physics engine updating ball position and collision trajectories at $60\text{ Hz}$ frame refresh rates.
