# 🖥️ 4-Bit CPU — CircuitVerse

A simple 4-bit processor built from scratch in [CircuitVerse](https://circuitverse.org), featuring an ALU, register file, instruction memory, data memory, and control unit.

---

## 📐 Architecture

```
┌─────────────────────────────────────────────────────┐
│                    4-bit CPU                        │
│                                                     │
│  ┌──────┐    ┌──────────────┐    ┌───────────────┐  │
│  │  PC  │───▶│  Instruction │───▶│ Control Unit  │  │
│  │      │    │    Memory    │    │               │  │
│  └──────┘    └──────────────┘    └───────┬───────┘  │
│     ▲                                    │          │
│     │              ┌─────────────────────▼──────┐   │
│     │              │   Register File (R0–R3)    │   │
│     │              └──────────┬─────────────────┘   │
│     │                        │                      │
│     │              ┌─────────▼──────────┐           │
│     │              │        ALU         │           │
│     │              │  (ADD, AND, OR...) │           │
│     │              └──────────┬─────────┘           │
│     │                        │                      │
│     │              ┌─────────▼──────────┐           │
│     └──────────────│   Data Memory      │           │
│                    │   (16×4b RAM)      │           │
│                    └────────────────────┘           │
└─────────────────────────────────────────────────────┘
```

---

## 🧩 Components

| Component | Description |
|---|---|
| **PC (Program Counter)** | 4-bit register holding the address of the current instruction |
| **Instruction Memory** | ROM storing the program instructions, or a manual 8-bit input for testing |
| **Register File** | 4 general-purpose registers: R0, R1, R2, R3 (4 bits each) |
| **ALU** | 4-bit arithmetic/logic unit (ADD, AND, OR, SUB) |
| **Control Unit** | Decodes instructions and generates control signals |
| **Data Memory** | 16×4-bit RAM for reading and writing data |

---

## 📋 Instruction Set Architecture (ISA)

Instructions are **8 bits** wide, but only the lower **4 bits** are used for the opcode and operand:

```
[ 7 ]   = Reset flag — set to 1 to asynchronously reset all registers
[ 6:4 ] = Unused
[ 3:2 ] = Opcode  (2 bits)
[ 1:0 ] = Operand (destination register / address)
```

| Opcode | Instruction | Description |
|--------|-------------|-------------|
| `00`   | ALU OP      | Arithmetic/logic operation between registers |
| `01`   | STORE       | Write register value to Data Memory |
| `10`   | LOAD        | Read value from Data Memory into register |
| `11`   | JUMP        | Jump to specified address |

### Control Signals

| Signal | Function |
|--------|----------|
| `ALU_OP0` | ALU operation bit 0 |
| `ALU_OP1` | ALU operation bit 1 |
| `RegWrite` | Enable write to register file |
| `MemWrite` | Enable write to data memory |
| `MemRead`  | Enable read from data memory |
| `Jump`     | Enable PC jump |

---

## 🛠️ How to Run

1. Open [CircuitVerse](https://circuitverse.org)
2. Import the file `cpu_4bit.cv` via **File → Import**
3. Load instructions into the ROM **or** connect a manual 8-bit input for quick testing
4. Press **Play** or enable the clock
5. Watch register and memory values update each clock cycle

### Resetting the CPU

- **Via ROM (bit 7):** Set bit 7 of any instruction to `1` — this triggers an asynchronous reset on all registers instantly during program execution
- **Manually:** Use the dedicated Reset button connected to the Asynchronous Reset pin of all flip-flops in the register file

---

## 📁 Project Structure

```
cpu_4bit/
├── cpu_4bit.cv    # Main CircuitVerse project file
└── README.md      # Documentation
```

---

## 🔧 Example ROM Program

```
Address | Value | Instruction
--------|-------|------------
0x0     | 0001  | ALU: R1 ← R0 op R1
0x1     | 0100  | STORE R0 → mem[0]
0x2     | 1000  | LOAD  R0 ← mem[0]
0x3     | 1100  | JUMP  → 0x0
```

---

## ⚙️ Technical Details

- **Data width:** 4 bits
- **Address width:** 4 bits (16 addressable locations)
- **Register type:** Synchronous D Flip-Flop with Enable
- **Clock:** Synchronous, positive edge-triggered
- **Instruction memory:** ROM (read-only)
- **Data memory:** 16×4-bit RAM
- **Simulator:** CircuitVerse (browser-based)

---

## 👤 Author
Fagadeanu Rares-Stefan
Built as a computer architecture learning project.

---

## 📜 License

MIT — free for educational use.
