# 🚀 Static Routing using SDN Controller

## 📌 Project Overview
This project demonstrates **static routing** using Software Defined Networking (SDN) by manually installing flow rules in OpenFlow switches.  
The routing path is fixed and controlled without using any dynamic routing protocol.

---

## 🎯 Objective
To implement a **deterministic routing path** where packets follow a predefined route using manually configured flow rules.

---

## 🛠️ Tools & Technologies
- Mininet  
- OpenFlow Protocol  
- Python  
- ovs-ofctl (Open vSwitch tool)  
- Ubuntu (Virtual Machine)

---

## 🌐 Network Topology


h1 ---- s1 ---- s2 ---- s3 ---- h2


- **Hosts:** h1, h2  
- **Switches:** s1, s2, s3  
- Linear topology with fixed path

---

## 🔄 Data Flow


h1 → s1 → s2 → s3 → h2


- Packets follow a **static path**
- No alternate routing is allowed
- Reverse path is used for replies

---

## ⚙️ How to Run

### 1️⃣ Start Mininet Topology
```bash
sudo mn --custom static_topo.py --topo static --controller=none
2️⃣ Test Connectivity (Before Rules)
pingall
3️⃣ Install Flow Rules
sudo ovs-ofctl add-flow s1 in_port=1,actions=output:2
sudo ovs-ofctl add-flow s1 in_port=2,actions=output:1

sudo ovs-ofctl add-flow s2 in_port=1,actions=output:2
sudo ovs-ofctl add-flow s2 in_port=2,actions=output:1

sudo ovs-ofctl add-flow s3 in_port=1,actions=output:2
sudo ovs-ofctl add-flow s3 in_port=2,actions=output:1
4️⃣ Test Connectivity (After Rules)
pingall
🔁 Regression Testing
Delete Flow Rules
sudo ovs-ofctl del-flows s1
sudo ovs-ofctl del-flows s2
sudo ovs-ofctl del-flows s3
Reinstall Rules and Test Again
pingall
📊 Results
Scenario	Packet Loss
Before Rules	100% ❌
After Rules	0% ✅
After Deletion	100% ❌
After Reinstallation	0% ✅
🔍 Key Concepts
SDN (Software Defined Networking): Separates control plane and data plane
Static Routing: Fixed path, no dynamic decision-making
Flow Rules: Define how packets are forwarded in switches
📌 Conclusion

Static routing was successfully implemented using SDN principles.
Manual flow rules ensured that packets followed a fixed path, and testing confirmed reliable and predictable network behavior.
