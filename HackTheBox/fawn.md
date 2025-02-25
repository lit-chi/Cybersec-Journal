This ctf is also very easy difficult and is also from starting point.

This ctf has a total of 11 tasks.

task 1-4 and 8,10,11 is common theory

![](<images/fawn_1.png>)
Checking the connectivity

nmap scan to see open ports
![](<images/fawn_2.png>)

task 5 is to find which ftp is running on target
We connect to ftp server by
![](<images/fawn_3.png>)
Here, we can see what ftp is used.

Task 6 is to find the OS running on target.
nmap -sV 10.129.167.206 gives the os that is being run.
![](<images/fawn_4.png>)
we can see the the os running is unix.

task 7 is the command used to display ftp client menu which is:
![](<images/fawn_5.png>)

task 9 is to find the response code on successfull login.
![](<images/fawn_6.png>)
we can see that the code is 230

To find the root flag we check the files in the ftp server. We see that there is a file called flag.txt.
![](<images/fawn_7.png>)
We use 'get' to download the flag.txt into our system and that file contains the root flag.
![](<images/fawn_8.png>)