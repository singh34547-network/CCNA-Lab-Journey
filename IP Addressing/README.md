## 🧾 1. Project Title

**Basic Network Configuration using Router, Switch, and PC**

---

## 🎯 2. Objective

To configure a simple network topology and verify connectivity by assigning:

- IP Address
- Subnet Mask
- Default Gateway

---

## 🧱 3. Topology Overview

**Devices Used:**

- 1 × Cisco 2911 Router
- 3 × Cisco 2960 Switch
- 3 × PCs

**Connection Type:**

- PC ↔ Switch → Straight-through
- Switch ↔ Router → Straight-through

---

## 🌐 4. Network Diagram (Logical)

---

!IP Adreesing Topology.png

--- 

## 📊 5. IP Addressing Table

| Device | Interface | IP Address | Subnet Mask | Default Gateway |
| --- | --- | --- | --- | --- |
| Router | G0/0 | 201.191.20.254 | 255.255.255.0 | — |
| Router | G0/1 | 182.98.255.254 | 255.255.0.0 | — |
| Router | G0/2 | 15.255.255.254 | 255.0.0.0 | — |
| PC0 | Fa0/1 | 201.191.20.1 | 255.255.255.0 | 201.191.20.254 |
| PC1 | Fa0/1 | 182.98.0.1 | 255.255.0.0 | 182.98.255.254 |
| PC2 | Fa0/1 | 15.0.0.1 | 255.0.0.0 | 15.255.255.254 |

---

## ⚙️ 6. Configuration Steps

### 🔹 Router Configuration

```
enable
configure terminal
interface g0/0
ip address192.168.1.1255.255.255.0
no shutdown
exit

ip name-server8.8.8.8
```

---

### 🔹 Switch Configuration (Optional Management IP)

```
enable
configure terminal
interface vlan1
ip address192.168.1.2255.255.255.0
no shutdown
exit

ip default-gateway192.168.1.1
```

---

### 🔹 PC Configuration

Configure via GUI:

- IP Address: `192.168.1.10 / 11`
- Subnet Mask: `255.255.255.0`
- Default Gateway: `192.168.1.1`
- DNS: `8.8.8.8`

---

## 🔍 7. Verification & Testing

### ✅ Commands Used

```
ping192.168.1.1
ping192.168.1.11
```

### ✅ Expected Result

- Successful replies from all devices
- Network connectivity verified

---

## ⚠️ 8. Troubleshooting

| Issue | Cause | Solution |
| --- | --- | --- |
| Ping fails | Wrong IP | Check IP config |
| No link | Wrong cable | Use straight-through |
| Interface down | Missing `no shutdown` | Enable interface |
| Gateway unreachable | Wrong gateway | Fix gateway IP |

---

## 📌 9. Key Learnings

- Difference between **Layer 2 and Layer 3 devices**
- Importance of **default gateway**
- Basic **IP addressing and connectivity testing**
- Proper use of **cables in Packet Tracer**

---

## 🧠 10. Conclusion

The lab successfully demonstrated how to configure a basic network and verify communication between devices using proper IP addressing and connectivity tools.
