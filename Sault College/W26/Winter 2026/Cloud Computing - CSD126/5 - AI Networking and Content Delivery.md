# Section 1: Networking basics

## Networks

A computer network is two or more client machines that are connected together to share resources. A network can be logically partitioned into subnets. Networking requires a networking device (such as a router or switch) to connect all the clients together and enable communication between them.

## IP addresses

Each client machine in a network has a unique Internet Protocol (IP) address that identifies it. An IP address is a numerical label in decimal format. Machines convert that decimal number to a binary format.

In this example, the IP address is 192.0.2.0. Each of the four dot (.)-separated numbers of the IP address represents 8 bits in octal number format. That means each of the four numbers can be anything from 0 to 255. The combined total of the four numbers for an IP address is 32 bits in binary format.

## IPv4 and IPv6 addresses

A 32-bit IP address is called an IPv4 address.

IPv6 addresses, which are 128 bits, are also available. IPv6 addresses can accommodate more user devices.

An IPv6 address is composed of eight groups of four letters and numbers that are separated by colons (:). In this example, the IPv6 address is 2600:1f18:22ba:8c00:ba86:a05e:a5ba:00FF. Each of the eight colon-separated groups of the IPv6 address represents 16 bits in hexadecimal number format. That means each of the eight groups can be anything from 0 to FFFF. The combined total of the eight groups for an IPv6 address is 128 bits in binary format.

## Classless Inter-Domain Routing (CIDR)

A common method to describe networks is Classless Inter-Domain Routing (CIDR). The CIDR address is expressed as follows:

- An IP address (which is the first address of the network).
- Next, a slash character (/)
- Finally, a number that tells you how many bits of the routing prefix must be fixed or allocated for the network identifier

The bits that are not fixed are allowed to change. CIDR is a way to express a group of IP addresses that are consecutive to each other.

In this example, the CIDR address is 192.0.2.0/24. The last number (24) tells you that the first 24 bits must be fixed. The last 8 bits are flexible, which means that 28(or 256) IP addresses are available for the network, which rangefrom 192.0.2.0 to 192.0.2.255. The fourth decimal digit is allowed to change from 0 to 255.

If the CIDR was 192.0.2.0/16, the last number (16) tells you that the first 16 bits must be fixed. The last 16 bits are flexible, which means that 216(or 65,536) IP addresses are available for the network, ranging from 192.0.0.0 to 192.0.255.255. The third and fourth decimal digits can each change from 0 to 255.

There are two special cases
- Fixed IP addresses, in which every bit is fixed, represent a single IP address (for example, 192.0.2.0/32). This type of address is helpful when you want to set up a firewall rule and give access to a specific host.
- The internet, in which every bit is flexible, is represented as 0.0.0.0

## Open Systems Interconnection (OSI) model

The Open Systems Interconnection (OSI) model is a conceptual model that is usedto explain how data travels over a network. It consists of seven layers and shows the common protocols and addresses that are used to send data at each layer. For example, hubs and switches work at layer 2 (the data link layer). Routers work at layer 3 (the network layer). The OSI model can also be used to understand how communication takes place in a virtual private cloud (VPC), which you will learn about in the next section.

ICA is Independent Computing Architecture, developed by Citrix Systems to facilitate efficient data transfer between a server and a client.

# Section 2: Amazon VPC




