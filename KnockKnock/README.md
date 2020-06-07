# KnockKnock

`export IP=10.10.163.186`

## Pwn the box
First stage is to do an initial nmap Scan of the IP address given using the nmpa command `nmap -sC -sV -oN nmap/initial $IP`
Once the results from this scan are given which shows that port 80 is open we can do some web enumeration will running a full port scan of the box `nmap -p- -sC -sV -oN nmap/Full $IP`

While that is running we can use gobuster to do a full website `gobuster dir -u http://$IP:80 -w /usr/share/wordlist/dirbuster/directory-list-2.3-medium.txt > gobuster/sitescan`
We can also check out the website and see if that holds any clues manually.

![]()

This page allows us to download a  [pcap file]()

opening the pcap file it allows us to find that the following ports need to be knocked 7000 8000 9000 7000 8000 9000 8888, to knock the box we will use a python script downloaded from the git repo [knock](https://github.com/grongor/knock) built by grongor.

Using the knock script and telneting to port 8888 with the following code `python3 knock.py 7000 8000 9000 7000 8000 9000 8888 && telnet $IP 8888` it responds with the following directory `burgerworld`

![]()

this is then used to browse the webpage `http://10.10.163.186/burgerworld` this opens a new web page which can download a new [pcap file]()

![]()

When looking at the new pcap file there are a lot information put there is one which is a large tcp stream

![]()

if looking at the stream you can see that it ends in the german eins drein eins sieben or 1 3 1 7. We can use this information to knock those ports on the box `python3 knock.py 1 3 1 7 && telnet $IP 1317`

this then allow us to respond with the following `/iamcornholio/` and so we can go to that webpage `http://10.10.163.186/iamcornholio` this returns a page with the following base64 message  `T3BlbiB1cCBTU0ggIDg4ODggOTk5OSA3Nzc3IDY2NjYK` This can be decoded using [CyberChef](https://gchq.github.io/CyberChef/) and decodes to `Open up SSH  8888 9999 7777 6666` 

![]()

Now that we have that information we can knock the ports and listen on ssh with the following command `python3 knock.py 8888 9999 7777 6666 && SSH $IP` this then opens an SSH shell and gives us the username and password for a ssh user

![]()

We can then use SSH directly to get a better view of the box and try to get the final flag so we loginto ssh with the following `ssh butthead@$IP` and enter the password `nachosrule` but when we log in we get a message saying that `You are only logged in for a split second!What do you do!`

![]()

searching the internet for if you have issues with bash shell you can come accrosss the following [stackexchange page.](https://unix.stackexchange.com/questions/238690/ssh-into-a-server-that-has-a-broken-bash-install)
Using that page It tells us to edit the ssh login to `ssh -t butthead@$IP /bin/bash`

![]()

now that we have access to  the box we want to be able to esculate our permission to root. While trying some of the simple exploits like `sudo -l` to see if there are any exact issues we find out using `uname -a` the linux verison that is being run is onl version at being `3.13.0`. Searching the web for exploits we come across the following exploit within the exploits db: [exploit 37292](https://www.exploit-db.com/exploits/37292)

Using that information we need to download the exploit and wget it onto our box in the temp folder then once the c code is in on the box in our temp folder we run the following commands
`
gcc 37292.c -o ofs
`
and when using id it shows we are now root
![]()

now that we are root we can go to `/root` and find the file `SECRETZ`
![]()