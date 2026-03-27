# Day 5 - Ethernet LAN Switching (Part 1)

Today's session was theory heavy and mainly focused on what is in a Ethernet Header and Trailer and the process of devices communicating with eachother in the same LAN. 

## Feynman Method
For starters, a LAN is just a network contained in a relatively small area. It is the role of a router to connect these LANs together. 

The main protocol used at Layer 2 (Data Link Layer) is Ethernet. Ethernet is used to define communication between devices within a LAN. Within an Ethernet frame there is the header, the data, and the trailer. 

**Ethernet Header and Trailer**

The Ethernet Header is made up of five components
1. Preamble - The main goal of the preamble to is synchronise the clock of the receiving device. It does this by sending 7 bytes of alternative 1's and 0's i.e. 10101010. 
2. Start Frame Delimeter - The start frame delimeter aims to indicate where the end of the preamble is. It is only 1 byte and it looks like this 10101011. The last 1 indicates that the preamble is complete
3. Source Address - The source address is a 6 byte MAC address that indicates where the frame came from. We will discuss what a MAC address is below
4. Destination Address - The desination address is a 6 byte MAC address that indicates where the frame is headed to.
5. Type/Length - This flag has a dual function, if the value is set to under 1500, then it specifies the length of the Ethernet frame. However, if the value is over 1536, it will specify whether the type of the header is IPv4 or IPv6. This value is 2 bytes in lenght

There is only one component of an Ethernet Trailer which is called the Frame Check Sequence (FCS). The purpose of this is to detect for any corrupted data after the frame has been sent. It uses a 'Cyclic Redundancy Check' algorithm to do this. Specifics of the CRC algorithm are not necessary for the CCNA.


**What is a MAC address**

We touch on it earlier but a MAC address is a physical address that is unique to every hardware device. It is 48 bits in length (6 bytes) and is 'burned into' every device, meaning it cannot change. There are two components to the MAC address; the first three bytes represent the OUI or Organisation Unique Identifier. This refers to the organisation who created the device i.e. Cisco, Dell etc. and they will mark the first three bits with the same hexidecimal numbers across all of their products. The last three bits are unique to the device itself and act as a way to identify it.


**How frames are sent over a LAN**

Take this image as a example scenario. 

<img width="1604" height="756" alt="image" src="https://github.com/user-attachments/assets/94944aca-12ed-4466-81d1-73bd88c8e3d1" />

If PC1 wants to communicate with PC2, they will do so via the switch. PC1 will first send it back to the F0/1 interface of SW1. The switch contains a MAC address table, this essentially is a guide for the switch to understand who to forward frames to. By PC1 sending a frame destined for PC2 throguh the switch, the switch configures what is called a Dynamic MAC address entry within its MAC address table. This just means that the switch 'learned' that PC1's MAC address was AAAA.AA.00.0001, instead of it being statically configured. 

Now that the switch has the frame and has learned that PC1 resides at MAC address AAAA.AA00.0001, it has a problem. It does not know where PC2 resides.

<img width="1616" height="775" alt="image" src="https://github.com/user-attachments/assets/535ebf61-6ec6-49c7-9f6a-45a6a788aaff" />

In this scenario, where PC2's MAC address is not present on the switches' MAC address table, it is called a Unknown Unicast Frame. A Unicast frame is just the name for a frame that is sent to just one target. 

In this event the switch has to perform a flood to all hosts that it is connected to. This means that the frame is sent to everyone. Now, PC3 will read the destination address of the frame and release that it is not destined for them, therefore it will drop it. But PC2 will now be able to receive the frame.

On the reverse, if PC2 wants to send information back to PC1, it will reply to the switch. This time the switch will dynamically learn the MAC address of PC2 now, similar to what it did in PC1. The MAC address of PC1 is already known in the switches MAC address table therefore, the swtich directly forwards the packet to PC1. This is known as a 'Known Unicast Frame'

<img width="1645" height="797" alt="image" src="https://github.com/user-attachments/assets/894a13b7-a95a-49a8-b542-838f2c927cb8" />

Note, if the device has sent no activity within 5 minutes, its entry will be cleared from the MAC address table on the switch
