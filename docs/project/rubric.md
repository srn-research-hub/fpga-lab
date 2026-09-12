# Capstone Project Evaluation Rubric

Total Points: **100 Points** (constituting 25% of the overall course grade).

---

## Detailed Scoring Breakdown

### 1. Proposal & Architectural Specification (10 Points)
- **Clear Objectives & Scope (3 pts)**: Problem statement, target user experience, and feature list.
- **Hierarchical Block Diagram (4 pts)**: Clean interface definitions, bus widths, and control signal flow between modules.
- **Milestone Schedule (3 pts)**: Realistic task breakdown assigned to individual team members.

### 2. Behavioral Simulation & Testbenches (20 Points)
- **Corner-Case Verification (8 pts)**: Testbench exercises reset conditions, arithmetic boundary limits, and unexpected inputs.
- **Self-Checking Testbenches (7 pts)**: Automated `$display` or `$error` assertions checking outputs against gold models.
- **Annotated Waveforms (5 pts)**: High-resolution waveform screenshots with key signals clearly highlighted.

### 3. Hardware Implementation & Vivado Design Flow (20 Points)
- **Timing Closure (8 pts)**: Setup/hold slack are positive ($WNS \ge 0\text{ ns}$); no timing violations on the 100 MHz clock domain.
- **Synthesis Quality (6 pts)**: Zero inferred latches, no multi-driven nets, and clean synthesis report warnings.
- **Resource Utilization (6 pts)**: Efficient utilization of Artix-7 LUTs, Slice Registers, BRAM blocks, and DSP slices.

### 4. Live Hardware Demonstration (30 Points)
- **Functional Requirements (18 pts)**: System executes all core functionality smoothly on the physical Basys 3 board.
- **Robust User Interface (6 pts)**: Buttons are debounced with zero glitching; displays are stable and flicker-free.
- **Q&A Technical Mastery (6 pts)**: Each team member articulates their subsystem design decisions and trade-offs.

### 5. Technical Report & Code Repository (20 Points)
- **IEEE Formatting & Organization (5 pts)**: Professional structure (Abstract, Introduction, Architecture, Results, Conclusion).
- **RTL Code Quality (8 pts)**: Clean modular code, descriptive naming conventions, and inline comments.
- **Reproducibility (7 pts)**: Well-structured Git repository with Vivado TCL rebuild scripts or project instructions.
