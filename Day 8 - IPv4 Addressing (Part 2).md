# Day 8 - IPv4 Addressing (Part 2)

Today's session was relatively short, it mainly focused on wrapping up the intro to IPv4 Addressing. The main thing covered was figuring out the maximum hosts in the network, the first usable address and the last usable address. 

## Feynman Method
In order to find the maximum number of addresses in a network, we need to remember the Class system that IPv4 addresses follow. Class A addresses use the /8 network mask, where only 8 bits are dedicated to the network portion and 24 bits are dedicated to the host portion. 

The formula in order to find out how many addresses in a network is 2^n-2. This means that in a Class A network, it would be 2^24-2 = 16,777,214.

The reason why we take 2 is for the two addresses of a network that cannot be assigned to a host; a network address and a broadcast address. 

The process is the same for **Class B  (/16)** and **Class C (/24)** addresses. 

Class B - 2^16 -2 = 65,534 total addresses, with the first address being for example 154.123.0.0/16 and the last being 154.123.255.254/16

Class C - 2^8 -2 = 254 total addresses, with the first address being, for example, 192.168.1.0/24 and the last being 192.168.1.254

## Lab

Lab Instructions:

**1. Configure R1's hostname**

<img width="1037" height="249" alt="image" src="https://github.com/user-attachments/assets/f1b1a183-650f-4880-98c5-b4c86e0cbfa1" />

**2. Use a 'show' command to view a list of R1's interfaces, their IP addresses, status, etc.**

This can be done using the 'show ip interfaces brief

<img width="1329" height="244" alt="image" src="https://github.com/user-attachments/assets/ceb7b950-cbbd-410a-8586-2d1cf4ef5e16" />

**3. Configure the appropriate IP addresses on R1's interfaces, and enable the interfaces**

Inteface G0/0's IP Address in our topology is 15.255.255.154. To set this on the router:
<img width="863" height="123" alt="image" src="https://github.com/user-attachments/assets/2f1e584b-f8e3-4b64-971a-bf1135ed6b5b" />

For G0/1, the IP address in the topology is 182.98.255.254. To set this on the router:

<img width="870" height="164" alt="image" src="https://github.com/user-attachments/assets/69172173-b8c9-4269-904d-7f4b04ecd08e" />

Finally, for interface g0/2, the IP address in our topology is 201.191.20.254. To set this on the router:

<img width="907" height="102" alt="image" src="https://github.com/user-attachments/assets/ed9ad0cb-3911-4c06-aba7-f2527ef81c3b" />

_Note: I realised following assigning IP addresses to all interfaces I forgot to include a 'no shutdown' command, so I went back over all of them and fixed it :)_

**4. Use a 'show' command to verify R1's interfaces again.**

<img width="1312" height="212" alt="image" src="https://github.com/user-attachments/assets/c19babdb-0927-4aa7-a827-a3acd9b72bac" />


**5. View the running config to confirm the configuration changes, then save the config**

<img width="780" height="433" alt="image" src="https://github.com/user-attachments/assets/4387183b-643a-4c7a-94bb-f4e5370dd7c2" />

**6. Configure the IP addresses of PC1, PC2, and PC3**
   (Watch the video to learn how to do this in Packet Tracer)

I will use the GUI in packet tracer to statically set the IP addresses.

PC1:

<img width="1654" height="575" alt="image" src="https://github.com/user-attachments/assets/80e2b7f4-b4d5-41c4-8bf9-90d02895e040" />

PC2: 

<img width="1654" height="408" alt="image" src="https://github.com/user-attachments/assets/6b518447-2c69-4aa9-be12-fa250341dbae" />

PC3: 

<img width="1683" height="415" alt="image" src="https://github.com/user-attachments/assets/e1357234-3b09-4f7e-8983-1c0f7d11e8a1" />


**7. Ping from PC1 to PC2 and PC3 to test connectivity**

At first I actually had a 75% packet loss rate from PC1 to PC2 and PC3 respectively, I assume that this was because the ARP request and reply exchange that was occurring the first time around. Once I pinged again however I managed to get 100% packet delivery on each of the hosts

PC1 - PC2:

<img width="856" height="458" alt="image" src="https://github.com/user-attachments/assets/bea91736-8e93-4405-9297-57b0045282c6" />

PC1 - PC3:

<img width="837" height="452" alt="image" src="https://github.com/user-attachments/assets/e50658b0-009f-4e9a-9a63-366c22eecc82" />
