# 🖥️ Project 01: Multi-Node Proxmox VE Cluster & Storage Integration

## 📌 Executive Summary
This project details the setup, hardware allocation, and virtual networking of a 3-node **Proxmox Virtual Environment (VE)** cluster paired with a dedicated Network Attached Storage (NAS) node. The primary goal was to establish a resilient, high-density compute foundation to isolate security workloads, Active Directory infrastructure, and offensive testing environments across physical hardware nodes.

---

## 🛠️ Cluster Hardware Architecture & Node Roles

The cluster consists of three physical **Dell OptiPlex 7090 Ultra** nodes managed under a unified Proxmox datacenter interface, alongside a dedicated NAS host:

| Host / Node | Physical Specs | Dedicated Role | Guest VMs / Containers |
| :--- | :--- | :--- | :--- |
| **PVE Node 1** | Dell OptiPlex 7090 | Defensive Monitoring / SIEM | **Wazuh Manager** (Ubuntu Server / Elastic Indexer Stack) |
| **PVE Node 2** | Dell OptiPlex 7090 | Enterprise Target Infrastructure | **Windows Server 2022** (Domain Controller) & **Windows 10 Pro** |
| **PVE Node 3** | Dell OptiPlex 7090 | Offensive Security & Auditing | **Kali Linux** (Attack Simulations) |
| **NAS Host** | Dedicated PC (6x 500GB RAID 5) | Shared Storage & Log Archives | OpenMediaVault / TrueNAS (NFS & SMB Shares) |

---

## ⚙️ Key Implementation & Configuration Steps

### 1. Cluster Creation & Quorum Setup
1. Installed **Proxmox VE** on each individual Dell OptiPlex node.
2. Created a unified cluster on Node 1 via the Proxmox Datacenter web console:
   ```bash
   pvecm create proxmox-cluster
