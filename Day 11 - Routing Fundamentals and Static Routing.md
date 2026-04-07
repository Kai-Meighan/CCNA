# Day 11 - Routing Fundamentals and Static Routing

Today, over two parts, we covered routing fundamentals looking at local and connected routes and then static routing, looking at how routers know where to send packets when the destination is not in their route table. As always, I'll go through the subjects and teach it using the Feynman Technique.

## Feynman Technique
**What is the function of a router**

The function of a router is to forward packets outside of your local network. This is how two separate local area networks can communicate with one another over a large geographical distance. This briefly touches on the itnroduction of WANs or Wide Area Networks, which are just networks that span over a large geographical distance. 

**How do routers know where to route**

Routers know where to forward packets to by keeping a route table saved locally on the device. This is not to dissimilar to a MAC address table that is located on a switch, but this operates at layer using IP addresses. 

**Dynamic vs Static Routing**

There is two types of methods in which routers 'learn' or adopt routes to know where to forward packets to. There is:
- **Dynamic Routing**: Which is where the routers 'learn' routes off of other routers. THis is where protocols such as OSPF come in, but that it to be covered later in the course. 
- **Static Routing:** This is the type of routing that we are concerned with in this lecture. It is where an network engineer or administrator will manually configure the router with the route a packet should be forwarded to, on its way to its final destination. 

**Local Routes and Connected Routes**

When a router's interface is assigned a route. There are two main ones that we are concerned with when it comes to static routing. There is:
- **Connected Routes:** This refers to the network that the router is connected to. For example, this could be the edge router and its connected office network with PCs, Printers and Servers. A connected route is usually denoted with a /24 netmask in the route table of the router. This may look something like '192.168.1.0 /24'. This essentially means that the packet is destined for a device on the connected network.
- **Local Routes:** This refers to when a packet is directly destined for the router itself, this is usually denoted with a /32 netmask. For example, 192.168.1.1 /32, this only refers to once device, in this case the router, so it knows not to forward the packet on to any other device. 

You may be thinking, but 192.168.1.1/32 is apart of the 192.168.1.0/24 network, and you'd be correct. When a router is looking for where to route the packet and is faced with this scenario where multiple routes may apply, it chooses the **most specific route**. In this case, there are 256 possible addresses on the 192.168.1.0 /24 network, whereas there is only 1 within the 192.168.1.1 /32 address, therefore it must choose 192.168.1.1 /32 as it is the most specific. 

When a router doesn't know where to forward a packet as its destination is not in its route table, it simply drops the packet. This differs from the behaviour of a switch. If a switch didn't know the MAC address of the destination device, it would flood the network to figure out who has the MAC address it is looking for, a router does not behave in this way. 

**What is the problem static routing looks to solve**

By default, routers do not know where to forward packets to. As mentioned above, there are two ways of configuring these routes, static routing and dynamic routing. We will cover dynamic routing a bit later, but static routing aims to solve this problem by manually configuring a routing path that a router can forward packets across in order to reach a pre-determined destination

For example, in the following topology, network engineers need to manually configure a routing path for PC1 to communicate with PC4

<img width="2357" height="520" alt="image" src="https://github.com/user-attachments/assets/4b12458b-d181-4e52-a425-7ff7a7b46300" />

This can be done via static routing with a network engineer configuring R1 to forward packets to R3, then to R4 then to PC4 if PC1 wants to communicate with it. In the lab, we will go through this process in detail with exact commands shown. 

**What is a default gateway**

A default gateway is another term for a router. It can be thought of as a gateway to outside of your local network out into the world. 

**What is a default route**

A default route is often used to denote the Internet, and is often represented as 0.0.0.0/0. The way that this address is laid out means that it encompassess all IPv4 addresses and is therefore the least-specific possible route. This means that if there is no other route in a router's route table, the default route will be able to be leveraged to send the packet out to the Internetn

**What is two-way reachability**

Finally, if PC1 can talk to PC4 and wants to send say a ICMP echo request. If the reverse of the static routes have not been configured to allow PC4 to communicate with PC1, the ICMP echo reply, will not be sent back. This means that whenever a network engineer or administrator wants to allow two devices in separate networks to communicate, two-way reachability is a critical design consideration. 


## Lab (Part 1)

**Topology**

<img width="761" height="293" alt="image" src="https://github.com/user-attachments/assets/1616fa07-b238-47ce-a654-26904d904f0b" />

**Instructions**
All devices have NO pre-configurations:

1. Configure the PCs and routers according to the network diagram (hostnames, IP addresses, etc.)
    Remember to configure the gateway on the PCs.
    (You don't have to configure the switches)

2. Configure static routes on the routers to enable PC1 to successfully ping PC2.

Ok first things first. Hostnames and IP addresses. 

_PC1_

<img width="1662" height="217" alt="image" src="https://github.com/user-attachments/assets/8039b336-0da3-4b83-8bb0-e5592c137377" />

PC2

<img width="1648" height="303" alt="image" src="https://github.com/user-attachments/assets/80977e88-58de-4f69-a097-b775ba7f7375" />

_R1 G0/1 Interface_

<img width="902" height="124" alt="image" src="https://github.com/user-attachments/assets/a3e3f27f-2424-4bb2-b08e-d24fd43385a6" />

_R1 G0/0 Interface_

<img width="861" height="95" alt="image" src="https://github.com/user-attachments/assets/924309d5-0683-4593-ba00-c3ee85491353" />

_R2 G0/0 Interface_

<img width="876" height="70" alt="image" src="https://github.com/user-attachments/assets/7d08efa8-3c88-4fca-a1db-cc1e1d946b95" />

_R2 G0/1 Interface_

<img width="901" height="98" alt="image" src="https://github.com/user-attachments/assets/f5dbf2a4-0c19-45da-af0b-55883d2b3b45" />

_R3 G0/0 Interface_

<img width="888" height="64" alt="image" src="https://github.com/user-attachments/assets/4c700137-e0aa-4bbc-935e-263a059137a3" />

_R3 0/1 Interface_

<img width="875" height="60" alt="image" src="https://github.com/user-attachments/assets/8be1cf04-73aa-42a3-916e-90d530cd3526" />

Note: all interfaces were configured with a no shutdown command. I may or may not have forget to put it in and gone back and done it later :)

