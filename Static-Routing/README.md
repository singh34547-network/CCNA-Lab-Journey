## 🗒️ 1. Project Title

**Basic Static Routes Configuration using Router, Switch, and PC**

---

### 🎯 2. Objective

To configure a static routes, network topology and verify connectivity by assigning:

- IP Address
- Subnet Mask
- Default Gateway
- Static Route

---

## 🧱 3. Topology Overview

**Device Used:**

- 3 x Cisco 2911 Router
- 2 x Cisco 2960 Switch
- 2 x PCs

---

## 🌐 4. Network Diagram(Logical)

!image.png

---

## 📊 5. IP Addressing Table

| Device | Interface | IP Address | Subnet Mask | Default Gateway |
| --- | --- | --- | --- | --- |
| Router1 | G0/0 | 192.168.12.1 | 255.255.255.0 | — |
|  | G0/2 | 192.168.1.254 | 255.255.255.0 | — |
| Router2 | G0/1 | 192.168.12.2 | 255.255.255.0 | — |
|  | G0/2 | 192.168.13.2 | 255.255.255.0 | — |
| Router3 | G0/0 | 192.168.13.3 | 255.255.255.0 | — |
|  | G0/1 | 192.168.2.254 | 255.255.255.0 | — |
| PC1 | Fa0/1 | 192.168.1.1 | 255.255.255.0 | 192.168.1.254 |
| PC3 | Fa0/1 | 192.168.2.1 | 255.255.255.0 | 192.168.2.254 |

---

## 🛣️ 6. IP Routes Table

| Router | Destination  | Next-hop |
| --- | --- | --- |
| R1 | 192.168.1.0 | Connected |
|  | 192.168.2.0 | 192.168.12.2 |
| R2 | 192.168.1.0 | 192.168.12.1 |
|  | 192.168.2.0 | 192.168.13.3 |
| R3 | 192.168.1.0 | 192.168.13.2 |
|  | 192.168.2.0 | Connected |

---

## ⚙️ 7. Configuration Steps

### 🔹Router1 Configuration

```bash
enable
configure terminal
interfacee g0/0
ip address  192.168.12.1 255.255.255.0
speed 1000
duplex full
no shutdown
exit
```

```bash
interfacee g0/2
ip address  192.168.1.254 255.255.255.0
no shutdown
speed 1000
duplex full
exit
```

```bash
ip route 192.168.2.0 255.255.255.0 192.168.12.2
exit
write memory - save running config
```

### 🔹Router2 Configuration

```bash
enable
configure terminal
interfacee g0/1
ip address  192.168.12.2 255.255.255.0
no shutdown
speed 1000
duplex full
exit
```

```bash
interfacee g0/2
ip address  192.168.13.2 255.255.255.0
no shutdown
speed 1000
duplex full
exit
```

```bash
ip route 192.168.1.0 255.255.255.0 192.168.12.1
ip route 192.168.2.0 255.255.255.0 192.168.13.3
exit
write memory - save running config
```

### 🔹Router3 Configuration

```bash
enable
configure terminal
interfacee g0/0
ip address  192.168.13.3 255.255.255.0
no shutdown
speed 1000
duplex full
exit
```

```bash
interfacee g0/1
ip address  192.168.2.254 255.255.255.0
no shutdown
speed 1000
duplex full
exit
```

```bash
ip route 192.168.1.0 255.255.255.0 192.168.13.2
exit
write memory - save running config
```

---

### 🔹 PC1 Configuration

Configure via GUI:

- IP Address: `192.168.1.1`
- Subnet Mask: `255.255.255.0`
- Default Gateway: `192.168.1.254`

### 🔹 PC2 Configuration

Configure via GUI:

- IP Address: `192.168.2.1`
- Subnet Mask: `255.255.255.0`
- Default Gateway: `192.168.2.254`

---

## 🔍 8. Verification & Testing

### ✅ Commands Used PC1 & PC3

```
ping 192.168.2.1
ping 192.168.2.254
```

```
ping 192.168.1.1
ping 192.168.1.254
```

### ✅ Expected Result

- Successful replies from all devices
- Network connectivity verified

---

## ⚠️ 9. Troubleshooting

| Issue | Cause | Solution |
| --- | --- | --- |
| Ping fails | Wrong IP | Check IP config |
| Invalid next hop address (it's this router) | R3(G0/0) config in R2(0/1) | Correct IP Address |

**Error :** Router2(config)#ip route 192.168.2.0 255.255.255.0 192.168.13.3

Result - %Invalid next hop address (it's this router)

---

## 📌 10. Key Learnings

- How devices communicate with each in a network.
- How packet travels in network
- Importance of **default gateway**
- How to configure static routes
- Basic **IP addressing and connectivity testing**
- Proper use of **cables in Packet Tracer**

---

## 🧠 11. Conclusion

The lab successfully demonstrated how to configure a static routes and IP address in a network and verify communication between devices using proper IP addressing and connectivity tools(ping).
