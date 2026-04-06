# Homelab-Portfolio

This homelab is a self-hosted infrastructure environment designed to build and demonstrate practical skills in systems administration, networking, virtualization, and cybersecurity monitoring. It functions as both a learning platform and a production-style environment, with a focus on reliability, documentation, and iterative improvement rather than one-off experiments.

The lab is designed to simulate a small-scale enterprise environment, incorporating centralized services, containerized workloads, network-level filtering, and log monitoring. This allows for hands-on experience with real-world scenarios such as service deployment, network troubleshooting, system hardening, and security event detection.

The primary goal of this project is to apply and expand upon the knowledge gained through my CompTIA certifications in a practical, continuously evolving environment. It also serves as a professional portfolio to demonstrate technical capability, problem-solving, and documentation skills to potential employers.

---

## Skills Practiced by Certification

### CompTIA A+
- Foundational IT Operations
- Hardware and system troubleshooting
- OS installation and configuration

### CompTIA Network+
- Network architecture and design
- DNS and network services
- Switching, traffic flow, and segmentation
- Availability and redundancy concepts

### CompTIA Security+
- Monitoring and detection
- Least privilege and access control
- Service isolation
- Risk management and security best practices

---

## The Hardware

This project is built primarily using repurposed and recycled hardware to reduce e-waste while creating a functional and scalable lab environment. This approach reflects real-world constraints where maximizing available resources is often necessary.

### Parts List

| Part | Description | Notes |
| --- | --- | --- |
| TP-Link TL-SG108 | Unmanaged Switch | Provides basic network connectivity across the lab. Planned upgrade to a managed switch for VLAN and traffic segmentation. |
| Dell Optiplex 7060 Micro | Virtualization Host | Planned to run a hypervisor (Proxmox) for managing virtual machines and containerized services such as SIEM and infrastructure tools. |
| Raspberry Pi 3 B+ (x1) | DNS Filtering Node | Currently running Pi-hole for centralized DNS filtering. Planned migration to a containerized deployment for improved management. |
| Raspberry Pi 3 B+ (x3) | Kubernetes Cluster | Forms a lightweight cluster for experimenting with container orchestration and distributed workloads. |
| 6x 500GB SSD | NAS Storage | Configured for RAID 5 to provide centralized storage for backups, shared data, and log ingestion for monitoring systems. |

---

## Design Philosophy

- **Centralization:** Core services are consolidated to improve manageability and visibility
- **Scalability:** Infrastructure is designed to grow (additional nodes, services, and segmentation)
- **Resilience:** Redundancy and fault tolerance are considered where possible
- **Security:** Emphasis on monitoring, logging, and service isolation
- **Documentation:** Every major change and deployment is documented to reflect real-world IT practices

---

## Planned / In-Progress Improvements

- Migration to Proxmox-based virtualization cluster
- Containerization of services using Docker
- SIEM deployment (Wazuh) for centralized logging and monitoring
- Expanded automation and scripting for deployment and maintenance
- Update hardware to Managed Switch to work on VLAN configuation
- Network segmentation via managed switch and VLAN configuration

---

## Network Diagram

