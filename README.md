# ⏱️ Digital Clock in Verilog

This project implements a **synchronous digital clock** using Verilog Hardware Description Language (HDL). It counts **seconds**, **minutes**, and **hours** using modular counters (`mod_60_counter` and `mod_24_counter`) and cascades them through conditional enables.

---

## 📁 Files Included

- `digi_clk.v` – Top-level module that integrates seconds, minutes, and hours
- `mod_60_counter.v` – Parameterized counter that counts from 0 to 59
- `mod_24_counter.v` – Parameterized counter that counts from 0 to 23

---

## 🧠 Module: `digi_clk`

### 📥 Inputs:
| Signal | Width | Description        |
|--------|-------|--------------------|
| `i_clk` | 1     | Clock input        |
| `i_rst` | 1     | Active-high reset  |
| `i_en`  | 1     | Global enable      |

### 📤 Outputs:
| Signal | Width | Description     |
|--------|-------|-----------------|
| `o_sec` | 6     | Seconds (0–59)  |
| `o_min` | 6     | Minutes (0–59)  |
| `o_hr`  | 5     | Hours (0–23)    |

---

## 🔄 Internal Working

1. **Seconds Counter**  
   - Uses `mod_60_counter`, enabled by `i_en`
   - Output: `o_sec[5:0]`

2. **Minutes Counter Enable Logic**  
   - Minute increments when seconds = 59  
   - Detected using:
     ```verilog
     min_en = o_sec[0] & o_sec[1] & ~o_sec[2] & o_sec[3] & o_sec[4] & o_sec[5];
     ```

3. **Minutes Counter**  
   - Uses `mod_60_counter`, enabled by `min_en`

4. **Hours Counter Enable Logic**  
   - Hour increments when seconds = 59 and minutes = 59  
   - Detected using:
     ```verilog
     hr_en = min_en & o_min[0] & o_min[1] & ~o_min[2] & o_min[3] & o_min[4] & o_min[5];
     ```

5. **Hours Counter**  
   - Uses `mod_24_counter`, enabled by `hr_en`

---

## 🧪 Simulation/Testbench

You can test the `digi_clk` module by applying a clock, reset, and enable signal, then observe:
- `o_sec` increments every clock cycle (if `i_en` is held high)
- `o_min` increments after 60 seconds
- `o_hr` increments after 60 minutes

> You can simulate this using tools like ModelSim, Vivado, or EDA Playground.

---

## 🛠️ Tools Used

- Verilog HDL
- Simulation: Vivado
- Optional Synthesis: Xilinx

---

## 📌 To-Do / Extensions

- Add 12-hour format with AM/PM toggle
- Add display driver modules (7-segment / LCD / VGA)
- Debounce logic for external `i_en` or manual increment
- FPGA implementation using onboard LEDs or displays

---

## 📝 License

This project is open-source and free to use for academic or personal purposes.

---

## 🙋 Author

**Anita Sahoo**  
[GitHub Profile](https://github.com/AnitaSahoo2002)

---

# DIGITAL-CLOCK
