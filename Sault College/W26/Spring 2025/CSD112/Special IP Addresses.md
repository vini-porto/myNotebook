**Special IP addresses** are certain reserved addresses that **cannot be assigned to devices** because they have specific purposes in networking. Here are the main ones you should know:

---
### 1. **Network Address**
- This address identifies the **network itself**, not a device.
- It’s always the **first address** in a subnet (all host bits are 0).  
    **Example:** In the network `192.168.1.0/24`, the address `192.168.1.0` represents the **whole network**, not any computer or router.
---
### 2. **Broadcast Address**
- Used to **send messages to all devices** on a network simultaneously.
- It’s always the **last address** in a subnet (all host bits are 1).  
    **Example:** In `192.168.1.0/24`, the broadcast address is `192.168.1.255`.
---
### 3. **Loopback Address**
- Used by a device to **communicate with itself** for testing and diagnostics.
- Any address from `127.0.0.0` to `127.255.255.255` belongs to this range, but the most common one is `127.0.0.1`.  
    **Example:** `127.0.0.1` is known as **localhost**.
---
### 4. **Link-Local Address**
- Automatically assigned when a device **cannot get an IP** from a DHCP server.
- Used for communication **only within the same local network**.
- Range: `169.254.0.0 – 169.254.255.255`.
---
### 5. **Reserved Addresses**
- Certain ranges are reserved for **future use**, **documentation**, or **special protocols**.
- Example:
    - `0.0.0.0` — represents “any” or “unknown” address (used during startup or routing).
    - `255.255.255.255` — used for **limited broadcast**.
    - `192.0.2.0/24`, `198.51.100.0/24`, `203.0.113.0/24` — used only for **examples and documentation**.