**Name** - Ruwindu De Silva

**SLIIT ID** - IT12044528

**Curtin ID** - 18297188

#Levoathan 0 to 1
In overthewire wargames site, leviathan 0 page provides the user name and password ro the leviathan 0

Using the "ls" command we can find there is another derectory called ".backup".
Inside of that there is a html file with full of text. So to retrieve the password we use cat command with grep by giveing a keyword as password.

Leviathan 1 pic

The password for the next level is **"rioGegei8m"**

#Bandit 1 to 2
We have retrived the password for this level in previous level.

Using "ls" command we found that there is an exicutable file and executed it. It has protected with password and probably it may contains the password for the next level. To check which function the executable runs we uses the command "ltrace". We can see it runs "strcmp()" function and it compare the user input with the string "sex" and that means the password for that is "sex".

It guids us to another session and by entering "whoami" it says that it is leviathan2. So by entering quick "cat" command we can find the password for the next level.

Leviathan 2 pic
```
leviathan1@melinda:~$ ls -al
total 28
drwxr-xr-x   2 root       root       4096 Nov 14  2014 .
drwxr-xr-x 167 root       root       4096 Jul  9 16:27 ..
-rw-r--r--   1 root       root        220 Apr  9  2014 .bash_logout
-rw-r--r--   1 root       root       3637 Apr  9  2014 .bashrc
-rw-r--r--   1 root       root        675 Apr  9  2014 .profile
-r-sr-x---   1 leviathan2 leviathan1 7493 Nov 14  2014 check
leviathan1@melinda:~$ ./check
password: leviathan1
Wrong password, Good Bye ...
leviathan1@melinda:~$ ltrace ./check
__libc_start_main(0x804852d, 1, 0xffffd7a4, 0x80485f0 <unfinished ...>
printf("password: ")                             = 10
getchar(0x8048680, 47, 0x804a000, 0x8048642password: leviathan
)     = 108
getchar(0x8048680, 47, 0x804a000, 0x8048642)     = 101
getchar(0x8048680, 47, 0x804a000, 0x8048642)     = 118
strcmp("lev", "sex")                             = -1
puts("Wrong password, Good Bye ..."Wrong password, Good Bye ...
)             = 29
+++ exited (status 0) +++
leviathan1@melinda:~$ ./check
password: sex
$ whoami
leviathan2
$ cat /etc/leviatham
cat: /etc/leviatham: No such file or directory
$ cat /etc/levithan_pass/leviathan2
cat: /etc/levithan_pass/leviathan2: No such file or directory
$ cat /etc/leviathan_pass/leviathan2
ougahZi8Ta
$ ougahZi8Ta

```

The password for the next level is **"ougahZi8Ta"**

#Leviathan 2 to 3
We have located an executable file called printfile in the "/home/leviathan2". When we execute that it requires a text file to continue. So We creates a .txt file at /tmp/ans/ derectory and ryn the executable with ltrace. It shows that access() does is check permissions based on the process’ real user ID rather than the effective user ID. Using that vulnerability we get the password for the next level.

```
leviathan2@melinda:~$ ls -la
total 28
drwxr-xr-x   2 root       root       4096 Nov 14  2014 .
drwxr-xr-x 167 root       root       4096 Jul  9 16:27 ..
-rw-r--r--   1 root       root        220 Apr  9  2014 .bash_logout
-rw-r--r--   1 root       root       3637 Apr  9  2014 .bashrc
-rw-r--r--   1 root       root        675 Apr  9  2014 .profile
-r-sr-x---   1 leviathan3 leviathan2 7498 Nov 14  2014 printfile
leviathan2@melinda:~$ ./printfile
*** File Printer ***
Usage: ./printfile filename
leviathan2@melinda:~$ mkdir /tmp/ans
leviathan2@melinda:~$ touch /tmp/ans/ans\ file.txt
leviathan2@melinda:~$ ls /tmp/ans
ans file.txt
leviathan2@melinda:~$ ltrace ./printfile /tmp/ans/ans\ file.txt
__libc_start_main(0x804852d, 2, 0xffffd784, 0x8048600 <unfinished ...>
access("/tmp/ans/ans file.txt", 4)               = 0
snprintf("/bin/cat /tmp/ans/ans file.txt", 511, "/bin/cat %s", "/tmp/ans/ans fil  e.txt") = 30
system("/bin/cat /tmp/ans/ans file.txt"/bin/cat: /tmp/ans/ans: No such file or d  irectory
/bin/cat: file.txt: No such file or directory
 <no return ...>
--- SIGCHLD (Child exited) ---
<... system resumed> )                           = 256
+++ exited (status 0) +++
leviathan2@melinda:~$
leviathan2@melinda:~$
leviathan2@melinda:~$ ln -s /etc/leviathan_pass/leviathan3 /tmp/ans/ans
leviathan2@melinda:~$ ls /tmp/ans
ans  ans file.txt
leviathan2@melinda:~$ ./printfile /tmp/ans/ans
You cant have that file...
leviathan2@melinda:~$ ./printfile /tmp/ans/ans\ file.txt
Ahdiemoo1j
/bin/cat: file.txt: No such file or directory
leviathan2@melinda:~$ ~/
-bash: /home/leviathan2/: Is a directory
leviathan2@melinda:~$ cd ~/
leviathan2@melinda:~$ pwd
/home/leviathan2
leviathan2@melinda:~$
```

Password for the next level is "Ahdiemoo1j"

#Leviathan 3 to 4

Here we can find an executable file called "level3" and whrn it runs it requires a password. To get to know what string is the function is looking for, in other words that is the password, we enter the "strings" command nad it outputs all the strings that contains in the file "level3".

```
leviathan3@melinda:~$ strings ./level3
...
GLIBC_2.0
PTRh@
snlp
rintf
D$L1
D$#bombf
D$'ad
D$8...s
D$<3cr3f
D$@t
D$*h0nof
D$.33
D$1kakaf
D$5ka
D$B*32.
D$F2*[xf
D$J]
T$Le3
[^_]
[You've got shell]!
/bin/sh
bzzzzzzzzap. WRONG
Enter the password>
;*2$"
secret
GCC: (Ubuntu 4.8.2-19ubuntu1) 4.8.2
...
```
Here, clear text before "[You've got shell]!" text, "snlp" and "rintf" is suspicious as the password and we tried that and it gaves a new shell and it is Leviathan4 shell.
By giveing a symple cat command to "/etc/leviathan_pass/leviathan4" file we can retrieve the password for the next level.

```
$ whoami
leviathan4
$ cat /etc/leviathan_pass/leviathan4
vuH0coox6m
$
```
