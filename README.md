# Analyzing Packets with Wireshark Project

## Objective

For this lab, I used Wireshark to analyze a packet capture file. Wireshark is a network protocol analyzer that uses a graphical user interface (GUI). To access Wireshark, I used Myrtille as a remote access gateway to access a legacy version of Windows on a virtual machine. This lab involved a three-pronged approach: first, to identify source and destination IP addresses involved in this web browsing session; second, to examine the protocols that are used when the user makes the connection to the website, third; to analyze some of the data packets to identify the type of information sent and received by the systems that connect to each other when the network data is captured.

### Skills Learned

- Experience in applying filters to focus on specific packets or types of traffic, aiding in targeted analysis and troubleshooting.
- Ability to effectively inspect and interpret individual packets to understand their content and structure.
- Proficiency in using packet analysis to diagnose network issues such as latency, packet loss, and unusual traffic patterns.
- Deepened knowledge of various network protocols (TCP, UDP, HTTP, DNS, etc.) through practical application and analysis.
- Capability to identify performance bottlenecks by analyzing packet flow and network behavior.

### Tools
- Wireshark
- Myrtille

## Steps

### Step One

Description: Explore data with Wireshark

I accessed Wireshark through Myrtille, a remote access gateway that served as a virtual machine. For the purposes of this lab, I accessed the file ‘sample.pcap’, which displays network traffic to the website during a given period.

