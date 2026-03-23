# Day 1 - Network Devices


Day 1 was pretty stock standard stuff. Below, as I intended to do with all of my lectures and labs, I am going to explain the concepts like I am teaching someone else (the Feynman Technique). This will hopefully allow me to better retain the concepts and be able to articulate them better

Then following the discussion on the concepts learned, I will walk through the lab.
## Feynman Technique
So firstly:
What is a Network?
A network is devices that are connected together in order to share resources. 

What is a Client? 
A client is simply a device that is requesting services that are accessible from a server. 

The next obvious question is what is a server? 
A server is simply a device that provides a service to a client. 

Hence the most basic client-server relationship!

Next what is a Switch?
A switch forwards traffic between devices that are within the same LAN. A LAN is a group of connected devices that are in a closer vicinity i.e. home, office or a small building. 

So how do LANs communicate with eachother?
This is where a router comes in. A router just connects to LANs together over the Internet. 

In order to protect malicious traffic from getting into our LAN, we use a firewall. A firewall is usually a hardware device that filters network traffic based on pre-defined rules. There are a couple types of firewalls i.e. Host-based and Next Generation Firewalls (NGFW), but to keep it simple, we weill just stick with the standard firewall

## Lab
Today's lab was just getting aquinted with Cisco's packet tracker. The goals of the lab were the following:
Create the network diagram displayed at 16:40 of the Day 1 video.

    Use the following devices:

        Cisco 2911 routers (x2)

        Cisco 2960 switches (x2)

        Cisco 5505 Firewalls (x2)

        PCs (x2)

        Servers (x2)

        Use a Laptop as the 'attacker' in the diagram.

**Connect the devices together using Packet Tracer's
'Automatically Choose Connection Type' function**


The lab consisted of selecting the correct devices from the 'Network Devices' and 'End Devices' tabs
<img width="846" height="185" alt="image" src="https://github.com/user-attachments/assets/8e6e0773-f42c-497d-9d2d-a722dfe00ee6" />


Then simply connecting them using Packet Tracer's built in connections feature
<img width="486" height="183" alt="image" src="https://github.com/user-attachments/assets/51605dd4-2681-4be9-83fe-e4eb09b822e2" />


From here is was as easy as placing the relevant devices and then connecting them up, making the final product
<img width="1539" height="705" alt="image" src="https://github.com/user-attachments/assets/8a03b60d-9114-41d2-aad8-3738f787c0e5" />


