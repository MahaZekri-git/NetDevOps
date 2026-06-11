# EVE-NG Lab: Enterprise Network Redundancy and High Availability (FHRP)

## 📌 Project Overview
This lab environment, built in EVE-NG, demonstrates a resilient enterprise network architecture focusing on gateway redundancy. It simulates a scenario where end-user devices (PC1 and PC2) maintain uninterrupted connectivity to an external network (Net) even in the event of a primary gateway failure.

## 🏗️ Topology Details
The architecture follows a classic hierarchical design:
*   **Edge/Gateway Layer:** Two multilayer switches/routers, **Sw1** and **Sw2**, acting as redundant exit points to the external network [1].
    *   **Sw1 IP:** `192.168.2.1`
    *   **Sw2 IP:** `192.168.2.2`
    *   **Virtual IP (VIP):** `192.168.2.254` (Configured via HSRP or VRRP)
*   **Distribution/Access Layer:** A central switch (**SW**) aggregating traffic from end-points.
    *   Connections: Sw1 `Gi0/0` to SW `e0/3` and Sw2 `Gi0/0` to SW `e0/2`.
*   **End-Point Layer:** 
    *   **PC1:** `192.168.2.10` connected to SW `e0/1`.
    *   **PC2:** `192.168.2.20` connected to SW `e0/0`.
*   **External Network:** A "Net" node representing the ISP/Internet, connected via `Gi0/1` on both Sw1 and Sw2.

## 🚀 Implemented Technologies
*   **FHRP (First Hop Redundancy Protocol):** Implementing HSRP to provide a single virtual gateway (`.254`) for all hosts.
*   **VLAN Management:** Segmentation of traffic at the Access Layer (SW).
*   **Interface Tracking:** Advanced HSRP configuration to monitor the health of the `Gi0/1` uplink to the Net.
*   **Spanning Tree Protocol (STP):** Optimization to ensure the Root Bridge aligns with the Active HSRP gateway.

## 🛠️ How to Use
1. Import the `.unl` file into your EVE-NG instance.
2. Ensure you have the **Cisco IOSvL2** and **vPC** images.
3. Start all nodes and verify connectivity by pinging from PC1 to the external "Net" IP.
2. Practical Scenario: "The Transparent Uplink Failure"
The Setup: You have configured Sw1 as the "Active" gateway with a priority of 110 and Sw2 as "Standby" with a priority of 100
. Both PCs are configured with their default gateway set to the Virtual IP: 192.168.2.254
.
The Incident: The upstream link from Sw1 to the Net (Gi0/1) experiences a hardware failure
. However, the link between Sw1 and the internal switch (SW) remains active.
## The Solution:
Configure Object Tracking: On Sw1, configure HSRP to track the status of interface Gi0/1.
Priority Decrement: If Gi0/1 goes down, Sw1's HSRP priority should automatically decrement by 20 (dropping from 110 to 90).
Active/Standby Handover: Because Sw1's priority is now lower than Sw2's (100), Sw2 must immediately transition to the "Active" state to handle all traffic directed to the .254 gateway
.
## Verification:
Run a traceroute from PC1 to the Net. You should see the traffic path switch from 192.168.2.1 to 192.168.2.2 transparently, without the PC ever losing connection to its gateway.
##
<img width="720" height="772" alt="image" src="https://github.com/user-attachments/assets/e8579425-09d8-4b22-98d9-88fbc591e19e" />



