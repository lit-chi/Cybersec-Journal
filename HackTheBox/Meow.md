A record of the first CTF complete. It is from the starting point at very easy difficulty.

First 5 tasks were common knowledge theory questions.

![alt text](<images/2025-02-24 20_39_57-HTB Viewer.png>)
Pinged the IP initially to check if connection was succesfully established.

Task 6 was to find service in tcp port 23.

![alt text](<images/2025-02-24 20_40_38-HTB Viewer.png>)
Using nmap I found the open port 23 with Telnet service.

Task 7 is to find username with blank password.
By telnet 10.129.49.242 23
I connected to target machine. 
![alt text](<images/2025-02-24 20_42_50-HTB Viewer.png>)
The machine accepted the username root with a blank password.
![alt text](<images/2025-02-24 20_43_20-HTB Viewer.png>)

Task 8 was to find the root flag.
![alt text](<images/2025-02-24 20_46_00-HTB Viewer.png>)
On checking the files we find flag.txt which containts the said root flag.
