### LEVEL 0  

First opened terminal and tried command ssh –help to know how ssh works 

Then, tried  

``ssh bandit0@bandit.labs.overthewire.org -p 2220 ``

 -p 2220 is port and bandit0 is both username and password and logged into the server. 

  

### LEVEL 0 to LEVEL 1 

I ran ls command in terminal to get list of contents in the directory. 

And opened a readme file where the password is stored by using  cat command. 

>Password in readme: NH2SXQwcBdpmTEzi3bvBHMM9H66vVXjL 

 

### LEVEL 1 to LEVEL 2 

I exited the previous server by command     exit 

Then logged into new server       ssh bandit1@bandit.labs.overthewire.org -p 2220      using the password we got in the previous level. 

Then got list of contents in the /home/bandit1 directory by command      ls 

I tried to open the file ‘-’ by using command      cat –   but got an error message because (-) is a special character. 

So, to access the dashed filename we use command     cat ./-  

Password in -:  rRGizSaX8Mk1RTb1CNQoXTcYZWU6lgzi 

 

### LEVEL 2 to LEVEL 3 

The password for the next level is stored in a file called spaces in this filename located in the home directory 

ssh bandit2@bandit.labs.overthewire.org -p 2220 

 ls  

Either use  $ cat ./spaces\ in\ this\ filename  

Or $ cat "spaces in this filename" to open the file. 

Password in the file: aBZ0W5EmUfAf7kHTQeOwd8bauFJ2lAiG 

 

### LEVEL 3 to LEVEL 4 

The password for the next level is stored in a hidden file in the inhere directory. 

$ ssh bandit3@bandit.labs.overthewire.org -p 2220 

$ ls	 

$ cd inhere/ 

To see the hidden file, we use $ ls –a to see all files in that directory 

$ ls –a 

$ cat .hidden 

Password in .hidden : 2EW7BBsr6aMMoJ2HjW067dm8EgX26xNe 

 

### LEVEL 4 to LEVEL 5 

The password for the next level is stored in the only human-readable file in the inhere directory.  

$ ssh bandit4@bandit.labs.overthewire.org -p 2220 

$ pwd   to check the current directory 

$ ls 

$ cd inhere/     to change into inhere directory 

$ file ./*   to check file and filetype 

./-file07: ASCII text 

$ cat ./-file07 

Password in ./-file07: lrIWWI6bB37kxfiCQZqUdOIYfr6eEeqR 

 

### LEVEL 5 to LEVEL 6 

The password for the next level is stored in a file somewhere under the inhere directory and has all of the following properties: 

    human-readable 

    1033 bytes in size 

    not executable 

 

~$ ssh bandit5@bandit.labs.overthewire.org -p 2220 

$ ls 

$ cd inhere/ 

~/inhere$ find / -type f -size 1033c ! -executable 

source: https://www.computerhope.com/unix/ufind.htm 

Then we check for the file which have the properties 

~/inhere$ cat /home/bandit5/inhere/maybehere07/.file2 

Password in the file: P4L4vucdmLnm8I7Vl7jG1ApGSfjYKqJU 

 

### LEVEL 6 to LEVEL 7 

The password for the next level is stored somewhere on the server and has all the following properties: 

    owned by user bandit7 

    owned by group bandit6 

    33 bytes in size 

 

~$ ssh bandit6@bandit.labs.overthewire.org -p 2220 

$ find / -user bandit7 -group bandit6 -size 33c ; ls –al 

$ cat /var/lib/dpkg/info/bandit7.password 

Password in file: z7WtoNQU2XfjmMtWA8u5rN4vzqu4v99S 

 

### LEVEL 7 to LEVEL 8 

The password for the next level is stored in the file data.txt next to the word millionth 

localhost:~# ssh bandit7@bandit.labs.overthewire.org -p 2220 

ls 

cat data.txt 

bandit7@bandit:~$ cat data.txt | grep millionth 

millionth       TESKZC0XvTetK0S9xNwm25STk5iWrBvP 

Password: TESKZC0XvTetK0S9xNwm25STk5iWrBvPP 

 

 

### LEVEL 8 to LEVEL 9 

The password for the next level is stored in the file data.txt and is the only line of text that occurs only once 

bandit7@bandit:~$ ssh bandit8@bandit.labs.overthewire.org -p 2220 

 ls 

cat data.txt 

To sort the password which is unique and occurs only once 

$ cat data.txt | sort | uniq –u 

Password : EN632PlfYiZbn3PhVK3XOGSlNInNE00t 

 

### LEVEL 9 to LEVEL 10 

The password for the next level is stored in the file data.txt in one of the few human-readable strings, preceded by several ‘=’ characters. 

$ ls 

~$ cat data.txt | strings | grep = 

Password: G7w8LIi6J3kTb8A7j9LgrywtEUlyyp6s 

 

### LEVEL 10 to LEVEL 11 

The password for the next level is stored in the file data.txt, which contains base64 encoded data 

`ssh bandit10@bandit.labs.overthewire.org -p 2220 

bandit10@bandit:~$ ls 

data.txt 

cat data.txt ` 

VGhlIHBhc3N3b3JkIGlzIDZ6UGV6aUxkUjJSS05kTllGTmI2blZDS3pwaGxYSEJNCg== 

bandit10@bandit:~$ echo 'VGhlIHBhc3N3b3JkIGlzIDZ6UGV6aUxkUjJSS05kTllGTmI2blZDS3pwaGxYSEJNCg==' | base64 --decode  

The password is: 6zPeziLdR2RKNdNYFNb6nVCKzphlXHBM 
