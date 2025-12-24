# 🧮 Low-Area 32-bit Calculator using Serial Datapath (RTL Design)

## 📌 Overview
This project implements a **32-bit calculator** supporting **Addition, Subtraction, Multiplication, and Division** using a **time-multiplexed serial datapath architecture**.  
The primary design goal is to **minimize hardware area and power consumption**, accepting **multi-cycle latency** as a trade-off.

Unlike a fully parallel ALU, this design reuses arithmetic hardware across cycles, making it suitable for **area- and power-constrained systems**.

---

## ✨ Key Features
- 32-bit arithmetic operations:
  - Addition
  - Subtraction
  - Multiplication
  - Division
- **Serial / time-multiplexed datapath** for low area
- FSM-based control with clean handshake:
  - `start`
  - `busy`
  - `done`
- Division-by-zero detection with error flag
- Fully synthesizable and implemented in Vivado
- Timing-closed after place & route

---

## 🧱 Architecture Overview

### Datapath
- **Serial Adder/Subtractor**
  - 1-bit full adder reused over 32 cycles
  - Two’s complement subtraction
- **Serial-Parallel Multiplier**
  - Shift-and-add algorithm
  - Completes in 32 cycles
- **Sequential Divider**
  - Restoring division algorithm
  - Completes in ~32 cycles
- Hardware reused across operations to reduce area

### Control
- FSM with three states:
  - `IDLE`
  - `RUN`
  - `FIN`
- Ensures only one operation runs at a time

---

## 🔁 Operation Latency

| Operation | Latency |
|---------|--------|
| ADD | 32 cycles |
| SUB | 32 cycles |
| MUL | 32 cycles |
| DIV | ~32 cycles |

---

## 📊 Resource Utilization (Post-Implementation)

Target: Xilinx FPGA (Vivado)

| Resource | Usage |
|--------|------|
| LUTs | **451** |
| Registers | **545** |
| DSPs | **0** |
| BUFG | 1 |

**Module-wise Breakdown:**
- Serial Adder/Subtractor: 140 LUTs
- Serial Multiplier: 166 LUTs
- Sequential Divider: 142 LUTs

➡️ Achieves **~3–6× area reduction** compared to a fully parallel ALU.

---

## ⏱ Timing Summary (Post-Implementation)

- **Clock Frequency:** 100 MHz
- **Setup Slack (WNS):** +3.856 ns
- **Hold Slack (WHS):** +0.015 ns
- **Timing Status:** ✅ All constraints met

Multi-cycle timing constraints were applied to serial datapaths, while FSM control paths remained single-cycle.

---

## 🔋 Power Analysis (Estimated)

- **Total On-Chip Power:** 0.245 W  
- **Dynamic Power:** ~25 mW  
- **Logic Dynamic Power:** ~2 mW  

> Note: Static power dominates on FPGA; comparison is based on **dynamic logic power**, which is significantly lower due to reduced switching activity.

---

## 📐 Design Trade-offs

| Metric | Parallel ALU | This Design |
|------|-------------|------------|
| Latency | 1 cycle | 32 cycles |
| Area | High | **Low** |
| DSP Usage | Yes | **No** |
| Max Frequency | Lower | Higher |
| Power (Dynamic) | High | **Low** |

---

## 🧪 Verification
- RTL simulation using Vivado Simulator
- Functional verification for:
  - All arithmetic operations
  - Negative subtraction results
  - Division-by-zero handling
- Timing and power verified after implementation

---

## 🛠 Tools Used
- **Language:** Verilog HDL
- **EDA Tool:** Xilinx Vivado
- **Simulation:** Vivado Simulator
- **Target:** FPGA (generic)

---

## 🚀 Applications
- Area-constrained embedded systems
- Low-power arithmetic units
- Educational RTL / VLSI projects
- Base architecture for ALU / CPU datapath design

---

## 📚 Key Takeaway
This project demonstrates how **architectural choices** (serial vs parallel) directly impact **area, power, and performance**, and how to close timing correctly for multi-cycle datapaths.

---

## 👤 Author
**RK**  
Electronics & Communication Engineering .
