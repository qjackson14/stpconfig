<p align="center">

</p>

<h1></h1>
<br />


<h2>Video Demonstration</h2>

- ### [YouTube: Day 21 Lab Configuring STP](https://www.youtube.com/watch?v=obM2_dG0YwU&t=31s)

<h2>Environments and Technologies Used</h2>

- Jeremy's IT Lab Youtube Channel
- Cisco Packet Tracer
  

  
<h2>Operating Systems Used </h2>

- Cisco IOS


<h2>Step-by-Step</h2>
✅ <b>Step 1: Identify Current STP Topology</b>

- Command:
- show spanning-tree

- What you’re looking for:
- Root bridge (look for: “this bridge is the root”)
- Root ports
- Blocking ports

- 👉 In this lab:
- SW2 = Root bridge (default)
- Others have root ports pointing toward SW2

- <b>⚖️ Step 2: Load Balancing with STP (VERY IMPORTANT)</b>
- Instead of 1 root for everything → split traffic across VLANs
- Configure:
- On SW1:
- spanning-tree vlan 1 root primary
- spanning-tree vlan 2 root secondary

- On SW2:
- spanning-tree vlan 1 root secondary
- spanning-tree vlan 2 root primary
-💡 What This Does
- VLAN 1 traffic → prefers SW1
- VLAN 2 traffic → prefers SW2
- 👉 Result: Load balancing across links

- 🎯 <b>Step 3: Change STP Cost (Influence Path Selection)</b>
- Command:
- interface f0/2
- spanning-tree vlan 1 cost 100
- 🔑 Key Rule:
- Lower cost = preferred path
- 👉 When you increase cost:
- That path becomes less desirable
- Switch picks a different root port

- 🎯 <b>Step 4: Change Port Priority (Tie-breaker ONLY)</b>
- Command:
- spanning-tree vlan 1 port-priority 240
- ⚠️ Important:
- Port priority is the LAST tie-breaker
- Order of root port selection:
- Cost (MOST important)
- Bridge ID
- Port Priority (LAST)
- 👉 That’s why:
- Changing priority often does nothing unless everything else ties

- ⚡<b>Step 5: PortFast + BPDU Guard (EXAM FAVORITE)</b>
- Enable PortFast:
- spanning-tree portfast
- Enable BPDU Guard:
- spanning-tree bpduguard enable
