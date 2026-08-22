
# Module 1 – Introduction to Verilog RTL Design and Synthesis

## Overview

Module 1 introduces the basic concepts of RTL design, Verilog HDL, logic synthesis, standard cell libraries, Yosys, Icarus Verilog, GTKWave, netlists and SKY130 technology.

In this module, a 2:1 Multiplexer (MUX) was designed using Verilog RTL, simulated using Icarus Verilog, verified using GTKWave and synthesized using Yosys.

---

# 1. RTL Design

RTL stands for **Register Transfer Level**.

RTL design is a behavioral representation of the required digital circuit specification.

The digital circuit is described using a Hardware Description Language (HDL), such as Verilog.

The RTL code describes how the circuit should behave, and the synthesis tool converts this RTL description into a gate-level implementation.

### RTL Design Flow

```text
RTL Verilog Code
       ↓
    Synthesis
       ↓
Gate-Level Netlist
       ↓
Digital Logic Circuit
````

---

# 2. Logic Synthesis

Logic synthesis is the process of converting RTL code into a gate-level representation of a digital circuit.

The synthesis tool reads the Verilog RTL and maps the required logic to standard cells available in the technology library.

The final output of synthesis is called a **netlist**.

### Basic Synthesis Flow

```text
Verilog RTL
     +
Technology Library (.lib)
     ↓
   Yosys
     ↓
Gate-Level Netlist
```

The netlist represents the actual hardware structure using available standard cells.

---

# 3. Synthesizer – Yosys

**Yosys** is an open-source RTL synthesis tool.

It is used to convert Verilog RTL designs into gate-level netlists.

In this module, Yosys was used to synthesize the 2:1 MUX and map it to SKY130 standard cells.

The basic flow is:

```text
Verilog RTL
     ↓
   Yosys
     ↓
Logic Optimization
     ↓
Technology Mapping
     ↓
Gate-Level Netlist
```

---

# 4. Yosys Setup

The synthesis environment contains the RTL design and the required technology library.

The `.lib` file provides information about the available standard cells to the synthesis tool.

Yosys reads the Verilog design and the library information and generates the corresponding gate-level implementation.

## Screenshot – Yosys Setup

(set_up.png)

# 5. Standard Cell Library – .lib

A `.lib` file is a standard cell library file.

It contains information about different logic cells available in a particular technology.

The library can contain cells such as:

* AND gates
* OR gates
* NOT gates
* NAND gates
* NOR gates
* Multiplexers
* Flip-flops
* Other digital logic cells

The library also contains information such as:

* Cell functionality
* Cell delay
* Power characteristics
* Area
* Timing information

---

# 6. Different Flavours of Standard Cells

Different versions, or flavours, of the same logic cell can have different timing, area and power characteristics.

For example, a library may contain:

```text
Fast Cell
Medium Cell
Slow Cell
```

The synthesis tool selects suitable cells depending on the design requirements and constraints.

---

# 7. Faster Cells vs Slower Cells

The load in a digital logic circuit is mainly associated with capacitance.

The faster the capacitance can be charged and discharged, the smaller the cell delay becomes.

To charge and discharge capacitance quickly, transistors capable of providing more current are required.

Therefore:

```text
Wider Transistor
       ↓
More Current
       ↓
Faster Charging / Discharging
       ↓
Lower Delay
       ↓
Higher Area and Power
```

Similarly:

```text
Narrower Transistor
       ↓
Less Current
       ↓
Slower Charging / Discharging
       ↓
Higher Delay
       ↓
Lower Area and Power
```

Therefore, faster cells do not come for free. They generally have an area and power penalty.

---

# 8. Why Do We Need Slow Cells?

It may seem that using faster cells everywhere would make the circuit better.

However, this is not always true.

Digital circuits have both **setup-time** and **hold-time** requirements.

Consider the following path:

```text
DFF A
  ↓
Combinational Logic
  ↓
