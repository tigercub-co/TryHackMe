#Blue

`export IP=10.10.231.245`

Deploy & hack into a Windows machine, leveraging common misconfigurations issues.

##Recon

``
sudo nmap -sC -sS -oN nmap/Initial $IP
``

2)
How many ports are open with a port number under 1000?
``
3
``

3)
What is this machine vulnerable to? (Answer in the form of: ms??-???, ex: ms08-067)
``
MS17-010
``

##Gain Access
1) 	
Start Metasploit
 	
2)
Find the exploitation code we will run against the machine. What is the full path of the code? (Ex: exploit/........)
``
exploit/windows/smb/ms17_010_eternalblue
``

3) 	
Show options and set the one required value. What is the name of this value? (All caps for submission)
``
RHOSTS
``

4) 	
Run the exploit!

5) 	
Confirm that the exploit has run correctly. You may have to press enter for the DOS shell to appear. Background this shell (CTRL + Z). If this failed, you may have to reboot the target VM. Try running it again before a reboot of the target. 

# Escalate 

1) 	
If you haven't already, background the previously gained shell (CTRL + Z). Research online how to convert a shell to meterpreter shell in metasploit. What is the name of the post module we will use? (Exact path, similar to the exploit we previously selected) 
``
post/multi/manage/shell_to_meterpeter
``

2 	
Select this (use MODULE_PATH). Show options, what option are we required to change? (All caps for answer)
``
SESSION
``

3 	
Set the required option, you may need to list all of the sessions to find your target here. 

4 	
Run! If this doesn't work, try completing the exploit from the previous task once more.

5 	
Once the meterpreter shell conversion completes, select that session for use.

6 	
Verify that we have escalated to NT AUTHORITY\SYSTEM. Run getsystem to confirm this. Feel free to open a dos shell via the command 'shell' and run 'whoami'. This should return that we are indeed system. Background this shell afterwards and select our meterpreter session for usage again. 

7 	
List all of the processes running via the 'ps' command. Just because we are system doesn't mean our process is. Find a process towards the bottom of this list that is running at NT AUTHORITY\SYSTEM and write down the process id (far left column).

8 	
Migrate to this process using the 'migrate PROCESS_ID' command where the process id is the one you just wrote down in the previous step. This may take several attempts, migrating processes is not very stable. If this fails, you may need to re-run the conversion process or reboot the machine and start once again. If this happens, try a different process next time. 

#Cracking 
1)
Within our elevated meterpreter shell, run the command 'hashdump'. This will dump all of the passwords on the machine as long as we have the correct privileges to do so. What is the name of the non-default user? 
``
Jon
``

2) 	
Copy this password hash to a file and research how to crack it. What is the cracked password?
``
alqfna22
``

#Find Flags
`find -f flag*.txt`
`type flag8.txt`

1 	Flag1? (Only submit the flag contents {CONTENTS})
``
access_the_machine
``

2 	

Flag2? Errata: Windows really doesn't like the location of this flag and can occasionally delete it. It may be necessary in some cases to terminate/restart the machine and rerun the exploit to find this flag. This relatively rare, however, it can happen. 
``
sam_database_elevated_access
``

3 	
flag3?
admin_documents_can_be_valuable