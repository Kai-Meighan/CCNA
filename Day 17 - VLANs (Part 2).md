# Day 17 - (VLANs Part 2)

Today covered a fair bit of new content. Luckilly, the main points can be boiled down to the below  points. As always, I'll try to take this information and regurgitate it in my own works

## Feynman Method

**What is a trunk port and what is its purpose?**

A trunk port carries traffic from multiple VLANs over a single interface. This prevents the switch from having to have multiple interfaces dedicated to individual VLANs.

**What is 802.1q encapsulation**

802.1q encaspulation inserts a 'tag' into the Ethernet frame, between the Source MAC Address and the Type/Length field. The main purpose of this tag is to denote which VLAN the traffic belons to. The switch reads this tag and can forward traffic to the appropriate VLAN

**What is a Native VLAN**

A native VLAN is the VLAN that traffic that is not tagged will be assigned to. It is important these these are properly synchronised between switches to ensure that all untagged traffic is forward to the appropriate destination, or it can be best practice to change this to a random VLAN number if not used for security purposes

**What is Router on a Stick**

A router on a stick involves configuring multiple sub-interfaces on a single interface. This allows traffic from multiple VLANs to be routed without having to use a single, dedicated interface per VLAN
 
## Lab

**Topology**

<img width="712" height="373" alt="image" src="https://github.com/user-attachments/assets/b534ef13-660f-4a97-982f-0817f4b659db" />


**Instructions**
1. Configure the switch interfaces connected to PCs as access ports in the correct VLAN.

2. Configure the connection between SW1 and SW2 as a trunk, allowing only the necessary VLANs.
    Configure an unused VLAN as the native VLAN.
    **Make sure all necessary VLANs exist on each switch**

3. Configure the connection between SW2 and R1 using 'router on a stick'.
     Assign the last usable address of each subnet to R1's subinterfaces.

4. Test connectivity by pinging between PCs.  All PCs should be able to reach each other.

  

For Step 1. This should be relatively easy as we did this yesterday.

<img width="807" height="129" alt="image" src="https://github.com/user-attachments/assets/30eadf94-d660-482d-a08b-4b754c59cff2" />

I will repeat this process for all interfaces connected to PC's ensuring that they are connected to the correct VLAN

_SW1 Verification_

<img width="1308" height="384" alt="image" src="https://github.com/user-attachments/assets/d5ed5895-3500-4dbf-ba9c-4cc4595149eb" />

_SW2 Verification_

<img width="1317" height="378" alt="image" src="https://github.com/user-attachments/assets/7d43c18f-72d4-4900-9468-4e14661de57c" />

2. So in modern switches there is no support for ISL, so therefore, there is no need to specify we want to use 802.1q for tagging. So we just move on and make the interface a trunk

<img width="679" height="61" alt="image" src="https://github.com/user-attachments/assets/10279193-fd82-463a-832a-eb1ff3380706" />


Then we specify allowed VLANs, in this case 10 and 30

<img width="851" height="41" alt="image" src="https://github.com/user-attachments/assets/c24ea7cf-6689-458c-b4ea-f8554fec7380" />


To verify:

<img width="1074" height="305" alt="image" src="https://github.com/user-attachments/assets/6da3f8d2-aa3e-4ba7-877b-c9c315023f7f" />

I will do the same on SW2 and show the verification

<img width="1090" height="292" alt="image" src="https://github.com/user-attachments/assets/2a3c8b30-0977-4665-8bac-994dbf7bb1d0" />

I will also set the native VLAN as VLAN 1001 for security reasons. Note: This will be done on both switches

<img width="899" height="42" alt="image" src="https://github.com/user-attachments/assets/d20c9c3f-2e92-4341-9c87-4dcc0a4ce667" />

3. Now onto the Router-on-a-Stick Configuration.

Firstly, I will set up the switch interfaces as I usually would allowing all three VLANs to pass over SW2's g0/2 interface 

<img width="881" height="63" alt="image" src="https://github.com/user-attachments/assets/b247054c-1117-48c0-9c1e-baf0879b9bb9" />

Now on R1, I will begin to configure sub interfaces, starting with VLAN 10 in sub interface g0/0.10

<img width="965" height="75" alt="image" src="https://github.com/user-attachments/assets/d499d315-6521-4f07-921f-6c312f145027" />

_Interface g0/0.2_

<img width="966" height="73" alt="image" src="https://github.com/user-attachments/assets/fac37678-cb63-41f0-8e79-949e03d2c193" />

_Interface g0/0.3_

<img width="900" height="72" alt="image" src="https://github.com/user-attachments/assets/2ef6071b-e573-4a10-a798-75c5702da061" />

Verification
<img width="1349" height="310" alt="image" src="https://github.com/user-attachments/assets/99c9869a-9b59-491b-aec6-5d0847298975" />

4. Time to verify it all works
PC1 - PC5

<img width="941" height="432" alt="image" src="https://github.com/user-attachments/assets/29a58419-fe34-4ffd-8ddc-57014a2dff49" />

PC2 - PC3
<img width="999" height="437" alt="image" src="https://github.com/user-attachments/assets/5a74c5d9-0933-47d6-b0d6-c1e785f6a1fc" />


Perfect all works as expected and we managed to set up inter-vlan routing using trunk ports with a router on a stick configuration
