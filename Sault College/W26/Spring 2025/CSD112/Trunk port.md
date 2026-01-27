A **trunk port** is a special type of switch port used to **carry traffic for multiple VLANs** between switches or between a switch and a router.
- Normally, a switch port belongs to **one VLAN only** (access port).
- A **trunk port** can carry **many VLANs simultaneously** by adding a **tag** to each frame to indicate which VLAN it belongs to (using **802.1Q tagging**).
- This allows VLANs to **extend across multiple switches**, keeping devices in the same VLAN able to communicate even if they are on different switches.

**Example:**

- VLAN 10 (HR) and VLAN 20 (IT) exist on two switches.    
- A trunk port connects the switches and carries **both VLAN 10 and VLAN 20 traffic** over the same cable.