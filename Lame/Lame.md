##### Nmap Scan against Lame Machine on 10.10.10.3

nmap -A -T4 -p- 10.10.10.3<br><br>
Findings:<br>

![nmap scan](Images/nmapscan.png)<br>
There are a couple vulnerabilities on this machine. vsFTPd 2.3.4 could be used, as well as Samba 3.0.20. <br>
![vsFTP exploit](Images/vsftp.png)<br>
![Samba exploit](Images/msf1.png)<br>
I used the Samba module. First to set are the RHost & LHost options. Targeting is automated. After that run the module.<br>
![Shell](Images/shell.png)
And we have a shell with root access. 