DFF B
```

The data launched from DFF A must reach DFF B within the required clock period.

For setup timing:

```text
TCLK > TCQ + TCOMB + TSETUP
```

where:

* `TCLK` = Clock period
* `TCQ` = Clock-to-Q delay
* `TCOMB` = Combinational path delay
* `TSETUP` = Setup time

However, if data reaches the receiving flip-flop too quickly, a **hold-time violation** may occur.

Therefore, slow cells can be useful for increasing the delay of very short paths and avoiding hold-time violations.

### Main Idea

```text
Fast cells
    ↓
Low delay
    ↓
Good performance
    ↓
But higher area and power

Slow cells
    ↓
Higher delay
    ↓
Can help fix hold problems
    ↓
Lower area and power
```

---

# 9. Cell Selection

The synthesis tool needs guidance to select the appropriate standard cell flavour.

Using too many fast cells can result in:

* Higher area
* Higher power
* Possible hold-time problems

Using too many slow cells can result in:

* Higher delay
* Poor performance
* Failure to meet timing requirements

Therefore, the synthesis tool uses **constraints** to select suitable cells.

The objective is to achieve an appropriate balance between:

* Timing
* Area
* Power

---

# 10. 2:1 Multiplexer Design

A 2:1 Multiplexer has:

* Two data inputs: `i0` and `i1`
* One select input: `sel`
* One output: `y`

The operation is:

```text
sel = 0  →  y = i0

sel = 1  →  y = i1
```

### Block Representation

```text
          ┌─────────┐
i0 ──────►│         │
          │   MUX   ├──────► y
i1 ──────►│         │
          │         │
sel ─────►│         │
          └─────────┘
```

---

# 11. Verilog RTL Code

The 2:1 MUX was implemented using Verilog RTL.

```verilog
module good_mux (
    input i0,
    input i1,
    input sel,
    output reg y
);

always @(*) begin
    if (sel)
        y <= i1;
    else
        y <= i0;
end

endmodule
```

The `always @(*)` block represents combinational logic.

When `sel` is HIGH, `i1` is selected.

When `sel` is LOW, `i0` is selected.

---

# 12. Viewing the Verilog File

GVim / Neovim was used to view and edit the Verilog source files.

The main design file used was:

```text
good_mux.v
```

The testbench file used was:

```text
tb_good_mux.v
```

The design and testbench were examined before performing simulation.

## Screenshot – Verilog MUX Code

(givm_mux.png)


# 13. Testbench

A testbench is used to verify the functionality of the RTL design.

The testbench instantiates the MUX as the **Unit Under Test (UUT)**.

The inputs are changed at different time intervals to check whether the output behaves correctly.

The testbench contains:

* Input registers
* Output wire
* UUT instantiation
* Input stimulus
* VCD dump commands

The VCD file is generated using:

```verilog
$dumpfile("tb_good_mux.vcd");
$dumpvars(0, tb_good_mux);
```

The simulation was performed for:

```text
300 ns
```

---

# 14. Icarus Verilog Simulation

Icarus Verilog was used to compile and simulate the design.

The following command was used:

```bash
iverilog good_mux.v tb_good_mux.v
```

This generates the simulation executable:

```text
a.out
```

The simulation was executed using:

```bash
./a.out
```

The simulation generated the VCD waveform file:

```text
tb_good_mux.vcd
```

---

# 15. Simulation Command

The terminal was used to compile the Verilog design and run the simulation.

The generated VCD file was then used for waveform analysis.

## Screenshot – Simulation Commands

(givm_mux-1.png)

# 16. GTKWave

GTKWave is a waveform viewer used to analyze digital simulation results.

The generated VCD file was opened using:

```bash
gtkwave tb_good_mux.vcd
```

The following signals were observed:

```text
i0
i1
sel
y
```

The waveform helps verify whether the MUX output follows the correct input according to the select signal.

---

# 17. MUX Waveform

The waveform shows the changes of the inputs and output with respect to simulation time.

When:

```text
sel = 0
```

the output follows:

```text
y = i0
```

When:

```text
sel = 1
```

the output follows:

```text
y = i1
```

The simulation was successfully observed up to approximately:

```text
300 ns
```

## Screenshot – GTKWave

(gtkwave_mux.png)
---

# 18. Yosys Synthesis of MUX

After verifying the RTL functionality through simulation, the design was synthesized using Yosys.

Yosys converts the RTL description into a gate-level netlist.

The synthesis process maps the MUX functionality to a standard cell available in the SKY130 library.

The synthesized design used the standard cell:

```text
sky130_fd_sc_hd__mux2_1
```

---

# 19. Synthesized Netlist

The synthesized netlist represents the actual gate-level implementation of the MUX.

The RTL:

```text
if (sel)
    y = i1;
