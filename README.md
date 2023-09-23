<h1>Attacks on TCP/IP</h1>


<h2>Description</h2>
The learning objective of this lab is to gain first-hand experience on some TCP/IP vulnerabilities and attacks against these vulnerabilities. It includes performing nmap scans, TCP SYN flooding and reset attacks on a server, as well as a TCP session hijacking attack.
<br />


<h2>Languages and Utilities Used</h2>

- <b>VMWare Workstation Pro</b>
- <b>Nmap</b>
- <b>Nping</b>
- <b>Wireshark</b>


<h2>Environments Used </h2>

- <b>Ubuntu Linux</b>
- <b>Labtainer Lab Environment</b> 

<h2>Lab Topology </h2>
<img src="https://i.imgur.com/z64NcNJ.png" height="80%" width="80%" alt="diagram"/>
<br />
<br />


<p align="center">

<h2>SYN Flooding Attack</h2>

<h3> Topology </h3>
<img src="https://i.imgur.com/BTzNJVE.png" height="80%" width="80%" alt="create VM"/>

<h3> Walkthrough </h3>

Perform a ping sweep on the network segment from the attacker terminal<br/>
<img src="https://i.imgur.com/GDaNDBo.png" height="80%" width="80%" alt="create VM"/>
<br />
<br />
Perform a Port Scan on the Server, enable OS detection <br/>
<img src="https://i.imgur.com/5yyX8Si.png" height="80%" width="80%" alt="network security group"/>
<br />
<br />
Open WireShark on the Server and starts capturing packets so that we can later analyze the attack.<br/>
<img src="https://i.imgur.com/W8I9qDF.png" height="80%" width="80%" alt="create LAW"/>
<br />
<br />
Use nping on the attacker terminal to start sending SYN packets to the server, use source IP 192.168.10.10 instad of random because in this case we want to avoid using a public IP address. Send a total of 20 packets.<br/>
<img src="https://i.imgur.com/oz8CgOp.png" height="80%" width="80%" alt="inbound rule"/>
<br />
<br />
Run the command netstat -na on the server and notice the SYN_RECV state of the active internet connection from our attack <br/>
<img src="https://i.imgur.com/M5lrV2c.png" height="80%" width="80%" alt="create LAW"/>
<br />
<br />
Go back to WireShark and examine the traffic generated from the attack<br/>
<img src="https://i.imgur.com/eXVGTEh.png" height="80%" width="80%" alt="change settings"/>
<br />
<br />

<h2>TCP RST Attacks on telnet and ssh Connections</h2>

<h3> Walkthrough </h3>

Start a WireShark capture on the server <br/>
<img src="https://i.imgur.com/W8I9qDF.png" height="80%" width="80%" alt="change settings"/>
<br />
<br />
From the client terminal, log into the server using telnet <br/>
<img src="https://i.imgur.com/0W6CU86.png" height="80%" width="80%" alt="connect VM"/>
<br />
<br />
Back on WireShark, examine the capture and get the sequence number as well as the source and destination ports of the last TCP packet. <br/>
<img src="https://i.imgur.com/ujROB63.png" height="80%" width="80%" alt="setup Microsoft Sentinel"/>
<br />
<br />
On the attacker terminal, create an nping command that sends an RST packet that matches the sequence number and ports from the last tcp packet and consequently terminates the session<br/>
<img src="https://i.imgur.com/NJMUKPn.png" height="80%" width="80%" alt="turn firewall off"/>
<br />
<br />
Back on the client, check that the session was terminated <br/>
<img src="https://i.imgur.com/aIvd9Em.png" height="80%" width="80%" alt="install DHCP"/>
<br />
<br />

<h2>TCP Session Hijacking</h2>

<h3> Topology </h3>
<img src="https://i.imgur.com/F04MKlG.png" height="80%" width="80%" alt="create VM"/>

<h3> Walkthrough </h3>

Start a WireShark capture on the server <br/>
<img src="https://i.imgur.com/W8I9qDF.png" height="80%" width="80%" alt="change settings"/>

On the Client Terminal, use telnet to log into the server as the user Joe<br/>
<img src="https://i.imgur.com/U4E6Eot.png" height="80%" width="80%" alt="powershell script"/>
<br />
<br />
Go to the folder /home/joe/documents and check that the file delete-this.txt exists<br/>
<img src="https://i.imgur.com/lPo8w3a.png" height="80%" width="80%" alt="verification"/>
<br />
<br />
Back on WireShark, examine the capture and get the sequence number as well as the source and destination ports of the last TCP packet. <br/>
<img src="https://i.imgur.com/Tx0MsTM.png" height="80%" width="80%" alt="setup Microsoft Sentinel"/>
<br />
<br />
<img src="https://i.imgur.com/j05tVcZ.png" height="80%" width="80%" alt="test"/>
<br />
<br />
On the attacker terminal, create an nping command that sends an RST packet that matches the sequence number, acknoledment number and ports from the last tcp packet and sends a payload containing a command that will delete the file delete-this.txt. Use a website or other tool to convert the command from ASCII into hex format <br/>
<img src="https://i.imgur.com/saLRX76.png" height="80%" width="80%" alt="create custom log"/>
<br />
<br />
Go back to the client terminal and see that it is now frozen <br/>
<img src="https://i.imgur.com/f3WihMm.png" height="80%" width="80%" alt="review custom log"/>
<br />
<br />
On a different client terminal, log back in as joe and check that the file has been deleted <br/>
<img src="https://i.imgur.com/7zJSBuI.png" height="80%" width="80%" alt="run custom log query"/>
<br />
<br />


<h2>Key Takeaways </h2>
Depth of TCP/IP Vulnerabilities: The exercise provided a hands-on experience showcasing the inherent vulnerabilities in the TCP/IP protocol stack. The lab emphasized that even foundational internet protocols, such as TCP/IP, have potential weak points.
<br />
<br />
Tool Efficacy: Tools like nmap and nping are not only used for legitimate network diagnostics but can also be weaponized to exploit vulnerabilities in network protocols. It underlines the importance of understanding tool capabilities, both for defense and ethical penetration testing purposes.
<br />
<br />
Mitigation Importance: Observing how SYN flooding attacks, RST attacks, and session hijacking can be executed underscores the need for effective security measures. These can range from Intrusion Detection Systems (IDS) to robust server configurations that resist such attacks.
<br />
<br />
Seamlessness of Attacks: One key observation was the stealth and speed with which certain attacks (like session hijacking) can be executed. This emphasizes the importance of real-time monitoring and rapid incident response capabilities.
