# 9T SRAM Cell

A transistor-level implementation of a **9-Transistor (9T) SRAM cell** designed in **Cadence Virtuoso**. This cell serves as the fundamental building block for the complete Compute-in-Memory (IMC) SRAM architecture implemented in this repository.

The design focuses on achieving reliable read and write operations while providing an independent read path to improve read stability compared to a conventional 6T SRAM cell.


<img width="260" height="230" alt="9tsramcell_overview" src="https://github.com/user-attachments/assets/055770b8-874e-4493-bfe2-a100112c5a54" />

---

# Objective

The objective of this module is to design and verify a robust 9T SRAM cell before integrating it into a larger SRAM array for in-memory computing applications.

---

# Cell Architecture

The 9T SRAM cell consists of:

- Two cross-coupled CMOS inverters for data storage
- Two write access transistors controlled by the Write Word Line (WWL)
- Three additional transistors forming an independent read path controlled by the Read Word Line (RWL)

This separation of the read and write paths reduces read disturbance and improves overall cell stability.

<p align="center">
<img width="300" height="228" alt="9tsramcell_zoom1" src="https://github.com/user-attachments/assets/fe8fa1f2-fc8e-4011-b622-da229d56c548" />
</p>
<p align="center">
<img width="326" height="192" alt="9tsramcell_writedriver" src="https://github.com/user-attachments/assets/afc98cc4-e83d-4a18-935a-3163fdc2abc9" />
</p>


---

# Working Principle


<img width="1920" height="1080" alt="Screenshot from 2026-06-11 14-23-34" src="https://github.com/user-attachments/assets/f5ff4571-d18f-447e-8d07-f1be944e4fc3" />

## Hold Operation

When both the Write Word Line (WWL) and Read Word Line (RWL) are disabled, the two cross-coupled inverters continuously reinforce each other, allowing the stored bit to remain unchanged without external intervention.

---

## Write Operation

To write new data into the cell:

1. The required data is driven onto the Bit Line (BL) and Bit Line Bar (BLB).
2. The Write Word Line (WWL) is enabled.
3. The access transistors connect the storage nodes to the bitlines.
4. The new data overwrites the previously stored value.
5. WWL is disabled, returning the cell to the hold state.


---

## Read Operation

The read path is isolated from the storage nodes.

1. The Read Bit Line (RBL) is precharged.
2. The Read Word Line (RWL) is enabled.
3. Depending on the stored data, the read transistor stack either discharges the RBL or leaves it unchanged.
4. The Sense Amplifier detects the resulting voltage difference and converts it into a digital logic value.

Since the storage nodes are isolated from the read bitline, the stored data is not disturbed during the read operation.

---

# Design Specifications

| Parameter | Value |
|-----------|-------|
| SRAM Type | 9T SRAM |
| Design Level | Transistor Level |
| Technology | 45 nm CMOS |
| Design Tool | Cadence Virtuoso |
| Simulator | Spectre |
| Supply Voltage | 1.8V |

---

# Transistor Sizing

The transistor dimensions were selected to achieve a balance between stability, write ability, and read performance.

| Transistor Group | Width (W) | Length (L) | Description |
|------------------|----------:|-----------:|-------------|
| **PMOS (Cross-Coupled Latch)** | 180 nm | 45 nm | Pull-up transistors forming the storage latch. |
| **NMOS (Cross-Coupled Latch)** | 280 nm | 45 nm | Pull-down transistors providing strong data retention and read stability. |
| **Write Access Transistors** | 180 nm | 45 nm | Controlled by the Write Word Line (WWL) to enable write operations. |
| **Read Path Transistors** | 120 nm | 45 nm | Three NMOS transistors forming the independent read path controlled by the Read Word Line (RWL). |
# Pin Description

| Pin | Direction | Description |
|------|-----------|-------------|
| **VDD** | Input | Power supply for the SRAM cell. |
| **GND** | Input | Ground reference for the SRAM cell. |
| **BL** | Input / Output | True write bitline used during write operations. |
| **BLB** | Input / Output | Complementary write bitline used during write operations. |
| **WWL** | Input | Write Word Line. Enables the write access transistors during write operations. |
| **RWL** | Input | Read Word Line. Enables the independent read path. |
| **RBL** | Output | True read bitline. Precharged before a read operation and conditionally discharged depending on the stored data. |
| **RBLB** | Output | Complementary read bitline. Used with **RBL** for differential sensing to improve read reliability. |
| **Q** | Output | Internal storage node holding the stored logic value. |
| **QB** | Output | Complementary internal storage node of **Q**. |


# Simulation Results

## WRITE ,PRECHARGE & READ '1'

<p align="center">

<img width="1920" height="1080" alt="Screenshot from 2026-06-11 14-21-54" src="https://github.com/user-attachments/assets/846db071-37dc-47b5-95cd-9954b88e46e1" />
</p>

---

## WRITE ,PRECHARGE & READ '0'

<p align="center">
<img width="1920" height="1080" alt="Screenshot from 2026-06-11 14-56-17" src="https://github.com/user-attachments/assets/d73db5d6-5614-4d89-9ffb-db005099bf74" />
</p>

---
# Symbol
<img width="331" height="220" alt="image" src="https://github.com/user-attachments/assets/e06439f4-dc8b-45a1-abfa-02dd6d64fc75" />

# Key Features

- Transistor-level 9T SRAM implementation
- Independent read path
- Improved read stability
- Separate read and write word lines
- Cadence Virtuoso implementation
- Spectre simulation verification
- Foundation for SRAM-based Compute-in-Memory architecture


After validating the functionality of the 9T SRAM cell, the next step is to design the peripheral circuits required to build a complete SRAM array:

- Precharge Circuit
- Write Driver
- Row Decoder
- Column Decoder
- Transmission Gate
- Sense Amplifier

These blocks are later integrated to construct an **8×8 SRAM array** capable of performing Compute-in-Memory (IMC) operations.
