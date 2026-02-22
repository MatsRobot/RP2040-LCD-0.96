# 📟 RP2040-LCD-0.96: Modular MicroPython Implementation

**RP2040-LCD-0.96** is a professional-grade library framework for the integrated Waveshare 0.96" display board. This repository provides a **Modular Driver Architecture**, moving away from factory "all-in-one" scripts to establish a scalable environment for real-time robotic telemetry.

---

<table width="100%">
  <tr>
    <td width="60%" align="left" valign="middle">
      <h2>🚀 Engineering Objective: Native Integration</h2>
    </td>
    <td width="40%" align="center" valign="middle">
      <img src="https://github.com/user-attachments/assets/c3657bc8-787d-4498-a4cc-5451ca208107" alt="RP2040-LCD-0.96 IPS LCD Telemetry Test" width="250" style="border-radius: 8px;" />
    </td>
  </tr>
  <tr>
    <td colspan="2">
      <p>
        The RP2040-LCD-0.96 is a compact, high-density development board, but factory support is often locked into monolithic CircuitPython scripts. For robotics applications requiring low-level hardware control, this introduces unnecessary overhead.
      </p>
      <p>
        I have engineered this framework to bridge the gap: providing a stable <b>MicroPython UF2</b> environment and a <b>decoupled ST7735 driver</b>. This allows the RP2040 to act as a high-speed telemetry node, utilizing hardware SPI to drive the 160x80 IPS panel with precision and REPL accessibility.
      </p>
    </td>
  </tr>
</table>

---

## ✨ Key Technical Features

* **MicroPython Native Implementation:** Optimized for the standard Pico ecosystem, facilitating shared codebases across robotics hardware.
* **Modular Driver Stack:** Display initialization (MADCTL, COLMOD) is isolated from application logic, allowing for clean `import` architectures.
* **Hardware SPI Optimization:** Leverages the RP2040's native SPI peripherals to maximize bus frequency for 65K color rendering.
* **BOOTSEL Recovery Workflow:** Specific protocols for wiping factory demo-loops and restoring serial control via Thonny.
* **RGB565 Asset Compatibility:** Fully compatible with 16-bit color mapping for high-contrast telemetry displays.

## 🛠️ Hardware Stack & Specs

* **MCU:** Raspberry Pi Pico (RP2040 Dual-core Cortex M0+).
* **Display:** 0.96-inch IPS LCD, 160×80 resolution (ST7735).
* **Clock Frequency:** Standard 133MHz (Overclockable for high-FPS rendering).
* **Validated Firmware:** `pico_micropython_20210121.uf2` for guaranteed LCD clock stability.

---

## 🔌 System Logic & Deployment

### Recovering Serial Access
Out-of-the-box, these boards often execute a non-interruptible loop. This repository provides the tools to perform a **forced Flash Wipe**:
1. Enter **BOOTSEL** mode.
2. Flash the custom MicroPython UF2.
3. Establish 115200 baud REPL communication.

### Modular Register Mapping
Instead of baking registers into your `main.py`, the driver logic is handled by:
1. **The Core Module:** Manages the SPI bus and ST7735 command set.
2. **The Telemetry Script:** Inherits the driver class, focusing purely on data visualization and sensor input.

---

## 📐 Repository Structure

| Folder / File | Technical Description |
| :--- | :--- |
| **`/modules`** | Decoupled display drivers (ST7735 logic). |
| **`/examples`** | SPI bus verification and geometric rendering sweeps. |
| **`/firmware`** | Verified MicroPython UF2 binaries for display stability. |
| **`WS_0-96_160x80_MIN.py`** | Lightweight register initialization for rapid prototyping. |
| **`graphicstest.py`** | Full RGB565 stress-test for visual debugging. |

---

## ⚡ Quick Start

1. **Firmware Deployment:** Drop the included `.uf2` into the RP2040 mass-storage drive.
2. **Filesystem Setup:** Upload the `/modules` folder to the board's root directory.
3. **Execution:** Run `MIN.py` to verify the SPI handshaking and display panel initialization.

---

<small>© 2026 MatsRobot | Licensed under the [MIT License](https://github.com/MatsRobot/matsrobot.github.io/blob/main/LICENSE)</small>
