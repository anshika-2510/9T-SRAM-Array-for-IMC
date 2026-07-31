# 8×8 9T SRAM Array

This module integrates the previously designed **9T SRAM cell** with all the required peripheral circuits to build a complete **8×8 SRAM array**. The array supports reliable read and write operations and serves as the hardware platform for implementing Compute-in-Memory (IMC) operations in the following stages of this project.
<p align="center">
<img width="1011" height="475" alt="image" src="https://github.com/user-attachments/assets/ca795580-fa2d-4e75-810b-5a1fb3d19c79" />
</p>

---

# Overview

The 8×8 SRAM array consists of **64 identical 9T SRAM cells** arranged in 8 rows and 8 columns. Each memory cell stores one bit of data, allowing the complete array to store **64 bits**.

To enable efficient memory operation, several peripheral circuits are integrated with the array, including row and column decoders, write drivers, precharge circuitry, transmission gates, multiplexers, and sense amplifiers.

<p align="center">
<img src="images/array_overview.png" width="850">
</p>

---

# Architecture

The complete SRAM array consists of the following building blocks:

- 64 × 9T SRAM Cells
- Row Decoder
- Column Decoder
- Precharge Circuit
- Write Driver
- Transmission Gates (TG)
- Multiplexers
- Sense Amplifier (SA)

Together, these blocks enable accurate addressing, writing, reading, and future Compute-in-Memory operations.



---

# Block Diagram

```
                    Address Inputs
                           │
          ┌────────────────┴────────────────┐
          │                                 │
     Row Decoder                     Column Decoder
          │                                 │
          │                         Transmission Gates
          │                                 │
          ▼                                 ▼
               8 × 8 9T SRAM Array
                       │
                Sense Amplifier
                       │
                    Data Output
```

---

# Peripheral Circuits

## Row Decoder

The row decoder activates one wordline corresponding to the selected memory row.

Its responsibilities include:

- Selecting one of eight rows
- Driving the Write Word Line (WWL)
- Driving the Read Word Line (RWL)
- Ensuring only the desired row is accessed during normal memory operation

<p align="center">
<img width="598" height="434" alt="image" src="https://github.com/user-attachments/assets/533eecf8-8d27-43f6-81c0-7285f0d132e2" />

</p>
<p align="center">
<img width="510" height="425" alt="image" src="https://github.com/user-attachments/assets/6d541b6b-214a-4948-a1ed-f53df03b3804" />
</p>

---

## Column Decoder

The column decoder selects the required column within the SRAM array.
Similar to row decoder except that its outputs control the transmission gates, allowing only the selected column to connect to the peripheral circuitry.


<p align="center">
<img src="images/column_decoder.png" width="650">
</p>
<p align="center">
<img width="563" height="310" alt="image" src="https://github.com/user-attachments/assets/ef8ceb0d-3490-475e-807d-ec96956cc959" />
</p>

---

## Transmission Gates (TG)

Transmission gates act as bidirectional switches between the SRAM array and the peripheral circuits.

Functions:

- Column selection
- Signal routing
- Isolation of unselected columns
- Reduced signal degradation compared to single MOS switches

<p align="center">
<img width="526" height="393" alt="image" src="https://github.com/user-attachments/assets/3a313337-8517-455b-8052-3decd1d82123" />
</p>
<p align="center">
<img width="421" height="400" alt="image" src="https://github.com/user-attachments/assets/af9a6be2-3e7f-46e5-bdd1-2951e529eeba" />
</p>

---

## Precharge Circuit

Before every read operation, the read bitlines are precharged to a known voltage level.

This improves:

- Read reliability
- Sense amplifier accuracy
- Read speed

<p align="center">
<img width="856" height="393" alt="image" src="https://github.com/user-attachments/assets/4be12ecd-efa0-42c1-9d60-8f06c13d23c4" />
</p>
<p align="center">
<img width="584" height="380" alt="image" src="https://github.com/user-attachments/assets/0ecf6b22-5f84-4456-8f36-95638979dec1" />
</p>

---

## Write Driver

The write driver forces the desired logic value onto the write bitlines.

During a write operation:

