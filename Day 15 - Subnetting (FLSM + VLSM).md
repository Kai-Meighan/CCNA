# Day 13, 14 AND 15 - Subnetting
I have decided to combine days 13, 14 and 15 together as they all dicuss subnetting. Now subnetting is a fundamental component of the CCNA, however there is not a great deal of theory on it. It is more _how_ to subnet that the actual concepts behind it. Therefore, for the theory sections of these documents, I'll keep it brief as I will be mainly practicing how to subnet over actually talking about it. 

## Feynman Technique
**What is a Subnet**
A subnet is just a division of a network to reduce wasted IP ranges. Since you are only given a set amount of IP ranges, it is important that you maximise usage of them and not waste any addresses that could be allocated to something else. An example of this is in a P2P network with two hosts. By applying a /24 address with 254 possible, usable address combinations. Now applying this to only two hosts is wasteful as you are leaving 252 addresses on the table, hence subnetting was born.

There are two types of subnetting:
1. Fixed-Length Subnet Masks - This is where all subnets have the same number of hosts
2. Variable-Length Subnet Masks - This is where some subnets may have more hosts that others, therefore not all subnets will have the same size and hence, subnet mask. i.e. /25 for one subnet with 100 hosts and a /27 for another with only 22 hosts

In order to complete VLSM, there are some rules you have to apply. First, you must start with the subnet with the most amount of hosts and assign this the start of the address space, then the second and so on and so forth until you get to the smallest subnet. 

There are two important formula's to keep in mind also. 
Number of hosts = (2^Host Bits) - 2 
Number of subnets = 2^ Network Bits.

These two formulas will help with most subnetting questions. Also another pro-tip is to do the binary to dotted decimal conversion as this simplifies the process massively despite being slightly longer to write out. 

# Lab
**Topology**
<img width="712" height="306" alt="image" src="https://github.com/user-attachments/assets/f3c6e58f-dd64-4c25-86d7-a0b43d82ceeb" />

**Instructions**
Subnet the 192.168.5.0/24 network to provide sufficient addressing for each LAN.
(Also, the point-to-point connection between R1 and R2).

Assign the first usable address to the PC in each LAN.

Assign the last usable address to the router's interface in each LAN.

Configure static routes on each router so that all PCs can ping eachother.


**Step 1**
Assign the largest subnet the start of the address space. In our case that would be LAN2 with 64 hosts. 

So in order to determine our prefix length we need to make sure the subnet suits our 64 hosts. Initally, I thought a /26 network would suffice, but when you take away the network and broadcast addresses, you are left with 62 hosts. Not enough, so /25 provides us 126 usable addresses


**_LAN2_**
Network Address: 192.168.5.0
Broadcast Address: 192.168.5.127
1st Usuable Address: 192.168.5.1
Last Usuable Address: 192.168.5.126

PC2 IP address:

<img width="1715" height="688" alt="image" src="https://github.com/user-attachments/assets/404d67c4-a323-489e-92a1-9c3f2e366c94" />

R1 g0/1 Interface

<img width="907" height="63" alt="image" src="https://github.com/user-attachments/assets/c7a8cbef-e5da-485e-860f-14d47575921c" />


**_LAN1_**

Next up is LAN 1 with 45 hosts. This time a /26 host should suffice as we can keep 6 host bits allowing for 62 usuable addresses
Network Address: 192.168.5.128 /26
Broadcast Address: 192.168.5.191 /26
1st Usable Addrress: 192.168.5.129 /26
Last Usable Address: 192.168.5.190 /26

PC1 IP Address

<img width="1694" height="686" alt="image" src="https://github.com/user-attachments/assets/de3df8eb-6175-4710-aa3b-aae7d619ebb4" />

R1 g0/0 Interface: 

<img width="883" height="93" alt="image" src="https://github.com/user-attachments/assets/64b34b0e-c379-4821-b24f-e36050a4a186" />


_**LAN3**_

LAN3 has 14 hosts so doing the hosts formula, I can see that a /28 prefix length will work perfectly as that gives us 16 hosts, minus the broadcast and network addresses, that leaves us with 14
Network Address: 192.168.5.192
Broadcast Address: 192.168.5.207
1st Usable Address: 192.168.5.193
Last Usable Address: 192.168.5.206

PC3 IP Address

<img width="1696" height="641" alt="image" src="https://github.com/user-attachments/assets/0916454b-75f8-4ecb-aea1-e6756aa49f88" />

R2 g0/0 Interface:

<img width="923" height="41" alt="image" src="https://github.com/user-attachments/assets/bf52ec3f-aba5-42c6-87c6-80643e673f63" />


_**LAN4**_

LAN4 with only 9 hosts. Here a /29 wouldn't work as there would only be 8 total addresses, 6 of them being usable. So a /28 again it is. That means there will be 14 usable addresses, more than enough.
Network Address: 192.168.5.208
Broadcast Address: 192.168.5.223
1st Usable Address: 192.168.5.209
Last Usable Address: 192.168.5.222

PC4

<img width="1668" height="577" alt="image" src="https://github.com/user-attachments/assets/f1dcf3cb-5876-4cdd-bb58-7efc853ebb60" />


R2 g0/1 Interface:

<img width="877" height="37" alt="image" src="https://github.com/user-attachments/assets/809a8629-9cbf-4d2f-8c8e-7f6ecbb75a31" />


_**P2P Link**_

For the P2P, we can use a /30 address and this will give us 4 addresses to work with, minus two for the broadcast and network addresses
Network Address: 192.168.5.224
Broadcast Address: 192.168.5.227
1st Usable Address: 192.168.5.225
Last Usable Address: 192.168.5.226


R1 g0/0/0 interface:

<img width="900" height="64" alt="image" src="https://github.com/user-attachments/assets/58de0245-f13c-48be-87a0-5227229af6fd" />


R2: g0/0/0 interface 

<img width="886" height="68" alt="image" src="https://github.com/user-attachments/assets/4217805d-0365-490c-9342-467cfa52a114" />

**Static Routes**

Now to round off the lab and verify connectivity, lets configure static routes

From R2 - LAN1

<img width="1036" height="47" alt="image" src="https://github.com/user-attachments/assets/82237fbf-40c3-4385-9d09-61a7d2ecccc3" />


From R2 to LAN2

<img width="1010" height="31" alt="image" src="https://github.com/user-attachments/assets/a9d9c615-9e55-4821-b439-70c6e22a8009" />


R2 Validation

<img width="1136" height="305" alt="image" src="https://github.com/user-attachments/assets/0431fa05-13d0-4314-bed2-320ab3370236" />


R1 - LAN3

<img width="1097" height="38" alt="image" src="https://github.com/user-attachments/assets/d3234845-953e-43c1-a068-b8540da48850" />


R1 - LAN4

<img width="1036" height="35" alt="image" src="https://github.com/user-attachments/assets/5b2b7fac-785c-42fb-b8e9-b91a194de07a" />


R1 Validation:

<img width="1102" height="311" alt="image" src="https://github.com/user-attachments/assets/a5d4e8e8-c1c5-4ed0-865f-084171ab02f5" />
