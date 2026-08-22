# Lab 1 - Introduction to Verilog RTL Design and Simulation

## Objective

The objective of this lab is to understand the basic RTL design
flow using Verilog HDL and become familiar with the tools used
for writing, compiling, simulating and observing Verilog designs.

## Tools Used

- Linux environment
- VirtualBox
- Verilog HDL
- Icarus Verilog (iverilog)
- GTKWave
- GVim/Neovim

## RTL Design

RTL (Register Transfer Level) is used to describe the behavior
of a digital hardware circuit using Verilog HDL.

The RTL description represents the required functionality of
the digital circuit before synthesis.

## Basic Verilog Flow

The basic flow followed in the lab was:

Verilog RTL Code
        ↓
   Verilog Compiler
        ↓
    Simulation
        ↓
   VCD Waveform
        ↓
     GTKWave

## Work Performed

1. Set up the VSD RTL Design and Synthesis workshop environment
   inside the Linux virtual machine.

2. Navigated through the required workshop directories using
   Linux terminal commands.

3. Located the Verilog source files and testbench files.

4. Used a text editor such as GVim/Neovim to view and edit
   Verilog source files.

5. Understood the basic structure of a Verilog module.

6. Identified inputs, outputs, wires and registers used in
   Verilog designs.

7. Understood the role of a testbench in verifying an RTL design.

8. Compiled Verilog source code using Icarus Verilog.

9. Executed the generated simulation output.

10. Generated a VCD (Value Change Dump) file during simulation.

11. Opened the VCD file using GTKWave.

12. Observed the changes in input and output signals with respect
    to simulation time.

13. Verified the relationship between the applied inputs and the
    corresponding output.

## Important Concepts Learned

### RTL

RTL is a behavioral description of the required hardware
functionality using a hardware description language such as
Verilog.

### Testbench

A testbench is used to apply different input conditions to the
design under test and verify its output.

### Icarus Verilog

Icarus Verilog is used to compile and simulate Verilog designs.

### VCD

VCD stands for Value Change Dump. It stores signal changes
generated during simulation.

### GTKWave

GTKWave is a waveform viewer used to analyze the signals
generated during simulation.

## Simulation Flow

The complete simulation process can be represented as:

Verilog Design + Testbench
             ↓
       Icarus Verilog
             ↓
          Simulation
             ↓
           VCD File
             ↓
          GTKWave
             ↓
      Waveform Analysis

## Result

The basic Verilog RTL simulation environment was successfully
understood and tested. The Verilog design was compiled and
simulated, and the generated signal activity was observed using
GTKWave.

## Learning Outcome

This lab provided a basic understanding of the RTL design and
simulation flow. It also established the foundation required
for designing, simulating and verifying digital circuits using
Verilog HDL in the following labs.