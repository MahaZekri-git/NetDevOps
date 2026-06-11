# EVE-NG Lab: Multi-Protocol EtherChannel & Hierarchical Redundancy

## 📌 Project Overview
This laboratory environment explores advanced link aggregation techniques in a hierarchical Cisco-based network. The goal is to implement and compare various Port-Channel protocols (LACP, PAgP, and Static) across both Layer 2 and Layer 3 boundaries to ensure high bandwidth, redundancy, and loop-free topology.

## 🏗️ Topology Architecture
The design utilizes a redundant four-switch mesh consisting of:
*   **Distribution Layer (DS-1 & DS-2):** Serving as the core of the lab, managing inter-switch traffic and Layer 3 routing [1].
*   **Access Layer (AS-1 & AS-2):** Managing end-point connectivity and redundant uplinks [1].

## ⚙️ Configuration Matrix
The lab implements several distinct EtherChannel types:
*   **Inter-Distribution Link:** Layer 2 LACP between DS-1 and DS-2 [1].
*   **Distribution-to-Access (Layer 3):**
    *   **LACP (Po2):** Between DS-1 (`.1`) and AS-2 (`.2`) on the `192.168.2.0/24` subnet [1].
    *   **PAgP (Po3):** Between DS-2 (`.1`) and AS-2 (`.2`) on the `192.168.3.0/24` subnet [1].
    *   **Static/On (Po30):** Between DS-2 (`.1`) and AS-1 (`.2`) on the `192.168.4.0/24` subnet [1].
*   **Distribution-to-Access (Layer 2):** PAgP (Po10) between DS-1 and AS-1 [1].
*   **Access-to-Access (Layer 2):** Static Port-Channel (Po1) between AS-1 and AS-2 [1].

## 🚀 Learning Objectives
1. **Protocol Interoperability:** Mastering the differences between Cisco-proprietary PAgP and industry-standard LACP [1].
2. **L3 EtherChannel Routing:** Configuring `no switchport` interfaces for direct routed aggregation [1].
3. **STP Convergence:** Analyzing Spanning Tree behavior across redundant Layer 2 Port-Channels [1].
4. **Load Balancing:** Testing hashing algorithms across diverse physical links (Gi0/x and Gi1/x) [1].

## 🛠️ Requirements
*   **EVE-NG** (Community or Professional)
*   **Cisco IOSvL2** Image
<img width="947" height="592" alt="Capture d’écran 2026-06-11 115733" src="https://github.com/user-attachments/assets/ecf670ea-1b93-4387-9b82-71d5d2d139ce" />

  
