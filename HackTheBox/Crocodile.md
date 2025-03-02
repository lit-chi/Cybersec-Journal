This is a very easy difficulty ctf from tier 1 of starting point.
based on ftp i think

Task1 is a theory question on what swithc employes scanning defaults scripts which is -sC.

task 2 requires us to find the service running on port 21.
![alt text](images/crocodile_1.png)

task  3 is to find the code returned to us for 'anonymous login allowed' message:
![alt text](images/crocodile_2.png)

task 4 is to login to ftp server anonymously:
![alt text](images/crocodile_3.png)

task 5: we use get command to download the files from FTP server.
![alt text](images/crocodile_4.png)

task 6:
![alt text](images/crocodile_5.png)
from these usernames, the higher privileage username seem's like the obvious 'admin' username.

task7:
in our nmap scan earlier for the version we also saw an appache http server running on port 80.

task8:
The switch used to search for specific file extensions in gobuster is -x.

task9:
We use gobuster to search for the files with .php
![alt text](images/crocodile_6.png)

Now to find the flag.
we know that there exists a login page. So we go to the site http://10.129.50.226/login.php
![alt text](images/crocodile_8.png)

We need username and password. If we recall, we had got a file allowed.userlist from ftp server. We had a password file in that server too. So we go and install that. Therby getting username and password.
![alt text](images/crocodile_7.png)
we have the last username as admin and the last password in the password file would be it's password.
![alt text](images/crocodile_9.png)
We are redirected to a site. There the flag is given. Therefore flag obtained.