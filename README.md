
# Cisco-ACI-Lab 
# 🧪 **Lab – Deployment of the Cisco ACI Simulator on VMware Workstation & Integration of the First Nodes**

## 📘 **Overview**

In this lab, I describe the steps taken to **deploy the Cisco ACI Simulator** on **VMware Workstation**, initialize the APIC, and integrate the first **Leaf nodes** into the ACI fabric.

This project helped me strengthen my understanding of **Cisco ACI (Application Centric Infrastructure)**, a modern SDN architecture used in datacenter environments.

---

# 🔵 **1. Introduction to Cisco ACI**

Cisco ACI is a datacenter architecture based on **Software-Defined Networking (SDN)**, enabling:

* **automation** of configurations,
* **centralization** of network control,
* **programmability** of the fabric.

### 🔧 Comparison with other SDN solutions

| Domain                  | Technology       |
| ----------------------- | ---------------- |
| WAN                     | **Cisco SD-WAN** |
| LAN                     | **Cisco DNA**    |
| Datacenter              | **Cisco ACI**    |
| Virtualization (VMware) | **VMware NSX**   |
| Arista                  | **CloudVision**  |

### 🧩 Main Components of an ACI Fabric

* **APIC (Application Policy Infrastructure Controller)** → the brain
* **Spines** → the core of the network, managing the control plane & data plane
* **Leafs** → switches connecting servers, firewalls, and endpoints
* **Fabric** → automated system thanks to Zero Touch Provisioning (ZTP)

The APIC orchestrates everything:
node discovery, policy management, fabric consistency, and global supervision.

---

# 🔵 **2. Lab Objectives**

✔️ Deploy the Cisco ACI Simulator (OVA) on VMware Workstation
✔️ Initialize and configure the first APIC
✔️ Add a first Leaf switch to the fabric
✔️ Understand the LLDP discovery process and node enrollment

---

# 🔵 **3. Environment & Prerequisites**

### 🖥️ **Hardware Used**

* VMware Workstation
* 8 vCPUs
* 32 GB RAM
* Sufficient storage for the ACI OVA (~70 GB)

### ⚙️ **Allocated Resources**

The recommended specs are higher, but I adapted them:

| Component | Recommended Resources | Allocated Resources   |
| --------- | --------------------- | --------------------- |
| APIC      | 8 CPU / 24–32 GB RAM  | **4 CPU / 16 GB RAM** |
| Leafs     | 4 CPU / 8 GB RAM      | Standard              |

### 📥 **File Used**

* **Cisco ACI Simulator OVA** (provided by Cisco DevNet)

---

# 🔵 **4. Lab Steps**

---

## **Step 1 – Deploying the ACI Simulator OVA**

1. Import the OVA into VMware Workstation
2. Adjust CPU / RAM resources
3. Resolve a blocking message related to insufficient CPU
4. Start and fully initialize the APIC VM
5. Perform the initial setup:

   * IP Address
   * Gateway
   * APIC credentials
   * Fabric Name

📌 *Despite the limited resources, the APIC successfully completed initialization.*

---

## **Step 2 – Setting Up the ACI Fabric**

### 🔍 2.1 Automatic Node Discovery (LLDP)

When the ACI Simulator starts:

* Leaf switches announce themselves using **LLDP**,
* The APIC automatically detects them,
* The fabric offers enrollment with a unique node ID.

### 🧩 2.2 Adding the First Leaf Switch

I integrated the first switch by specifying:

* **Node ID**
* **Node Name**
* **Role** (Leaf / Spine)
* **Pod Assignment**

This allowed me to visualize:

* the discovery process
* topology creation
* the node transitioning from *"In Discovery"* to *"Registered"*
* fabric consistency controlled by the APIC

---

# 🔵 **5. Results & Lessons Learned**

This lab helped me better understand:

### ✔ **The internal architecture of the ACI fabric**

Spines and Leafs communicate through an automated underlay.

### ✔ **The central role of the APIC controller**

A single interface for policies, discovery, and fabric-wide management.

### ✔ **The Zero Touch Provisioning (ZTP) process**

Nodes configure themselves automatically as soon as they join the fabric.

### ✔ **Datacenter automation with ACI**

ACI simplifies network operations by reducing manual configuration.

---

# 🔵 **6. Features I Will Add Later (Roadmap)**

* Deployment of **EPGs**, **Bridge Domains**, **VRFs**
* Configuration of ACI Contracts
* Integration of a hypervisor (VMware ESXi)
* Automation using REST API & Python
* Adding Spine switches to the fabric

---

# 🎯 **Conclusion**

This lab gave me a complete first immersion into Cisco ACI, from installation to the integration of the first Leaf switch.
It helped me reinforce my understanding of:

* the logic of the fabric
* automatic discovery
* the importance of the APIC
* and automation at the heart of ACI architecture
