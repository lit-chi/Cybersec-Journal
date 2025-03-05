This is the Archetype CTF from tier 2 starting point.
It's based on mysql, smb ,powershell...

Let's first connect to the network and check if the system is running.
![alt text](images/archetype_1.png)
As we can see the ping is succesfull so we know our machine is up and running.

task1:
Our task is to find the TCP port hosting a database service. On performing a nmap scan we see,
![alt text](images/archetype_2.png)
Port 1433 is running a ms-sql-s which is a databse service. Therefore the port 1433 is the answer for task1.

task2:
First we list out the avaiable shares on the target machine using smbclient.
![alt text](images/archetype_3.png)
On listing it out we can see that there are three admin shares (the ones that end with $).
The task is to find the non-administrative share. The only non admin share is 'backups'.

task3:
