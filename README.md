# Bandit-The-Game

## Week_2 Write up 

### LEVEL 11 to LEVEL 12 

Level Goal 

The password for the next level is stored in the file data.txt, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions 

``ssh bandit11@bandit.labs.overthewire.org -p 2220`` 

`ls` 

``cat data.txt`` 

define a shell function. Here’s how you can define a rot13 function: 

  ![Screenshot from 2023-10-27 19-13-34](https://github.com/Harsha-creates/Bandit-The-Game/assets/68886253/78230066-64b9-47da-8723-9ab2280b98b9)


***The password is JVNBBFSmZwKKOP0XbFXOoW8chDz5yVRv*** 

[SOURCE](https://devicetests.com/decode-rot13-text-command-line)


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

### Level 15 → Level 16

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

### Level 16 → Level 17

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

`ssh -i wood bandit17@localhost -p 2220`


### Level 17 → Level 18

Level Goal

There are 2 files in the homedirectory: passwords.old and passwords.new. The password for the next level is in passwords.new and is the only line that has been changed between passwords.old and passwords.new

`ssh -i wood bandit17@localhost -p 2220`

`ls`
>passwords.new  passwords.old

To see the difference b/w two files use `diff` command

`diff passwords.new passwords.old`

![image](https://github.com/Harsha-creates/Bandit-The-Game/assets/68886253/1346d858-74b9-48e1-9a4b-a4b26cee2ea2)

 ***Password is hga5tuuCLF6fFzUpnagiMN8ssu9LFrdg***

 
### Level 18 → Level 19

Level Goal

The password for the next level is stored in a file readme in the homedirectory. Unfortunately, someone has modified .bashrc to log you out when you log in with SSH.

Unfortunately, we cannot logged in 

In order retrieve the password use `cat` along with log in command

`ssh bandit18@bandit.labs.overthewire.org -p 2220 cat readme`

![image](https://github.com/Harsha-creates/Bandit-The-Game/assets/68886253/75a3dfb7-29dc-4b4c-b23f-c8a9792efa7c)

***password: awhqfNnAbc1naukrpqDYcF95h7HoMTrC***

### Level 19 → Level 20

Level Goal

To gain access to the next level, you should use the setuid binary in the homedirectory. Execute it without arguments to find out how to use it. The password for this level can be found in the usual place (/etc/bandit_pass), after you have used the setuid binary.

`ssh bandit19@bandit.labs.overthewire.org -p 2220`

`./bandit20-do`
>Run a command as another user.
>Example: ./bandit20-do id

` ./bandit20-do cat /etc/bandit_pass/bandit20`

***VxCazJaVykI6W36BkBU0mJTCM8rR95XT***

### Level 20 → Level 21

Level Goal

There is a setuid binary in the homedirectory that does the following: it makes a connection to localhost on the port you specify as a commandline argument. It then reads a line of text from the connection and compares it to the password in the previous level (bandit20). If the password is correct, it will transmit the password for the next level (bandit21).

use `nc -l`

`nc -l 1239`

`./suconnect 1239`

![image](https://github.com/Harsha-creates/Bandit-The-Game/assets/68886253/badba239-3da9-415f-a213-a78275745c55)

***NvEJF7oVjkddltPSrdKEFOllh9V1IBcq***

### Level 21 → Level 22

Level Goal

A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.

`cd /etc/cron.d/`

`ls`

`cat cronjob_bandit22`
>@reboot bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
>* * * * * bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null

`cat /usr/bin/cronjob_bandit22.sh`

![image](https://github.com/Harsha-creates/Bandit-The-Game/assets/68886253/745ac82d-c288-4000-8f4f-3893e68e891f)

***WdDozAdTM2z9DiFEQ2mGlwngMfj4EZff***

