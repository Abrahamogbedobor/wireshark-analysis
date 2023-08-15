
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
I double click the first packet with TCP protocol which then gave me access to a packet detailed pane window as shown above. The upper section of this window contains subtrees where Wireshark provides me with an analysis of the various parts of the network packet. The lower section of the window contains the raw packet data displayed in hexadecimal and ASCII text. There is also placeholder text for fields where the character data does not apply, as indicated by the dot (“.”). The first subtree, from the pane window is named 'Frame', this provides me with details about the overall network packet, or frame, including the frame length and the arrival time of the packet. At this level, i started viewing information about the entire packet of data.
</p>
<br />

<p>
<img src="https://i.imgur.com/KQuEIhJ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/1a2nX8O.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
The above pictures are Internet Information Services installation steps in windows. IIS is windows web server, as os-ticket uses web browser thus, it was required to enable IIS or instal it as a prerequisites before os-ticket installation. Notably, this IIS web server is then used to serve os web aplication on the installed computer. Also, the folder in which the installed IIS file is saved is been highlighted above.
</p>
<br />

<p>
<img src="https://i.imgur.com/bOfXH2J.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
The above figure is a web platform installer, that was installed in remote desktop windows, and it was used in installing other bunch of softwares such as MYSQL 5.5 databse, and some simple versions of x86 php files based on os-ticket prerequisite requirements.
</p>
<br />

<p>
<img src="https://i.imgur.com/KMrXf6t.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
The above figure is a database as previously mentioned that is required for os-ticket to function. Any password of my choice was used, and the user name is 'roo't. Also, during installation some php files was unsuccessful however, they were seperately downloaded to complete the prerequisites installation steps as shown below. These files are Microsft c++ redistributable packages and php manager.
</p>
<br />

<p>
<img src="https://i.imgur.com/e5ZzcYZ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
 The above figures (c++ redistributable and php manager are the downloaded files that failed previously)
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

