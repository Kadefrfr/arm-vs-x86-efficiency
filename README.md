# Energy Efficiency of Containerized Applications on Low-Power ARM and x86 Architectures

## 🧠 Research Question
**How do low-power ARM and x86 architectures of comparable performance classes differ in energy efficiency, thermal scaling, and container runtime overhead when executing heterogeneous workloads?**

---

## 📘 Overview
This project investigates the **energy efficiency, thermal behavior, and performance scaling** of containerized workloads running on two low-power computing platforms:
- **ARM:** Raspberry Pi 5 (Cortex-A76, 8 GB)
- **x86:** AMD Athlon 3000G (Zen 1, 8 GB DDR4)

Both systems will run identical Linux environments and container runtimes (Docker or Podman).  
The results will help quantify performance-per-watt tradeoffs between **ARM-based edge devices** and **x86-based microservers**.

---

## 🎯 Goals
1. Quantify **power efficiency** and **energy-per-task** between ARM and x86.  
2. Evaluate **thermal scaling** and throttling behavior under sustained workloads.  
3. Measure **container runtime overhead** between Docker and Podman.  
4. Identify which architecture provides **better performance-per-watt** for edge or small-scale systems.  

---

## 🧱 Hardware Setup

| Platform | CPU | Architecture | RAM | Storage | OS | Cooling |
|-----------|-----|---------------|------|----------|----|----------|
| **ARM** | Raspberry Pi 5 | Cortex-A76 (4c @ 2.4 GHz) | 8 GB LPDDR4X | NVMe M.2 SSD via PCIe adapter | Arch Linux ARM / Ubuntu Server 22.04 | Active Fan |
| **x86** | AMD Athlon 3000G | Zen 1 (2c 4t @ 3.5 GHz) | 8 GB DDR4-3200 | NVMe M.2 SSD | Arch Linux x86_64 / Ubuntu Server 22.04 | Stock Cooler |

Both systems will use identical services, power-logging intervals, and benchmarking scripts to maintain parity.

---

## ⚙️ Software Environment
- **Operating Systems:** Arch Linux / Ubuntu Server 22.04 (minimal install)  
- **Container Runtimes:** Docker CE / Podman  
- **Benchmark Tools:**  
  - `sysbench` (CPU + memory tests)  
  - `stress-ng` (load control)  
  - `hyperfine` (timed task benchmarking)  
  - `bzip2` / `xz` for I/O workloads  
  - `lm-sensors` / `/sys/class/thermal` for temperature data  
- **Logging & Analysis:**  
  - Python 3 (pandas + matplotlib + psutil)  
  - Inline wattmeter or smart-plug energy meter  

---

## 🔬 Methodology

### 1. Workload Categories
| Type | Example Task | Tool |
|------|---------------|------|
| **CPU-bound** | Prime generation, SHA-256 hashing | `sysbench cpu`, `openssl speed` |
| **Memory-bound** | Matrix sorting, large array processing | `sysbench memory` |
| **I/O-bound** | File compression / decompression | `bzip2`, `xz` |
| **Mixed / Real-world** | Local web-server load test | `nginx`, `ab` (Apache Benchmark) |

### 2. Measurement Variables
- **Power Draw (W)**
- **Energy Used (J or Wh)**
- **Average CPU Temp (°C)**
- **Execution Time (s)**
- **Performance per Watt (ops/W)**

### 3. Controlled Variables
- Ambient room temperature  
- OS kernel version  
- Identical workloads and input sizes  
- 25 %, 75 %, 100 % load levels  
- CPU governor modes (Performance, Powersave)

---

## 📊 Planned Analysis
- Plot **Power vs Performance** for each workload and architecture.  
- Compare **Performance-per-Watt** across CPU-, memory-, and I/O-bound tests.  
- Analyze **thermal scaling curves** under sustained load.  
- Compare **Docker vs Podman overhead** on each architecture.  
- Generate summary tables and visualizations for publication.

---

## 🧾 Data Collection
All measurements will be logged in `data/` as CSV or JSON.

**Example Directory:**
