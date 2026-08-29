# RTL to Gate-Level Synthesis and GLS – Sequence Detector

## Project Overview

This repository documents the complete work completed for assessment **25eg504h06**, from the initial RTL design through functional simulation, synthesis, post-synthesis/Gate-Level Simulation (GLS), waveform analysis, and RTL-vs-GLS verification.

### Complete Flow

```text
RTL Design
   ↓
Functional / Pre-Synthesis Simulation
   ↓
RTL Waveform Verification
   ↓
Logic Synthesis
   ↓
Synthesized Gate-Level Netlist
   ↓
Post-Synthesis / Gate-Level Simulation (GLS)
   ↓
GLS Waveform Verification
   ↓
RTL vs GLS Comparison
   ↓
Final Functional Conclusion
```

---

## 1. Project Directory

Working directory:

```bash
~/BabySoC_Simulation/assesments/25eg504h06
```

Files observed in the project:

```text
25eg504h06/
├── rtl/
├── tb/
│   └── tb.v
├── synthesized.v
├── pre_synth_sim.out
└── dump.vcd
```

During GLS debugging, a corrected local SKY130 model was also created:

```text
sky130_fd_sc_hd_gls.v
```

---

## 2. RTL Design

The design is a Verilog **finite-state-machine based sequence detector**.

Main module:

```verilog
module sequence_detector(clk, reset, din, detected);
```

Important signals:

| Signal | Description |
|---|---|
| `clk` | Clock input |
| `reset` | Reset input |
| `din` | Serial data input |
| `detected` | Sequence detection output |
| `state[2:0]` | Current FSM state |
| `next_state[2:0]` | Next FSM state |

The RTL describes the intended behavior of the sequence detector. The FSM state changes according to the input `din`, and `detected` indicates a successful sequence detection.

### Screenshot 1 – RTL Code

Add:

```text
images/01_rtl_code.png
```

![rtl code](<ChatGPT Image Aug 29, 2026, 09_49_42 PM-1.png>)
---

## 3. Testbench

The testbench is located at:

```text
tb/tb.v
```

It instantiates the design as:

```verilog
sequence_detector dut (
    .clk(clk),
    .reset(reset),
    .din(din),
    .detected(detected)
);
```

### Clock

The testbench generates the clock using:

```verilog
always #4 clk = ~clk;
```

Therefore:

```text
Clock period = 8 ns
```

### Input sequence

The testbench applies a long sequence of `0` and `1` values using:

```verilog
drive_bit(1'b0);
drive_bit(1'b1);
```

and so on.

### Detection counting

The testbench also maintains:

```verilog
integer detection_count = 0;
```

and counts detection events when:

```verilog
if (!reset && detected)
    detection_count = detection_count + 1;
```

This count is useful for comparing RTL and GLS behavior.

### VCD generation

The testbench contains:

```verilog
$dumpfile("dump.vcd");
$dumpvars(0, tb);
```

Therefore, the simulation waveform is saved as:

```text
dump.vcd
```

> **Important:** the correct testbench path is `tb/tb.v`, not `tab/tb.v`.

---

# 4. Functional / Pre-Synthesis Simulation

Before synthesis, the original RTL was simulated with the testbench.

The simulation produced:

```text
pre_synth_sim.out
dump.vcd
```

The VCD file was opened using GTKWave.

### Important signals checked

```text
clk
reset
din
detected
state[2:0]
next_state[2:0]
detection_count
```

### Purpose

The purpose of pre-synthesis simulation was to verify that:

- reset initializes the FSM,
- input data is applied correctly,
- FSM states change according to the input,
- `detected` responds to the required sequence,
- the expected detection events are produced.

### Screenshot 2 – Pre-Synthesis RTL Waveform

Add:

```text
images/02_pre_synthesis_waveform.png
```
![pre synthesis](<Screenshot 2026-08-29 103857.png>)

---

# 5. Waveform Analysis

