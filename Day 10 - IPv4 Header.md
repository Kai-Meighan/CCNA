# Day 10 - IPv4 Headers

Today's session covered the contents of an IPv4 Header, going through and explaning what each component was for. Today will be slightly different, I will try to recall how many components I can from the IPv4 Header to start but will inevitably end up looking at my notes to confirm. I will also run a sample Wireshark capture of a simple ping request I did to observe all relevant IPv4 Header Fields.

## Feynman Technique
**Version (4 Bits)** - Indicates if the IP header is IPv4 (0100) or IPv6 (0110)

**Internet Header Length (4 Bits)** - Indicates how long the IP header is, not including the encapsulated packet

**Differentiated Services Code Point (6 Bits)** - Used for Quality of Service (QoS). Prioritises traffic like video, voice and streaming

**Explicit Congestion Notification (2 Bits)** - Used to indicate if there is a congestion on the network

**Total Length (16 Bits)** - Length of the IP Header + Encasulated Data

**Identification (16 Bits)** - Identifies which packet a fragment belongs to

**Flags (3 Bits)** - There are three bits. Bit 0 is always reserved and set to 0. Bit 1 is called Don't Fragment and is set to 0 if the packet has not been fragmented and set to 1 if it has. Bit 2 is the More Fragments bit, and is set to 1 if there are more fragments coming as part of the packet and 0 if it is the last fragment

**Fragment Offset (13 Bits)** - Indicates where in the packet the fragment belongs. Used to reassemble the packet in order

**Time to Live (8 Bits)**  - This is used to prevent infinite loops where a packet keeps hopping between routers. Every time a packet reaches a router, this value is decreased by 1

**Protocol  (8 Bits)** - This value indicates the protocol of the encapsulated L4 segment. Common values are TCP (6), UDP (17), ICMP (1) and OSPF (89)

**Header Checksum (16 Bits)** - This value is used to detect any errors in the IP Header. The router will calculate a checksum of the packet and compare against this value. If they are different, the router will drop the packet

**Source Address (32 Bits)** - Indicates where the packet is coming from

**Destination Address (32 Bits)** - Indicates the receiver of the packet

**Options (0-320 Bits)** - Rarely Used

## Personal Wireshark Lab
Below is a simple packet capture of a ping request to Google's DNS Servers (8.8.8.8). 

<img width="1430" height="362" alt="image" src="https://github.com/user-attachments/assets/29d00158-192f-4d32-8173-c03a9662e583" />

As you can see, the **version** field indicates that we are using IPv4.

The **header** field is set to the minimum value of 5, as we did not use any options in this header. 

Both the **differentiated services codepoint** and the **explicit congestion notification** fields are set to 0, as there is no traffic being prioritised here and there is no network congestion.

The **total length** is 60, which is IP header + encapsulated data

The **identification** flag is not super necessary here as the packet is under the MTU limit of 1500 bytes and does not need to be fragmented. 

All **flag** values have been set to 0 as this packet has not been fragemented and hence, the last fragment (and only) of the packet

**TTL** is set to 128, the **protocol** is obviously ICMP because we are using the 'ping' command.

**Header checksum** is not being used here. 

**Source IP** is my IP address and **destination IP** is Google's DNS Servers (8.8.8.8)
