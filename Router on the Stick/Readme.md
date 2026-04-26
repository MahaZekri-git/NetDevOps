🌐 Project: Router on the Stick
#
Layer 2 Isolation & Layer 3 Routing
#
This lab explores a standard hierarchical network architecture, focusing on the logical separation of server resources through VLAN configuration.

--------------------------------------------------------------------------------
🏗️ The Infrastructure
#
The topology utilizes a structured approach to connect and manage network endpoints:
🔘 The Gateway (R1): A central Router providing the path for inter-VLAN communication
.
🔁 The Distribution (S1): A Switch managing the physical connections and logical VLAN assignments
.
🖥️ The Endpoints: Three Servers (SRV1, SRV2, SRV3) distributed across different network segments
.

--------------------------------------------------------------------------------
🎨 Logical Segmentation
The network is partitioned into two distinct virtual segments to manage traffic flow:
🏷️ VLAN 10
Host: 🖥️ SRV1
Access Port: Connected to interface E0/0 on the switch
.
🏷️ VLAN 20
Hosts: 🖥️ SRV2 & 🖥️ SRV3
Access Ports: Connected to interfaces E0/1 and E0/2 respectively
.

--------------------------------------------------------------------------------
🔌 Physical Connection Map
This table details the cabling and interface assignments for the entire topology:
Device
Local Port
Remote Device
Remote Port
Purpose
🔘 R1
E0/0
🔁 S1
E0/3
Trunk Link
🔁 S1
E0/0
🖥️ SRV1
Ens2
VLAN 10 Access
🔁 S1
E0/1
🖥️ SRV2
Ens2
VLAN 20 Access
🔁 S1
E0/2
🖥️ SRV3
Ens2
VLAN 20 Access

--------------------------------------------------------------------------------
🧪 Deployment Goals
VLAN Implementation: Assign specific switch ports to their respective VLANs (10 or 20)
.
Inter-VLAN Routing: Configure the 🔘 Router to enable communication between 🖥️ SRV1 and the servers in the other segment
.
Local Connectivity: Verify that 🖥️ SRV2 and 🖥️ SRV3 can communicate directly within the same segment

<img width="847" height="618" alt="image" src="https://github.com/user-attachments/assets/c97ca84f-91fc-435b-ae45-ce6e7da5c33f" />


