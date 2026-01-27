An **access port** is a switch port that **belongs to a single VLAN** and carries traffic **only for that VLAN**.

- Devices connected to an access port are unaware of VLAN tagging — the switch automatically assigns all their traffic to the port’s VLAN.
- Access ports are typically used for **end devices** like computers, printers, or IP phones.
- Unlike a trunk port, an access port **cannot carry multiple VLANs**.

**Example:**
- A computer connected to an access port assigned to VLAN 10 will only communicate with other devices in VLAN 10 unless a router performs inter-VLAN routing.
