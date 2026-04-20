# Day 16 - VLANs

Today was the introduction to what VLANs are and the basics in how to configure them. As always I will try to recap the main concepts using the Feynman method and try to explain them in my own words.

## Feynman Method

A LAN is a singular broadcast domain. This begs the question, what is a Broadcast Domain? A Broadcast Domain refers to teh devices on a network that will receive a broadcast frame when sent by one of its devices.

Broadcast traffic is not always very helpful on a network. This is fundamentally for two reasons, performance and security. A lot of nececessary broadcast traffic can slow down overall network performance as this traffic is received by all hosts and is usually dropped, unless it is specified for them. More importantly, in a flat network, broadcast traffic is sent to all devices on a network. This could present an issue regarding the security of that traffic as that broadcast frame may be sent to a device that was not intended to receive it. 

If you just rely on subnetting however to try to segment your network, this will not solve the problem of your network being flooded by broadcast traffic. This is because subnetting is the logical division of a network at Layer 3, broadcast domains operate at Layer 2. Therefore, if a device in one subnet sends a broadcast frame, it will be sent out all interfaces of the switch regardless of any subnetting. This presents the problem that VLANs intend to solve

A VLAN is a logical segementation of a network at Layer 2. It is configured on switches and ensures that broadcast traffic sent by one device in the VLAN, will only be received by other devices in that VLAN as well. If a device in one VLAN wants to communicate with a device in another VLAN, the most basic method of doing so is for the traffic to be forwarded through the switch, to the router/firewall (where security polcies can be applied), then back to the switch and to the other device in another VLAN. 

That is the majority of the basic concepts discussed today when looking at VLANs. Let's move onto the lab

## Lab

**Topology**

<img width="861" height="396" alt="image" src="https://github.com/user-attachments/assets/9b85b170-f90b-4af2-a69c-9172b62e0e59" />


**Instructions**
1. Configure the correct IP address/subnet mask on each PC.
    Set the gateway address as the LAST USABLE address of the subnet.

2. Make three connections between R1 and SW1.
    Configure one interface on R1 for each VLAN.
    Make sure the IP addresses are the gateway address you configured on the PCs.

3. Configure SW1's interfaces in the proper VLANs.
    Remember the interfaces that connect to R1!
    Name the VLANs
     (Engeering, HR, Sales)

4. Ping between the PCs to check connectivity.
    Send a broadcast ping from a PC (ping the subnet broadcast address),
     and see which PCs devices receive the broadcast
      (use Packet Tracer's 'Simulation Mode')



1. The first thing I did was set up the IP address on all of the relevant interfaces on the route. For simplicity sake I mapped g0/0 = Engineering Subnet, g0/1 = HR Subnet and g0/2 = Sales subnet.

<img width="1307" height="193" alt="image" src="https://github.com/user-attachments/assets/a2930abc-0ba3-4988-827e-b859bbf76d3b" />

Now for the PCs

_PC1_

<img width="1687" height="544" alt="image" src="https://github.com/user-attachments/assets/d09ea8ec-93b6-4b4a-b0df-e67996b05557" />

_PC2_

<img width="1686" height="619" alt="image" src="https://github.com/user-attachments/assets/b9cf4749-b7b2-469c-b028-61175158d4c5" />

_PC3_

<img width="1685" height="523" alt="image" src="https://github.com/user-attachments/assets/9a526e43-dbe3-4329-b483-15085dffe8a8" />

_PC4_

<img width="1687" height="572" alt="image" src="https://github.com/user-attachments/assets/8a64b17c-84ab-49d9-846d-84fd544a6fab" />

_PC5_

<img width="1690" height="612" alt="image" src="https://github.com/user-attachments/assets/2771a27f-7b15-4780-84de-f1fcdb0d4db0" />

_PC6_

<img width="1692" height="484" alt="image" src="https://github.com/user-attachments/assets/57711589-a2a3-4852-bc27-78511189f7fb" />

2. The first thing I did here was make three connections from SW1 to R1

<img width="354" height="437" alt="image" src="https://github.com/user-attachments/assets/412ec201-a688-40e5-8a7c-1938b59b2a4c" />

The we already configured R1's interfaces withthe last available IP address in each subnet, so no work needed here

3. Ok let's first configure VLAN10
I will use interface ranges to make this quicker

_VLAN 10_

<img width="818" height="114" alt="image" src="https://github.com/user-attachments/assets/5372068a-8cb5-4c7a-915a-c8a5e854bb85" />

Note: an access port just means that that interface is only dedicated to one VLAN. This will be different to a trunk port which can carry multiple VLANs but we will cover that later.

_VLAN 20_

<img width="878" height="196" alt="image" src="https://github.com/user-attachments/assets/d5465ae2-4094-408c-8b71-67fef156dec9" />

_VLAN 30_

<img width="893" height="163" alt="image" src="https://github.com/user-attachments/assets/6b1dc746-c50a-4588-bb18-cdeee7f3b5cc" />

Now for verification

<img width="1294" height="325" alt="image" src="https://github.com/user-attachments/assets/a160c603-7fb4-41d1-8806-ef0fb7a30b43" />


And for names!

<img width="1349" height="316" alt="image" src="https://github.com/user-attachments/assets/3cbd9323-f3dc-4b99-95bb-5bdee628fbfb" />

4. Check for connectivity.

To ping PC3 in a separate VLAN, this will work. 

<img width="935" height="415" alt="image" src="https://github.com/user-attachments/assets/1d4b4c0c-4b28-4e6a-bfed-65e91355e730" />

However in simulation mode we can see the ping goes through the router first, not just through the switch via a broadcast frame in the form of say an ARP request


