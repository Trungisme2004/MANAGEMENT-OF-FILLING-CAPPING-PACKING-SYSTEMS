# 🍾 Automated Bottle Filling & Capping System

![PLC](https://img.shields.io/badge/PLC-Siemens_S7_1200-00B0F0)
![Software](https://img.shields.io/badge/Software-TIA_Portal_v18-FF6600)
![Status](https://img.shields.io/badge/Status-Phase_1_Complete-00AA00)
![HMI](https://img.shields.io/badge/HMI-Integrated-9900CC)

## 📌 Project Overview

This project implements an **automated bottle filling and capping line** using a Siemens S7-1200 PLC. The system handles bottles through five coordinated stations: grabbing, liquid filling, cap dispensing, capping, and ejection.

**Real-world application:** Small to medium-scale beverage or pharmaceutical bottling lines where consistency and cycle time matter.

## 🎯 Problem Solved

Manual bottle filling is:
- ❌ Inconsistent (varying fill levels)
- ❌ Slow (operator-dependent)
- ❌ Prone to contamination
- ❌ Difficult to track quality

**This solution:** Fully automated sequence from bottle arrival to finished product ejection.

## ⚙️ System Components

| Station | Actuators | Sensors | Function |
|---------|-----------|---------|----------|
| **Grabber** | M2, M3, M4, M5 (4 motors) | PS4 (bottle present), PSRight, PSLeft | Secures bottle during filling |
| **Belt** | Motor 1 (FWD/REV) | LS1 (home), LS2 (end) | Moves bottle between stations |
| **Liquid Filling** | Cylinder 3, Pump 1 | LS6 (home), LS7 (end) | Lowers nozzle, fills for 5 sec |
| **Cap Dispenser** | Motor M7 | PS1, PS2 (cap detection) | Feeds exactly one cap |
| **Capping** | Cylinder 2, Motor M6 | LS3 (home), LS4 (end), PS3 (bottle arrival) | Lowers, tightens cap for 5 sec |
| **Ejection** | Cylinder 1 | LS5 (home return) | Pushes finished bottle out |

## 📊 I/O Count

| Type | Count |
|------|-------|
| Digital Inputs | 14 |
| Digital Outputs | 12 |
| **Total** | **26 I/O points** |

## 🔄 Sequence of Operations
Step 1: Bottle arrives → PS4 detects → Belt stops
Step 2: Grabber closes (M2-M5) → PSRight & PSLeft confirm
Step 3: Cylinder 3 lowers nozzle → Pump runs 5 sec → Cylinder 3 raises
Step 4: Belt runs → Bottle moves to capping station → PS3 detects → Belt stops
Step 5: M7 runs → PS1 & PS2 detect cap → M7 stops (cap hangs, bottle grabs it)
Step 6: Cylinder 2 lowers capper → M6 runs 5 sec → Cylinder 2 raises
Step 7: Belt runs to end position → LS2 detects → Belt stops
Step 8: Cylinder 1 pushes bottle out → Returns to LS5
Step 9: Cycle repeats from Step 1

text

## ✅ What Works (Phase 1)

- [x] Bottle detection via PS4
- [x] 4-motor grabber with dual proximity verification
- [x] Timed liquid filling (5 seconds)
- [x] Single-cap dispensing with dual-sensor confirmation
- [x] Belt positioning (home/end limits)
- [x] Timed capping (5 seconds)
- [x] Automatic ejection with home return
- [x] Emergency stop (cuts all outputs immediately)
- [x] Full cycle repeat

## 🔜 Future Improvements (Phase 2)

| Improvement | Why It Matters |
|-------------|----------------|
| Grabber closure timeout | Prevents cycle stall if bottle misaligned |
| Cap jam detection (PS1) | Prevents dry-feeding empty caps |
| Pump dry-run protection | Prevents pump damage |
| Signal tower (Green/Yellow/Red) | Visual status for operators |
| Fault logging to HMI | Easier troubleshooting |
| Production counter | Track bottles/hour |

> *"Phase 1 proved the nominal sequence works. Phase 2 adds industrial robustness."*

## 🛠️ Tech Stack

| Category | Technology |
|----------|------------|
| PLC | Siemens S7-1200 |
| Software | TIA Portal v18 |
| Programming Language | Ladder Logic |
| HMI | Integrated TIA Portal HMI |
| Emergency Stop | Hardware input cuts all outputs |

## 🚀 How to Use This Repository
## 📚 Documentation

- **[Full Ladder Logic PDF](03_Documentation/Ladder_Logic.pdf)** – Complete export from TIA Portal v18 with comments
- [I/O List](03_Documentation/I_O%20list%20for%20bottle%20filling%20conveyor%20-%20Sheet1.csv)
- [Sequence of Operations](03_Documentation/Sequence_of_Operations.md)
- [Fault Matrix](03_Documentation/Fault_Matrix.md)
- [HMI Design Description](03_Documentation/HMI_Design_Description.md)

## 📈 Performance Metrics

| Metric | Value |
|--------|-------|
| Cycle time per bottle | ~30 seconds |
| Fill time | 5 seconds (fixed) |
| Cap tightening time | 5 seconds (fixed) |
| Bottles per hour (theoretical) | 120 |

## 👨‍💻 Author

**Afnan Jawad**
- GitHub: [@afnanjawad](https://github.com/afnanjawad)
- LinkedIn: [linkedin.com/in/afnanjawad](https://linkedin.com/in/afnanjawad)

## 📝 License

This project is open for portfolio and learning purposes.

---

*Built with Siemens S7-1200, TIA Portal v18, and Ladder Logic.*
