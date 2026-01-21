# Homelab-Portfolio
This homelab is a self-hosted infrastructure environment designed to build and demonstrate practical skills in systems administration, networking, storage, and virtualization. It functions as both a learning platform and a production-style environment, emphasizing reliability, documentation, and iterative improvement rather than one-off experiments.

The idea of starting this lab was to give myself a way of applying the skills that I learned from my collection of CompTIA certifications. I also wanted to use this as a proof of knowledge and skill for possible employeers.

Skills practiced by certification:
* CompTIA A+
  * Foundational IT Operations
* CompTIA Network+
  * Network Architecture, DNS, Switching, Traffic Flow, Availablity & Redundancy
* CompTIA Security+
  * Monitoring, Detection, Least Privilege, Service Isolation, Risk Management

## The Hardware
This project was created using mostly recycled hardware from multiple sources to reduce e-waste and to breath new life into hardware that would otherwise be trash.

### Parts List
| Part | Description | Notes |
| --- | --- | --- |
| Netgear GS308 | Unmanaged Switch | This will be used to push network across the lab. I plan on replacing this with a managed switch once I can aquire one. |
| Dell Optiplex 7060 Micro | Primary Pc | Loaded with Ubuntu this will be used to run Kurbenetes, a SIEM, and other programs needed in the function of this lab. |
| 1.Raspberry Pi 3 B+ | PiHole | This will be used for centralized DNS filterning to remove Ads from my network. |
| 2.Raspberry Pi 3 B+ | Pi Cluster | This will be one of the three Raspberry Pi's in my cluster used for resource sharing and running services across my network. |
| 3.Raspberry Pi 3 B+ | Pi Cluster | This will be one of the three Raspberry Pi's in my cluster used for resource sharing and running services across my network. |
| 4.Raspberry Pi 3 B+ | Pi Cluster | This will be one of the three Raspberry Pi's in my cluster used for resource sharing and running services across my network. |
| 6x 500GB Seagate HDD | NAS Mass Sotrage | This will be used in a RAID 5 configuration and will store data from across my home and will be used to store logs for my SIEM |

### Network Diagram
![Network Diagram](https://github.com/ncbaker0411/Homelab-Portfolio/blob/fc5436a4ef5d7c18476187ed2f924b0c9d3cdcbb/Assets/Network%20Diagram.jpg)
