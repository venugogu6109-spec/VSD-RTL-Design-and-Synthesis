# VSDIAT Chip Design Program

Welcome to my **VSDIAT Chip Design Program** repository.

This repository contains my practical work and learning progress in **RTL design, Verilog HDL, simulation, synthesis, optimization, gate-level simulation, and ASIC design concepts**.

---

## About Me

**Name:** Gogu Venu
**University:** Anurag University
**Program:** B.Tech
**Branch:** Electronics and Communication Engineering (ECE)

---

## Tools Used

* **Verilog HDL** – RTL design
* **Icarus Verilog** – Simulation
* **GTKWave** – Waveform analysis
* **Yosys** – Synthesis and optimization
* **SKY130 HD** – Standard-cell library
* **Ubuntu VDI** – VLSI development environment
* **Oracle VirtualBox** – Virtual machine environment

---

# Module 1 – RTL Design and Synthesis

Module 1 introduced the basic concepts required for RTL-based digital design and synthesis.

### Work Covered

* Verilog RTL coding
* Writing testbenches
* DUT creation
* RTL simulation
* Generating simulation waveforms
* Viewing waveforms using GTKWave
* Introduction to logic synthesis
* Yosys synthesis commands
* Understanding synthesized logic
* Standard-cell libraries
* SKY130 technology
* RTL-to-gate-level conversion
* Basic timing concepts
* Setup and hold timing

### Outcome

I learned how a Verilog RTL description can be simulated, synthesized, optimized, and converted into a gate-level hardware representation.

**Status:** ✅ Completed

---

# Module 2 – Sequential Logic and Hierarchical RTL

Module 2 focused on sequential circuits and the organization of RTL designs into multiple modules.

### Work Covered

### Flip-Flop Design

* D Flip-Flop implementation
* Synchronous reset
* Asynchronous reset
* Different sequential coding styles
* RTL simulation
* Synthesized flip-flop structures

### Hierarchical Design

* Creating multiple RTL modules
* Module instantiation
* Connecting submodules
* Hierarchical design
* Flat synthesis
* Comparison of hierarchical and flat synthesis

### Synthesis

* Yosys RTL synthesis
* Logic optimization
* SKY130 technology mapping
* Gate-level netlist generation
* Netlist inspection

### Outcome

I understood how sequential RTL is represented as hardware and how hierarchical designs are processed during synthesis.

**Status:** ✅ Completed

---

# Module 3 – RTL Optimization

Module 3 concentrated on the optimization of different RTL structures during synthesis.

## Combinational Logic

Experiments were performed on:

* Logic simplification
* Constant propagation
* Redundant logic removal
* Multi-module optimization
* Technology mapping

## Sequential Logic

The module also covered:

* Sequential RTL optimization
* D Flip-Flop based designs
* Constant-driven sequential logic
* Optimized sequential structures

## Counter Design

Counter-based RTL was studied with emphasis on:

* Counter implementation
* Synthesis
* Optimization
* Standard-cell mapping
* Synthesized hardware structure

### Outcome

I learned how synthesis tools analyze RTL and remove unnecessary logic while maintaining the required functionality.

**Status:** ✅ Completed

---

# Module 4 – Gate-Level Simulation

Module 4 focused on the behavior of synthesized designs and the differences that can occur between RTL simulation and gate-level simulation.

### Work Covered

* RTL simulation
* Synthesis
* Gate-level netlist generation
* Gate-Level Simulation (GLS)
* RTL and gate-level waveform comparison
* Synthesis-simulation mismatch
* Blocking assignment behavior
* Ternary-operator based MUX
* Synthesized MUX structure
* Gate-level waveform analysis

### Outcome

I learned the importance of writing RTL carefully so that the intended behavior is maintained through both **RTL simulation and synthesized hardware**.

**Status:** ✅ Completed

---

# Module 5 – Conditional RTL Constructs and Synthesis

Module 5 focused on Verilog conditional constructs and how synthesis interprets them as hardware.

### Conditional Statements

* `if`
* `if-else`
* `case`
* Partial case assignments
* Incomplete conditional assignments

### Hardware Inference

The experiments covered:

* Combinational logic inference
* Latch inference
* MUX implementation
* DEMUX implementation
* Generate constructs
* Repeated hardware structures

### Arithmetic Hardware

* Ripple Carry Adder
* RTL implementation
* Simulation
* Synthesis
* Synthesized hardware analysis

### Outcome

I learned that incomplete assignments in combinational RTL can result in unintended hardware such as **latches**, and that RTL coding style has a direct effect on synthesized hardware.

**Status:** ✅ Completed

---

# RTL Design Flow

The practical workflow followed during the training can be summarized as:

```text
RTL Coding
    ↓
Testbench Development
    ↓
RTL Simulation
    ↓
Waveform Verification
    ↓
RTL Synthesis
    ↓
Logic Optimization
    ↓
Technology Mapping
    ↓
Gate-Level Netlist
    ↓
Gate-Level Simulation
    ↓
Hardware Verification
```

--

# Overall Progress

| Module   | Area                          | Status |
| -------- | ----------------------------- | ------ |
| Module 1 | RTL Design & Synthesis        | ✅      |
| Module 2 | Sequential & Hierarchical RTL | ✅      |
| Module 3 | RTL Optimization              | ✅      |
| Module 4 | Gate-Level Simulation         | ✅      |
| Module 5 | RTL Constructs & Synthesis    | ✅      |

---

# Key Takeaway

The VSDIAT program has given me practical experience in connecting **Verilog RTL with synthesized digital hardware**.

The major concepts covered so far include:

* RTL design
* Sequential and combinational logic
* Simulation
* Waveform analysis
* Synthesis
* Optimization
* Gate-level netlists
* Gate-Level Simulation
* Standard-cell mapping
* SKY130 technology
* Synthesis-aware RTL coding

---

## Author

**Gogu Venu**
B.Tech – Electronics and Communication Engineering
**Anurag University**

**VSDIAT Chip Design Program – Modules 1 to 5 Completed ✅**
