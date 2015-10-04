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

The password for the next level is "ougahZi8Ta"
