# Day 7 - IPv4 Addressing (Part 1)

Today's lecture focused on introducing IP addressing and the different components of an IP address. To ensure that I understand the concepts, I will teach them from memory without notes, illustrating a type of Feynman Technique.

## Feynman Technique

**What are IP Addresses**

An IP address is a logical identifier for a device. IP addressing is used at layer 3 to identify devices when sending packets across multiple LANs via a router. 

IP addresses are 32-bits in length and are split up into 4 8-bit octets i.e. 192.168.1.1

**Binary to Decimal Translation**

Although us humans read IP addresses in what is called dotted decimal, computers just interpret it as 1's and 0s. In order to convert a binary IP address into decimal you must do the following. 

Take this octet for example '01110110'
<img width="1256" height="213" alt="image" src="https://github.com/user-attachments/assets/bdea9082-b7ae-4c73-9403-6fea3959242d" />

To convert this, first place the orders of 2 (binary is calculated within powers of two) above the below ones and zeros. This gives us a guide to calculate the translations. 
Next complete:
0 x 128 +

1 x 64 +

1 x 32 +

1 x 16 +

0 x 8 +

1 x 4 + 

1 x 2 + 

0 x 1


This equals **118**. 

**Decimal to Binary Translation**

To do the opposite, again begin by writing out the decimal values above all binary numbers, giving you a guide to subtract from.

<img width="1677" height="682" alt="image" src="https://github.com/user-attachments/assets/67fe5fc4-2c2e-4f51-a23e-2116b95e56c3" />

From there subtract you starting number, in this case '221' from each number where a 1 is present i.e.
221 - 128 = 93

93 - 64 = 28

28 - 16 = 12

12 - 8 - 4


4 - 4 = 0 

Which equals **11011100**

**Network Portion versus Host Portion**
Every IP address has two parts. It has a network portion, which defines the address of the network the device resides in, and it also has a host portion, which is a unique identfier for an device on that network. Depending on the subnet mask i.e. '/24, or /16', this will dicate how long the respective network portions and host portions are and how many networks and device on that network are available.

For example, a IP address of '192.168.1.1/24' 

Means that the network is '192.168.1'

and the host is identified as '.1'


**IPv4 Address Classes**

This brings us on nicely to IPv4 Address Classes. IPv4 addresses are split up into classes to provide a hierarchical method in assigning IP addresses based on the amount of networks and addresses needed within each class. Each class is defined below

| Class | First Octet | First Octet in Numeric Range | Prefix Length/Purpose |
|-------|-------------|------------------------------|-----------------------|
| A | 0xxxxxxx | 0 - 127 (127 is generally used for the loopback addressed | /8 |
| B | 10xxxxxx | 128 - 191 | /16 | 
| C | 110xxxxx | 192-223 | /24 | 
| D | 1110xxxx | 224 - 239  | Used for Multicast addresses |
| E | 1111xxxx| 240 - 255 | Used for experimental purposes |

**Netmask**

Cisco devices do not use the /24 to indicate the netmask. Instead they use the longer hand dotted decimal form. So for example a /24 address would be have a netmask of 255.255.255.0


**Loopback, Broadcast and Network Addresses**

There are some IP addresses that cannot be assigned to end hosts as they serve other purposes. 
- The loopback address (127.0.0.0) is used to test the network stack. For example, if a device were to ping this address, they would be simply pinging themselves and the roundtime of the ping would be 0ms as the request never left the device
- The Network address is the identfier of the network and cannot be assigned. For example, 192.168.1.0
- Finally, the broadcast address, very similarly to the broadcast frames in Layer 2, is for sending a packet to all devices on the network. For this prupose, the .255 host portion is used. 
