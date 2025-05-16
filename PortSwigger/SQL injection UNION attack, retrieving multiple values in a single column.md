# SQL injection UNION attack, retrieving multiple values in a single column
<hr><br>

<div style="border: 1px solid black; padding: 10px; margin: 10px;">
This is a box created with HTML.
</div>
<br>
This lab seems to be quite similar to the previous one. I had to get username and password from the users table in the previous lab. This lab seems to ask the same.<br><br>
Anyways, proceeding with the lab. I first access the lab and start burp on the side.<br>
Since the category filter is vulnerable to SQL injection attack, I will forward that request to the repeater so that I can modify it and send it.<br><br>
On accessing the lab, we get to see this page.<br>

![alt text](<images/SQL injection UNION attack, retrieving multiple values in a single column_1.png>)
<br><br>
To check the number of columns I use order by clause to order the data based on a column number.<br>
Initially I check with 2 as I know at least 2 columns are present.
![alt text](<images/SQL injection UNION attack, retrieving multiple values in a single column_2.png>)
<br>Shows successfull<br><br>
Now I try with column 3.
![alt text](<images/SQL injection UNION attack, retrieving multiple values in a single column_3.png>)
<br>Shows error. So there are 2 columns in the table.<br><br>
Now since i'm given the name of the columns and the name of the table, I'll try to directly access the data from that table. I will add inject select query for that to the existing query in the URL.
![alt text](<images/SQL injection UNION attack, retrieving multiple values in a single column_4.png>)
<br>It shows a server error for some reason.<br><br>
The error must have been due to the incorrect type of columns between the two select statements in UNION. When using UNION operator, both querys must have equal number of columns that are of same type in their respective order. That is, if column 1 of first query is varchar then column 1 of second query must also be varchar and if column 2 of first query is integer then column 2 of second query must also be integer.<br>
To check this now, I will use "UNION select" to check the type of the columns. I just need the column with type varchar.<br>
Initially I tried both columns to confirm my suspicions.<br>
![alt text](<images/SQL injection UNION attack, retrieving multiple values in a single column_5.png>)
<br>Yes!! The reason was that the columns weren't both of type varchar.<br><br>
Now i'll put column 2 as varchar to check if it is of that type.<br>
![alt text](<images/SQL injection UNION attack, retrieving multiple values in a single column_6.png>)
<br>Success!! So column 2 is the column where we can display our username and passowrd<br><br>
Unlike the other lab where we displayed both the username and password in different columns, we only have one column available to display over here. So use two selection queries and add them to the URL using UNION so that we can select both the username and password and display them in one column itself.<br>
![alt text](<images/SQL injection UNION attack, retrieving multiple values in a single column_7.png>)
<br><br>
The query went through successfully. We can now get our credentials as marked in the image.
![alt text](<images/SQL injection UNION attack, retrieving multiple values in a single column_8.png>)
<br><br>
Enter the credentials into the login page.
![alt text](<images/SQL injection UNION attack, retrieving multiple values in a single column_9.png>)
<br><br>
![alt text](<images/SQL injection UNION attack, retrieving multiple values in a single column_10.png>)<br>
Logged in as administrator successfully.<br>
The lab is solved.✔️