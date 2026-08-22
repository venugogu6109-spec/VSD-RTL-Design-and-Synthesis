
# 🚀 VSDIAT Chip Design Program

This repository documents my hands-on learning journey through the **VSDIAT (VLSI System Design – Anurag Institute Chip Design Program)**.

The repository contains my practical work in **Verilog RTL design, functional simulation, waveform analysis, RTL synthesis, logic optimization, gate-level simulation, standard-cell mapping, and ASIC design concepts**.

It serves as a record of my progress from writing RTL code to understanding how that RTL is transformed into synthesized digital hardware.

---

## 👨‍🎓 Student Information

* **Name:** Gogu Venu
* **University:** Anurag University
* **Program:** B.Tech
* **Branch:** Electronics and Communication Engineering (ECE)

---

## 🛠️ Development Environment

| Tool / Environment    | Description         |
| --------------------- | ------------------- |
| Operating System      | Windows 11          |
| Virtual Machine       | Ubuntu – VSDIAT VDI |
| Virtualization        | Oracle VirtualBox   |
| RTL Simulator         | Icarus Verilog      |
| Waveform Viewer       | GTKWave             |
| Synthesis Tool        | Yosys               |
| Standard Cell Library | SKY130 HD           |
| HDL                   | Verilog             |

---

# 📁 Repository Structure

```text
VSDIAT-Chip-Design/
│
├── README.md
│
├── Module_1/
│
├── Module_2/
│   ├── 01_Hierarchical_vs_Flat_Synthesis/
│   ├── 02_Flip_Flop_Coding_Styles/
│   └── 03_Synthesis_Optimizations/
│
├── Module_3/
│   ├── README.md
│   ├── 01_Combinational_Optimization/
│   ├── 02_Sequential_Optimization/
│   └── 03_Counter_Optimization/
│
├── Module_4/
│   ├── README.md
│   ├── bad_mux_tb_sim.png
│   ├── blocking_caveat_sim.v.png
│   ├── blocking_caveat_synth.png
│   ├── GLS_blocking_caveat.png
│   ├── GLS_tb_bad_mux.v.png
│   ├── GTKWave_ternary_mux_GLS.png
│   ├── sim_ternary_operator_mux.png
│   └── ternary_operator_mux_synth.png
│
└── Module_5/
    ├── README.md
    ├── Ripple_Carry_Adder/
    ├── bad_case/
    ├── comp_case/
    ├── demux_case/
    ├── incomp_if/
    ├── incomp_if2/
    ├── mux_generate/
    └── partial_case_assign/
```

---

# 📚 Program Progress

| Module       | Focus Area                                               | Status      |
| ------------ | -------------------------------------------------------- | ----------- |
| **Module 1** | RTL Design, Verilog, Simulation & Synthesis Fundamentals | ✅ Completed |
| **Module 2** | Sequential Logic, Hierarchical Design & RTL Synthesis    | ✅ Completed |
| **Module 3** | Combinational, Sequential & Counter Optimization         | ✅ Completed |
| **Module 4** | Gate-Level Simulation & RTL–Synthesis Mismatch           | ✅ Completed |
| **Module 5** | RTL Constructs, `if`/`case` & Synthesis                  | ✅ Completed |

---

# 📘 Module 1 – RTL Design and Synthesis Fundamentals

Module 1 established the foundation for understanding the **RTL-to-hardware design flow**.

The module focused on how digital hardware functionality is described using **Verilog HDL**, verified through simulation, and transformed into hardware structures using synthesis tools.

### Topics Covered

* Verilog HDL fundamentals
* RTL design methodology
* RTL as a behavioral representation of hardware
* Testbench development
* Design Under Test (DUT)
* RTL functional simulation
* Waveform generation
* Waveform analysis using GTKWave
* Introduction to logic synthesis
* RTL-to-gate-level transformation
* Yosys synthesis flow
* Standard-cell libraries
* SKY130 technology
* Synthesized hardware inspection
* Basic timing concepts
* Setup and hold timing
* Cell delay and capacitance
* Area, power and performance trade-offs

### Key Learning

Module 1 helped establish the connection between **Verilog RTL and physical hardware implementation**.

The important concept learned was that RTL code is not simply software code; it is a description of the hardware that synthesis tools can convert into gates and standard cells.

🔗 **Explore Module 1 →**
`Module_1/`

---

# ⚙️ Module 2 – Sequential Logic, Hierarchical Design and RTL Synthesis

Module 2 focused on **sequential RTL design, hierarchical design, synthesis and technology mapping**.

Different sequential coding styles were implemented and analyzed to understand how coding style affects the synthesized hardware.

### Topics Covered

* D flip-flop design
* Synchronous reset
* Asynchronous reset
* Sequential RTL coding styles
* Hierarchical RTL design
* Module instantiation
* Hierarchical versus flat synthesis
* RTL synthesis using Yosys
* Logic optimization
* SKY130 standard-cell mapping
* Synthesized netlist generation
* Netlist inspection
* Sequential hardware structures

