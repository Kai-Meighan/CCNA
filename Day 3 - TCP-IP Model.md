# Day 3 - TCP/IP Model 

Day 3 of the CCNA lectures introduced the TCP/IP Model and layered models in general in order to demonstrate how data moves through a network from one device to another and the protocols that dicate the rules between this communication and movement. As always, in order to try an reaffirm my concepts, I'll teach the model 'Feynman-Technique Style'.

## Feynman Technique

What are the TCP/IP Layers, what is the function of each layer and common protocols at each
As mentioned above the TCP/IP model is a illustration of how data moves through a Network, between devices. Below I will go through each layer and explain their role in this process

**Application Layer**

The application layer focuses on protocols of communication between applications and how to create and interpret the data they send to eachother. For example, HTTP is used between two applications in order to create and properly structure web pages, or SMTP is used to coordinate the appropriate structuring of email messaging.
Common protocols you would find here include HTTP, FTP and SMTP

**Transport Layer**

The transport layer focuses on establishing where data should sent to _on_ the receiving device. For example, say a server is running both a web service and a file transfer service, the transport layer's job is to coordinate which service the data is sent to. It does this through the use of port numbers. In our example, the web service would typically use either port 80 or 443 (HTTP or HTTPS) and the file service would potentially utilise port 21 (FTP).
Common protocols used here include TCP and UDP

**Network/Internet Layer**

In the lecture this was referred to as the Internet layer but from years of referencing the OSI model, this is burnt into my brain as the Network Layer. The role of this layer is to correctly address the message that is being sent to the correct destination. For example if PC1 is looking to send a message to SRV1, the network layer will utilise IP addresses to ensure that the message is appropriately addressed to he correct place. 
Common protocols used here include Internet Protocol (IP) and Internet Message Control Protocol (ICMP)

**Data Link Layer**
The data link layer is focused on sending the message to the next hop, on the messages way to the recipient. For example, PC1, sending a message to Router1 via a switch, that is an example of the message being transferred to the next hop. The Data Link layer will repeat this process until the message reaches the specified location as defined by the IP address. 
Common protocols used here are Ethernet and Wi-Fi

**Physical Layer**

Finally, the physical layer is the actual medium in which data is sent over in bits format across a wire. 
Common cabling used here includes Copper-Cable UTP for electrical signals, fibre-optic for optical signals and radio transmission for wireless signals.  

**What is encapsulation and decapsulation**

Encapsulation refers the process of information being added to data as it moves down the TCP/IP stack. This is where each layer services the layer beneath it. For example, once the data is prepared at the application layer, it needs to have a port number to direct it to on the recipient server, therefore a layer 4 header with this information is appended to the data prepared in the level above. Or for example, once the IP address header is added to create the packet at the Network layer, it then needs to know the address of the next hop. For this, the Data Link layer adds a layer 2 header and trailer to the packet creating a frame, and directing that frame to the next hop. 

Decapsulation is the reverse of this process, once a frame is recieved over the physical medium, it is then progressively stripped of these headers that provide information about how the message is intended to be received. For example, as the packet reaches the Transport Layer, it needs to know what port to send the message to on the recipient server. It reads the layer 4 header and for example, it may be referencing port 80. Therefore, the segment/datagram knows that it is likely to be sent to a web server. 

This process of encapsulation and decapsulation occurs during every time two devices communicate over a network to eachother. 

**What is the name given at each stage of the encapsulation/decapsulation process**

At each layer the Protocol Data Uni (PDU) is given a specific name to reference its state at each layer. Below are the three names and corresponding layers associated.

- Layer 4 (Transport) - Segment(TCP)/Datagram (UDP)

- Layer 3 (Network) - Packet

- Layer 2 (Data Link) - Frame



## Lab

Today's lab was rather simple. A network was already constructed and it was our job to use Packet Tracer's Simulation feature to analyse data at different TCP/IP layers. Here were the official instructions: 

1. Use 'simulation mode' to analyze the various traffic being sent throughout the network.
    What layers of the OSI model are being used?

2. Release and renew PC1's IP adress to generate some Layer 7 traffic.
    Analyze the traffic with simulation mode.

This here was the initial network
<img width="821" height="409" alt="image" src="https://github.com/user-attachments/assets/658fc4c1-e352-421a-9e56-8227cde8329c" />

Clicking through each step in the simulation we can analyse packets at different layers. For example at Layer 2, we have communication using Spanning Tree Protocol (STP) 
<img width="728" height="583" alt="image" src="https://github.com/user-attachments/assets/8d97f93b-b47f-4307-9089-52de88ed11b8" />

We can see the encapsulation process as the Ethernet Header and Trailer is applied in order to create an Ethernet Frame, then moving to the physical layer, where the frame was sent out over the Ethernet connection

Another example involved releasing then renewing the IP address assigned by DHCP. To do this, we used the ipconfig /release and ipconfig /renew commands. That created the following outputs in simulation mode. 
<img width="726" height="660" alt="image" src="https://github.com/user-attachments/assets/16713626-070e-48c5-bb2a-f6597b4704ee" />

This time we can see activity at Layer 7, or the application layer in our TCP/IP model. We can see how our command has cause a DHCP discover command to be sent out in order to allocate a new IP address to the device. Then systematically, we can analyse the movement of the data down the layers from Layer 7, to Layer 4 to port 68 (UDP port for DHCP), then continuing down the layers. To validate we can look at the last DHCP frame in this sequence
<img width="736" height="734" alt="image" src="https://github.com/user-attachments/assets/fd1c20a8-43e6-42ce-b903-4322214a7528" />

And can see that the DHCP client has correctly recieved the IP address allocated to it. 
<img width="841" height="392" alt="image" src="https://github.com/user-attachments/assets/c97021f7-80c0-4f24-b9e0-30ad6377011c" />




