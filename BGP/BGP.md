# Multi-Site Enterprise Redundancy: BGP Multi-Homing & HSRP Lab

## 📌 Project Overview
This project simulates a high-availability enterprise network architecture across multiple Autonomous Systems (AS). It demonstrates advanced routing and redundancy techniques, including **BGP Multi-Homing** for resilient internet/WAN connectivity and **HSRP (Hot Standby Router Protocol)** for internal gateway redundancy.

## 🗺️ Topology Diagram
The lab environment is structured across five distinct Autonomous Systems to simulate real-world service provider interactions:

*   **AS 65011 (Customer Site A):** Dual-homed edge with Routers **C1A** and **C1B** providing redundancy via **HSRP** to the local LAN (192.0.2.0/24).
*   **AS 65001, 65002, 65003 (Service Providers):** A multi-provider core (SP1A, SP1B, SP2, SP3) facilitating diverse paths between sites.
*   **AS 65012 (Customer Site B):** A remote site connected via redundant links to the provider core.

## 📊 Key IP & Routing Data

| Segment | AS Number | Networks / VIPs | Key Nodes |
| :--- | :--- | :--- | :--- |
| **Site A LAN** | 65011 | 192.0.2.0/24 (HSRP VIP: .1) | C1A, C1B, PC1 |
| **Provider Core 1**| 65001 | 172.16.4.0/30, 198.51.100.0/30 | SP1A, SP1B |
| **Provider Core 2**| 65002 | 172.16.1.0/30, 209.165.201.0/30| SP2 |
| **Provider Core 3**| 65003 | 172.16.2.0/30 | SP3 |
| **Site B LAN** | 65012 | 203.0.113.0/24 | C2, PC2 |

## 🚀 Lab Objectives
1.  **First-Hop Redundancy:** Implement **HSRP** on C1A and C1B to ensure PC1 has a continuous default gateway even if one edge router fails.
2.  **External BGP (eBGP):** Configure eBGP peering between the Customer AS (65011, 65012) and the Service Provider ASs to exchange reachability information.
3.  **Path Manipulation:** Use BGP attributes (such as AS-Path Prepending or Local Preference) to influence traffic entry and exit points across the redundant WAN links.
4.  **Full Connectivity:** Ensure end-to-end communication between **PC1** (Site A) and **PC2** (Site B) through the multi-provider mesh.

## 🛠️ Configuration Highlights

### 1. HSRP Gateway Redundancy (Site A)
Providing a virtual IP (.1) for the internal LAN hosts.
```ios
! R1 (C1A)
interface Gi0/1
 ip address 192.0.2.2 255.255.255.0
 standby 1 ip 192.0.2.1
 standby 1 priority 110
 standby 1 preempt
2. eBGP Multi-Homing (Site A to SPs)
Establishing peering with multiple providers for redundancy.
! R1 (C1A)
router bgp 65011
 neighbor 198.51.100.2 remote-as 65001
 neighbor 10.0.0.2 remote-as 65011 (iBGP to C1B)
 network 192.0.2.0 mask 255.255.255.0
✅ Verification & Troubleshooting
HSRP Status: show standby brief on C1A/C1B to verify Active/Standby states.
BGP Adjacencies: show ip bgp summary to ensure all eBGP and iBGP sessions are "Established".
Best Path Selection: show ip bgp to examine the BGP table and verify which provider path is preferred for specific prefixes.
Failover Test: Shut down the primary link on C1A and verify that traffic reroutes through C1B via BGP convergence.
<img width="1737" height="842" alt="Capture d’écran 2026-07-04 132836" src="https://github.com/user-attachments/assets/4e29504d-cf10-4091-9484-635b65a093e5" />