Next we have to configure static routes on the routers to allow for communication between PC1 and PC2. The way I'll do this is to forward any packets destined to PC2 from PC1 first from R1 to R2, then from R2 to R3. Ensuring we also do the reverse to ensure two way reachability. 

<img width="998" height="126" alt="image" src="https://github.com/user-attachments/assets/326d4939-ab25-48d5-9020-2a7160faaf4d" />


Verification on R1 route table: 

<img width="1123" height="100" alt="image" src="https://github.com/user-attachments/assets/68c2f49c-41fe-4efa-892c-84a56d898449" />

Now onto R2

<img width="1106" height="75" alt="image" src="https://github.com/user-attachments/assets/7bde12a7-1fec-4bf7-86cc-3e33e77ea8dd" />


I also ensured two way reachability by doing the reverse in order for PC2 to be able to communicate with PC1

Now to test reachability 

_From PC1 to PC2_

<img width="919" height="440" alt="image" src="https://github.com/user-attachments/assets/585e1249-a32e-4f47-aa86-63fc0484beb2" />

_From PC1 to PC2_

<img width="960" height="426" alt="image" src="https://github.com/user-attachments/assets/34a1dd94-ba49-4df6-8d72-1ac049012e0d" />

All is working now with static routes configured, PC1 and PC2 can now communicate with one another. 

## Lab (Part 2) 

## Topology

<img width="761" height="293" alt="image" src="https://github.com/user-attachments/assets/2a68a8d3-23c4-42cd-908a-5ed051779d23" />

## Instructions

PC1 and PC2 are unable to ping eachother.

There is one misconfiguration on each router.

Find and fix the misconfigurations.

You have successfully completed the lab when PC1 and PC2 can ping eachother.

Ok lets start with R1, the first thing I will do is to use the command 'show ip interface brief' to check that all interfaces are up

<img width="979" height="275" alt="image" src="https://github.com/user-attachments/assets/3410d33d-b801-46e6-b7ac-a305451ddf1d" />

So they are, and I can see that the IP addresses match the topology so its not that. Lets look at the  route table

<img width="1112" height="138" alt="image" src="https://github.com/user-attachments/assets/f7003361-0734-4851-b1a9-54635b4f70f8" />

Here's the mistake. The next hop IP address has been set to 192.168.12.3, not 192.168.12.2, like in the topology. I will use the command 'no ip route <route>' to delete that and put in the correct one.

<img width="1142" height="267" alt="image" src="https://github.com/user-attachments/assets/cd0f1ff7-54f1-4d11-b0ab-a5ca7249ea05" />

That should be that one fixed, now onto R2. We will follow the same process as R1 to make sure all interfaces are administratively up.

<img width="1350" height="205" alt="image" src="https://github.com/user-attachments/assets/0698712e-dbb5-4335-b888-7a634613935e" />

Which they are, but I have already spotted the problem. Both g0/0 and g0/1 have been assigned the same IP address. Lets change that by configuring the g0/0 interface with the correct IP address

<img width="1376" height="217" alt="image" src="https://github.com/user-attachments/assets/381676f6-3565-4347-aab5-bc9a79bdb95a" />

That should work a bit better. Now finally, to R3. Same process again

<img width="1353" height="212" alt="image" src="https://github.com/user-attachments/assets/bffae283-7afe-4fc1-a692-d610924488bd" />

Both interfaces are up, but the g0/0 IP address is wrong, it should be 192.168.13.3. Let's fix that like the last one. 

<img width="1336" height="216" alt="image" src="https://github.com/user-attachments/assets/24978e31-e821-48de-b61e-954e120bb36c" />

Now lets check to see if that solved all problems with PC1 reaching PC2 or if there are more problems waiting to be found. 

_PC1 to PC2_
No luck.

<img width="770" height="282" alt="image" src="https://github.com/user-attachments/assets/f0fc89f3-e806-4d71-9484-4d66de7a3cac" />


In investigating R2's route table the entry for packets from PC1 to PC2 looks funny, so let me rewrite that

<img width="1086" height="196" alt="image" src="https://github.com/user-attachments/assets/73292c3c-1f4e-4d7a-a803-9e102a61a8be" />

<img width="1127" height="235" alt="image" src="https://github.com/user-attachments/assets/3cb6592e-f8df-4596-b73a-88b4f8dfeaa2" />


Problem Solved!!

<img width="965" height="413" alt="image" src="https://github.com/user-attachments/assets/6817b034-a666-49b7-8649-0bc519ab3678" />


_PC2 to PC1_

<img width="981" height="459" alt="image" src="https://github.com/user-attachments/assets/38d5fd52-97d4-4a8e-a531-0d92e2e7e6f6" />

Success!! Now the network is fixed and the two devices can now communicate with one another.


