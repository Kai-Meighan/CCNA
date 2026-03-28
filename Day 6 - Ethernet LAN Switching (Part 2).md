# Day 6 - Ethernet LAN Switching (Part 2) 

Today's session wrapped up Ethernet LAN switching by introducing two important protocols ARP and ICMP. 

## Feynman Method
Firstly, before talking about ARP. Let's briefly touch on a few important characteristics on Ethernet frames. An Ethernet frame has to be at least 64 bytes in length, this is inclusive of the header, data and trailer. The header and the trailer are always 18 bytes. If the data or payload is less than 46 bytes, then it will use 0's to pad the data up to the minimum of 46 bytes required for a payload.

Also, remember how within the TCP/IP model will go down the layers, gaining more information from the upper layers, until it reaches the physical layer. Within the data for the Ethernet frame, the source IP and destination IP addresses will be encapsulated within. This unfortunately does not allow us to just use an IP address to direct the frame to the relevant recipient, as switches are layer 2 devices and cannot comprehend IP addresses.

Therefore, we need a way in which a device can find out another devices MAC address that is located on the same LAN. This is where ARP comes in. **ARP or Address Resolution Protocol** is used for the discovery of the layer 2 address of a known layer 3 address. In simple terms and very similar to our example above, we have the IP address, but now we need the MAC address to forward it to the destination within our LAN.

The ARP protocol is made of two components, **an ARP request and an ARP reply**. An ARP request is essentially saying, "who is 192.168.1.2", then in theory the device who has that IP address will send back their MAC address in a reply, saying "Hey, I am 192.168.1.2, here is my MAC address."

Since the source device and the switch do not know who to send this initial request to, it is broadcasted to all devices on the network, except the source. This is known as a Broadcast Frame. Contrasted to a Unicast frame, which is designated for one person.

Next in our sequence of events, all devices will have now received the ARP request. Devices that have read the request and have seen that the identified IP address does not match their own, simply drop the packet. But the intended recipient, who sees that they have got the IP address that is being looked for, will respond with an ARP reply, which includes their MAC address. 

As the switch sees this ARP reply, it now knows that the MAC address belongs to the recipient, so what it does is store that address its own MAC address table. This is used now to set up unicast communication between devices, as it can forward traffic to the appropriate device, instead of always having to send broadcast frames. Furthermore, on the initial sender device, they will also store the output of the ARP reply on their own device in what's known as an ARP table. This can be viewed on Windows through the following command 'arp -a'

This is the basic method of how devices find out eachother's MAC addresses.

Now let's move on to **ICMP**. ICMP or Internet Control Message Protocol is used to test network reachability between two devices. If a device wants to know if it can reach another device, it will send a ping request with that devices IP address. Generally, on Windows, pings will generate four ICMP echo requests, which essentially prompt the device if it is reachable. If the device is reached, it will reply within a ICMP echo reply. The results of these four pings will be outputted to the user, describing the roundtrip time between ICMP Echo Requests and Replies.

## Lab
The instructions of this lab were as follows:
Both switches have an empty MAC address table, and all PCs have an empty ARP table.

1. If PC1 pings to PC3, what messages will be sent over the network, 
     and which devices will receive them?

2. Send the ping and use Packet Tracer's 'simulation mode' to verify your answer.

3. Use pings to generate network traffic and allow the switches to learn the MAC addresses 
     of all PCs on the network.

4. Use 'show' commands on the switches to identify the MAC address of each PC.

5. Clear the dynamic MAC addresses from the MAC address table of each switch.

In order to answer question 1, we will look at ARP first. If, as the instructions say, we assume that all PCs have an empty ARP table and the switches have empty MAC address tables, then we can conclude that no one knows where anyone is on the LAN. So firstly, PC1 will send an ARP request to SW1, from here SW1, will broadcast that ARP request to all devices on the network. PC2 and PC4 will dropp the frame as they realise that it is not intended for them. PC3 however, will realise that the ARP request is meant for it. It will then send a ARP Reply back to PC1 via SW1 and SW2. Now PC1 has a record of PC3's MAC address in its ARP table and SW1 and SW2, have a record of PC3's MAC address stored in their respective MAC address tables. 
Now PC1 and the two switches know exactly where to forward the ICMP traffic to. Below, I have detailed this in packet tracer to answer question 2. 

**Initial Ping Command**

<img width="1211" height="156" alt="image" src="https://github.com/user-attachments/assets/ff0b136d-2d12-4cca-9c28-1e609b4467cd" />

**ICMP + ARP Entry**

<img width="501" height="423" alt="image" src="https://github.com/user-attachments/assets/2723bab7-dad9-43a5-87ca-8000aa764076" />

**ARP Request Broadcasted to all devices on the LAN**

<img width="912" height="428" alt="image" src="https://github.com/user-attachments/assets/ea665b51-8a46-4895-b03d-49a0aa3e8d06" />

**ARP Frame showing Broadcast FFFF.FFFF.FFFF**

<img width="878" height="674" alt="image" src="https://github.com/user-attachments/assets/6c8acf08-8f5b-4a75-b4da-8894b8ef795c" />

**PC3 will respond with ARP reply with its own MAC address**

<img width="872" height="775" alt="image" src="https://github.com/user-attachments/assets/6a6b3db4-ae21-44aa-928a-c873e5c140b8" />

**ARP Reply from PC1**

<img width="630" height="380" alt="image" src="https://github.com/user-attachments/assets/5da291d3-f349-4e4f-ba07-08eba2121ac1" />

**PC1 now knows PC3's MAC address**

<img width="875" height="743" alt="image" src="https://github.com/user-attachments/assets/de25d590-ec51-4d64-950e-42427e232ce5" />

**ICMP Echo Request and Reply**

<img width="873" height="776" alt="image" src="https://github.com/user-attachments/assets/73333023-f271-41cd-b112-e765b6cc18ac" />

**For question 3, a similar process was done for the switches to learn the MAC addresses of PC2 and PC4.**

<img width="782" height="246" alt="image" src="https://github.com/user-attachments/assets/869df6c2-5912-45f3-a8a1-3990dd215cbe" />

**Both SW and SW2 now know that**

PC1 - 00d0.d3ad.9cab

PC2 - 0060.5c56.14d3

PC3 - 0004.9a6e.d870

PC4 - 0001.647b.3119



Finally, to clear the dynamic MAC address table from each switch run the following command 'clear mac address-table dynamic'.
<img width="762" height="349" alt="image" src="https://github.com/user-attachments/assets/27a4c29c-fba1-4640-b36e-6364d8fcd510" />
