# Bandit-The-Game
Write up 

### LEVEL 12 to LEVEL 13 

Level Goal 

The password for the next level is stored in the file data.txt, which is a hexdump of a file that has been repeatedly compressed. For this level it may be useful to create a directory under /tmp in which you can work using mkdir. For example: mkdir /tmp/myname123. Then copy the datafile using cp, and rename it using mv (read the manpages!) 

 

``ssh bandit12@bandit.labs.overthewire.org -p 2220``

``mkdir /tmp/nuke ``
``cp data.txt /tmp/nuke``
``bandit12@bandit:~$ cd /tmp/nuke``

``bandit12@bandit:/tmp/nuke$ ls``
>data.txt

``bandit12@bandit:/tmp/nuke$ file data.txt`` 
>data.txt: ASCII text

``bandit12@bandit:/tmp/nuke$ xxd -r data.txt``
>�h44�z��A����@=�h4hh������hd����������������9���1����������;,�
�����2�3d*58�~  �S�ZP^��luY��Br$�FP!%�s��h�?�)[=�h��O(B��2A���)�tZc��:�pã)�A�ˈ�0���΅A�yjeϢx,�(����z�E�+"�2�/�-��e"���^����t�j���$�d�@�dJơ'7\���$��m1c��#>�aԽ�EV��F��OCӐc@M�C���]��Y2^h8���D=��~	O�I��NDpF�+�|b#Jv�#�J��d�LފW$�Û�͖y�`
                                                                                           �\&	��[�@*w�M�0θ��nr��C��`e$b�
                                                                                                                          ~�{���
                                                                                                                                ��`�<����a��?e:T���e�T4±b����)


``xxd -r data.txt nuke1``

 
![Screenshot from 2023-10-28 11-00-20](https://github.com/Harsha-creates/Bandit-The-Game/assets/68886253/acd38d18-57cf-4af2-90d1-58703ee28049)

***The password is wbWdlBxEir4CaE8LaPhauuOo6pwRmrDw***


### Level 13 to Level 14

Level Goal

The password for the next level is stored in /etc/bandit_pass/bandit14 and can only be read by user bandit14. For this level, you don’t get the next password, but you get a private SSH key that can be used to log into the next level. Note: localhost is a hostname that refers to the machine you are working on

`ssh bandit13@bandit.labs.overthewire.org -p 2220`

`ls`
>sshkey.private

`ssh bandit14@localhost -i sshkey.private`
>!!! You are trying to log into this SSH server on port 22, which is not intended.

bandit14@localhost: Permission denied (publickey).

So we have use the port 2220

`ssh bandit14@localhost -i sshkey.private -p 2220`

### Level 14 to Level 15

Level Goal

The password for the next level can be retrieved by submitting the password of the current level to port 30000 on localhost.

To get the current level password change the directory into `/etc/bandit_pass`

`cd /etc/bandit_pass/`

`cat bandit14`
>fGrHPx402xGC7U7rXKDaxiWFTOiF0ENq

Use `telnet` to connect localhost at port `30000`

`telnet localhost 30000`

![Screenshot from 2023-10-28 17-02-35](https://github.com/Harsha-creates/Bandit-The-Game/assets/68886253/44c7d3f9-7b75-4817-823e-62b888c55cf8)

***Password is jN2kgmIXJ6fShzhT2avhotn4Zcka6tnt***

###Level 15 → Level 16

Level Goal

The password for the next level can be retrieved by submitting the password of the current level to port 30001 on localhost using SSL encryption.

`ssh bandit15@bandit.labs.overthewire.org -p 2220`

get the password of current level by using command 

`cat /etc/bandit_pass/bandit15`

>jN2kgmIXJ6fShzhT2avhotn4Zcka6tnt

Connect to localhost using`ssh` through `s_client` at port `30001`

`openssl s_client -connect localhost:30001`

![Screenshot from 2023-10-28 17-37-01](https://github.com/Harsha-creates/Bandit-The-Game/assets/68886253/b360b3e0-646e-4277-b3ba-56438e23c16d)

>Password is JQttfApK4SeyHwDlI9SXGR50qclOAil1

[Source](https://www.openssl.org/docs/man1.0.2/man1/openssl-s_client.html)

###Level 16 → Level 17

Level Goal

The credentials for the next level can be retrieved by submitting the password of the current level to a port on localhost in the range 31000 to 32000. First find out which of these ports have a server listening on them. Then find out which of those speak SSL and which don’t. There is only 1 server that will give the next credentials, the others will simply send back to you whatever you send to it.

get the password of current level by using command 

`cat /etc/bandit_pass/bandit16`

>JQttfApK4SeyHwDlI9SXGR50qclOAil1

scan ports using `nmap` to know how to use nmap use command `nmap --help`

`nmap localhost -p 31000-32000`

![Screenshot from 2023-10-28 18-22-23](https://github.com/Harsha-creates/Bandit-The-Game/assets/68886253/a61bd4bc-046b-452f-9076-c096f217afe0)


`nmap localhost -p 31046,31518,31691,31790,31960 -sV`

![image](https://github.com/Harsha-creates/Bandit-The-Game/assets/68886253/b728a48b-75f8-4d19-a562-0bf413d9a68f)

Try both ports

`openssl s_client -connect localhost:31518` doesn't give the password

`openssl s_client -connect localhost:31790` give RSA Private key

![image](https://github.com/Harsha-creates/Bandit-The-Game/assets/68886253/323f7490-194e-4c0a-9d4e-d23afffe13af)

create a new directory in `/tmp/` 

`mkdir /tmp/nuke`

Store RSA key in a file using `nano`

`nano wood`

check permissions of RSA file using `ls -la`

change the perrmission to private usng command `chmod 600 wood`













