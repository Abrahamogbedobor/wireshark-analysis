
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

<p>
<img src="https://i.imgur.com/ZAN0JYb.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
As shown above, the os-Ticket V1.15.8 was downloaded and extracted from the download folder. Furthermore, there is an 'upload' folder among the downloaded os-Ticket files, this folder was then copied into IIS server as shown in the below figures. Specifically, into c:\inetpub\wwwroot and then the 'upload' folder within this wwwroot was renamed as osTicket. In summary, the installed os-Ticket application was dumped into IIS server.
</p>
<p>
<img src="https://i.imgur.com/oCFUcMD.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<br />
 
 <p>
<img src="https://i.imgur.com/ABuN04A.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
From  the above figure, the 'upload' folder from os application that was copied and dumped into IIS server was renamed as 'osTicket'. Furtheermore, from IIS   manager page on start-up menu ISS server was then reloaded to complete os integration into IIS server.
</p>
<br />

<p>
<img src="https://i.imgur.com/fMllqpn.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
After restarting IIS server, on the left hand side the following link was clicked site..>default..>osTicket then on the right hand side 'Browse * 80'(http) was clicked as shown above. Basically, when port 80 is entered it then open the osTicket page as shown below.
</p>
<br />

<p>
<img src="https://i.imgur.com/plCKtU5.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
The above is a web application that was configured using IIS on a remote desktop computer in microsoft Azure. Also, some extension were not enabled during the loading of the osTicket web application as shown above. Hence, the below figure is used to show the steps used in enabling them.
</p>
<br />

<p>
<img src="https://i.imgur.com/xg0333K.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
On ISS server, these steps 'Site..>Degfault..>osTicket' then double-clicked on PHP file. Lastly, the enable/disable link was clicked and the following extensions (php_imap.dll, php_intl.dll, php_opache.dll), were enabled. After enabling them all osTicket aplication browser was then refreshed on the site, which then provide the below changes to the osTRicket web application as shown below.
</p>
<br />

<p>
<img src="https://i.imgur.com/lmXkywl.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
This steps involves browsing on the C:Drive where osTicket is stored and search for this file and extention (C:\inetpub\wwwroot\osTicket\include\ost-sampleconfig.php then rename it to C:\inetpub\wwwroot\osTicket\include\ost-config.php).
</p>
<br />

<p>
<img src="https://i.imgur.com/GDInySf.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
This step involves renaning ost-sampleconfig.php file to ost-config.php
</p>
<br />

<p>
<img src="https://i.imgur.com/2MLTYrH.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/x4J3nLx.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
After renaming the file to ost-config.php, permission was then assigned to it. The steps of assinging permission includes right clight on the file, then property, security, advance, disable inheritance (i.e stopping it from receiving permission from its parent folder and then create a new permission), remove all permission, then add, select principles (i.e account or person(s)), everyone, click on check name and ok, allow everyone full control, then ok and lastly, continue on the osTicket browser to see the above display ticekting page. Furthermore, the helpdesk user (someone who will use the ticketing platform) and system admin details was then used to complete the above osTicket.
</p>
<br />

<p>
<img src="https://i.imgur.com/rZ9mYND.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
 <img src="https://i.imgur.com/pVKzDpU.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
This part of the osTicket form is the database. Previously, DB was created (MySQL), at this stage of filling-out the form a client called (HeidiSQL) was installed. The reason for installing this client is to enable users and osTicket admin to be able to connect to the database that was created (i.e helping them to use and edit data/tructure running on their installed computer with MySQL).
</p>
<br />

<p>
<img src="https://i.imgur.com/OfQPR0Z.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
This was the heidiSQL client that was installed previously. This steps involves creating a new connection as shown above using root as the username and same password that was created during DB set-up.
</p>
<br />

<p>
<img src="https://i.imgur.com/BOT5hN3.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
 <img src="https://i.imgur.com/ynuTDVI.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
This steps involves creating new database. Note, on the left-side there are some defult DB that was created during installation. By right clicking on 'unnamed' a new database was then created which was referred as 'osTicket'. 
</p>
<br />

<p>
<img src="https://i.imgur.com/FvEN1XC.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Back to the osTicket installation form, the new database that was created (osTicket, with MySQL usrname and password was inputted to complete the osTicket installation as shown above)
</p>
<br />

<p>
<img src="https://i.imgur.com/SuLudPB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Here is the complete osTicket page at the time of this lab with some URLs beneath the page. The first url is for end users (http://localhost/osTicket/) incase they needed to raise a ticket, second is for staff control panel which is help desk professional and admin that needed to log into the osTicketing system (http://localhost/osTicket/scp). Finally, the following folder (C:\\inetpub\wwwroot\osTicket\setup) on computer C:DRIVE was deleted as a requirement from osTicket, and this folder (C:\\inetpub\wwwroot\osTicket\include\ost-config.php) was set to "Read-only" (read/execue and read).
</p>
<br />

