#Crack The Hash

##Level 1

1)
48bb6e862e54f2a795ffc4e541caed4d	=>	MD5
`hashcat -d 2 -m 0 /home/tigercub/Documents/hash /opt/rockyou.txt`
easy

2)
CBFDAC6008F9CAB4083784CBD1874F76618D2A97	=> sha1
`hashcat -d 2 -m 100 /home/tigercub/Documents/hash /opt/rockyou.txt`
password123

3)
1C8BFE8F801D79745C4631D09FFF36C82AA37FC4CCE4FC946683D7B336B63032	=> sha256
`hashcat -d 2 -m 1400 /home/tigercub/Documents/hash /opt/rockyou.txt`
letmein

4)
$2y$12$Dwt1BZj6pcyc3Dy1FWZ5ieeUznr71EeNkJkUlypTsgbX1H68wsRom	=> bcrypt
`hashcat -d 2 -m 3200 /home/tigercub/Documents/hash /opt/rockyou.txt`
bleh

5)
279412f945939ba78ce0758d3fd83daa	=> md4
`hashcat -d 2 -m 900 /home/tigercub/Documents/hash /opt/rockyou.txt`
Eternity22

##Level 2
1)
F09EDCB1FCEFC6DFB23DC3505A882655FF77375ED8AA2D1C13F640FCCC2D0C85 => sha256
`hashcat -d 2 -m 1400 /home/tigercub/Documents/hash /opt/rockyou.txt`
paule

2)
1DFECA0C002AE40B8619ECF94819CC1B => NTLM
`hashcat -d 2 -m 1000 /home/tigercub/Documents/hash /opt/rockyou.txt`
n63umy8lkf4i

3)
$6$aReallyHardSalt$6WKUTqzq.UQQmrm0p/T7MPpMbGNnzXPMAXi4bJMl9be.cfi3/qxIf.hsGpS41BqMhSrHVXgMpdjS6xeKZAs02. 
Salt: aReallyHardSalt
Rounds: 5 =>SHA512crypt
`hashcat -d 2 -m 1800 /home/tigercub/Documents/hash /opt/rockyou.txt`

waka99

4)
e5d8870e5bdd26602cab8dbe07a942c8669e56d6
Salt: tryhackme => Sha1 with salt
`hashcat -d 2 -m 110 /home/tigercub/Documents/hash /opt/rockyou.txt`
481616481616