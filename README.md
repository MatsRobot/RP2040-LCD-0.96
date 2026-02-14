# 📟 RP2040-LCD-0.96: MicroPython Implementation

A streamlined, modular approach to driving the Waveshare RP2040-LCD-0.96 using MicroPython, moving away from monolithic scripts toward a reusable library structure.

<p align="center">
  <img width="592" src="https://github.com/user-attachments/assets/c3657bc8-787d-4498-a4cc-5451ca208107" alt="RP2040-LCD-0.96 Running Test" />
</p>

---

## 🚀 The Backstory

The RP2040-LCD-0.96 is a powerful, compact board, but finding clear documentation for it can be a challenge. Out of the box, mine arrived pre-loaded with a CircuitPython demo that effectively "locked" the virtual drive, making it difficult to interrupt the execution and load new code.

Furthermore, while the official support leans heavily toward CircuitPython, my entire ecosystem of Raspberry Pi Pico projects runs on **MicroPython**. To make this board useful for my projects, I had to bridge the gap between "working demo code" and a "functional development library."

## ✨ Key Features

* **MicroPython Native:** Fully migrated from the factory CircuitPython to a stable MicroPython environment.
* **Modular Architecture:** Unlike standard examples that bake the driver into the main script, this project separates the display logic into a dedicated module.
* **Optimized SPI Performance:** Utilizes the high-speed SPI bus of the RP2040 to drive the 160x80 color IPS display.
* **Pre-Validated Examples:** Includes verified scripts for graphics testing and minimal setups to ensure your hardware is 100% functional.

## 🛠️ Setup & Firmware

To get started, the board must be flashed with a compatible MicroPython UF2. I found that the standard Pico builds sometimes struggle with the specific LCD timings, so I utilized:

* **Firmware:** `pico_micropython_20210121.uf2` (available in the repository).
* **Interface:** SPI (Serial Peripheral Interface).
* **Resolution:** 0.96-inch IPS LCD, 160×80 pixels, 65K colorful RGB.



## 📐 How It Works

### Breaking the Loop
The first hurdle was regaining control of the board. By flashing the MicroPython UF2 via the **BOOTSEL** mode, I was able to wipe the factory demo and establish a clean REPL environment via Thonny.

### Driver Modularization
Standard examples like `pico-LCD-0.96.py` or `graphicstest.py` are often "monolithic," meaning the driver code and the application code are mixed together. 
I have restructured these into:
1. **The Driver Module:** Handles the low-level SPI commands and pixel addressing.
2. **The Project Base:** A clean boilerplate script that imports the driver, allowing you to focus on your logic rather than display registers.

### Included Working Examples
If you are just testing your hardware, I have confirmed the following scripts work perfectly with this board:
* `WS_0-96_160x80_MIN.py`: The lightest possible implementation for basic output.
* `graphicstest.py`: A comprehensive test of colors, lines, and shapes (requires `sysfont.py`).

## 📁 Repository Structure

* `/modules`: Contains the split-out display drivers.
* `/examples`: Collection of working scripts to verify screen functionality.
* `/firmware`: The specific MicroPython UF2 used for this board.

---

## 📜 License

This project is open-source. Use it to jumpstart your own RP2040 wearable or IoT monitoring projects!

---
