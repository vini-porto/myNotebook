A **VLAN (Virtual Local Area Network)** is a way to **divide a physical network into multiple smaller, virtual networks** — all using the same switches and cabling.

---
# How VLANs work

- A **switch** can be configured with multiple VLANs.
- Each **VLAN** gets a unique **ID number** (for example, VLAN 10, VLAN 20, VLAN 30).
- When a device connects to a port, that port is assigned to a VLAN.
- Devices in **the same VLAN** can communicate **directly**.
- Devices in **different VLANs** need a **router (or Layer 3 switch)** to communicate — this is called **inter-VLAN routing**
---
### Example

Imagine an office with three departments:
- **VLAN 10** – HR
- **VLAN 20** – IT
- **VLAN 30** – Finance

All employees are plugged into the same physical switch, but:
- HR computers can only talk to HR computers.
- IT computers can only talk to IT computers.
- Finance computers can only talk to Finance computers.
---
# VLAN Numbers

VLANs are identified by numbers (1-4094):
- **VLAN 1:** Default VLAN (everything starts here)
- **VLANs 2-1005:** Normal range (works on all switches)
- **VLANs 1006-4094:** Extended range (newer switches only)

---

# VLAN Tagging and Trunking

When VLAN traffic needs to **travel between switches**, the connection between them is called a **[[Trunk port]]**.

- A **trunk** carries multiple VLANs over a single physical link.
- Each Ethernet frame is **tagged** with a VLAN ID (using IEEE 802.1Q standard) so the receiving switch knows which VLAN it belongs to.