GTKWave was used to inspect the generated VCD.

The waveform contains:

```text
clk
reset
din
detected
state
next_state
detection_count
```

The main purpose of this step was to establish the **functional RTL reference** before synthesis.

The RTL waveform is later compared against the GLS waveform.

---

# 6. Logic Synthesis

After verifying the RTL, the design was synthesized into a gate-level representation.

The generated netlist is:

```text
synthesized.v
```

The synthesized module was checked using:

```bash
grep -n "module sequence_detector" synthesized.v
```

The result obtained was:

```text
6:module sequence_detector(clk, reset, din, detected);
```

This confirmed that the expected `sequence_detector` module exists in the synthesized netlist.

### RTL vs synthesized representation

**RTL:**

Describes what the circuit should do using behavioral/FSM constructs.

**Synthesized netlist:**

Represents the implemented logic using gate/standard-cell structures.

### Screenshot 3 – Synthesis / Netlist

Add:

```text
images/03_synthesis.png
```

![synthesis](<Screenshot 2026-08-29 111917.png>)
---

# 7. Synthesized Gate-Level Netlist

The file:

```text
synthesized.v
```

is the output representation used for the next stage.

The flow is:

```text
RTL
 ↓
Synthesis
 ↓
synthesized.v
 ↓
Gate-Level Simulation
```

This is important because GLS does not simulate the original RTL module; it checks the synthesized implementation.

---

# 8. Post-Synthesis / Gate-Level Simulation (GLS)

The synthesized design was then prepared for Gate-Level Simulation.

GLS uses:

```text
tb/tb.v
synthesized.v
SKY130 standard-cell simulation model
```

The original SKY130 model was located at:

```text
/home/vsduser/BabySoC_Simulation/src/gls_model/sky130_fd_sc_hd.v
```

The purpose of GLS is to verify that the synthesized implementation still produces the intended functional behavior.

---

# 9. Initial GLS Compilation Problem

The initial GLS compilation command was:

```bash
iverilog -g2012 -o gls_sim.out tb/tb.v synthesized.v /home/vsduser/BabySoC_Simulation/src/gls_model/sky130_fd_sc_hd.v
```

Compilation failed with:

```text
sky130_fd_sc_hd.v:67667: syntax error
sky130_fd_sc_hd.v:67667: error: Invalid module item.
```

Because compilation failed, the executable was not generated:

```bash
ls -lh gls_sim.out
```

returned:

```text
ls: cannot access 'gls_sim.out': No such file or directory
```

---

# 10. Debugging the SKY130 Standard-Cell Model

The suspected declaration was searched using:

```bash
grep -n 'wire 1' /home/vsduser/BabySoC_Simulation/src/gls_model/sky130_fd_sc_hd.v | head
```

The result showed:

```text
67525:    wire 1;
67667:    wire 1;
```

The declaration:

```verilog
wire 1;
```

caused the Verilog parser error because `1` is not a valid signal identifier.

---

# 11. Creating a Corrected Local SKY130 Model

A local copy of the model was created:

```bash
cp /home/vsduser/BabySoC_Simulation/src/gls_model/sky130_fd_sc_hd.v ./sky130_fd_sc_hd_gls.v
```

The invalid declarations were changed using:

```bash
sed -i -E 's/^[[:space:]]*wire[[:space:]]+1[[:space:]]*;/    wire one;/' sky130_fd_sc_hd_gls.v
```

The correction was verified using:

```bash
grep -n 'wire 1\|wire one' sky130_fd_sc_hd_gls.v | head
```

The result became:

```text
67525:    wire one;
67667:    wire one;
```

The surrounding sections were checked with:

```bash
sed -n '67515,67535p' sky130_fd_sc_hd_gls.v
```

and:

```bash
sed -n '67655,67680p' sky130_fd_sc_hd_gls.v
```

This confirmed the corrected local model contained:

```verilog
wire one;
```

