```
Switch(config)# interface gigabitEthernet 0/1
Switch(config-if)# switchport mode trunk
Switch(config-if)# switchport trunk encapsulation dot1q
Switch(config-if)# switchport trunk native vlan 99
Switch(config-if)# switchport trunk allowed vlan 10,20,30

```

Translation:

1. Go to interface configuration
2. Make this a trunk port
3. Use 802.1Q tagging (dot1q = 802.1Q)
4. Set native VLAN to 99
5. Only allow VLANs 10, 20, and 30 on this trunk