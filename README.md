
<h1>wireshark-analysis</h1>
<h2>Project Description</h2>
At my previous organization, i was provided with a file (.pcap) that contains a capture packet data from a system used by a user, to connect to my organization website. I have been asked to analyze the capture file to gather relevant information, using wireshark. I used packet sniffer to filter the network traffic at the launch of the file to first identify the source and destination IP addresses that are involved in the web browsing session.<br />

<h2>Environments and Technologies Used</h2>

- (Virtual Machines/Computer)
- Remote Desktop

<h2>Operating Systems Used</h2>

- Windows 10 (21H2)

<h2>List of Prerequisites</h2>

- Microsoft Virtual Machine Set-up
- Remote Desktop Connection

<h2>Graphical Analysis</h2>

<p>
<img src="https://i.imgur.com/Bl3mW3o.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/GpUDTpP.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
First, after i opened the capture data file using wireshark, I started obseving wireshark Graphical User Interface, which comprises of lot of network packet traffic. Each packet in the interface, has the following key property columns;
No. : The index number of the packet in this packet capture file
Time: The timestamp of the packet
Source: The source IP address
Destination: The destination IP address
Protocol: The protocol contained in the packet
Length: The total length of the packet
Info: Some infomation about the data in the packet (the payload) as interpreted by Wireshark. I quickly observed the data as i searched for an "ECHO ping request" in the info column. The reason was because i want to know what protocol is in used. Next, i need to filter the inbuilt network packet traffic from wireshark, using this code (ip.addr == 142.250.1.139). This is the source IP address of the user under my investigation. This IP address was entered on the search tab in wireshark that says 'Apply a display filter'. The list of packets displayed is now significantly reduced and contains only packets where either the source or the destination IP address matches the address i entered. Now only two packet colors are used: light pink for ICMP protocol packets and light green for TCP (and HTTP, which is a subset of TCP) packets.
</p>
<br />

<p>
<img src="https://i.imgur.com/rl8wUXY.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
I double click the first packet with TCP protocol which then gave me access to a packet detailed pane window as shown above. The upper section of this window contains subtrees where Wireshark provides me with an analysis of the various parts of the network packet. The lower section of the window contains the raw packet data displayed in hexadecimal and ASCII text. There is also placeholder text for fields where the character data does not apply, as indicated by the dot (“.”). The first subtree, from the pane window is named 'Frame', this provides me with details about the overall network packet, or frame, including the frame length and the arrival time of the packet. At this level, i started viewing information about the entire packet of data. The subtree is also contains; Ethernet 11 (This item contains details about the packet at the Ethernet level, including the source and destination MAC addresses and the type of internal protocol that the Ethernet packet contains.), Internet Protocol Version 4 (This provides packet data about the Internet Protocol (IP) data contained in the Ethernet packet. It contains information such as the source and destination IP addresses and the Internal Protocol (for example, TCP or UDP), which is carried inside the IP packet.), and Transmission Control Protocol(This provides detailed information about the TCP packet, including the source and destination TCP ports, the TCP sequence numbers, and the TCP flags.

The source port and destination port listed here match the source and destination ports in the info column of the summary display for this packet in the list of all of the packets in the main Wireshark window.).
</p>
<br />

<p>
<img src="https://i.imgur.com/zTioMs8.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/oWiUV5r.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
This filter "ip.src == 142.250.1.139", is for a specific spurce IP address unlike the previous one that was for a specific IP address. The lists contains packets that only came from 142.250.1.139. Also, this filter "ip.dst == 142.250.1.139", returns lists of packets that only came from 142.250.1.139.
</p>
<br />

<p>
<img src="https://i.imgur.com/5g2EHT6.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/GwEr1At.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/LmJLUSm.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
This filter "eth.addr == 42:01:ac:15:e0:02", displays traffic to or from a specific Ethernet MAC address. This filters traffic related to one MAC address that was discovered previously in my investigation, regardless of the other protocols involved: Notably, the MAC address that was specified in the filter is listed as either the source or destination address in the expanded Ethernet II subtree. Aslo, the Protocol field in the Internet Protocol Version 4 subtree indicates which IP internal protocol is contained in the packet. From my investigation it was TCP protocol.
</p>
<br />

<p>
<img src="https://i.imgur.com/39X7Coi.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/64E9gJ5.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
This "udp.port == 53" filter, was used to further explore and examine DNS traffic, DNS traffic uses UDP port 53, so this will list traffic related to DNS queries and responses only as shown above. First, i selected i selected sample DNS traffic, then i drill down into the protocol to examine how the DNS packet data contains both queries (names of internet sites that are being looked up) and answers (IP addresses that are being sent back by a DNS server when a name is successfully resolved). From inspecting, the Domain Name System (query) subtree, as well as Queries subtree, i obseeved that the name of the website that was query is "opensource.google.com" as shown above.
</p>
<br />

<p>
<img src="https://i.imgur.com/0385lhn.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/5MrxAck.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
 This filter "tcp.port == 80" was lastly used to explore and examine TCP traffics on wireshark. TCP port 80 is the default port that is associated with web traffic: From my investigation, i noticed that quite a few packets were created when the user accessed the web page http://opensource.google.com. Finally, this filter "tcp contains "curl"", was used to select TCP packet data that contains specific text data. This filters to packets containing web requests made with the curl command in this sample packet capture file.
</p>
<br />
