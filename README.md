# 🌐 Real-World Network Design & Subnetting Project

## 📌 Project Overview

This project demonstrates the design and implementation of a small **real-world departmental network** using **Cisco Packet Tracer**.

The scenario involves connecting two departments:

* 💰 **Accounts Department**
* 🚚 **Delivery Department**

Each department requires multiple end devices, including PCs and a printer. The network is designed using **two separate subnets**, with a router providing communication between the departments.

The project also focuses on **IPv4 subnetting**, IP addressing, default gateways, network topology design, cabling, and end-to-end connectivity testing.

> 🎯 **Project Focus:** Real-world network design + IPv4 subnetting + inter-network communication

---

# 📋 Case Study

A company requires a network in Cisco Packet Tracer to connect the **Accounts** and **Delivery** departments.

### Requirements

1. 💻 Each department must contain at least **2 PCs**
2. 🔀 An appropriate number of switches and routers must be used
3. 🌐 All interfaces and end devices must have appropriate:

   * IP addresses
   * Subnet masks
   * Default gateways
4. 🔌 All devices must be connected using appropriate cables
5. 🧪 Communication between the Accounts and Delivery departments must be tested

---

# 🎯 Project Objectives

By completing this project, you will learn how to:

* 🔹 Analyze a real-world networking requirement
* 🔹 Design a suitable network topology
* 🔹 Determine the number of required subnets
* 🔹 Perform IPv4 subnetting
* 🔹 Calculate borrowed bits
* 🔹 Calculate subnet masks
* 🔹 Calculate block size
* 🔹 Identify network IDs
* 🔹 Identify valid host ranges
* 🔹 Identify broadcast addresses
* 🔹 Configure router interfaces
* 🔹 Configure end-device IP addresses
* 🔹 Configure default gateways
* 🔹 Connect devices using appropriate cables
* 🔹 Test communication within and between subnets

---

# 🏢 Network Design

The network contains two departments:

```text
                ┌─────────────────┐
                │     Router 0    │
                │                 │
                │ G0/0            │
                │ G0/1            │
                └───────┬─────────┘
                        │
              ┌─────────┴─────────┐
              │                   │
              │                   │
       ┌──────┴──────┐     ┌──────┴──────┐
       │ Accounts SW │     │ Delivery SW │
       └──────┬──────┘     └──────┬──────┘
              │                   │
        ┌─────┴─────┐       ┌─────┴─────┐
        │           │       │           │
      PC-1        PC-2     PC-3        PC-4
        │                           │
     Printer                     Printer
```

---

# 🖥️ Department Structure

## 💰 Accounts Department

* 🔀 1 Switch
* 💻 2 PCs
* 🖨️ 1 Printer
* 🌐 1 Subnet

## 🚚 Delivery Department

* 🔀 1 Switch
* 💻 2 PCs
* 🖨️ 1 Printer
* 🌐 1 Subnet

### Total Network Devices

| Device Type                   | Quantity |
| ----------------------------- | -------: |
| Router                        |        1 |
| Switches                      |        2 |
| PCs                           |        4 |
| Printers                      |        2 |
| **Total End/Network Devices** |    **9** |

---

# 🧮 IPv4 Subnetting

## Given Network

The base network provided for this project is:

```text
192.168.40.0/24
```

The case study requires **2 departments**, therefore we need:

```text
Number of Required Subnets = 2
```

---

## 1️⃣ Calculate Borrowed Bits

The subnetting formula is:

```text
2ⁿ ≥ Number of Required Subnets
```

For 2 subnets:

```text
2ⁿ ≥ 2

n = 1
```

Therefore:

```text
Borrowed Bits = 1
```

---

# 2️⃣ Calculate the New Subnet Mask

The original network is:

```text
192.168.40.0/24
```

We borrow **1 bit** from the host portion:

```text
Original:  /24
Borrowed:   1 bit

New Prefix = /25
```

### Binary Representation

```text
11111111.11111111.11111111.10000000
```

Converting to decimal:

```text
255.255.255.128
```

Therefore:

```text
Subnet Mask = 255.255.255.128
CIDR        = /25
```

---

# 3️⃣ Calculate Block Size

The block size is calculated using:

```text
256 - Subnet Mask Value
```

The interesting octet is the fourth octet:

```text
256 - 128 = 128
```

Therefore:

```text
Block Size = 128
```

This means each subnet contains **128 addresses**.

---

# 📊 Subnetting Table

