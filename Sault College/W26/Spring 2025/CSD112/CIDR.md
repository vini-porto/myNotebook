**CIDR notation (Classless Inter-Domain Routing)** is a short way to write an **IP address** together with its **subnet mask**.

It looks like this:
```
192.168.1.10/24
```

### Meaning
- `192.168.1.10` is the **IP address**.
- `/24` tells how many bits of the address are used for the **network part**.

In this case, `/24` means the first 24 bits (or the first three numbers: `192.168.1`) identify the **network**, and the remaining 8 bits (`.10`) identify the **device**.