else
    y = i0;
```

is converted into a technology-specific implementation using the available SKY130 standard cell.

## Screenshot – Yosys Netlist
(yosys_netlist.png)

# 20. Netlist Visualization

Yosys was also used to generate a graphical representation of the synthesized design.

The diagram shows:

```text
i0 ─────┐
        │
i1 ─────┤
        │ MUX ─────► y
sel ────┘
```

The graphical representation helps understand how the RTL description is converted into hardware.

The synthesized design is mapped to a SKY130 standard cell.

---

# 21. Synthesized MUX Using SKY130

The synthesized MUX was mapped to:

```text
sky130_fd_sc_hd__mux2_1
```

This is a SKY130 high-density standard cell implementing a 2:1 multiplexer.

The inputs are:

```text
A0
A1
S
```

and the output is:

```text
X
```

The synthesized circuit connects the RTL signals to these cell pins.

## Screenshot – Synthesized MUX
(good_mux.png)

# 22. RTL to Netlist Flow

The complete practical flow performed in this module was:

```text
Verilog RTL
    ↓
Testbench
    ↓
Icarus Verilog
    ↓
Simulation
    ↓
VCD File
    ↓
GTKWave
    ↓
RTL Verification
    ↓
Yosys
    ↓
Technology Mapping
    ↓
SKY130 Standard Cell
    ↓
Gate-Level Netlist
```

---

# 23. Tools Used

| Tool           | Purpose                     |
| -------------- | --------------------------- |
| Verilog HDL    | RTL design                  |
| GVim / Neovim  | Verilog code editing        |
| Icarus Verilog | RTL simulation              |
| GTKWave        | Waveform analysis           |
| Yosys          | Logic synthesis             |
| SKY130         | Standard cell technology    |
| Graphviz / Dot | Netlist visualization       |
| Linux Terminal | Commands and tool execution |

---

# 24. Files Used in the Lab

The important files used during the experiment include:

```text
good_mux.v
tb_good_mux.v
tb_good_mux.vcd
good_mux_netlist.v
```

### Description

**good_mux.v**

Contains the RTL description of the 2:1 MUX.

**tb_good_mux.v**

Contains the testbench used to verify the MUX.

**tb_good_mux.vcd**

Contains simulation waveform data.

**good_mux_netlist.v**

Contains the synthesized gate-level representation generated by Yosys.

---

# 25. What I Learned

Through Module 1, I learned:

1. What RTL design means.
2. How digital circuits are described using Verilog HDL.
3. What logic synthesis means.
4. How RTL is converted into a gate-level netlist.
5. What a `.lib` standard cell library is.
6. Why different flavours of standard cells are available.
7. Difference between faster and slower cells.
8. Relationship between transistor size, delay, area and power.
9. Why slow cells are required in some timing paths.
10. Basics of setup and hold timing.
11. How to design a 2:1 MUX using Verilog.
12. How to create a Verilog testbench.
13. How to compile Verilog using Icarus Verilog.
14. How to generate a VCD waveform file.
15. How to analyze waveforms using GTKWave.
16. How Yosys performs RTL synthesis.
17. How synthesis maps RTL to standard cells.
18. How to generate a synthesized netlist.
19. How to visualize the synthesized design.
20. How SKY130 standard cells are used in synthesis.

---

# 26. Conclusion

Module 1 provided a practical introduction to RTL design and logic synthesis.

A 2:1 Multiplexer was designed using Verilog RTL and verified using a testbench.

The design was simulated using Icarus Verilog and the generated waveform was analyzed using GTKWave.

After functional verification, the RTL was synthesized using Yosys and mapped to the SKY130 standard cell library.

The synthesized netlist was examined and visualized to understand how Verilog RTL is converted into an actual hardware implementation.

This module provided the basic foundation required for further RTL design, synthesis and VLSI implementation work.

````