### D Flip-Flop Experiments

Different D flip-flop configurations were designed and verified using Verilog.

The experiments helped understand:

* Clock-controlled sequential behavior
* Reset implementation
* Synchronous reset operation
* Asynchronous reset operation
* Simulation behavior
* Synthesized flip-flop structures

### Hierarchical Design

Hierarchical RTL design was studied to understand how a large design can be divided into smaller reusable modules.

The design hierarchy can be represented as:

```text
Top Module
    │
    ├── Submodule 1
    │
    ├── Submodule 2
    │
    └── Submodule 3
```

This approach improves **design organization, reusability, debugging and scalability**.

### Synthesis Flow

```text
Verilog RTL
     │
     ▼
RTL Elaboration
     │
     ▼
Logic Optimization
     │
     ▼
Technology Mapping
     │
     ▼
SKY130 Standard Cells
     │
     ▼
Gate-Level Netlist
```

### Key Learning

Module 2 demonstrated that different RTL coding styles can result in different synthesized structures.

It also provided practical understanding of how **sequential RTL is converted into standard-cell based hardware**.

🔗 **Explore Module 2 →**
`Module_2/`

---

# 🔬 Module 3 – Combinational, Sequential and Counter Optimization

Module 3 focused on understanding how synthesis tools analyze and optimize different types of RTL logic.

The experiments demonstrated that synthesis tools can simplify RTL while preserving the required functional behavior.

## Combinational Optimization

Topics included:

* Logic simplification
* Constant propagation
* Removal of redundant logic
* Multiple-module optimization
* Boolean optimization
* Technology mapping
* SKY130 standard-cell implementation

## Sequential Optimization

Topics included:

* D flip-flop based RTL
* Constant-driven sequential logic
* Sequential optimization
* Optimization of unnecessary logic
* Synthesized sequential structures

## Counter Optimization

Counter RTL was designed and synthesized to understand how sequential arithmetic structures are represented using standard cells.

Topics included:

* Counter RTL coding
* Counter synthesis
* Counter optimization
* Sequential logic analysis
* Standard-cell mapping
* Synthesized counter structures

### Key Learning

Module 3 demonstrated that synthesis is not simply a direct conversion of every RTL statement into a gate.

The synthesis tool analyzes the RTL and performs **optimization, simplification and technology mapping** to produce an efficient hardware implementation.

🔗 **Explore Module 3 →**
`Module_3/`

---

# 🧪 Module 4 – Gate-Level Simulation and RTL–Synthesis Mismatch

Module 4 introduced **Gate-Level Simulation (GLS)** and investigated situations where RTL simulation and synthesized hardware behavior can differ.

The module emphasized the importance of writing RTL that has predictable behavior during both simulation and synthesis.

### Topics Covered

* RTL simulation
* RTL waveform analysis
* Synthesis analysis
* Gate-level netlist generation
* Gate-Level Simulation
* RTL versus synthesized behavior
* Synthesis-simulation mismatch
* Blocking assignment behavior
* Ternary operator based multiplexers
* Gate-level waveform analysis
* Synthesized logic inspection

### RTL-to-GLS Flow

```text
RTL Code
   │
   ▼
RTL Simulation
   │
   ▼
Yosys Synthesis
   │
   ▼
Gate-Level Netlist
   │
   ▼
Gate-Level Simulation
   │
   ▼
Waveform Comparison
```

### Main Learning

The experiments showed that **RTL coding style directly influences the hardware inferred by synthesis**.

Careful use of Verilog constructs is therefore essential to avoid unexpected simulation and synthesis behavior.

🔗 **Explore Module 4 →**
`Module_4/`

---

# 🧩 Module 5 – RTL Constructs, `if`/`case` and Synthesis

Module 5 focused on common Verilog RTL constructs and their effect on synthesized hardware.

The experiments investigated how conditional statements describe combinational logic, multiplexers, demultiplexers and other hardware structures.

### Topics Covered

* `if` statements
* `if-else` statements
* `case` statements
* Incomplete conditional assignments
* Latch inference
* Combinational logic
* MUX implementation
* DEMUX implementation
* Generate constructs
* Partial case assignments
* Ripple Carry Adder
* RTL simulation
* RTL synthesis
* Synthesized hardware analysis

## Latch Inference

One of the important concepts studied was **latch inference**.

When a combinational block does not assign an output for every possible input condition, the synthesis tool may infer a latch to preserve the previous value.

```text
Complete Assignment
        │
        ▼
Combinational Logic
        │
        ▼
No Storage Element

Incomplete Assignment
        │
        ▼
Previous Value Required
        │
        ▼
Latch Inference
```

### Generate Constructs

Generate constructs were explored for creating repeated hardware structures.

They are particularly useful when designing hardware with multiple similar components.

### Ripple Carry Adder

