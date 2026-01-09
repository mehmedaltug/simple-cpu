# 8-Bit 4-Cycle CPU Design

## Overview

This repository hosts the design and simulation files for a custom **8-bit, 4-cycle Central Processing Unit (CPU)**. The design is implemented at the logic gate level, featuring a modular separation between the Datapath and the Control Unit.

The architecture is designed to be simple yet functional, capable of performing basic arithmetic and data movement operations through a hardwired 4-cycle instruction lifecycle.

## Features

* **Architecture:** 8-bit Data Bus / 8-bit Address Space.
* **Timing:** Fixed 4-cycle instruction execution (Fetch, Decode, Execute, Write-back).
* **Registers:**
* 8 General Purpose Registers (`R0` - `R7`).
* Dedicated Accumulator (`A`) and Operand Register (`B`) for ALU operations.
* Instruction Register (`IR`).


* **Control Unit:** Hardwired logic using a state counter and combinational decoding.
* **ALU:** Supports addition and subtraction.

## Architecture Details

### 1. The Datapath
<img width="1191" height="1138" alt="main" src="https://github.com/user-attachments/assets/9db849a2-d058-4181-bda9-a15da6160977" />

The main circuit integrates the registers, Arithmetic Logic Unit (ALU), and system bus.

* **Register Bank:** Contains registers `R0` through `R7`, which can store 8-bit values.
* **ALU Core:** The arithmetic operations utilize two specific registers, `A` and `B`.
* **Adder:** Computes `A + B`.
* **Subtractor:** Computes `A - B`.


* **Multiplexing:** A network of multiplexers (MUX) manages data flow, selecting whether the bus is driven by general registers, the ALU result, or external input (`Din`).

### 2. The Control Unit
<img width="1978" height="1641" alt="control-unit" src="https://github.com/user-attachments/assets/e6cf6e30-5d37-4fcd-a367-4f478e0e050e" />

The brain of the CPU, responsible for coordinating all components.

* **State Machine:** Utilizes a 2-bit counter to generate the 4 distinct clock cycles required for every instruction.
* **Instruction Decoder:** Takes the opcode from the Instruction Register (`IR`) and the current clock cycle state to trigger specific control lines.
* **Control Signals:** Outputs a wide array of enable/select signals (e.g., `Reg Write Enable`, `ALU Select`, `Bus Select`) to the main datapath.

---

## Instruction Set Architecture (ISA)

The CPU supports 4 primary operations encoded in the top 2 bits of the instruction.

| Opcode (Binary) | Mnemonic | Operation | Description |
| --- | --- | --- | --- |
| **00** | `MOV` | Move | Transfers data between registers (e.g., `MOV R1, R2`). |
| **01** | `MOVI` | Move Immediate | Loads an immediate value from input into a register. |
| **10** | `ADD` | Add | Adds the value of register B to A (`A = A + B`). |
| **11** | `SUB` | Subtract | Subtracts the value of register B from A (`A = A - B`). |

### Instruction Cycle (4-Cycle Timing)

Each instruction takes exactly 4 clock pulses to complete:

1. **T0 (Fetch):** The instruction is fetched from memory/input into the `IR`.
2. **T1 (Decode/Operand):** The operands are prepared or moved to temp registers (like `A` or `B`).
3. **T2 (Execute):** The ALU performs the calculation or data is moved across the bus.
4. **T3 (Write Back):** The result is latched into the destination register.

---

## Getting Started

### Prerequisites

This project appears to be designed using **Logisim** or **Logisim-Evolution**. You will need the software to open and simulate the circuit.

1. Download [Logisim-evolution](https://github.com/logisim-evolution/logisim-evolution) (recommended) or standard Logisim.
2. Clone this repository:
```bash
git clone https://github.com/yourusername/8bit-4cycle-cpu.git

```



### Running the Simulation

1. Open the main circuit file (`.circ`) in Logisim.
2. Ensure the simulation is enabled.
3. **Reset:** Toggle the `Reset` pin to `1` and back to `0` to initialize the Control Unit state counter.
4. **Input:** Provide data via the `Din` pin.
5. **Clock:** Enable the `Clock` to step through the cycles manually, or enable "Auto-Tick" to watch the CPU run.

## Pinout Definitions

* **Din (x8):** 8-bit Data Input (for loading instructions or immediate values).
* **Run:** Enable signal for the Control Unit.
* **Reset:** Resets the internal cycle counter to 0.
* **Clock:** System clock input.
* **Bus (x8):** 8-bit output for monitoring the current state of the main data bus.

## Collaborators

- mehmedaltug  
  Designed and implemented the main CPU circuit, including the datapath and core components.

- Orcun_ysr  
  Designed the Control Unit architecture, including state sequencing and control signal logic.

- ChestnutRisenKamehameha  
  Implemented the Control Unit logic and assisted with state machine behavior.


