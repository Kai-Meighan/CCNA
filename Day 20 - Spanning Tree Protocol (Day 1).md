# Day 20 - Spanning Tree Protocol (Part 1)

Today, we began spanning tree Protocol (STP). I will structure my notes in a Question, Evidence, Conclusion format for a clearer structure of points, then will discuss an analysis of STP in the lab. 

## Notes

**QUESTION**: Why is Redundancy so important in networks

- Modern networks are expected to be up 24/7/365
- There has to be little to no downtime of the network
- Most PC's only have a single NIC card, so they can only be plugged into one switch, this is a limit on redundancy, as if the connected switch goes down - that PC loses connectivity. Servers on the other hand, can have multiple NIC's which can support better redundancy

**CONCLUSION**: Most modern networks require 24/7/365 uptime, if one link were to fail, then this would be a massive problem, therefore, redundancy is pivotal. Since PCs only have a singular NIC connecting to one switch, if that switch were to go down, there are no redundant measures, therefore connectivity can be lost. Servers have multiple NICs so no issue

**QUESTION**: What is a Broadcast Storm:

- A Broadcast Storm occurs when a broadcast frame is continuously flooded out all interfaces of switches connected to each other
- Since Ethernet headers do not have a TTL field, like IPv4 Headers, then these frames will circulate the network forever, causing significant congestion
- This also causes continuous updating of the switches MAC address table, since the switch 'learns' the MAC address of one device, then receives another frame, then re-learns it all over again. This is known as MAC address flapping

**CONCLUSION**: Broadcast storms occur when Broadcast traffic is continuously looped and propagated between switches and devices indefinitely, causing severe network congestions


**QUESTION**: What is Spanning Tree Protocol

- Spanning tree is 802.1D
- STP prevents these layer 2 loops, by placing redundant ports in a blocked state, very similar to disabling an interface on a router
- If the currently forwarding interface fails, these interfaces act as a backup
- If a interface is in a blocking state, then it won't send and receive frames like a normal interface, it will only send or receive STP traffic called BDPU's on Bridge Protocol Data Units
- *"By selecting what ports are forwarding and what ports are blocking, STP creates a single path to/from each point in the network. This prevents Layer 2 loops*

**CONCLUSION**: Spanning Tree protocol aims to prevent against broadcast storms by intelligently determining a link that can be placed in a blocked state, therefore preventing a loop. 


**QUESTION**: What is the root bridge, and why are all interfaces in a forwarding state

- The root bridge acts as the master switch and ensures that there are no layer two loops in the topology <??>
- Switch with the lowest bridge ID = Root Bridge, then lowest MAC if there is a tie
- A designated port = forwarding state

**CONCLUSION**: The root bridge acts as a central reference point for all blocked versus forwarding configuration on a switch. By default all interfaces on a root bridge are designated ports, and calculations are made based off of that to determine which interfaces in a network can be blocked


**QUESTION:** What is PVST (Cisco Switches)

- Per-VLAN Spanning Tree is a whole new instance of STP per VLAN. Therefore, in each VLAN different interfaces may be blocking and forwarding compared to another

**CONCLUSION**: PVST is Cisco's way of setting up Spanning Tree for each individual VLAN


**QUESTION**: Discuss Spanning Tree Steps

1. Switch with lowest Bridge ID is elected as root port. All interfaces on this switch will be in a forwarding state. If Bridge ID is equal, then lowest MAC will be used.
2. Each other switch will elect one root port, in a forwarding state. Lowest Root Cost = Root port (See below table for root costs). REMEMBER: Add Root Cost of incoming interfaces as well as sending interface.
3. Note, all ports across from a root port will also be designated ports
4. Each remaining collision domain (link) will select a designated port. The other port will be blocking. Lowest Root Cost or Lowest Bridge ID to compare

**CONCLUSION:** The process of calculating which ports should be in a blocked state versus a forwarded state must be conducted by firstly determining a root bridge, then all ports connected to that bridge being assigned as designated ports. For all other links, the lowest root cost from the Root Bridge, will be the desingated port. All other interfaces must be in a non-designated or blocked state

## Lab

**Instructions**

*TURN OFF LINK LIGHTS IN PACKET TRACER FOR THIS LAB*

Options > Preferences > Show Link Lights

Which switch is the root bridge?

Identify the role (root/designated/non-designated) of each switch port:

SW1 F0/1:    F0/2:    F0/3:    F0/4:

SW2 F0/1:    F0/2:    F0/3:    G0/1:

SW3 F0/1:    F0/2:    F0/3:    G0/1:

SW4 G0/1:    G0/2:

Confirm your answers in the CLI (watch the video to learn how to do this)

**Topology**

<img width="992" height="395" alt="image" src="https://github.com/user-attachments/assets/d7de3097-536e-4e0a-8907-997187e923ef" />

So to follow our process, we need to identify the root bridge. Looking at the Priority ID, it is obvious that Switch 3's Bridge Priority is lowest at 24577. So SW3 will be the root bridge.

2. Now that we have identified the root bridge, we now know that all interfaces on the root bridge must be designated ports. So this includes F0/1, F0/2, F0/3 and G0/1.

Next to find the designated ports within the rest of the network. 

SW4's G0/2 will be a designated port, since it is connected to the root bridge with G0/1 being a designated port, so that one is easy enough. 

SW1's F0/3 and F0/3 interfaces will take a bit more work. Since, root cost, bridge ID and MAC address are all the same, it will come down to neighbour bridge ID, in this case F0/4 is lowest, since the neighbouring bridge ID is equal for SW3 but the lowest port ID is F0/1, F0/4 is our designated port. This means that F0/3 is non-designated

SW2 gets a bit tricky. F0/3 seems like the obvious choice for the root port, however, if you calculate the root cost of F0/3, it equals 19. But if you calculate the root cost of SW2's G0/2 interface it only is 8, therefore that is the root port and F0/3 becomes non-designated.  

Finally, for SW1's F0/1 and F0/2 interfaces and SW2's F0/1 and F0/2. Here we have to calculate the lowest root cost. In this case from G0/2 and G01 of SW4, has a root cost of 8, which is much lower than using the FastEthernet root costs, therefore both F0/1 and F0/2 on SW2 will both be designated ports and F0/1 and F0/2 on SW1 will be non-designated. 

Now to confirm via the CLI

_SW3 Root Bridge Confirmation_

<img width="1289" height="623" alt="image" src="https://github.com/user-attachments/assets/523fa01b-8f66-4713-8135-9a6d7568d2e2" />

_SW1 Verification_

<img width="1311" height="634" alt="image" src="https://github.com/user-attachments/assets/3483c95f-30a7-49ba-991a-68e040ca9ad6" />

_SW2 Verification_

<img width="1137" height="648" alt="image" src="https://github.com/user-attachments/assets/182c7e06-298b-4794-ac80-2f9e181baef6" />

_SW4 Verification_

<img width="1280" height="571" alt="image" src="https://github.com/user-attachments/assets/a26402f8-cf00-4e84-a314-6f36744dceb0" />