A Ripple Carry Adder was implemented to understand how multiple full-adder structures can be connected to perform multi-bit binary addition.

```text
A0 ──┐
B0 ──┤
Cin ─┤
     ▼
   Full Adder ── C1
     │
     ▼
   Full Adder ── C2
     │
     ▼
   Full Adder ── C3
     │
     ▼
   Full Adder ── Cout
```

### Main Learning

Module 5 reinforced the importance of writing **complete and synthesis-friendly RTL**.

The experiments demonstrated that coding decisions such as incomplete `if`/`case` assignments can directly influence the hardware inferred by synthesis.

🔗 **Explore Module 5 →**
`Module_5/`

---

# 🎯 Learning Objectives

Through the VSDIAT training, I am developing practical knowledge in:

* **Verilog HDL**
* **RTL design methodology**
* **Digital logic design**
* **Sequential logic design**
* **Combinational logic design**
* **Functional simulation**
* **Testbench development**
* **Waveform analysis**
* **RTL synthesis**
* **Logic optimization**
* **Gate-level netlist generation**
* **Gate-Level Simulation**
* **Standard-cell mapping**
* **SKY130 technology**
* **ASIC design concepts**
* **Synthesis-aware RTL coding**

---

# 🔄 RTL-to-Hardware Design Flow

The overall learning journey can be represented by the following flow:

```text
             Verilog RTL
                  │
                  ▼
          RTL Functional Simulation
                  │
                  ▼
            Waveform Analysis
                  │
                  ▼
             RTL Elaboration
                  │
                  ▼
           Logic Optimization
                  │
                  ▼
            Technology Mapping
                  │
                  ▼
         SKY130 Standard Cells
                  │
                  ▼
          Gate-Level Netlist
                  │
                  ▼
         Gate-Level Simulation
                  │
                  ▼
          Hardware Verification
```

This flow demonstrates how an RTL description gradually becomes a technology-mapped digital hardware implementation.

---

# 🧠 Important Concepts Learned

Throughout the modules, several important ASIC design principles were explored.

### 1. RTL is a Hardware Description

Verilog RTL describes the intended behavior and structure of digital hardware.

### 2. Coding Style Matters

The same functionality can sometimes be described using different coding styles, but the resulting synthesized hardware may differ.

### 3. Synthesis Performs Optimization

Yosys analyzes RTL and performs transformations such as:

* Constant propagation
* Logic simplification
* Redundant logic removal
* Sequential optimization
* Technology mapping

### 4. Incomplete Assignments Can Infer Latches

Combinational RTL should normally assign outputs for all possible input conditions to avoid unintended storage elements.

### 5. Simulation and Synthesis Must Agree

RTL should be written carefully so that simulation behavior and synthesized hardware behavior remain consistent.

### 6. Standard Cells Form the Synthesized Hardware

After synthesis and technology mapping, RTL logic can be represented using cells from a standard-cell library such as **SKY130**.

### 7. Gate-Level Simulation Provides Additional Verification

GLS allows the synthesized netlist to be simulated and analyzed to verify the behavior of the mapped hardware.

---

# 🧰 Core Tools

| Tool                  | Purpose                                            |
| --------------------- | -------------------------------------------------- |
| **Icarus Verilog**    | RTL simulation and functional verification         |
| **GTKWave**           | Waveform visualization and analysis                |
| **Yosys**             | RTL synthesis, optimization and netlist generation |
| **SKY130 HD**         | Standard-cell technology for synthesis and mapping |
| **Ubuntu VDI**        | Development environment for the VSDIAT flow        |
| **Oracle VirtualBox** | Virtualization environment                         |

---

# 📈 Skills Developed

The VSDIAT program has provided practical exposure to the following areas:

```text
Verilog HDL
     │
     ▼
RTL Design
     │
     ▼
Simulation
     │
     ▼
Waveform Analysis
     │
     ▼
Synthesis
     │
     ▼
Optimization
     │
     ▼
Technology Mapping
     │
     ▼
Standard Cells
     │
     ▼
Gate-Level Netlist
     │
     ▼
Gate-Level Simulation
```

These concepts form an important foundation for further learning in **ASIC Design, VLSI Design, RTL Design, Physical Design and Digital IC Design**.

---

# 🚀 Current Progress

## VSDIAT Modules 1–5 Completed ✅

The first five modules of the VSDIAT Chip Design Program have been completed with hands-on RTL design, simulation, synthesis and analysis exercises.

The repository will continue to be updated as I progress into additional **ASIC/VLSI design concepts, RTL experiments and practical implementation flows**.

---

# 📌 Key Takeaway

> **RTL coding style directly influences the hardware inferred by synthesis.**

The VSDIAT training has helped me understand the complete connection between **RTL code, simulation, synthesis, optimization, standard-cell mapping and gate-level hardware**.

Through hands-on experiments, I have learned that ASIC design is not only about writing correct Verilog code, but also about understanding **how synthesis tools interpret that code and transform it into real digital hardware structures**.


