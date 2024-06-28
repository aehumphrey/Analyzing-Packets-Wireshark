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
[Coming soon]

### Step Five
[Coming soon]

### Step Six

[Coming soon]

[Coming soon]

## Summary
