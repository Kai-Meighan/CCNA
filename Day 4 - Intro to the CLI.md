# Day 4 - Intro to the CLI

Today's lesson was less theory focused and more practical-focused, which was a nice change up from the heavy-theory topics we have been covering. As alwayss, below is my interpretation of the Feynman technique, as I try to show what I have learned. Also, since the lab of this lecture is just repeating the lecture commands, I will interweave the lab throughout the 'Feynman Technique Section' with screenshots directly from my lab environment 

## Feynman Technique
So what is a CLI? CLI stands for command-line interface and it is the terminal-style interface that administrators commonly use to configure devices and systems. Contrasting with a Graphical User Interface, which is much more visual and targets the end user experience. 

On Cisco devices, you can connect to the CLI by connecting to the console port directly on the device. In order to do this you need to use a rollover cable. A rollover cable is primarily used to access management interfaces on network devices. Often it comes as an RJ45 connector to a DB9 port, however you can buy adapters to change the DB9 connector to a USB for most modern computers. 

You then need to use a terminal emulator to access the CLI once physically plugged in. A terminal emulator is software that emulates the CLI within a GUI for admin access. A terminal emulator that may be used to connect to network devices may be something like PuTTY for example. 

Now we are into the terminal! Now what. 

Well firstly, there are three modes of operation that you will want to be familiar with. 

1. **User Exec Mode (Indicated by >)** - This is rather limited in what it can do. It mainly can just read configurations of the device, but not be able to change anything

2. **Privileged Exec Mode (Indicated by #)** - In this mode, you have complete access to the device's configuration and to restart the device
   
3. **Configure Terminal (Indicated by conf)** - This is the mode you access when you are actually configuration the settings on the device.

One of the first things you would want to do is set a password for privileged exec mode. This is relatively obvious, as we wouldn't want someone to just be able to plug into our device, elevate their privileges and change the configuration.
To do this use command 'enable password [password]' 

<img width="1191" height="104" alt="image" src="https://github.com/user-attachments/assets/91c51c4d-7d62-4ac4-91b7-8c4ed30c5440" />


If you type 'show running-config', you should be able to see the password within the devices configuration. 

<img width="1215" height="626" alt="image" src="https://github.com/user-attachments/assets/86a4bcf5-7cf1-412c-8f22-0ffbc3a4a6e5" />

This is a step up but not a large one since the password remains in clear text. 

Whilst on the topic, the running config is the device's active configuration during the session. This is contrasted by the start-up config, which is the configuration that is set upon the device booting up. In order to save the running-config to the start-up config, so you don't lose all of the configuration work you have done, you can use one of three commands. 
1. 'write'
2. 'write memory'
3. 'copy running-config startup-config'

<img width="838" height="630" alt="image" src="https://github.com/user-attachments/assets/d45dc6d0-052f-48ee-b58a-2edb5a82d223" />


Now back to passwords. 

In order to prevent a password being stored in plaintext, we need to encrypt it. Cisco have given us a mechanism to do so via there device-native encryption algorithm. To do this, type 'service password-encryption'. If you open the running config now, the password set should be encrypted. Also, note the number 7 next to the encrypted password. This number indicates what encryption method was used to encrypt the password, in this case, 7 maps to Cisco's encryption algorithm

<img width="1218" height="71" alt="image" src="https://github.com/user-attachments/assets/b3fad5e3-5805-4b8c-973e-bcc417fd910c" />


<img width="768" height="520" alt="image" src="https://github.com/user-attachments/assets/c3580f89-dc8d-46af-be9a-e20566ffb4f3" />


Unfortunately, this encryption algorithm is not very good and can be cracked using a very simple online tool. 

<img width="702" height="118" alt="image" src="https://github.com/user-attachments/assets/0e9bafe8-dceb-4a70-8921-186815beaf7f" />


A slightly better option however is to use the command 'enable secret'. This encrypts passwords, but instead of using Cisco's own proprietary encryption algorithm, it uses MD5. Another encryption algorithm that is still considered insecure, but is a bit better than the previous.

<img width="1207" height="92" alt="image" src="https://github.com/user-attachments/assets/a4e6864b-d5b5-4fa6-a8c7-4e7977f93651" />


When this command is used, you can view the running config and see the longer encrypted password. Note, when now authenticating with a password when moving from user mode to privileged exec mode, the password created with 'enable secret' will always take precedence over the one created with 'enable password' 

<img width="835" height="543" alt="image" src="https://github.com/user-attachments/assets/deedfe5a-b98d-4ab3-a361-f446f0a966e9" />
