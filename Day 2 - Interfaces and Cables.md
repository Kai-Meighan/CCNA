# Day 2- Interfaces and Cables

Day 2 focused heavily on interfaces and cables. There was a lot of information on the different types of cables, the wiring within them and for what situation each cable would be used.

## Ethernet
The first topic of discussion was **Ethernet**, what is it? Ethernet is just a collection of protocols and standards. 

Without knowing what a protocol is that definition is not very good. A **Protocol** are rules of communication between two devices. Kind of like how humans have rules of communicating by not shouting at eachother or speaking in languages the other does not understand.

So Ethernet is a collection of these rules that dictate how devices communicate over cabling. 

# UTP Cables
In terms of cable we will start with a **UTP cable**. What is a UTP cable you might ask. Let's break down UTP and some of its characteristics.
U = Unshielded
TP = Twisted Pair

<img width="1400" height="933" alt="image" src="https://github.com/user-attachments/assets/d1e003ae-2dbf-4221-afbb-6e07ecf3d519" />

With these cables the fact that they are unshielded means that there is a chance that they are subject to electromagnetic interference, however the twisted nature of the cabling actually helps prevent this. Also an interesting security fact, UTP cables can actually leak signal, meaning that it can actually be read be a malicious attacker.

Next was the introduction of the IEEE standards for ethernet cabling. This is not super relevant in day-to-day life, however I suspect it will be a question or two on the CCNA exam so it may be worth actually remembering it. 

| Speed | Common Name | IEEE Standard | Informal Name | Maximum Length|
|-------|-------------|---------------|---------------|---------------|
|10 Mbps | Ethernet| 802.3i | 10BASE-T | 100m |
|100 Mbps | Fast Ethernet | 802.3u | 100BASE-T | 100m |
|1 Gbps | Gigabit Ethernet | 802.3ab | 1000BASE-T | 100m |
|10 Gbps | 10 Gig Ethernet | 802.3an| 10GBASE-T | 100m |

For both 10BASE-T and 100BASE-T cables, they will only have 2 pairs (4 wires), whereas 1000BASE-T and 10GBASE-T wires will utlise all 8 pins on a RJ-45 connector. The reason for this is that in the 10BASE-T and 100BASE-T cables, there is a transmitting section and a receiving section (each use pins 1 and 2 for transmiting and 3 and 6 for receiving and vice versa for the other side)
This concept is known as Full-Duplex transmission, where both devices are able to send and receive information at the same time therefore they use separate wires for sending and receiving. 

In both 1000BASE-T and 10GBASE-T cables, this is slightly different as there is no transmiting and sending side rather all pins are bi-driectional. 

## Connecting Devices Together
In Connectinng devices together using UTP cables, there are some rules that need to be applied. Connecting a PC, Router or a Firewall to a switch, you would use whats called a 'straight-throguh cable'. This just means that all pins connect to their corresponding pins on the other side (for example 1:1, 2:2 etc)

However, if you want to connect a switch to another switch or a router to another router or PC, then you must use what is called a cross over cable. This essentially crossover opver the connections to the corresponding pins to ensure that there is a correct transmitting end and a correct receiving end (i.e. 1:3, 2:6. If you were to use a straight-through cable in this instance, it would not tranmsit any data.  

## Fiber Optic Cables
Fiber optic cables do not use electricity on a wire to send signal, instead they utilise light. In order to connect to a port or interface on a device they do not use standard RJ45 connectors, instead they use a SFP transceiver. SFP transciever just stands for 'small form factor plugable'. Then the fibre optic cable is attached to this device.

There are two types of fibre optic cable; single mode and multi-mode. Without going into the architectural differences between the two, here are the most important considerations when it comes to actually implementing these cables. 
- Multi-mode has less distance than single mode. Multi mode caps out at around 550m with single mode being able to supporot up to 30km.
- Single mode is generally mroe expensive as a result of the laser-based transcievers that are needed.

Here are some additional standards for fibre-optic

| Informal Name | IEEE Standard | Cable Type | Speed | Maximum Length|
|-------------|---------------|---------------|-------|---------------|
|1000BASE-LX | 802.3z| 1 Gbps | Multi-mode or Single-mode | 550 m (MM) 5KM(SM)
|10GBASE-SR | 802.3ae| 10 Gbps | Multi-mode | 400m
|1000BASE-LX | 802.ae| 10 Gbps | Single-mode | 10KM
|1000BASE-ER | 802.3ae| 10 Gbps |Single-mode | 30KM

# Lab
Today's lab focused on taking the principles learned in the lecture and actually internalising them and implementing them in connecting different devices together.
The instructions are listed below
  Connect the network devices together according to the labels.
  
  Use the appropriate type of cable .
  
  For practice, assume that Auto MDI-X is disabled, or not supported on the devices.
  
  NOTE: Packet Tracer doesn't differentiate between single-mode 
  and multimode fiber, but think about which one is appropriate when you 
  use a fiber connection.
 
The intial setup was as follows:
<img width="1382" height="855" alt="image" src="https://github.com/user-attachments/assets/e7e9f808-5c49-440a-9d2b-e561ad516642" />

I started off by just connecting the PC to switches using straight-through cables as the corresponding pins mapped well to eachother and a cross-over was not necessary

<img width="299" height="198" alt="image" src="https://github.com/user-attachments/assets/181fd7af-6805-4518-851b-feebc165c438" />

Next, we had to connect switches together. This required a cross-over cable to be used in order ensure both devices can send and transmit at the same time without colliding with one another

 <img width="307" height="230" alt="image" src="https://github.com/user-attachments/assets/9cd422a7-3d0d-46b2-bbf7-14eb9499cc99" />

Finally, routers had to be connected together over variable distances. For the shortest distance (50 meters), UTP cross-over cables can be used as it is within the UTP cables range as well as allowing for correct pin layout for transmitting and receiving information.
Next there was a three kilomterre distance that needed to be addressed. The best option here was a fibre optic, but in this case a single-mode fibre optic as it was over the limit of a multi-mode fibre optic cable distance. 
The last router that had to be connected was over a distance of 250 meters. Now, this was outside of the range of a standard UTP cable, however, it can be reached with a fibre optic. Two options were avaiable here, single-mode or multi-mode. Both options would work, but in order to be as cost effective as possible, a multi-mode fibre optic cable should be used to connect R3 and R4

<img width="1122" height="618" alt="image" src="https://github.com/user-attachments/assets/72833be9-d0eb-436e-903b-660127ee2abd" />

