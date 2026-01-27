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

Many of the concepts of an on-premises network apply to a cloud-based network, but much of the complexity of setting up a network has been abstracted without sacrificing control, security, and usability. In this section, you learn about Amazon VPC and the fundamental components of a VPC.

## Amazon VPC

Amazon Virtual Private Cloud (Amazon VPC) is a service that lets you provision a logically isolated section of the AWS Cloud (called a virtual private cloud, or VPC) where you can launch your AWS resources.

Amazon VPC gives you control over your virtual networking resources, including the selection of your own IP address range, the creation of subnets, and the configuration of route tables and network gateways. You can use both IPv4 and IPv6 in your VPC for secure access to resources and applications.

You can also customize the network configuration for your VPC. For example, you can create a public subnet for your web servers that can access the public internet. You can place your backend systems (such as databases or application servers) in a private subnet with no public internet access.

Finally, you can use multiple layers of security, including security groups and network access control lists (networkACLs), to help control access to Amazon Elastic Compute Cloud (Amazon EC2) instances in each subnet.

## VPCs and subnets

Amazon VPC enables you to provision virtual private clouds (VPCs). A VPCis a virtual network that is logically isolated from other virtual networks in the AWS Cloud. A VPC is dedicated to your account. VPCs belong to a single AWS Region and can span multiple Availability Zones.

After you create a VPC, you can divide it into one or more subnets. A subnetis a range of IP addresses in a VPC. Subnets belong to a single Availability Zone. You can create subnets in different Availability Zones for high availability. Subnets are generally classified as public or private. Public subnets have direct access to the internet, but private subnetsdo not.

## IP addressing

IP addresses enable resources in your VPC to communicate with each other and with resources over the internet. When you create a VPC, you assign an IPv4 CIDR block (a range of privateIPv4 addresses) to it. After you create a VPC, you cannot change the address range, so it is important that you choose it carefully. The IPv4 CIDR block might be as large as /16 (which is 216, or 65,536 addresses) or as small as /28 (which is 24, or 16 addresses).

You can optionally associate an IPv6 CIDR block with your VPC and subnets, and assign IPv6 addresses from that block to the resources in your VPC. IPv6 CIDR blocks have a different block size limit.

The CIDR block of a subnet can be the same as the CIDR block for a VPC. In this case,the VPC and the subnet are the same size (a single subnet in the VPC). Also, the CIDR block of a subnet can be a subset of the CIDR block for the VPC. This structure enables the definition of multiple subnets. If you create more than one subnet in a VPC, the CIDR blocks of the subnets cannot overlap. You cannot have duplicate IP addresses in the same VPC.

## Reserved IP addresses

When you create a subnet, it requires its own CIDR block. For each CIDR block that you specify, AWS reserves five IP addresses within that block, and theseaddresses are not available for use. AWS reserves these IP addresses for:

- Network address
- VPC local router (internal communications)
- Domain Name System (DNS) resolution
- Future use
- Network broadcast address

For example, suppose that you create a subnet with an IPv4 CIDR block of 10.0.0.0/24 (which has 256 total IP addresses). The subnet has 256 IP addresses, but only 251 are available because five are reserved.


## Public IP address type

When you create a VPC, every instance in that VPC gets a private IP address automatically. You can also request a public IP address to be assigned when you create the instance by modifying the subnet’s auto-assign public IP address properties.

An Elastic IP address is a static and public IPv4 address that is designed for dynamic cloud computing. You can associate an Elastic IP address with any instance or network interface for any VPC in your account. With an Elastic IP address, you can mask the failure of an instance by rapidly remapping the address to another instance in your VPC. Associating the Elastic IP address with the network interface has an advantage over associating it directly with the instance. You can move all of the attributes of the network interface from one instance to another in a single step.

Additional costs might apply when you use Elastic IP addresses, so it is important to release them when you no longer need them.

## Elastic network interfac

An elastic network interface is a virtual network interface that you can attach or detach from an instance in a VPC. A network interface's attributes follow it when it is reattached to another instance. When you move a network interface from one instance to another, network traffic is redirected to the new instance.

Each instance in your VPC has a default network interface (the primary network interface) that is assigned a private IPv4 address from the IPv4 address range of your VPC. You cannot detach a primary network interface from an instance. You can create and attach an additional network interface to any instance in your VPC. The number of network interfaces you can attach varies by instance type.

##  Route tables and route

A route table contains a set of rules(called routes)that directs network traffic from your subnet. Each route specifies a destination and a target. The destination is the destination CIDR block where you want traffic from your subnet to go. The target is the target that the destination traffic is sent through. By default, every route table that you create contains a local route for communication in the VPC. You can customize route tables by adding routes. You cannot delete the local route entry that is used for internal communications.

Each subnet in your VPC must be associated with a route table. The main route table is the route table is automatically assigned to your VPC. It controls the routing for all subnets that are not explicitly associated with any other route table. A subnet can be associated with only one route table at a time, but you can associate multiple subnets with the same route table.

# Section 3: VPC networking