![image](https://github.com/aehumphrey/Investigating-Packets-with-Wireshark-Project/assets/33531835/1cb2c157-7c6d-4623-a7c2-f5055652ce26)

*Ref 1. Wireshark program*

My team wants to know the protocol of the first packet in the list that sent an Echo (ping) request. To do this, I scrolled through the list until I found the packet (16) and selected it. This packet used the Internet Control Message Protocol (ICMP).

![image](https://github.com/aehumphrey/Investigating-Packets-with-Wireshark-Project/assets/33531835/be96d8b2-bf24-45cb-844d-9e9b664a6dd2)

*Ref 2. Identifying protocols in Wireshark.*

### Step Two

Description: Apply a basic Wireshark filter and inspect a packet

The security team has flagged an IP address as a potential source of concern. All traffic coming to or from this address needs to be looked at. To search for packets associated with this address, I entered the following into Wireshark:
![image](https://github.com/aehumphrey/Investigating-Packets-with-Wireshark-Project/assets/33531835/cafd95a9-2680-444d-9810-80dc2ede463b)

I’m curious about the first packet that lists TCP as the protocol. Where is this packet going? To learn this, I select packet 64 from the list. Once selected, I select the Transmission Control Protocol subtree. This provides detailed information about the TCP packet, including the source and destination TCP ports, the TCP sequence numbers, and the TCP flags.

In this case, the packet is destined for Port 80. This is the default port for unencrypted web pages using HTTP protocol.

![image](https://github.com/aehumphrey/Investigating-Packets-with-Wireshark-Project/assets/33531835/85129c7d-d741-4ff5-b1b0-01471a1b6d3b)

*Ref 3. Filtering packets by IP address*

![image](https://github.com/aehumphrey/Investigating-Packets-with-Wireshark-Project/assets/33531835/b37a7f85-f645-49f5-8e0d-eb5f2a634c5c)

*Ref 4. Opening the subtree for packet 64*

### Step Three

Description:  Use filters to select packets

Filtering by IP address didn’t give me very specific information. Next, I’d like to look at traffic coming from the IP address, destined to the IP address, and to or from the MAC address.

Similar to how I filtered the packets for IP addresses in step two, I can search for either source or destination IP addresses using the following filters:

![image](https://github.com/aehumphrey/Investigating-Packets-with-Wireshark-Project/assets/33531835/5b964207-c8fb-4e02-8d1e-3210ed80c64e)

![image](https://github.com/aehumphrey/Investigating-Packets-with-Wireshark-Project/assets/33531835/bce2c18c-fd2d-432f-8a7d-4f90a3954c18)

*Ref 5. Filtering in Wireshark by source IP address*

![image](https://github.com/aehumphrey/Investigating-Packets-with-Wireshark-Project/assets/33531835/daf48e71-0f09-4492-9bbf-f7f30657324a)

![image](https://github.com/aehumphrey/Investigating-Packets-with-Wireshark-Project/assets/33531835/eb047915-c6d8-48a8-8a8e-fd7717bb188d)

*Ref 6. Filtering in Wireshark by destination IP address*

![image](https://github.com/aehumphrey/Investigating-Packets-with-Wireshark-Project/assets/33531835/08b1f612-a3d7-462e-8799-26b551891c07)

![image](https://github.com/aehumphrey/Investigating-Packets-with-Wireshark-Project/assets/33531835/9615f7e9-b4e7-415c-b7c0-3765a29fd07b)

*Ref 7. Filtering in Wireshark by MAC address*

I’m interested in traffic associated with this MAC address. Specifically, I want to know what protocol is involved. Like I did in step one, I select a packet and open the relevant subtrees. In this instance, I select Internet Protocol Version 4 > Protocol, which indicates which IP internal protocol is contained in the packet. In this packet, TCP is used.

![image](https://github.com/aehumphrey/Investigating-Packets-with-Wireshark-Project/assets/33531835/2abd201a-e600-46f3-8067-d98fd212375e)

*Ref 8. Identifying Protocols in Wireshark*

### Step Four

Description: Use filters to explore DNS packets

Next, I’m going to take a look at a specific port number. DNS queries and responses use UDP port 53, which means that vulnerabilities in this port can be exploited by malicious actors (i.e., through DDoS attacks).

To select UDP port 53 traffic, I filtered for the following: 

![image](https://github.com/aehumphrey/Analyzing-Packets-Wireshark/assets/33531835/caf47812-8c45-4bc9-99f4-d0c38f5a1cef)

I’m interested in the fourth packet in this list (packet 12). Selecting this packet, I can then navigate to the Domain Name System (query) subtree. 

![image](https://github.com/aehumphrey/Analyzing-Packets-Wireshark/assets/33531835/bb490b8e-c5ab-4faf-ae4c-1ee24baabed6)

*Ref 9: Filtering packets by UDP port number*

![image](https://github.com/aehumphrey/Analyzing-Packets-Wireshark/assets/33531835/0b06607e-1500-4d0f-b297-99a05d8cad91)

*Ref 10: Navigating to the DNS Subtree in packet 12*

Within this subtree, the Queries item tells me that the name of the website that was queried is opensource.google.com. That means that this packet was sent by someone trying to access opensource.google.com.  The Answers data includes the name that was queried (opensource.google.com) and the addresses that are associated with that name. The IP address I filtered for in steps two and three (142.250.1.139) appears in the expanded Answers section.

![image](https://github.com/aehumphrey/Analyzing-Packets-Wireshark/assets/33531835/0075bfe3-691f-43a7-9a60-d5debd985acb)

*Ref 11: Queries and Answers within the DNS subtree*

### Step Five

Description: Use filters to explore TCP packets

In this final step, I’m interested in further examining TCP packets, as well as locating specific packets based on text that is present in payload data contained inside network packets. 

First, I want to filter by TCP port number. Similarly to what I did in step four, I entered the following filter to select TCP port 80 traffic.

![image](https://github.com/aehumphrey/Analyzing-Packets-Wireshark/assets/33531835/2850f600-05dd-43cd-867f-b1fb8f45e5f9)

![image](https://github.com/aehumphrey/Analyzing-Packets-Wireshark/assets/33531835/244ad98f-4178-4c68-8198-afeebbb96a9f)

*Ref 12: Filtering packets by TCP port number*

TCP port 80 is the default port associated with web traffic, so, unsurprisingly, quite a few packets were created when the user accessed this website!

I’m interested in the first packet from this list, with Destination IP 169.254.169.254. This is packet 37. Opening the Internet Protocol Version 4 subtree, I can see that the Time to Live value was 64. Time to Live (TTL) is a mechanism which limits the lifespan of a packet, preventing it from circulating indefinitely. 64 is the recommended TTL value for the Internet Protocol.

![image](https://github.com/aehumphrey/Analyzing-Packets-Wireshark/assets/33531835/5c56bd32-b7c8-4d7e-b890-4a4627221b24)

*Ref 13: Time to Live (TTL) for packet 37*

Within this same subtree, I can also see that the Header Length is 20 bytes.

![image](https://github.com/aehumphrey/Analyzing-Packets-Wireshark/assets/33531835/46280da6-3d74-4931-8b1c-0974daa0a129)

*Ref 14: Header Length of packet 37*

Next, I wanted to know the Frame Length of this packet. “Frame” refers to a unit of data in the Link Layer (Layer 2 on the OSI model). “Frame Length” is a measurement of data. The Frame Length of this packet is 54 bytes (432 bits : 1 byte = 8 bits).

![image](https://github.com/aehumphrey/Analyzing-Packets-Wireshark/assets/33531835/180ac44c-bbd3-4489-b946-62b12116efc1)

*Ref 15: Frame Length of packet 37*

Finally, I wanted to filter packets containing web requests made with the curl command. To do this, I entered the following to search for TCP packet data that contained specific text data:

![image](https://github.com/aehumphrey/Analyzing-Packets-Wireshark/assets/33531835/b923b61b-bffe-49dc-957b-f8420877c004)

![image](https://github.com/aehumphrey/Analyzing-Packets-Wireshark/assets/33531835/d5bc0fd2-c483-4bb3-84b6-e685449ce4df)

*Ref 16: Filtering for packets containing specific text*


## Summary

This project gave me practical experience using Wireshark to open saved packet capture files, view high-level packet data, and use filters to inspect detailed packet data.
