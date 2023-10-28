# Bandit-The-Game

## Week_2 Write up 

### LEVEL 11 to LEVEL 12 

Level Goal 

The password for the next level is stored in the file data.txt, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions 

``ssh bandit11@bandit.labs.overthewire.org -p 2220`` 

`ls` 

``cat data.txt`` 

define a shell function. Here’s how you can define a rot13 function: 

![Screenshot from 2023-10-27 19-13-34](https://github.com/Harsha-creates/Bandit-The-Game/assets/68886253/f58a372a-9115-4101-8479-8095cde80873)

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

 ![Screenshot from 2023-10-28 11-00-20](https://github.com/Harsha-creates/Bandit-The-Game/assets/68886253/d65c7aa4-b1c6-42da-bef4-930e68fa3f14)


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

![Screenshot from 2023-10-28 17-02-35](https://github.com/Harsha-creates/Bandit-The-Game/assets/68886253/b8a20c1d-9c59-4fc1-9c1f-4491640eb783)


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

![Screenshot from 2023-10-28 17-37-01](https://github.com/Harsha-creates/Bandit-The-Game/assets/68886253/84bafa51-6f48-4b72-8613-85f22b4f7bae)

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

![Screenshot from 2023-10-28 18-22-23](https://github.com/Harsha-creates/Bandit-The-Game/assets/68886253/e37086fa-031f-4ba1-aa1f-53201fcd44ef)

`nmap localhost -p 31046,31518,31691,31790,31960 -sV`

![Screenshot from 2023-10-28 18-26-57](https://github.com/Harsha-creates/Bandit-The-Game/assets/68886253/565fc6f5-997e-4cb6-a417-8e0e6dc98b24)

Try both ports

`openssl s_client -connect localhost:31518` doesn't give the password

`openssl s_client -connect localhost:31790` give RSA Private key

![Screenshot from 2023-10-28 18-36-18](https://github.com/Harsha-creates/Bandit-The-Game/assets/68886253/88b60c16-f7c6-4f1f-9887-1f655d88a32f)

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

![Screenshot from 2023-10-28 19-59-31](https://github.com/Harsha-creates/Bandit-The-Game/assets/68886253/fa35a114-af8f-4055-9231-4afd60259562)

 ***Password is hga5tuuCLF6fFzUpnagiMN8ssu9LFrdg***

 
### Level 18 → Level 19

Level Goal

The password for the next level is stored in a file readme in the homedirectory. Unfortunately, someone has modified .bashrc to log you out when you log in with SSH.

Unfortunately, we cannot logged in 

In order retrieve the password use `cat` along with log in command

`ssh bandit18@bandit.labs.overthewire.org -p 2220 cat readme`

![Screenshot from 2023-10-28 20-11-46](https://github.com/Harsha-creates/Bandit-The-Game/assets/68886253/608ffa93-d360-4661-8674-103caf7f6c3f)

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

![Screenshot from 2023-10-28 20-30-32](https://github.com/Harsha-creates/Bandit-The-Game/assets/68886253/733923c6-c4c7-4b6b-b8d4-57714f3f5137)

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

![Screenshot from 2023-10-28 20-38-00](https://github.com/Harsha-creates/Bandit-The-Game/assets/68886253/02aca5fd-8c8c-4554-9d45-6c4ef2182c5e)

***WdDozAdTM2z9DiFEQ2mGlwngMfj4EZff***

