Nmap Scan against Legacy Machine on 10.10.10.4

nmap -A -T4 -p- 10.10.10.4

Findings: <br><br>
![nmap scan](Images/nmapscan.png)

Open Ports 139 & 445 <br>
On Windows those Ports relate to smb (filesharing).<br><br>
Host Script findings: <br>
Windows XP (Windows 2000 LAN Manager) Definitive OS fingerprint. <br>
smb-security-mode: message singing disabled. Could lead to a remote shell. <br>

![host scripts](Images/HostScript.png)<br><br>
First try to attack:<br>
Pre installed on kali comes smbclient. I'll try to connect directly to check if it is password protected. In this case, it is.<br>
![smbclient](Images/smbclient.png)<br><br>
The next step will be Metasploit. First I use an auxiliary module to scan for the SMB version. This is important, because SMB can be very vulnerable (WannaCry, Eternal Blue). <br>
Sadly the SMB version doesnt come up, but we can work with the SMB Windows Service Pack version.<br>
![metasploit](Images/metasploit.png)<br>
After short reconnaissance i have found an exploit on https://www.rapid7.com/db/modules/exploit/windows/smb/ms08_067_netapi/. So i went back to my Metasploit console and searched for the exploit module. <br>
![metasploit](Images/netapiconfig.png)<br>
Some options had to be set before the module could be used.<br>
First the RHost IP, second the target. Metasploit used my VM IP as the LHost Setting, so I didnt change that. Metasploit has an automated Target detection, but I wanted to be sure to set the right one.
![metasploit](Images/rhost target.png)<br>
After setting the Target i ran the first attempt: <br>
![metasploit](Images/run1.png)<br>

I checked my Interface and changed the LHost to the tun0 IP.
![metasploit](Images/interface.png)<br>
![metasploit](Images/lhost.png)<br>
After that i ran the next attempt. This time it worked fine. I had a shell on Legacy.
![metasploit](Images/proof.png)<br> 