- BL receives the input data
- BLB receives the complement
- WWL is asserted
- Data is written into the selected SRAM cell

<p align="center">
<img width="727" height="421" alt="image" src="https://github.com/user-attachments/assets/5f9cc15e-34ed-4f59-83f1-9e631ca96159" />
</p>
<p align="center">
<img width="694" height="445" alt="image" src="https://github.com/user-attachments/assets/cd294947-2acd-42ce-97d4-af9be5aec4e2" />
</p>

---

## Sense Amplifier

The sense amplifier detects the small voltage difference developed on the read bitlines after a read operation.

Its functions include:

- Fast read operation
- Reliable logic detection
- Amplification of small voltage differences
- Digital output generation

<p align="center">
  <img width="591" height="427" alt="image" src="https://github.com/user-attachments/assets/8264ee86-82eb-40c0-ac8e-a60bdfd9e3e3" />

</p>

---
> **Note:**  
> Small capacitive loads are added to the **Q** and **QB** nodes in the 8×8 SRAM array. Unlike the standalone 9T SRAM cell, these capacitors emulate the parasitic capacitance introduced by array interconnects and neighboring circuitry, allowing the simulations to capture realistic charging/discharging behavior and RC delay during read and write operations.
# Array Operation

## Write Operation

1. Input address is applied.
2. The row decoder activates the selected Write Word Line (WWL).
3. The write driver places the required data on BL and BLB.
4. The selected SRAM cell stores the new value.
5. WWL is disabled, returning the cell to the hold state.

---

## Read Operation

1. Read bitlines are precharged.
2. The row decoder activates the Read Word Line (RWL).
3. The selected SRAM cell conditionally discharges the read bitline.
4. The column decoder connects the selected column through the transmission gate.
5. The sense amplifier detects the voltage difference and generates the output data.

---

# Design Specifications

| Parameter | Value |
|-----------|-------|
| Array Size | 8 × 8 |
| Total Cells | 64 |
| SRAM Cell | 9T SRAM |
| Capacity | 64 bits |
| Read Architecture | Independent Read Port |
| Design Level | Transistor Level |
| Design Tool | Cadence Virtuoso |
| Simulator | Spectre |
| Technology | 45 nm CMOS |

---

# Pin Description
## External signals
| Pin | Direction | Description |
|------|-----------|-------------|
| VDD | Input | Power supply |
| GND | Input | Ground |
| ROW_ADDR[2:0] | Input | Row address input |
| COL_ADDR[2:0] | Input | Column address input |
| BL | Input / Output | Write bitlines |
| BLB | Input / Output | Complementary write bitlines |
| RBL | Output | Read bitlines |
| RBLB | Output | Complementary read bitlines |

## Internal signals
| Signal | Description |
|---------|-------------|
| WWL| Write Word Lines generated by the row decoder |
| RWL | Read Word Lines generated by the row decoder |
| Q | Internal storage nodes |
| QB | Complementary storage nodes |
---

# Verification

The complete SRAM array was verified through:

- Single Cell Read
- Single Cell Write
- Multiple Address Read
- Multiple Address Write
- Row Selection
- Column Selection
- Decoder Verification
- Sense Amplifier Verification
- Transmission Gate Verification



# Simulation Results

## Write,Precharge & Read '1 '

<p align="center">
<img width="1391" height="632" alt="WhatsApp Image 2026-07-12 at 12 43 41 AM" src="https://github.com/user-attachments/assets/78311241-1df3-4350-a123-5399c6aa96d3" />
 Operation
</p>

## Write,Precharge & Read '0'

<p align="center">
<img width="1391" height="632" alt="WhatsApp Image 2026-07-12 at 12 43 41 AM" src="https://github.com/user-attachments/assets/78311241-1df3-4350-a123-5399c6aa96d3" />
 Operation
</p>

---

# Key Features

- 64 Transistor-Level 9T SRAM Cells
- Independent Read Architecture
- Integrated Row & Column Decoders
- Precharge Circuit
- Write Driver
- Transmission Gate Based Column Selection
- Sense Amplifier Assisted Read
- Fully Functional 8×8 SRAM Array
- Designed for Compute-in-Memory (IMC) Extension

---
