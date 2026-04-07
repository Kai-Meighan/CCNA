# Day 12 - The Life of a Packet

Today's lesson was relatively straightforward. It did not introduce any new concepts, rather put toghether older ones across layer 2 and 3. I will explain the process of a packet moving from PC1 to PC4, and the reverse, without looking at my notes, in an attempt to practice the Feynman Technique. The only thing I will allow myself to look as it the below topolgy to remember all related components. 

## Feynman Technique

Here is the topology we will discuss

<img width="1681" height="763" alt="image" src="https://github.com/user-attachments/assets/dc454135-39ad-4405-8c42-cf9966b599c7" />

So there is some main principles here that we will commonly discuss. Firstly we are operating off of the assumption that all static routes have been configured and no device knows any other device's MAC addresses.

That will be a key point here as there is a lot of ARP requests and replies made between the devices.

Also assume the route we will take will be from PC1 -> SW1 -> R1 -> R2 -> R4 -> SW4 -> PC4 and vice versa.

Firstly, PC1 wants to send a packet to PC4, but it does not know the default gateways MAC address. So it prepares an ARP request stating 'who is 192.168.1.25'. This is forwarded via the switch to R1. Here R1 replies to this ARP request and says 'I am 192.168.1.254 and my MAC address is aaaa'. 

During this process SW1 g0/1 and g0/0 interfaces will also 'learn' the MAC addresses of its connected devices and add to its MAC address table. 

Now that PC1 knows the MAC address of R1, it prepares a packet that is encapsulated by an Ethernet frame and sends to R1. 

R1 decapsulates the packet and views the destination IP address where the packet is targeted to go. It looks up its route table, and since static routes are already configured, it notices that it should forward the packet to R2's g0/0 interface on 192.168.12.2.

However, same problem again, R1 does not know R2's MAC address. So it sends out an ARP request out of its g0/0 interface saying 'who is 192.168.12.2'. R2 will receive the frame and respond with an ARP reply of 'I am 192.168.12.2 and my MAC address is cccc'.

Now R1 will encapsulate the packet in an Ethernet frame and send to R2. R2 will decapsulate the packet, read the source IP address and lookup its route table. It will notice that it is to forward the packet to R4's g0/1 interface on 192.168.24.4.

Once again, R2 does not know R4's MAC address. So it will prepare an ARP request saying 'who is 192.168.24.4' and send it out of its g0/1 interface. R4 will receive this frame and response with 'I am 192.168.24.4 and my MAC address is eeee'.

R2 will prepare the ethernet frame which encapsulates the packet containing the same source IP and destination IP as it was at PC1.

R4 will decapsulate the frame, read the destination IP address and look up its route table. It will see that it has a connected route as the most specific route in the 192.168.4.0 network. 

One more time however, R4 does not know PC4's MAC address, so it will send out an ARP request out of its g0/2 interface to all connected devices (in this case just SW4) saying 'who is 192.168.4.1' and PC4 will respond saying 'I am 192.168.4.1 and my MAC address is 4444. 

Now R4 will encapsulate the packet in an ethernet frame and send directly PC4 via SW4 using PC4's newly discovered MAC address. PC4 now has received the packet from PC1. 

In the response, the major difference will be that there will be no need for all of the ARP requests and reply's as all devices (outside of R3) now know eachother MAC address, so the packet can just be encapsulated and sent.

# Lab
Note the lab today was just viewing this process in packet tracer's simulation mode. So I will not be doing any documentation for this.