| Subnet      | Network ID          | Valid Host Range                  | Broadcast ID     |
| ----------- | ------------------- | --------------------------------- | ---------------- |
| 🟢 Accounts | `192.168.40.0/25`   | `192.168.40.1 – 192.168.40.126`   | `192.168.40.127` |
| 🔵 Delivery | `192.168.40.128/25` | `192.168.40.129 – 192.168.40.254` | `192.168.40.255` |

### Important

Each `/25` subnet provides:

```text
128 total addresses
126 usable host addresses
```

Because:

```text
Network Address = 1
Broadcast Address = 1

128 - 2 = 126 usable hosts
```

---

# 🌐 Final IP Addressing Plan

## 💰 Accounts Department

Network:

```text
192.168.40.0/25
```

Router interface:

```text
G0/0
192.168.40.1/25
```

End devices:

| Device           | IP Address     | Subnet Mask       | Default Gateway |
| ---------------- | -------------- | ----------------- | --------------- |
| Accounts PC-1    | `192.168.40.2` | `255.255.255.128` | `192.168.40.1`  |
| Accounts PC-2    | `192.168.40.3` | `255.255.255.128` | `192.168.40.1`  |
| Accounts Printer | `192.168.40.4` | `255.255.255.128` | `192.168.40.1`  |

---

## 🚚 Delivery Department

Network:

```text
192.168.40.128/25
```

Router interface:

```text
G0/1
192.168.40.129/25
```

End devices:

| Device           | IP Address       | Subnet Mask       | Default Gateway  |
| ---------------- | ---------------- | ----------------- | ---------------- |
| Delivery PC-1    | `192.168.40.130` | `255.255.255.128` | `192.168.40.129` |
| Delivery PC-2    | `192.168.40.131` | `255.255.255.128` | `192.168.40.129` |
| Delivery Printer | `192.168.40.132` | `255.255.255.128` | `192.168.40.129` |

---

# 🔌 Network Cabling

The devices are connected using appropriate Ethernet connections.

### Connections

```text
Router G0/0
     ↓
Accounts Switch
     ↓
Accounts PCs + Printer
```

and:

```text
Router G0/1
     ↓
Delivery Switch
     ↓
Delivery PCs + Printer
```

For a Packet Tracer lab, **Automatic Connection** can be used to select the appropriate cable type.

---

# ⚙️ Router Configuration

## 1️⃣ Enter Privileged EXEC Mode

```bash
enable
```

## 2️⃣ Enter Global Configuration Mode

```bash
configure terminal
```

## 3️⃣ Configure G0/0 — Accounts

```bash
interface gigabitEthernet 0/0
ip address 192.168.40.1 255.255.255.128
no shutdown
exit
```

## 4️⃣ Configure G0/1 — Delivery

```bash
interface gigabitEthernet 0/1
ip address 192.168.40.129 255.255.255.128
no shutdown
exit
```

---

# 🔍 Verify Router Interfaces

Use:

```bash
show ip interface brief
```

Expected:

```text
Interface              IP-Address       Status    Protocol

GigabitEthernet0/0     192.168.40.1     up        up
GigabitEthernet0/1     192.168.40.129   up        up
```

🟢 `up/up` indicates that the interface is operational.

---

# 🖥️ Configure Accounts Devices

### Accounts PC-1

```text
IP Address:       192.168.40.2
Subnet Mask:      255.255.255.128
Default Gateway:  192.168.40.1
```

### Accounts PC-2

```text
IP Address:       192.168.40.3
Subnet Mask:      255.255.255.128
Default Gateway:  192.168.40.1
```

### Accounts Printer

```text
IP Address:       192.168.40.4
Subnet Mask:      255.255.255.128
Default Gateway:  192.168.40.1
```

---

# 🚚 Configure Delivery Devices

### Delivery PC-1

```text
IP Address:       192.168.40.130
Subnet Mask:      255.255.255.128
Default Gateway:  192.168.40.129
```

### Delivery PC-2

```text
IP Address:       192.168.40.131
Subnet Mask:      255.255.255.128
Default Gateway:  192.168.40.129
```

### Delivery Printer

```text
IP Address:       192.168.40.132
Subnet Mask:      255.255.255.128
Default Gateway:  192.168.40.129
```

---

# 🧪 Connectivity Testing

After configuring all devices, communication should be tested.

## Test 1 — Accounts PC to Accounts PC

From Accounts PC-1:

```bash
ping 192.168.40.3
```

Expected:

```text
Reply from 192.168.40.3
```

✅ Same-subnet communication successful.

---

## Test 2 — Delivery PC to Delivery PC

From Delivery PC-1:

```bash
ping 192.168.40.131
```

Expected:

```text
Reply from 192.168.40.131
```

✅ Same-subnet communication successful.

---

## Test 3 — Accounts to Delivery

From Accounts PC-1:

