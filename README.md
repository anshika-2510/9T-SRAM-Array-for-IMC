# 9T SRAM Compute-in-Memory (IMC)

A transistor-level implementation of a **9T SRAM Compute-in-Memory (IMC)** architecture designed in **Cadence Virtuoso**. This project demonstrates how a conventional SRAM array can be extended to perform Boolean and arithmetic computations directly inside memory, reducing unnecessary data movement between memory and processing units.


<img width="260" height="230" alt="9tsramcell_overview" src="https://github.com/user-attachments/assets/6f9e49ff-9857-40ac-b10e-5ecb270e34db" />

---

## Project Overview

Traditional computing systems spend significant time and energy moving data between the processor and memory. Compute-in-Memory (IMC) addresses this limitation by performing computations directly within the memory array.

This project builds a complete IMC system from the ground up, starting with the design of a single 9T SRAM cell and progressively integrating peripheral circuits, an 8×8 SRAM array, Boolean logic operations, and arithmetic computation.

---

## Project Flow

```
9T SRAM Cell
      │
      ▼
Peripheral Circuits
(Precharge, Write Driver,
Decoder, MUX, Transmission Gate,
Sense Amplifier)
      │
      ▼
8×8 SRAM Array
      │
      ▼
Boolean IMC
(AND • OR • NAND • NOR • XOR • XNOR)
      │
      ▼
Arithmetic IMC
(Half Adder • Full Adder • MAC)
```

---

# Repository Structure

```
01_9T_SRAM_Cell/
02_Precharge_Circuit/
03_Write_Driver/
04_Decoders_and_MUX/
05_Transmission_Gate/
06_Sense_Amplifier/
07_8x8_SRAM_Array/
08_IMC_Boolean_Operations/
09_IMC_Arithmetic/
```

---

# Design Methodology

## Step 1 – 9T SRAM Cell

The project begins with the design of a transistor-level 9T SRAM cell. Compared to a conventional 6T SRAM, the additional transistors provide an independent read path, reducing read disturbance and improving stability.

The cell is verified through:

- Hold operation
- Read operation
- Write operation

<p align="center">
<img src="images/9t_cell.png" width="700">
</p>

---

## Step 2 – Peripheral Circuits

Several supporting circuits are designed before constructing the memory array.

### Precharge Circuit

Precharges the bitlines before every read operation to ensure accurate sensing.

### Write Driver

Drives logic '0' or logic '1' onto the bitlines during write operations.

### Row & Column Decoder

Selects the required memory location using the input address.

### Multiplexer

Routes the required signals between different blocks.

### Transmission Gate

Provides controlled signal transfer while minimizing voltage degradation.

### Sense Amplifier

Detects the small voltage difference generated during read operations and converts it into a full digital logic level.

---

## Step 3 – 8×8 SRAM Array

After validating every individual building block, the 9T SRAM cell is replicated to construct an **8×8 SRAM array**.

The array integrates:

- Row Decoder
- Column Decoder
- Precharge Circuit
- Write Driver
- Sense Amplifier
- Transmission Gates

to perform complete read and write operations across all memory locations.

<p align="center">
<img src="images/array.png" width="750">
</p>

---

## Step 4 – Boolean Compute-in-Memory

Instead of simply storing data, the SRAM array is extended to perform Boolean operations directly inside memory.

By activating multiple wordlines simultaneously and utilizing the bitline behavior, logic functions can be computed without transferring data outside the memory array.

Implemented operations include:

- AND
- OR
- NAND
- NOR
- XOR
- XNOR

<p align="center">
<img src="images/boolean.png" width="700">
</p>

---

## Step 5 – Arithmetic Compute-in-Memory

The Boolean outputs are further processed using digital arithmetic circuits.

Implemented arithmetic blocks include:

- Half Adder
- Full Adder
- Multiply-and-Accumulate (MAC)

These operations demonstrate how SRAM can be extended beyond data storage to support more complex in-memory computation.

<p align="center">
<img src="images/mac.png" width="700">
</p>

---

# Simulation Results

Simulation results include:

- 9T SRAM Hold Operation
- 9T SRAM Read Operation
- 9T SRAM Write Operation
- 8×8 Array Verification
- Boolean IMC Operations
- Half Adder
- Full Adder
- MAC Operation

---

# Design Tools

- Cadence Virtuoso
- Cadence ADE
- Spectre Simulator
- CMOS Technology Library

---

# Future Work

Future improvements to this project include:

- Larger SRAM arrays (16×16, 32×32)
- Multi-bit MAC operations
- Monte Carlo variation analysis
- Process corner analysis
- Power and delay optimization
- Post-layout verification

---

# References

- Research papers on 9T SRAM
- Compute-in-Memory (IMC) architectures
- SRAM-based Boolean and Arithmetic IMC implementations

---