instead of the invalid:

```verilog
wire 1;
```

---

# 12. GLS Compilation

The corrected local SKY130 model should be used for GLS:

```bash
iverilog -g2012 -o gls_sim.out tb/tb.v synthesized.v sky130_fd_sc_hd_gls.v
```

If compilation succeeds, the executable is:

```text
gls_sim.out
```

Run the simulation using:

```bash
vvp gls_sim.out
```

The testbench generates:

```text
dump.vcd
```

which can be opened with:

```bash
gtkwave dump.vcd
```

---

# 13. GLS Waveform Analysis

The GLS waveform was inspected in GTKWave.

Important signals include:

```text
clk
reset
din
detected
detection_count
state[2:0]
next_state[2:0]
```

The waveform shows **four detection events**.

The first GLS detection observed in the recorded waveform occurs at approximately:

```text
1169 ns
```

The detection counter reaches:

```text
4
```

at the end of the relevant detection sequence.

### Screenshot 4 – GLS Waveform

Add:

```text
images/04_gls_waveform.png
```
![gls waveform](<Screenshot 2026-08-29 121732.png>)

The screenshot should clearly show `detected` and `detection_count`, including the four detection events.

---

# 14. RTL vs GLS Comparison

The same testbench input sequence is used to verify the synthesized implementation.

### Comparison

| Item | RTL | GLS |
|---|---|---|
| Clock | Same testbench clock | Same testbench clock |
| Reset | Same | Same |
| `din` sequence | Same | Same |
| Detection functionality | Preserved | Preserved |
| Number of detection events | 4 | 4 |
| First GLS detection | — | ~1169 ns |

The key result is:

```text
RTL detection events = 4
GLS detection events = 4
```

This shows that synthesis preserved the functional detection behavior for this testbench.

GLS can also show timing differences compared with ideal RTL simulation because the design is represented at gate level.

### Screenshot 5 – RTL vs GLS Comparison

Add:

```text
images/05_rtl_vs_gls_comparison.png
```
![rtl vs gls](<Screenshot 2026-08-29 214411.png>)

---

# 15. Final Conclusion

**Conclusion:** Yes, the synthesized implementation preserves the functional behavior of the RTL for the given testbench. Both RTL and GLS simulations produce **four detection events**, confirming that the synthesized gate-level implementation maintains the intended sequence-detection functionality.

The recorded GLS waveform shows the first detection at approximately **1169 ns**. Any gate-level timing difference observed in the waveform does not change the logical detection result for this testbench.

---

# 16. Complete RTL-to-GLS Flow

```text
              ┌──────────────────┐
              │    RTL DESIGN    │
              └────────┬─────────┘
                       │
                       ▼
          ┌────────────────────────┐
          │ FUNCTIONAL SIMULATION  │
          │     / PRE-SYNTHESIS    │
          └───────────┬────────────┘
                      │
                      ▼
              ┌──────────────┐
              │ RTL WAVEFORM │
              └──────┬───────┘
                     │
                     ▼
              ┌─────────────┐
              │  SYNTHESIS  │
              └──────┬──────┘
                     │
                     ▼
             ┌────────────────┐
             │ synthesized.v │
             └───────┬────────┘
                     │
                     ▼
          ┌────────────────────────┐
          │ GATE-LEVEL SIMULATION  │
          │          (GLS)         │
          └───────────┬────────────┘
                      │
                      ▼
               ┌─────────────┐
               │ GLS WAVEFORM│
               └──────┬──────┘
                      │
                      ▼
            ┌─────────────────────┐
            │ RTL vs GLS CHECK    │
            └──────────┬──────────┘
                       │
                       ▼
             ┌──────────────────┐
             │ FINAL VERIFICATION│
             └──────────────────┘
```

---

# 17. Screenshots Required in GitHub

Create an `images` folder:

```text
images/
```

Recommended files:

