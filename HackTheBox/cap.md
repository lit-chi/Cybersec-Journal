# Cap [MACHINE]
<hr><br>

### <u>Level:</u> Easy

This is the first machine i've done in HTB other than the starting point.
<br><br>
To begin with I spawn the machine and then just ping it to confirm we are connected. I also conduct an nmap scan to see the services running on the ports.<br><br>
![alt text](images/cap_1.png)
<br><br>
there is an ftp and ssh session. I initially thought i'd try anonymous login but it didn't work. SSH session can't be started without any key. There was also http service running on port 80. SO i entered the url into the browser.
I was directed to this site.<br>
![alt text](images/cap_2.png)
<br><br>
The site has a user profile and seems to be able to monitor and give information regarding the users network. Like when we go to the Network status option, we can see the output of a netstat command. In fact the url itself mentions the netstat command.<br>
![alt text](images/cap_3.png)
<br>Similarly, the IP config option gives us the result of an ifconfig.<br><br>
On clicking on the security snapshot we are redirected to the dashboard and we see some information such as number of packets sent, number of ip packets etc. <br><br>
There is also a donwnload option which gives us a packet capture file that we can go through using wireshark. 
<br><br>
I was a bit lost after this as I didn't do what do to immediately. Therefore i went to the guided mode and there they had asked the question "Are you able to get to other users' scans?" and the hint was "Try modifying the URL and see what happens. You could also fuzz with a tool like ffuf or wfuzz."<br><br>
So i used fuff on the scan output page url to get this...<br>
![alt text](images/cap_4.png)
I see that all of the directories we enumerated are numbers. On going to those URL's i notice changes in the output of the scan which implies that i'm accessing the scan results of other users. I had noticed among the different directories there was a 0. I went through some other ones but most of them gave me 0 for all the fields in the scan.So i download the results of the 0 directory URL and then use wireshark again to go through it.<br>
This is what it somewhat looks like..<br>
![alt text](images/cap_5.png)
<br><br>
On searching through these packets I come across a series of requests for a login. And these request's contain some sensitive information.<br>
![alt text](images/cap_6.png)
<br>Therefore i've now acquired the username and password that i can use to access the ftp hopefully. <br>
We can use this to access both ssh and ftp. And ssh is the way to go since the aim is to implement a reverse shell that can help us get the flag in the system. That execution of file can be done only in ssh and not in ftp. However I did waste a bit of time in ftp. The user flag i got though and then i went and logged into the ssh session
![alt text](images/cap_7.png)
<br>
![alt text](images/cap_8.png)
<br>
So we've now got into the session as nathan.<br><br>
I then tried the directly putting linpeas through the link in github.
![alt text](images/cap_9.png)
<br>But unfortunately it seems like there isn't an active network connection for the server in question so it's not able to connect to github. I tried checking that by simply pinging github.com and it didn't work.
<br><br>
Now that I can't directly put it into my kali machine, I get linpeas.sh from the github repo and then using a bash tcp file transfer send it from my machine to the target machine.
![alt text](images/cap_10.png)
<br><br>
I was able to succesfully execute it and and then i go through the information that linpeas has given me.
Linpeas says that it marks the critacl vulnerabilities with red and yellow so i look at those first.<br><br>
I notice this vulnerability,<br>
![alt text](images/cap_11.png)
This says that python is allowed to setuid. So python is able to set user id. The userid of root is 0. Therefore running a script which has some commands to change the uid should essentially allow me to become root.<br>
This is the simple script...the first line is setuid and the second one is restartign shell as root.<br>
![alt text](images/cap_13.png)
<br>
Sending this across..<br>
![alt text](images/cap_12.png)
<br>We have successfully become root.<br><br>
Now on simply going to the root directory we can get the root flag.<br><br>
![alt text](images/cap_14.png)
<br><br>
And the machine is solved. ✔️