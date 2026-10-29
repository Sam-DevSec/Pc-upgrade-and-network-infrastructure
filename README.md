# 🏗️ Host Platform Upgrade, Hardware Maintenance, and InfoSec Lab Network Architecture

A comprehensive hands-on project covering core hardware engineering, platform modernization, system stress-testing, and isolated network infrastructure design for a security testing homelab.

## 🛠️ Phase 1: Hardware Upgrade, Maintenance & Thermal Validation
*   **Platform Modernization:** Completely dismantled the legacy system; installed and integrated a new CPU and motherboard from scratch.
*   **Deep Hardware Maintenance (TO):** 
    *   Performed full dust blow-out of the chassis and cooling radiators.
    *   Applied fresh, high-performance thermal paste to the CPU.
    *   Serviced the GPU: replaced the thermal fluid on the crystal die and fully renewed thermal pads on the VRAM modules and VRM power phases.
*   **Stress-Testing & Thermal Validation:** Verified cooling efficiency and ensured zero thermal throttling post-assembly by running stress tests under peak load using specialized hardware monitoring utilities.
*   **Memory Subsystem Optimization (BIOS):** Activated XMP/DOCP profiles in BIOS, successfully overclocking the RAM frequency from stock **2133 MHz to the rated 3200 MHz** to eliminate memory bottlenecks during multi-VM utilization.

## 💾 Host OS Deployment & Migration
*   **Clean OS Installation:** Prepared a clean bootable flash drive using Rufus and performed a fresh Windows installation on the new hardware platform to mitigate any driver conflicts from the legacy chipset.
*   **Data Migration:** Successfully migrated environment profiles, workspaces, and VirtualBox VM configuration files from the legacy system drive.

## 🌐 Lab Network Architecture & Infrastructure Design (VirtualBox)
Designed an isolated virtual network topology built around strict security perimeter principles:
1.  **Network Segmentation:** Isolated all core lab machines (`Main_server`, `Kali Linux`, `Wazuh SIEM`) from the external physical network by grouping them into a custom backend **NAT Network (NatNetwork)** driven by a local DHCP server.
2.  **Engineering Management Access (SSH Port Forwarding):** Eliminating the overhead of heavy graphical VM windows, configured seamless port forwarding via the host loopback interface (`127.0.0.1`), enabling direct terminal management from the Windows host:
    *   `127.0.0.1:2222` -> Main_server Management (Ubuntu)
    *   `127.0.0.1:2223` -> Kali Linux Management
    *   `127.0.0.1:2224` -> Wazuh SIEM Server Management
3.  **Service Automation & Persistence:** Switched Linux netplan interfaces to automated IP leasing, enabled persistence for the SSH daemon (`systemctl enable ssh`) across all nodes, and validated active network socket availability across hard reboots (`sudo reboot`).
