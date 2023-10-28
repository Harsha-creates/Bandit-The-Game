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


