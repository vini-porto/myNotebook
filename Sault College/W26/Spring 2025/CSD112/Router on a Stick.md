A **Router on a Stick** is a network setup where a **single physical router interface** is used to route traffic between **multiple VLANs** on a switch.

Here’s how it works:
1. The switch has **multiple VLANs** (e.g., VLAN 10, VLAN 20).
2. One **trunk link** connects the switch to a **single router interface**.
3. The router interface is **subdivided into virtual subinterfaces**, one for each VLAN, each with its **own IP address**.
4. When devices in different VLANs want to communicate, their traffic goes **through the router**, which routes it between VLANs.

**Example:**
- VLAN 10 (192.168.10.0/24)
- VLAN 20 (192.168.20.0/24)
- Router interface Gi0/0 has subinterfaces:
    - Gi0/0.10 → IP 192.168.10.1 (VLAN 10)
    - Gi0/0.20 → IP 192.168.20.1 (VLAN 20)

**Benefits:**
- Allows **inter-VLAN communication** using a single router port.
- Saves hardware, as you don’t need multiple router interfaces for each VLAN.