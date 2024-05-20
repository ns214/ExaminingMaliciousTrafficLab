<h1>Combining Tools to Analyze Malicious Traffic</h1>


<h2>Description and Summary</h2>
The goal of this project was to examine a packet capture and form an understanding of what took place. <br />
<br/>

I used a combination of Wireshark, NetworkMiner, VirusTotal, and DynamiteLabs to determine that this traffic shows evidence of a CryptoWall ransomware infection. 
 
<br />


<h2>Utilities Used</h2>

- <b>Wireshark</b> 
- <b>NetworkMiner</b>
- <b>VirusTotal</b>
- <b>DynamiteLab</b>

<h2>Environments Used </h2>

- <b>Windows 10</b>
<h2>Walk-through:</h2>

I opened the PCAP with NetworkMiner to separate all the devices included in the capture, and identify the one likely to be infected. In this case, it was "Leonardo-PC", a Windows machine with IP address 192.168.137.85. <br/>
 
![Image Description Here](https://github.com/ns214/ExaminingMaliciousTrafficLab/blob/main/NetworkMiner%20-%20Infected%20Host%20Machine.png?raw=true)
<br />
<br />
In Wireshark, I identified a suspicious HTTP GET request from Leonardo-PC to an unknown IP address (188.165.164.184). This is the source of infection.  <br/>

![Image Description Here](https://github.com/ns214/ExaminingMaliciousTrafficLab/blob/main/Wireshark%20-%20Suspicious%20HTTP%20Request.png?raw=true)
<br />
<br />
After uploading the PCAP to VirusTotal, it was immediately recognized as CryptoWall ransomware installed by the Fiesta exploit kit. <br/>

![Image Description Here](https://github.com/ns214/ExaminingMaliciousTrafficLab/blob/main/VirusTotal%20-%20CryptoWall%20and%20Fiesta%20Exploit%20Kit.png?raw=true)
<br />
<br />
The malware caused the infected machine to connect to many different IPs. I noticed a consistent pattern where the infected machine makes connections to these different CNC servers. It seems to make the same connections in (almost) the same order every time, with the first and last of each grouping being to the same IP 213.238.166.230, and domain beybladeoyunlari.org. The connections are evenly spread amongst the 7 different IPs highlighted in red by DynamiteLab.  <br/>

![Image Description Here](https://github.com/ns214/ExaminingMaliciousTrafficLab/blob/main/DynamiteLabs%20-%20Infection%20Timeline.png?raw=true)
<br />
<br />
Zooming out on the timeline shows a repetitive pattern of communications to the same group of IP adresses, and in nearly the same order every time. This is beaconing, a classic symptom of an infected machine communicating with command and control servers. <br/>

![Image Description Here](https://github.com/ns214/ExaminingMaliciousTrafficLab/blob/main/DynamiteLabs%20-%20Evidence%20of%20Beaconing.png?raw=true)
<br />
<br />
DynamiteLab shows that the exploit was enabled by an outdated flash version on Leonardo-PC. <br/>

![Image Description Here](https://github.com/ns214/ExaminingMaliciousTrafficLab/blob/main/DynamiteLabs%20-%20Outdated%20Flash%20created%20the%20vulnerability.png?raw=true)
<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
