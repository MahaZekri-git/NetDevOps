# Enterprise Edge NAT/PAT Implementation Lab (EVE-NG)

## 📌 Project Overview
This lab demonstrates the implementation of **Dynamic NAT with Overload (PAT)** on an Enterprise Edge router. The objective is to allow multiple internal hosts with private IPv4 addresses (192.168.2.0/24) to access external resources on a public network (192.168.1.0/24) using a single public-facing IP address.

## 🗺️ Topology Diagram
The lab is built in **EVE-NG** and follows a standard edge-to-core architecture:

*   **Internal LAN (Private):** Subnet `192.168.2.0/24` containing PC1, PC2, PC3, a Windows Server, and an internal router (R1).
*   **CDR (Core/Distribution):** The central switching/routing node for the LAN.
*   **EDG (Edge Router):** The NAT boundary device between the private LAN and the external network.
*   **Net (External/Public):** Subnet `192.168.1.0/24` where the Linux host resides.

## 📊 IP Addressing Table

| Device | Interface | IP Address | Description |
| :--- | :--- | :--- | :--- |
| **PC1** | eth0 | 192.168.2.1/24 | Internal Host |
| **PC2** | eth0 | 192.168.2.2/24 | Internal Host |
| **PC3** | eth0 | 192.168.2.3/24 | Internal Host |
| **Winserver**| e0 | 192.168.2.10/24 | Internal Enterprise Server |
| **CDR** | e0/0 | 192.168.2.20/24 | Core Node |
| **EDG** | fa1/0 | 192.168.2.254/24| NAT "Inside" Interface |
| **EDG** | fa0/0 | 192.168.1.100/24| NAT "Outside" Interface (Public)|
| **Linux** | e0 | 192.168.1.x/24 | External Target Host |

## 🚀 Lab Objectives
1.  **Interface Designation:** Define the "inside" and "outside" NAT domains on the EDG router.
2.  **Traffic Identification:** Create an Access Control List (ACL) to identify the internal private traffic eligible for translation.
3.  **PAT Configuration:** Configure NAT Overload (PAT) on the external interface to map the entire LAN to the public IP `192.168.1.100`.
4.  **End-to-End Verification:** Confirm that internal hosts can reach the Linux host and verify translation entries in the NAT table.

## 🛠️ Configuration Highlights (EDG Router)

### 1. Interface NAT Roles
Assigning roles to the physical interfaces.
```ios
interface FastEthernet1/0
 ip nat inside

interface FastEthernet0/0
 ip nat outside
2. NAT ACL & Translation Rule
Defining which traffic to translate and applying the PAT rule.
access-list 1 permit 192.168.2.0 0.0.0.255
ip nat inside source list 1 interface FastEthernet0/0 overload

<img width="1041" height="582" alt="image" src="https://github.com/user-attachments/assets/7978a153-fd9a-443d-a902-3829cbfaa0f6" />
