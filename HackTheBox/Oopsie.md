This is the oopsie challenge from starting point tier 2. It's difficulty is also very easy as all the others.

First we connect using openVPN and use ifconfig to confirm the same.
Now we need to start our target machine. Let's check if the machine is up and running too.
![alt text](images/oopsie_1.png)
Our machine is up and running so let's continue on with the tasks.

task1:
A proxy would be a server that acts as an intermediary between the user's device and net intercepting all web requests and responses before they reach the intended destination.
Answer is "proxy".

task2:
Now to find that we open BurpSuite and then open the link in our browser. When we are led to the webpage we see Burp list out the discovered URL's in the Dashboard and Site map section. There we find our login page URL.
![alt text](images/oopsie_2.png)
When we visit this login URL we see this..
![alt text](images/oopsie_3.png)

task3:
Web apps use cookies to keep track of user logged in. So if access to upload page depends on that cookie we can modify the cookie in the browser to gain access.
The answer to this task is "cookie"

task4:
If we click on log in as guest we see this..
![alt text](images/oopsie_4.png)
We can see that the upper ribbon has a "logged in as guest" confirming we've logged in as guest. 
Now if we go to the accounts section in the ribbon and navigate to the storage section through inspect we see that our URL is a bit different and it specifies ID.
![alt text](images/oopsie_5.png)
Let's try changing that ID number. Since it's 2 for guest, i would assume it would be 1 for something else.
Trying value 1..
![alt text](images/oopsie_6.png)
We've succesfully got the access ID of admin user.
access ID is-> 34322

task5:
Now since we have the access ID we can modify the cookie's as such...
![alt text](images/oopsie_7.png)
and thus we get to the uploads page.
![alt text](images/oopsie_8.png)

Using gobuster in directory enumeration mode we can find the directories in the server.
![alt text](images/oopsie_9.png)
here we can see that there is an "uploads" folder which should be the one which contains the files we are uploading.

We will establish a reverse shell connection by uploading php reverse shell.
We modify the port and ip and also start a netcat listener.
After uploading the file through our uploads we enter the file location url and press enter.
![alt text](images/oopsie_11.png)
we will now have our reverse shell..
![alt text](images/oopsie_10.png)

On going throught the folder we get to a login folder in var/www/html
in that if we search for passw using grep we can try to find matching lines with password in it. And we do findd it.
![alt text](images/oopsie_12.png)

if we navigate to the /etc/ folder we see a passwd file...
on opening that
![alt text](images/oopsie_13.png)
we can find a user called robert at the bottom. So we now try to login as robert..
When we try to enter the password with the one we found earlier however, it registers as a failure..
![alt text](images/oopsie_14.png)

while searching for the password i stumbled upon a robert folder which had the user.txt (user flag)
![alt text](images/oopsie_15.png)
flag-> f2c74ee8db7983851ab2a96a44eb7981

We find our password in the db.php file in the login folder..
![alt text](images/oopsie_16.png)
On using that password we are able to succesfully enter...
![alt text](images/oopsie_17.png)
therefore the password was in file db.php

