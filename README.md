# Hardware Prototyping & Custom Interconnect Extension of ARM Cortex-M3 SoC

A customized, fully synthesizable System-on-Chip (SoC) architecture built around an **ARM Cortex-M3 32-bit RISC processor core** coupled with an IoT compute subsystem. This project executes an architectural migration from an Intel platform over to a **Xilinx Artix-7 FPGA**, resolving prior peripheral density constraints by expanding the system's underlying bus matrix infrastructure.

---

## 📊 Physical FPGA Implementation & Performance Metrics

The complete hardware netlist was mapped, routed, and structurally verified on a physical **Arty A7-100T FPGA platform**. The design performance metrics extracted directly from Xilinx Vivado reporting windows are detailed below:

### 1. Power Analysis Breakdown (Vivado Implemented Netlist)
*   **Total On-Chip Power:** 0.368W
*   **Dynamic Circuit Power:** 0.265 (72%)
*   **Device Static Power:** 0.103 (28%)

### 2. Device Resource Utilization (Artix-7 XC7A100T)
*   **Slice Look-Up Tables (LUTs):** 25,397 / 63,400 (**40.06% Utilization**)
    *   *LUT as Logic:* 24,482
    *   *LUT as Memory:* 915
    *   *LUT as Distributed RAM:* 152
    *   *LUT as Shift Register:* 763
*   **Slice Registers (Flip-Flops):** 14,071 / 126,800 (**11.10% Utilization**)
*   **F7 Muxes:** 145
*   **F8 Muxes:** 19

---

## ⚡ Hardware Customization & Interconnect Engineering

The fundamental engineering modification overcomes legacy platform limitations by redesigning the bus infrastructure to drastically expand peripheral capacity:

### 1. Matrix Bus Expansion (18-Port Topology)
*   **Bus Upgrade:** Modified the Advanced High-Performance Bus (AMBA AHB-Lite) and Advanced Peripheral Bus (APB) matrices to increase total accessible channels to **18 master and slave ports** (upgraded from an 8-port baseline).
*   **Decoder Resolution:** Developed a 32-bit address decoding logic block for the AHB matrix. The APB decoder utilizes partial bit-toggling boundaries to cleanly isolate incoming CPU peripheral requests.

### 2. Tightly-Coupled Memory & Storage Expansion
*   **SRAM Subsystem:** Redesigned the memory layout into a dedicated block-RAM instantiation, expanding total SRAM capacity up to **128KB**.
*   **Primary Flash:** Expanded non-volatile code memory space from **256KB up to 512KB** to accommodate complex firmware stacks.

### 3. FPGA Clock Tree Restructuring
*   Replaced the standard design's input clock network with an on-chip **Mixed-Mode Clock Manager (MMCM)**. The MMCM locks onto the Arty-100T physical onboard crystal oscillator to synthesize highly stable, customized internal clock lines for independent system blocks.

---

## 🛠️ Toolchain Workflow & Execution

The hardware-software co-design flow bypasses traditional simulation limitations by running hardware-in-the-loop emulation:

1.  **Software Compilation:** Embedded C-code applications are written and compiled inside **Keil uVision5** to produce tightly optimized binary image files.
2.  **RTL Simulation:** Hardware Verilog descriptions and custom interconnect layers are structurally verified using **Xilinx Vivado** simulation engines.
3.  **Physical Deployment:** Vivado synthesizes the unified netlist and generates a hardware `.bit` configuration file. This file is flashed onto the Arty-100T board over JTAG, running firmware immediately upon a hardware CPU reset condition.

---

## 📂 Repository Layout & Project Artifacts

All project blueprints, physical verification artifacts, and implementation toolchain reports are hosted directly within the root directory for direct access:

*   `Cortex-M3 Design with IOT subsystem.jpg` — Baseline architectural block schematic showing the integrated processor and bus infrastructure.
*   `Modified Interconnect Platform.jpg` — Hardware routing layout showcasing the custom address decoding logic and the extended 18-port matrix expansion.
*   `lut_report.jpg` — Target board resource utilization log confirming precise slice and Look-Up Table metrics on the Artix-7 FPGA.
*   `power_report.jpg` — Vivado implementation dynamic and device-static power analysis layout (0.368W total on-chip footprint).
*   `Screenoutput.jpg` — Hardware-in-the-loop terminal capture verifying reliable runtime execution and memory code loading.
*   `README.md` — Main technical specification and portfolio landing page.

---

## 📜 Citation & Publication Details
This SoC architecture and physical verification pipeline are published and detailed in the following paper:
*   **Trisha Maddanna**, Vaishnavi U, Gahan A V, *"Hardware Implementation of ARM Cortex-M3 Design on FPGA,"* **International Educational Applied Scientific Research Journal (IEASRJ)**, Vol. 9, No. 12, 2024.
