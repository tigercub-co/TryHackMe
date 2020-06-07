# RP:Nmap

`export IP= 10.10.140.3`

##Nmap Quiz
1) 	
First, how do you access the help menu?
``
nmap --help / nmap -h
``

2) 	
Often referred to as a stealth scan, what is the first switch listed for a 'Syn Scan'?
``
-sS
``

3) 	
Not quite as useful but how about a 'UDP Scan'?
``
-sU
``

4)
What about operating system detection?
``
-O
``

5)
How about service version detection? 
``
-sV
``

6)
Most people like to see some output to know that their scan is actually doing things, what is the verbosity flag?
``
-v
``

7)
What about 'very verbose'? (A personal favorite)
``
-vv
``

8)
Sometimes saving output in a common document format can be really handy for reporting, how do we save output in xml format?
``
-oX
``

9)
Aggressive scans can be nice when other scans just aren't getting the output that you want and you really don't care how 'loud' you are, what is the switch for enabling this? 
``
-A
``

10) 	
How do I set the timing to the max level, sometimes called 'Insane'?
``
-T5
``

11)
What about if I want to scan a specific port?
``
-p
``

12)
How about if I want to scan every port?
``
-p-
``

13)
What if I want to enable using a script from the nmap scripting engine? For this, just include the first part of the switch without the specification of what script to run.
``
--script
``

14)
What if I want to run all scripts out of the vulnerability category? 
``
--script vuln
``

15)
What switch should I include if I don't want to ping the host?
``
-Pn
``

##Nmap Scanning
1)
Let's go ahead and start with the basics and perform a syn scan on the box provided. What will this command be without the host IP address?
``
nmap -Ss
``

2)
After scanning this, how many ports do we find open under 1000?
`sudo nmap -sS $IP`
``
2
``

3)
What communication protocol is given for these ports following the port number?
``
tcp
``

4)
Perform a service version detection scan, what is the version of the software running on port 22?
``
sudo nmap -sV -p 22 $IP
22/tcp open  ssh     OpenSSH 6.6.1p1 Ubuntu 2ubuntu2.10 (Ubuntu Linux; protocol 2.0)
``

5)
Perform an aggressive scan, what flag isn't set under the results for port 80?
``
sudo nmap -A -p 80 $IP
PORT   STATE SERVICE VERSION
80/tcp open  http    Apache httpd 2.4.7 ((Ubuntu))
| http-cookie-flags: 
|   /: 
|     PHPSESSID: 
|_      httponly flag not set
| http-robots.txt: 1 disallowed entry 
|_/
|_http-server-header: Apache/2.4.7 (Ubuntu)
| http-title: Login :: Damn Vulnerable Web Application (DVWA) v1.10 *Develop...
|_Requested resource was login.php
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Aggressive OS guesses: Linux 3.10 - 3.13 (95%), ASUS RT-N56U WAP (Linux 3.4) (95%), Linux 3.16 (95%), Linux 3.1 (93%), Linux 3.2 (93%), AXIS 210A or 211 Network Camera (Linux 2.6.17) (92%), Sony Android TV (Android 5.0) (92%), Android 5.0 - 6.0.1 (Linux 3.4) (92%), Android 5.1 (92%), Android 7.1.1 - 7.1.2 (92%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 2 hops
``

6)
Perform a script scan of vulnerabilities associated with this box, what denial of service (DOS) attack is this box susceptible to? Answer with the name for the vulnerability that is given as the section title in the scan output. A vuln scan can take a while to complete. In case you get stuck, the answer for this question has been provided in the hint, however, it's good to still run this scan and get used to using it as it can be invaluable. 
``
http-slowloris-check
``