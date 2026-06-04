    ### Condition:

- Assign the first usable address to the  PC in each LAN.
- Assign the last usable address to the router’s interface in each LAN

---

## 🗒️ 1. Project Title

**Subnetting VLSM and Static Routes Configuration using Router, Switch, and PC**

---

### 🎯 2. Objective

To configure a subnetting, static routes, network topology and verify connectivity by assigning:

- IP Address
- Subnet Mask
- Default Gateway
- Static Route

---

## 🧱 3. Topology Overview

**Device Used:**

- 2 x Cisco ISR 4331 Router
- 4 x Cisco 2960 Switch
- 4 x PCs

---

## 🌐 4. Network Diagram(Logical)

!Subnetting_VLSM.png

---

## 📊 5. IP Addressing Table

| Device | Interface | IP Address | Subnet Mask | Default Gateway |
| --- | --- | --- | --- | --- |
| Router1 | G0/0/0 | 192.168.5.225 | 255.255.255.252 | — |
|  | G0/0/1 | 192.168.5.190 | 255.255.255.192 | — |
|  | G0/0/2 | 192.168.5.126 | 255.255.255.128 | — |
| Router2 | G0/0/0 | 192.168.5.226 | 255.255.255.252 | — |
|  | G0/0/1 | 192.168.5.206 | 255.255.255.240 | — |
|  | G0/0/2 | 192.168.5.222 | 255.255.255.240 | — |
| PC1 | Fa0/1 | 192.168.5.129 | 255.255.255.192 | 192.168.5.190 |
| PC2 | Fa0/1 | 192.168.5.1 | 255.255.255.128 | 192.168.5.126 |
| PC3 | Fa0/1 | 192.168.5.193 | 255.255.255.240 | 192.168.5.206 |
| PC4 | Fa0/1 | 192.168.5.209 | 255.255.255.240 | 192.168.5.222 |

---

## 🛣️ 6. IP Routes Table & VLSM Calculation

### 🔹IP Routes

| Router | Destination(Network Address) | Subnet Mask | Next-hop |
| --- | --- | --- | --- |
| R1 | 192.168.5.192 | 255.255.255.240 | 192.168.5.226 |
|  | 192.168.5.208 | 255.255.255.240 | 192.168.5.226 |
| R2 | 192.168.5.0 | 255.255.255.128 | 192.168.5.225 |
|  | 192.168.5.128 | 255.255.255.192 | 192.168.5.225 |

### 🔹VLSM

| Network | Needed Hosts | Subnet | CIDR |
| --- | --- | --- | --- |
| LAN1 | 45 | 192.168.5.128 | /26 |
| LAN2 | 65 | 192.168.5.0 | /25 |
| LAN3 | 14 | 192.168.5.192 | /28 |
| LAN4 | 9 | 192.168.5.208 | /28 |
| WAN | 2 | 192.168.5.224 | /30 |

---

## ⚙️ 7. Configuration Steps

### 🔹Router1 Configuration

```bash
enable
configure terminal
interface g0/0/2
ip address  192.168.5.126 255.255.255.128
no shutdown

interface g0/0/1
ip address  192.168.5.190 255.255.255.192
no shutdown

interface g0/0/0
ip address  192.168.5.225 255.255.255.252
no shutdown
```

```bash
ip route 192.168.5.192 255.255.255.240 192.168.5.226
ip route 192.168.5.208 255.255.255.240 192.168.5.226
exit
write memory - save running config
```

### 🔹Router2 Configuration

```bash
enable
configure terminal
interface g0/0/1
ip address  192.168.5.206 255.255.255.240
no shutdown

interface g0/0/2
ip address  192.168.5.222 255.255.255.240
no shutdown

interface g0/0/0
ip address  192.168.5.226 255.255.255.252
no shutdown
```

```bash
ip route 192.168.5.0 255.255.255.128 192.168.5.225
ip route 192.168.5.128 255.255.255.192 192.168.5.225
exit
write memory - save running config
```

---

### 🔹 PC1 Configuration

Configure via GUI:

- IP Address: `192.168.5.129`
- Subnet Mask: `255.255.255.192`
- Default Gateway: `192.168.5.190`

### 🔹 PC2 Configuration

Configure via GUI:

- IP Address: `192.168.5.1`
- Subnet Mask: `255.255.255.128`
- Default Gateway: `192.168.5.126`

### 🔹 PC3 Configuration

Configure via GUI:

- IP Address: `192.168.5.193`
- Subnet Mask: `255.255.255.240`
- Default Gateway: `192.168.5.206`

### 🔹 PC4 Configuration

Configure via GUI:

- IP Address: `192.168.5.209`
- Subnet Mask: `255.255.255.240`
- Default Gateway: `192.168.5.222`

---

## 🔍 8. Verification & Testing

### ✅ Commands Used R1 & R2

```
show ip route
show ip interface brief
tracert
```

!image.png

### ✅ Commands Used PC1 & PC4

```
ping 192.168.5.193
ping 192.168.5.209
```

```
ping 192.168.5.1
ping 192.168.5.129
```

!image.png

### ✅ Expected Result

- Successful replies from all devices
- Network connectivity verified

---

# 🔌 9. Hardware and Interface Learning

## Router Interface Architecture

During this project, practical understanding was gained regarding the physical and modular architecture of the Cisco ISR 4331 router.

The router contains built-in Gigabit Ethernet interfaces:

- GigabitEthernet0/0/0
- GigabitEthernet0/0/1

Additional interfaces can be added using expansion modules and SFP transceivers depending on network requirements.

---

## SFP Transceivers and Media Types

Different SFP modules were studied to understand how routers support multiple transmission media.

### Copper Ethernet SFP

- GLC-T
- Used for RJ45 Gigabit Ethernet connections
- Supports copper Ethernet cables such as Cat5e/Cat6

### Single-Mode Fiber SFP

- GLC-LH-SMD
- Used for long-distance fiber optic communication
- Supports single-mode fiber cables

### Fiber Ethernet SFP

- GLC-GE-100FX
- Used for fiber optic Ethernet communication
- Supports fiber-based network connectivity

---

## 📌 10. Key Learnings

- Understanding VLSM practically
- IP address Planning
- Router interface configuration
- Static routing configuration
- End device configuration
- Connectivity troubleshooting

---

## 🧠 11. Conclusion

This project successfully demonstrated the implementation of VLSM subnetting and static routing using Cisco routers, switches, and PCs. Multiple subnet sizes were designed and configured efficiently to optimize IP Address.

Through this project, practical knowledge was gained in subnetting, router configuration, IP addressing and network troubleshooting .
