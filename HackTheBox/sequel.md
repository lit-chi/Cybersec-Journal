This is a ctf of very easy difficulty from tier 1 starting point.

This ctf is also on mysql and vulnerabilities through it.
There are 8 tasks.

Task 1 asks us to find the port serving MySQL
we can find this my a nmap scan
![alt text](images/sequel_1.png)
we see that it is running on port 3306

However the version wasn't displayed so we use '-sC' instead of '-sV'
Task 2 is to find the version
so using nmap again with -sC we can find the version to be mariadb
![alt text](images/sequel_2.png)

task 3,4,5,6 are theory questions which involve some mysql questions
we first connect to the mysql server through the MySQL command line client