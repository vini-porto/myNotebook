# 2. Create the VLAN

```
Switch(config)# vlan 10
Switch(config-vlan)# name ENGINEERING

```

Translation: "Create VLAN 10 and name it ENGINEERING"

# 2. Assign Ports to the VLAN

```
Switch(config)# interface gigabitEthernet 0/1
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 10

```
Translation:

1. Go to interface configuration
2. Set this port as an "access port" (connects to end devices)
3. Put this port in VLAN 10