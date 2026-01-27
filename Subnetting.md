## Host Calculation Formula

$$\text{Usable Hosts} = 2^{\text{host bits}} - 2$$

**Why subtract 2?**

- Network address (e.g., `.0`)
- Broadcast address (e.g., `.255`)

**Example:** `/24` network

- Host bits: 8
- $2^8 - 2 = 254$ usable hosts

---

## Understanding /24 Networks

**Example:** `192.168.10.0/24`

- **Network portion:** `192.168.10`
- **Host portion:** last octet (`.0` to `.255`)
- **Network address:** `.0` (all host bits = 0)
- **Broadcast address:** `.255` (all host bits = 1)

---
## Process

1. **"Steal" host bits** → becomes network bits
2. **Calculate:**
    - New networks: $2^{\text{stolen bits}}$
    - Hosts per subnet: $2^{\text{remaining host bits}} - 2$

---

## Example 1: Creating 2 Networks (/25)

**Steal 1 bit:** Binary `10000000` = `.128`

|Network|First Host|Last Host|Broadcast|
|---|---|---|---|
|.0|.1|.126|.127|
|.128|.129|.254|.255|

- **New subnet:** `/25` (24 + 1)
- **Subnet mask:** `255.255.255.128`
- **Usable hosts:** $2^7 - 2 = 126$ per subnet

---

## Example 2: Creating 4 Networks (/26)

**Steal 2 bits:** Binary `11000000` = `.192`

|Network|First Host|Last Host|Broadcast|
|---|---|---|---|
|.0|.1|.62|.63|
|.64|.65|.126|.127|
|.128|.129|.190|.191|
|.192|.193|.254|.255|

- **New subnet:** `/26` (24 + 2)
- **Subnet mask:** `255.255.255.192`
- **Usable hosts:** $2^6 - 2 = 62$ per subnet

---
## Key Takeaway

> More stolen bits = More subnets but fewer hosts per subnet
