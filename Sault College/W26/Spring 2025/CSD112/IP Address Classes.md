Before **[[CIDR]]** was introduced, IP addresses were divided into fixed **classes (A, B, C, D, and E)** to define how many networks and devices (hosts) each range could have.

|**Class**|**Starting IP Range**|**Default Subnet Mask**|**Use**|**Number of Hosts**|
|---|---|---|---|---|
|**A**|1.0.0.0 – 126.255.255.255|255.0.0.0 (/8)|Very large networks|~16 million|
|**B**|128.0.0.0 – 191.255.255.255|255.255.0.0 (/16)|Medium networks|~65,000|
|**C**|192.0.0.0 – 223.255.255.255|255.255.255.0 (/24)|Small networks|254|
|**D**|224.0.0.0 – 239.255.255.255|—|Multicasting|—|
|**E**|240.0.0.0 – 255.255.255.255|—|Experimental (research)|—|

### Example:
- A **Class A** address like `10.0.0.1` belongs to a large organization with many devices.
- A **Class C** address like `192.168.1.10` fits small local networks like home or office LANs.