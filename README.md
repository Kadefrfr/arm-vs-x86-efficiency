# arm-vs-x86-efficiency
# Comparative Analysis of Energy Efficiency and Runtime Overhead between ARM and x86 Low-Power Architectures Using Containerized Workloads

## 🧠 Research Question
**How do low-power ARM and x86 architectures of comparable memory and performance classes differ in energy efficiency, thermal scaling, and container runtime overhead when executing heterogeneous workloads using Docker and Podman?**

---

## 📘 Overview
This project evaluates the **energy efficiency**, **thermal behavior**, and **runtime overhead** of containerized workloads running on two low-power computing platforms:

| Platform | CPU | Architecture | RAM | OS | Notes |
|-----------|-----|--------------|-----|----|-------|
| **ARM System** | Broadcom BCM2712 (Raspberry Pi 5) | ARM Cortex-A76 (4 cores @ 2.4 GHz) | 4 GB LPDDR4X | Arch Linux ARM | Active fan, NVMe via PCIe HAT |
| **x86 System** | Intel Alder Lake-N N95 Mini PC | x86 64-bit (4 cores @ 3.4 GHz Turbo) | 4 GB DDR4 | Arch Linux x86 | Stock cooler |

Both devices will run identical Linux kernels, system configurations, and container workloads.  
The project aims to quantify performance-per-watt efficiency, thermal scaling, and container runtime impact on different architectures.

---

## 🎯 Goals
1. Measure **energy efficiency** and **performance per watt** under real workloads.  
2. Compare **Docker** and **Podman** container overhead.  
3. Evaluate **thermal scaling** and throttling behavior under sustained load.  
4. Develop and publish **heterogeneous workload programs** written in C / Python to run consistently on both platforms.  
5. Provide open-source scripts and raw data for reproducibility.

---

## 🧱 Hardware Setup
- **Raspberry Pi 5 (4 GB, 128 GB SSD)**  
  - Boot via NVMe (PCIe x1 Gen 2 adapter)  
  - Actively cooled  
  - Powered through USB-C PD (5 V 5 A)

- **Intel N95 Mini PC (4 GB RAM, 256 GB SSD)**  
  - Integrated Ethernet + NVMe  
  - Passive/stock cooling  
  - Standard 12 V DC input  

Both systems will connect to the same network and be monitored using identical power-measurement tools.

---

## ⚙️ Software Environment
- **Operating System:**  Arch Linux (ARM & x86_64)  
- **Container Runtimes:** Docker CE v27 and Podman v5  
- **Benchmark Tools:**  
  - `sysbench`, `stress-ng`, `hyperfine`  
  - `bzip2` / `xz` for I/O tasks  
  - `lm-sensors` / `/sys/class/thermal` for temperature
- **Languages for Custom Workloads:** C and Python 3  
  - `gcc`, `make`, `python3`, `numpy`, `psutil`  

---

## 🔬 Methodology

### 1️⃣ Workload Types
| Type | Description | Example Implementation |
|------|--------------|------------------------|
| **CPU-bound** | Pure compute tasks such as prime generation, hashing, or Fibonacci sequences. | `sysbench cpu` / custom C program (`prime.c`) |
| **Memory-bound** | Matrix operations, large-array transformations, or data sorting. | Python (`numpy_sort.py`) |
| **I/O-bound** | File compression, decompression, and block copying. | `bzip2`, `xz`, `dd` |
| **Mixed / Network** | Lightweight web-server or REST API load tests. | Python Flask + `ab` benchmark |

### 2️⃣ Measurement Variables
- Power draw (W)  
- Energy used (J or Wh)  
- Average CPU temperature (°C)  
- Task completion time (s)  
- Performance-per-Watt (ops/W)  
- Container runtime overhead (%)

### 3️⃣ Controlled Conditions
- Same ambient room temperature  
- Identical Linux kernel version  
- Same test input sizes  
- Three load levels: 25 %, 75 %, 100 %  
- CPU governor modes: `performance` and `powersave`  

---

## 📊 Planned Analysis
- Compare **average power usage vs. task completion time** for each workload.  
- Chart **thermal scaling curves** to show efficiency loss over time.  
- Calculate **Docker vs. Podman overhead** by comparing native vs. containerized runs.  
- Determine **energy cost per operation** (joules per task).  
- Generate graphs using Python (`matplotlib`, `pandas`).  

---

## 📂 Repository Structure
