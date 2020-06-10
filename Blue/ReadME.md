# Blue

`export IP=10.10.231.245`

## Recon

The first stage is to do recon on the machine to find out what ports are open on the Box using the command `sudo nmap -sC -sS -oN nmap/Initial $IP` [nmap file]()

When looking at this file there are 9 ports that are open within the box and as none of the ports look like being one which is acting as a webserver there is no point using a tool like gobuster to recon a webpage.

*Answer from looking at the nmap there are only 3 ports under 1000*

looking at the nmap result it shows that the box is running "Windows 7 Professional 7601 Service Pack 1" so we can google that operating system to find if there are any known vulnrabilities

![google search](https://github.com/tigercub-co/TryHackMe/blob/master/Blue/Images/Google%20search.PNG)

*Answer from the google search it shows that it is vunrable to MS17-010*

## Gain Access

The next stage is to start Metasploit

![metasploit start](https://github.com/tigercub-co/TryHackMe/blob/master/Blue/Images/Metasloit_Start.PNG)

Once it has started we then want to search the metasploit database for ms17-10 using the command `search ms17-010` and metasploit shoudl come back with a list of results

![metasploit search results](https://github.com/tigercub-co/TryHackMe/blob/master/Blue/Images/Metasloit_Search.PNG)

*Answer from the list of available exploits the path required is exploit/windows/smb/ms17_010_eternalblue*

Once we have the path of the exploit we then want to select that exploit from the database using the command `use 2` once it has been selcted we can use the command `info` to get more information about the exploit as well as the basic options.

![module info](https://github.com/tigercub-co/TryHackMe/blob/master/Blue/Images/Metasloit_info.PNG)

*Answer from the Basic Options it shows the required value is the RHOSTS*

as RHOSTS is the required option we want to use the command `set RHOSTS 10.10.209.230` as we want to set the RHOSTS to the IP of the machine.
Once this is done we can then just use the command `run` to run the exploit. and you should know if the exploit was succesful by there being a banner which says win.

![running the exploit](https://github.com/tigercub-co/TryHackMe/blob/master/Blue/Images/running%20the%20exploit.PNG)

once the win banner has been achived we need to run the command `ctrl+z` to allow for the exploit to be backgrounded so that we can try and conver the shell to a meterpreter shell.

## Escalation
As part of escalation is to first get a meterpreter shell so we will search for this within metasploit using the command `search shell_to_meterpreter` and you will recive the following results

![shell search results](https://github.com/tigercub-co/TryHackMe/blob/master/Blue/Images/search%20shell%20to%20meterpreter.PNG)

*Answer from the search results it can be seen the folder is at post/multi/manage/shell_to_meterpreter*

we can then use this result using the command `use 0` we can then use `info` to see the required options.

![Shell info](https://github.com/tigercub-co/TryHackMe/blob/master/Blue/Images/shell%20info.PNG)

*Answer the required option that does not have a prefilled in option is SESSION*

so we can set the require session to use for this exploit by first using the command `sessions` to view all running sessions as well as the ID for each session and then once we have got the required ID we can use the command `set SESSION 1`

![session for shell](https://github.com/tigercub-co/TryHackMe/blob/master/Blue/Images/session%20for%20shell.PNG)

once this has been done we can then just use the command `run` and we will be told that a new session was created and then we can acess that session with the command `sessions 2` to start that session
Once we are in taht session we want to use `ps` to list all processes running and then use `migrate <pid>` to change to a diffrent process.

![migration](https://github.com/tigercub-co/TryHackMe/blob/master/Blue/Images/)

## Cracking
 
Now that we should have a more stable shell on the box we want to try and get the passwords for users on the box we can do this with command `hashdump` 

![hashdump](https://github.com/tigercub-co/TryHackMe/blob/master/Blue/Images/migrate.PNG)

*Answer From the hashdump it shows that there is a user called JON*

![password hash crack](https://github.com/tigercub-co/TryHackMe/blob/master/Blue/Images/passwordhash.PNG)

*Answer it also shows his password hash is ffb43f0de35be4d9917ac0cc8ad57f8d which when cracked gives the answer of alqfna22*

## Find flags

The next stage is to find the three flags there are multiple ways in which this can be done you can search the box manually for the flags or we can try and find 1 flag and then use the box to search for the flag. The first place to search is the C:\ drive and within the C:\ drive we can find flag1.txt and then we can use cat to see the contents `cat flag1.txt`

![flag1](https://github.com/tigercub-co/TryHackMe/blob/master/Blue/Images/flag1.PNG)

*Answer flag 1 is access_the_machine*
now that we now the formation of the box we can run `search -f flag*.txt` which will display where to find the files 

![flag search](https://github.com/tigercub-co/TryHackMe/blob/master/Blue/Images/flagsearch.PNG)

Using the results we can just cat out the two other flags flag 2 and flag 3

![flag2](https://github.com/tigercub-co/TryHackMe/blob/master/Blue/Images/flag2.PNG)
![flag3](https://github.com/tigercub-co/TryHackMe/blob/master/Blue/Images/flag3.PNG)

*Answer flag2 is sam_database_elevated_access*
*Answer flag 3 is admin_documents_can_be_valuable* 
