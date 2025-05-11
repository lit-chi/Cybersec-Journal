# SQL injection attack, listing the database contents on Oracle<br><br><hr>
This lab is at practitioner level.<br><br>
The target in this lab is similar to the previous lab but the only difference is the databse. This time we have to target an Oracle DB.
<br>
On accessing the lab we're directed to the same page. I'm gonna start burp on the side.<br>
Everything is pretty similar, so i'm moving under the same assumptions about the data presented on the site like the previous labs. The category table has 2 columns both of type varchar.<br><br>
Now on injecting a query for checking the tables in all_tables (since oracle) that contain user, I'll get the value of the names of the tables which could contain user credentials in this databse.<br><br>
![alt text](<images/SQL injection attack, listing the database contents on Oracle_1.png>)

I'll try the table USERS_JKSIQW first as it seems intersting to me.<br>
![alt text](<images/SQL injection attack, listing the database contents on Oracle_2.png>)
<br> Now there seems to be a username and password column so i'm going to see the data available in the table.<br><br>
On displaying data we see,<br>
![alt text](<images/SQL injection attack, listing the database contents on Oracle_3.png>)<br>
The administrator username and password do exist in this table. Now all that's left is to go and put this in the login page.<br><br>
![alt text](<images/SQL injection attack, listing the database contents on Oracle_4.png>)
and on entering these...<br>
![alt text](<images/SQL injection attack, listing the database contents on Oracle_5.png>)
<br>Entered as administrator successfully.
<br>The lab is solved.