```text
images/
├── 01_rtl_code.png
├── 02_pre_synthesis_waveform.png
├── 03_synthesis.png
├── 04_gls_waveform.png
└── 05_rtl_vs_gls_comparison.png
```

### What each screenshot should show

**1. RTL Code**

Original sequence detector RTL.

**2. Pre-Synthesis Waveform**

Show:

```text
clk
reset
din
detected
state
next_state
```

**3. Synthesis**

Show the synthesized netlist/result.

**4. GLS Waveform**

Show:

```text
clk
reset
din
detected
detection_count
state
next_state
```

Make the four detection events visible.

**5. RTL vs GLS**

Show the relevant waveform evidence demonstrating that the detection behavior is preserved.

---

# 18. Repository Structure

Recommended final GitHub structure:

```text
25eg504h06/
│
├── README.md
│
├── rtl/
│   └── sequence_detector.v
│
├── tb/
│   └── tb.v
│
├── images/
│   ├── 01_rtl_code.png
│   ├── 02_pre_synthesis_waveform.png
│   ├── 03_synthesis.png
│   ├── 04_gls_waveform.png
│   └── 05_rtl_vs_gls_comparison.png
│
├── synthesized.v
├── pre_synth_sim.out
├── dump.vcd
└── sky130_fd_sc_hd_gls.v
```

---

# 19. Tools Used

| Tool | Purpose |
|---|---|
| Verilog | RTL design and testbench |
| Icarus Verilog (`iverilog`) | RTL/GLS compilation |
| `vvp` | Running simulation |
| Yosys | RTL synthesis |
| SKY130 standard-cell model | Gate-level cell simulation |
| GTKWave | Waveform analysis |
| Linux terminal | Compilation, file handling and debugging |
| Git/GitHub | Version control and submission |

---

# 20. Important Commands

### Check project files

```bash
ls
```

### Check testbench

```bash
ls tb
cat tb/tb.v
```

### Check synthesized module

```bash
grep -n "module sequence_detector" synthesized.v
```

### Find SKY130 model issue

```bash
grep -n 'wire 1' /home/vsduser/BabySoC_Simulation/src/gls_model/sky130_fd_sc_hd.v | head
```

### Make local model copy

```bash
cp /home/vsduser/BabySoC_Simulation/src/gls_model/sky130_fd_sc_hd.v ./sky130_fd_sc_hd_gls.v
```

### Correct invalid declaration

```bash
sed -i -E 's/^[[:space:]]*wire[[:space:]]+1[[:space:]]*;/    wire one;/' sky130_fd_sc_hd_gls.v
```

### Verify correction

```bash
grep -n 'wire 1\|wire one' sky130_fd_sc_hd_gls.v | head
```

### Compile GLS

```bash
iverilog -g2012 -o gls_sim.out tb/tb.v synthesized.v sky130_fd_sc_hd_gls.v
```

### Run GLS

```bash
vvp gls_sim.out
```

### Open waveform

```bash
gtkwave dump.vcd
```

---

# 21. Assessment Summary

**Assessment ID:** `25eg504h06`

**Design:** Sequence Detector

**Completed work:**

- RTL design
- Testbench
- Functional/pre-synthesis simulation
- VCD generation
- GTKWave waveform analysis
- Logic synthesis
- Synthesized netlist verification
- Post-synthesis / Gate-Level Simulation
- SKY130 model debugging
- GLS waveform analysis
- RTL vs GLS comparison
- Final functional verification

**Final observed result:**

```text
Detection events = 4
First GLS detection ≈ 1169 ns
```

**Final result:**

```text
The synthesized gate-level implementation preserves
the functional behavior of the RTL for the given testbench.
```

---

## Submission Note

This README records the work completed up to the current stage, starting from RTL and continuing through pre-synthesis simulation, synthesis, post-synthesis/GLS, debugging of the SKY130 simulation model, waveform analysis, and final RTL-vs-GLS verification.
