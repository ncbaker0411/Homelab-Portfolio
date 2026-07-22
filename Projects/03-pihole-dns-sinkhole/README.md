# 🎯 Project 03: Pi-hole Centralized DNS Filtering & Active Directory Integration

## 📌 Executive Summary
This project covers the deployment and network integration of **Pi-hole** running on a physical Raspberry Pi 3 B+ node. The primary objective was to establish a network-wide DNS sinkhole to block malicious domains, ad networks, and unwanted telemetry at the DNS layer. 

The installation was specifically configured to work alongside **Active Directory DNS** on Windows Server, enabling conditional forwarding to ensure seamless internal domain resolution (`.local` records) without compromising privacy or network-wide filtering.

---

## 🛠️ Network Architecture & DNS Resolution Flow

To avoid breaking local Active Directory authentication while maintaining ad/malware filtering, traffic is routed through a tiered DNS hierarchy:

[ Client Endpoint ] 
       │
       ▼ (1. Query for local or external domain)
[ Active Directory DC (10.10.10.10) ] 
       │
       ├─► Local domain query (.local) ──► Resolves internal IP directly
       │
       └─► External domain query ────────► (2. Forwarded via DNS Upstream)
                                                 │
                                                 ▼
                                     [ Pi-hole Sinkhole (10.10.10.15) ]
                                                 │
                                                 ├─► Domain in Blocklist? ──► Returns 0.0.0.0
                                                 │
                                                 └─► Clean Domain? ─────────► (3. Upstream Resolver e.g. 1.1.1.1)

---

##⚙️ Key Implementation & Configuration Steps
1. Pi-hole Base Installation & Network Configuration
Installed Raspberry Pi OS Lite on the Raspberry Pi 3 B+ node.
Configured a static IP address for the Pi-hole host to prevent management IP drift.
Deployed Pi-hole via automated script and configured the administrative web console:
curl -sSL [https://install.pi-hole.net](https://install.pi-hole.net) | bash
2. Active Directory Integration & Conditional Forwarding
Upstream Forwarder on AD DC: Configured Windows Server DNS (DC01) to use the Pi-hole IP (10.10.10.15) as its primary forwarder for all external root queries.
Conditional Forwarding on Pi-hole: Enabled Conditional Forwarding under Settings -> DNS -> Conditional Forwarding:
Local Network: 10.10.10.0/24
Domain Name: ShieldCorp.local
IP of DC: 10.10.10.10
Result: Hostnames in the Pi-hole query log display active Active Directory computer names instead of raw IP addresses.
3. Blocklist Management & Custom DNS Records
Ingested consolidated threat intelligence lists (e.g., StevenBlack blocklist) covering ad trackers, telemetry endpoints, and known phishing domains.
Configured local DNS records (Custom DNS -> Local DNS Records) to assign human-readable domain shortcuts to internal lab services (e.g., proxmox.lab, wazuh.lab).

---

##📊 Verification & Telemetry Testing
To confirm that domain sinkholing and conditional forwarding are working as intended:
Test 1: Testing Blocked Domain Resolution (nslookup)
Ran nslookup against a known test domain from a domain-joined client (WKSTN01):
nslookup doubleclick.net
Expected Result: Addresses returned as 0.0.0.0 or 127.0.0.1 (sinkholed by Pi-hole).
Test 2: Internal Domain Name ResolutionRan nslookup against an internal domain controller from WKSTN01:
nslookup dc01.ShieldCorp.local
Expected Result: Resolves directly to 10.10.10.10 via Active Directory DNS.

---

##💡 Lessons Learned & Technical Challenges
Issue: Infinite DNS loops occurred when Pi-hole forwarded queries to AD DC while AD DC simultaneously forwarded all queries to Pi-hole.
Resolution: Configured AD DC as the primary DNS server for all DHCP clients, setting Pi-hole purely as the upstream forwarder from the DC, eliminating the loop while keeping local .local queries on the DC.
Key Takeaway: Dual-DNS environments require strict parent-child routing boundaries to avoid query recursion loops and resolution bottlenecks.

---

##📁 Included Artifacts in this Directory
File Name  Description
pihole-dashboard.png  Screenshot of the Pi-hole web dashboard showing blocked queries and total domains on blocklists.
dns-lookup-test.txt  Terminal log of nslookup commands verifying blocked domains returning 0.0.0.0.
pihole-teleporter.tar.gz  Sanitized Pi-hole configuration export file containing custom blocklists and setup.
