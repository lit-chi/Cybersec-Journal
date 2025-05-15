# SQL injection UNION attack, retrieving data from other tables
<hr><br>
This is a practioner level lab.
<br><br>
This lab's aim is to retrive data from another table using SQL injection. The table in question is called "users" and has columns "username" and "password", whose data we need to get.
<br><br>
On accessing lab we get this site...<br>

![alt text](<images/SQL injection UNION attack, retrieving data from other tables_1.png>)
<br><br>
Checking the name and type of columns returned in the URL query.<br>
![alt text](<images/SQL injection UNION attack, retrieving data from other tables_2.png>)
<br>There's 2 columns of type varchar.
<br><br>
Since I know the name of the table and the 2 columns i need to display, I can directly add a select statement to the query using UNION.<br>
![alt text](<images/SQL injection UNION attack, retrieving data from other tables_3.png>)
<br>And i've got the credentials for administrator user.<br><br>
If i didn't know the table or column name i would need to go to and select from all_table or from the information_schema to get the table name first and then use that to check column names.<br><br>
Now I go to the login page of the site and enter the credentials.<br>
![alt text](<images/SQL injection UNION attack, retrieving data from other tables_4.png>)
<br><br>
![alt text](<images/SQL injection UNION attack, retrieving data from other tables_5.png>)
And i've succesfully entered as administrator and the lab is solved.
