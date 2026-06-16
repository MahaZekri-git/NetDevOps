# Site-to-Site GRE Tunnel with EIGRP Dynamic Routing (EVE-NG)

## 📌 Project Overview
This project demonstrates the implementation of a **Site-to-Site GRE (Generic Routing Encapsulation) Tunnel** overlaying a simulated Service Provider underlay. By utilizing **EIGRP** as the dynamic routing protocol, this lab provides automated route propagation between two isolated LANs, ensuring seamless end-to-end connectivity.

## 🗺️ Topology Diagram
The lab is built in **EVE-NG** and follows this architecture:

*   **Site A:** Border Router (R1) and local endpoint (PC1).
*   **ISP Core:** A central router providing public IPv4 reachability.
*   **Site B:** Border Router (R2) and local endpoint (PC2).
*   **Overlay:** A GRE Tunnel (172.16.1.0/24) spanning the ISP.
*   ## 📊 IP Addressing Table

| Device | Interface | IP Address | Description |
| :--- | :--- | :--- | :--- |
| **R1** | e0/0 | 1.1.1.1/24 | WAN Public Interface (Site A) |
| **R1** | e0/1 | 192.168.1.254/24 | LAN Gateway (Site A) |
| **R1** | Tunnel0 | 172.16.1.1/24 | GRE Tunnel Interface |
| **PC1** | eth0 | 192.168.1.1/24 | End Host (Site A) |
| **ISP** | e0/0 | 1.1.1.2/24 | Connection to Site A |
| **ISP** | e0/1 | 2.2.2.1/24 | Connection to Site B |
| **R2** | e0/0 | 2.2.2.2/24 | WAN Public Interface (Site B) |
| **R2** | e0/1 | 192.168.2.254/24 | LAN Gateway (Site B) |
| **R2** | Tunnel0 | 172.16.1.2/24 | GRE Tunnel Interface |
| **PC2** | eth0 | 192.168.2.2/24 | End Host (Site B) |
## 🚀 Lab Objectives
1.  **Underlay Reachability:** Configure the ISP and Site routers to ensure `1.1.1.1` can ping `2.2.2.2`.
2.  **GRE Tunnel Establishment:** Configure a logical Tunnel interface using public IPs as sources/destinations.
3.  **Dynamic Routing (EIGRP):** Deploy EIGRP AS 100 to exchange LAN routes (`192.168.1.0/24` and `192.168.2.0/24`) over the tunnel.
4.  **MTU Optimization:** Adjust the TCP MSS to 1360 to account for the GRE encapsulation overhead.
 
<img width="1091" height="507" alt="Capture d’écran 2026-06-16 234048" src="https://github.com/user-attachments/assets/c2043392-2e0a-41c1-9bb3-588b60de307b" />

