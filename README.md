# m4yestik Ubuntu Server Setup

This repository contains the ultimate optimization and setup script for deploying a state-of-the-art Local AI Agentic Server (Targeted for June 2026 standards).

## Target Hardware
- **CPU:** AMD Ryzen Threadripper PRO 7965WX (or similar HEDT processor)
- **GPU:** Dual NVIDIA GeForce RTX 5090 (Blackwell Architecture)
- **RAM:** 128GB DDR5 ECC
- **Storage:** NVMe PCIe Gen 5

## Features
This script performs a deep, end-game optimization of Ubuntu Server, ensuring zero bottlenecks and 100% hardware utilization for Massive LLM Inference (e.g., Qwen-Coder 72B) and Agentic Coding via Aider.

1. **Idempotent Execution:** Safe to run multiple times without duplicating configurations or appending redundant lines.
2. **Fail-Safe Mechanism:** Halts immediately on critical errors (`set -e`) but handles non-critical failures gracefully (`|| true`).
3. **Hardware-Level Tuning:**
   - Enables NUMA interleaving for Threadripper CPU architecture.
   - Configures IOMMU Pass-Through and PCIe ACS override to allow Dual-GPU Peer-to-Peer (P2P) transfers.
   - Sets CPU governor to `performance` and disables CPU security mitigations (e.g., Spectre/Meltdown) for maximum raw inference speed.
   - Bypasses OS I/O scheduling for Gen 5 NVMe SSDs to reduce latency.
4. **Memory and Network Optimization:**
   - Enables Transparent Huge Pages (THP) for faster tensor allocations.
   - Overrides Out-Of-Memory (OOM) killer to protect the Ollama service.
   - Increases global `ulimit` (fs.file-max) to 1,048,576 to allow AI agents to parse massive enterprise codebases without limits.
5. **Automated On-Demand Cleanup:**
   - Installs a systemd service that automatically purges orphaned packages, old systemd logs (>2GB), and stopped Podman containers safely during the system shutdown sequence.
6. **AI Toolchain Installation:**
   - Installs NVIDIA proprietary drivers and CUDA toolkit.
   - Installs Ollama (Inference engine) injected with Dual-GPU distribution configs and bound to 0.0.0.0 for Local Area Network (LAN) API access.
   - Installs Podman (Daemonless containers for Microservices architecture).

## Usage

1. Clone this repository:
   ```bash
   git clone git@github.com:xm4yestiK/m4yestik_ubuntu_server_setup.git
   cd m4yestik_ubuntu_server_setup
   ```
2. Make the script executable:
   ```bash
   chmod +x run.sh
   ```
3. Run the script as root/sudo:
   ```bash
   sudo ./run.sh
   ```
4. Reboot the server to apply GRUB, Kernel, and Systemd changes:
   ```bash
   sudo reboot
   ```

## Pre-requisites
- Ubuntu Server 24.04 LTS (or newer).
- BIOS configurations: Ensure "Above 4G Decoding" and "Re-Size BAR" are explicitly enabled in your motherboard settings.
