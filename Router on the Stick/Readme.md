🌐 Project: Router on the Stick <br>
Layer 2 Isolation & Layer 3 Routing<br>
This lab explores a standard hierarchical network architecture, focusing on the logical separation of server resources through VLAN configuration.

--------------------------------------------------------------------------------
🏗️ The Infrastructure<br>

The topology utilizes a structured approach to connect and manage network endpoints:<br>
🔘 The Gateway (R1): A central Router providing the path for inter-VLAN communication<br>

🔁 The Distribution (S1): A Switch managing the physical connections and logical VLAN assignments<br>

🖥️ The Endpoints: Three Servers (SRV1, SRV2, SRV3) distributed across different network segments<br>


--------------------------------------------------------------------------------
🎨 Logical Segmentation<br>
The network is partitioned into two distinct virtual segments to manage traffic flow:<br>
🏷️ VLAN 10<br>
Host: 🖥️ SRV1<br>
Access Port: Connected to interface E0/0 on the switch<br>

🏷️ VLAN 20<br>
Hosts: 🖥️ SRV2 & 🖥️ SRV3<br>
Access Ports: Connected to interfaces E0/1 and E0/2 respectively<br>


--------------------------------------------------------------------------------
🔌 Physical Connection Map<br>
This table details the cabling and interface assignments for the entire topology:<br>

| Device | Local Port | Remote Device | Remote Port | Purpose |
|--------|------------|---------------|-------------|---------|
| 🔘R1     | E0/0       | 🔁S1            | E0/3        | Trunk Link |
| 🔁S1     | E0/0       | 🖥️SRV1          | ens2        | VLAN 10 Access |
| 🔁S1     | E0/1       | 🖥️SRV2          | ens2        | VLAN 20 Access |
| 🔁S1     | E0/2       | 🖥️SRV3          | ens2        | VLAN 20 Access |
--------------------------------------------------------------------------------
🧪 Deployment Goals<br>
VLAN Implementation: Assign specific switch ports to their respective VLANs (10 or 20)<br>

Inter-VLAN Routing: Configure the 🔘 Router to enable communication between 🖥️ SRV1 and the servers in the other segment<br>

Local Connectivity: Verify that 🖥️ SRV2 and 🖥️ SRV3 can communicate directly within the same segment<br>


<img width="746" height="786" alt="image" src="https://github.com/user-attachments/assets/d7b3ed57-a634-4db4-87b8-c9e5af63fa23" />


