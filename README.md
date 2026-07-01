# 📡 Custom ESP32 Microcontroller Core PCB Design Project

Welcome to the official repository for the **Custom ESP32 System Breakout Hardware** project. This repository contains the complete programmatic schematic architectures, optimal 2-layer routing layouts, and fabrication-ready source files engineered entirely within the KiCad design suite.

This design focuses on optimizing power-rail decoupling loops for high-frequency RF applications, providing accessible interface headers for peripheral integration, and stabilizing programming pathways.

---

## 📐 1. Technical System Architecture

The hardware layout systematically segments power domains, USB transceiver configurations, and the core wireless MCU footprint to eliminate trace interference and parasitic noise loops:

### 🧠 Core Wireless Processor Node (`esp-32.kicad_sch`)
* **Module Core:** Features an **ESP32 WROOM Series** surface-mount processing module incorporating dual-core processing power and integrated Wi-Fi/Bluetooth capabilities.
* **Thermal Management:** Optimized using a dense matrix of twelve **0.2 mm thermal stitching vias** embedded directly inside the main central ground pad (`Pad 41`) to transfer module heat to the bottom ground plane.
* **Pin Configuration:** All active GPIO and system interface boundaries are routed symmetrically out to external pin headers for straightforward probing and instrumentation.

### 🔌 USB Telemetry & Serial Communications Array
* **Interface Bridge:** Implements a rugged hardware connection utilizing a specialized 16-pin USB Type-C receptacle interface (`J1`).
* **Signal Integrity:** USB differential pairs ($D+$ and $D-$) are tightly routed with specific trace geometry to prevent data cross-talk during rapid code flashing and debugging streams.

### ⚡ Power Management & Multi-Stage Decoupling
* **LDO Step-Down Topology:** Incorporates an **LM1117-5.0 Low-Dropout Linear Regulator** (`U2`) converting external incoming $V_{BUS}$ power cleanly down to system supply rails.
* **Filtering Network:** Employs a robust decoupling capacitor arrangement combining high-frequency $0.1\mu\text{F}$ surface-mount bypass capacitors right at the power input pins with larger bulk smoothing capacitors ($1\mu\text{F}$ and high-capacitance targets) to prevent supply voltage dips during transient RF current spikes.

---

## 🛠️ 2. PCB Layout & Manufacturing Disciplines

The board transitions from complex multi-layer configurations down to a highly optimized, cost-efficient **2-Layer PCB Architecture** satisfying precise industrial manufacturing constraints:

1. **Top Layer (`F.Cu`):** Handles primary component landings, high-speed signal routing traces, and localized power distribution tracks.
2. **Bottom Layer (`B.Cu`):** Serving as a continuous, low-impedance solid Ground Plane (`GND`) to significantly reduce electromagnetic emissions and secure return current paths.

* **⚙️ Design Constraints Cleared:** The board setup file is tuned to a high-density standard with a minimum global trace/pad clearance of **0.15 mm** and an ultra-fine **0.2 mm minimum hole / via drill limit** to handle small component pitches perfectly.
* **🎨 Silkscreen & Layout Visuals:** Clear, detailed layer mapping for text indicators to ensure easy component identification during manual assembly.

---

## 📋 3. Project Bill of Materials (BOM)

| Designator | Component Quantity | Component Value | Package Footprint | Purpose / Function |
| :--- | :---: | :--- | :--- | :--- |
| **U1** | 1 | ESP32 Module | Custom QFN-style SMD | Primary Dual-Core Wi-Fi/BT MCU Core |
| **U2** | 1 | LM1117-5.0 | SOT-223 / Equivalent | Main Low-Dropout Voltage Regulator |
| **J1** | 1 | USB_C_Receptacle_16P | USB4105-xx-A_16P_Horizontal | Main Power Input & Telemetry Interface |
| **SW1, SW2** | 2 | SW_Push | Tactile Switch 2-Pin | Flash Enable and System Master Reset |
| **C3** | 1 | 1uF / Chosen Value | C_1206_3216Metric | Input Voltage Bulk Filter Capacitor |
| **C5** | 1 | Chosen Filter Value | C_0805_2012Metric | Output Power Line Smoothing Filter |
| **C6** | 1 | Decoupling Value | C_1210_3225Metric | High-Frequency Bypass Filter Passive |
| **R3** | 1 | Current Limiter | R_0805_2012Metric | System Pull-up/Pull-down Configuration |

---

## 📂 4. Repository File Directory
```text
├── esp-32.kicad_pro    # Master project parameters tracking file links and layer limits
├── esp-32.kicad_sch    # Complete electrical circuit schematics and net labels
├── esp-32.kicad_pcb    # Completed physical 2-layer trace routing layout file
├── .gitignore          # Automatically ignores background autosaves and backup zip files
└── README.md           # This comprehensive documentation and specifications file
