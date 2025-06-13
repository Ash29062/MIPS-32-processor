# MIPS32 Pipeline Processor Simulation in Verilog

This repository provides a complete simulation and behavioral modeling of a pipelined MIPS32 processor using Verilog. It is based on lecture material from Prof. Indranil Sengupta, Department of Computer Science and Engineering.

---

## 📘 Overview

This project involves:
- Understanding MIPS32 instruction set and encoding
- Modeling a pipelined processor with Verilog
- Writing test benches to verify correct instruction execution
- Running example programs such as arithmetic operations and factorial computation

---

## 🧠 Instruction Set Architecture (ISA)

### MIPS32 Architecture Highlights
- **32-bit RISC architecture**
- **Registers**: 32 General Purpose Registers (GPRs), R0–R31
  - R0 is hardwired to 0
  - PC (Program Counter) is a special-purpose 32-bit register
- **No flags** (carry, zero, sign)
- **Memory Access**: Only through load/store
- **Memory**: Word-addressable, 32-bit word size

### Instruction Types
- **R-type**: Register-Register ALU operations (e.g., `ADD R1,R2,R3`)
- **I-type**: Immediate and memory instructions (e.g., `LW R2,124(R8)`)
- **J-type**: Jump instructions (`J Label`)

---

## 🧾 Instruction Encoding

### R-Type Encoding
```
| opcode | rs  | rt  | rd  | shamt | funct |
| 6 bits | 5b  | 5b  | 5b  | 5 bits| 6 bits|
```

### I-Type Encoding
```
| opcode | rs  | rt  | immediate (16 bits) |
```

### J-Type Encoding
```
| opcode | address (26 bits) |
```

---

## 🛠️ Pipeline Design

### Instruction Execution Stages
1. **IF** (Instruction Fetch)
2. **ID** (Instruction Decode / Register Fetch)
3. **EX** (Execute / Address Calculation)
4. **MEM** (Memory Access / Branch Completion)
5. **WB** (Write Back)

### Pipeline Latches
- `IF_ID`, `ID_EX`, `EX_MEM`, `MEM_WB` used to hold stage-specific data

### Special Flags
- `HALTED`: Set after `HLT` instruction is executed
- `TAKEN_BRANCH`: Controls flush behavior during branch execution

---

## 💻 Verilog Implementation

Located in `pipe_MIPS32` module:
- Register Bank: 32 registers of 32-bit each
- Memory: 1024 words
- Instructions coded using behavioral constructs
- Conditional branching, arithmetic, and memory instructions supported

---

## 🧪 Testbenches

### Test Case 1: Add Three Numbers
**Registers**: R1 = 10, R2 = 20, R3 = 25  
**Operation**: R4 = R1 + R2; R5 = R4 + R3  
**Expected Output**:
```
R4 = 30
R5 = 55
```

### Test Case 2: Memory Read/Write
**Memory[120]** = 85  
**Operation**: Add 45 → store to Memory[121]  
**Expected Output**:
```
Mem[120] = 85
Mem[121] = 130
```

### Test Case 3: Factorial
**Memory[200]** = N  
**Compute**: N! and store result in Memory[198]  
**Example Output for N=7**:
```
Mem[200] = 7
Mem[198] = 5040
```

---

## ⚠️ Notes

- **Data Hazards**: Avoided manually using dummy instructions
- **Behavioral Modeling**: Not synthesizable as-is; meant for simulation
- **Future Work**: Hazard detection, forwarding, and structural modeling can be added

---

## 📚 Topics Covered

- Verilog basics, dataflow, procedural blocks
- FSM modeling
- Pipeline implementation
- Writing testbenches
- Pipelined data path for MIPS32 subset

---

## ❗ Limitations

- No support for:
  - Synthesis
  - Structural hardware design
  - Advanced hazard resolution techniques

---

## 👨‍🏫 Credits

**Instructor**: Prof. Indranil Sengupta  
**Course**: Hardware Modeling Using Verilog  
**Institution**: Department of Computer Science and Engineering

---

## 📝 License

This project is for academic use only. Please credit the original instructor when using materials.