```bash
ping 192.168.40.130
```

Traffic follows:

```text
Accounts PC
     ↓
Accounts Switch
     ↓
Router G0/0
     ↓
Router G0/1
     ↓
Delivery Switch
     ↓
Delivery PC
```

✅ Successful communication confirms that the router is forwarding traffic between the two subnets.

---

## Test 4 — PC to Printer

From an Accounts PC:

```bash
ping 192.168.40.4
```

From a Delivery PC:

```bash
ping 192.168.40.132
```

✅ Successful replies confirm end-to-end IP connectivity.

---

# 🔍 Verification Checklist

| Requirement                                | Status |
| ------------------------------------------ | ------ |
| Accounts Department created                | ✅      |
| Delivery Department created                | ✅      |
| Minimum 2 PCs per department               | ✅      |
| Appropriate switches used                  | ✅      |
| Router used for inter-subnet communication | ✅      |
| IP addressing completed                    | ✅      |
| Subnet masks configured                    | ✅      |
| Default gateways configured                | ✅      |
| Devices properly connected                 | ✅      |
| Accounts connectivity tested               | ✅      |
| Delivery connectivity tested               | ✅      |
| Inter-department communication tested      | ✅      |

---

# 🧠 Key Networking Concepts Learned

### 📌 Subnetting

Subnetting divides one larger network into multiple smaller networks.

```text
192.168.40.0/24
        ↓
     Subnetting
        ↓
 ┌───────────────┐
 │               │
 ↓               ↓
/25             /25
```

---

### 📌 Borrowed Bits

To create 2 subnets:

```text
2¹ = 2
```

Therefore:

```text
Borrowed Bits = 1
```

---

### 📌 Block Size

With a subnet mask of:

```text
255.255.255.128
```

the block size is:

```text
256 - 128 = 128
```

---

### 📌 Network Address

The first address of a subnet.

Example:

```text
192.168.40.0
```

---

### 📌 Valid Host Range

Addresses available for devices.

Example:

```text
192.168.40.1 – 192.168.40.126
```

---

### 📌 Broadcast Address

The last address of the subnet.

Example:

```text
192.168.40.127
```

---

### 📌 Default Gateway

The router interface used by a host to communicate with another network.

Accounts:

```text
192.168.40.1
```

Delivery:

```text
192.168.40.129
```

---

# 🧩 Real-World Networking Concept

This project demonstrates a common small-business network design.

Instead of placing every department into one large network:

```text
Company Network
       │
       ├── Accounts
       │
       └── Delivery
```

each department receives its own subnet:

```text
192.168.40.0/25
        ↓
   Accounts

192.168.40.128/25
        ↓
   Delivery
```

This provides a foundation for:

* 🔐 Network segmentation
* 🚦 Traffic control
* 🛡️ Security policies
* 📊 Easier troubleshooting
* 📈 Future network expansion

---

# 🛠️ Tools Used

* 🖥️ Cisco Packet Tracer
* 🌐 IPv4
* 🧮 IPv4 Subnetting
* 🔀 Layer 2 Switching
* 🚦 Layer 3 Routing
* 📡 ICMP / Ping
* 🔌 Ethernet Cabling

---

# 🎓 Learning Outcome

After completing this project, I can:

> ✅ Analyze a real-world networking requirement, design a suitable topology, perform IPv4 subnetting, calculate network and broadcast addresses, assign IP addresses and gateways, configure router interfaces, connect network devices, and verify communication between multiple departments.

---

# 🚀 Future Improvements

This basic departmental network can be expanded into a more realistic enterprise environment by adding:

* 🔀 VLANs for department segmentation
* 🔗 Trunk links
* 🌐 Router-on-a-Stick
* 🔐 ACLs between departments
* 🖥️ DHCP server
* 🛡️ Port security
* 🔑 SSH remote management
* 🌳 Spanning Tree Protocol
* 📡 Wireless access points
* 🔄 Redundant switches and routers
* 📊 Network monitoring

---

# 🏁 Conclusion

This project demonstrates how a real-world business requirement can be converted into a functional network topology using **Cisco Packet Tracer**.

The project combines:

```text
Real-World Requirement
        ↓
Topology Design
        ↓
Subnetting
        ↓
IP Addressing
        ↓
Device Configuration
        ↓
Cabling
        ↓
Connectivity Testing
```

The key challenge in this project is **IPv4 subnetting**, where the original `/24` network is divided into two `/25` subnets for the Accounts and Delivery departments.

**Project Status:** 🟢 Completed

**Primary Skills:** `Network Design` `IPv4 Subnetting` `IP Addressing` `Routing` `Switching` `Troubleshooting`
