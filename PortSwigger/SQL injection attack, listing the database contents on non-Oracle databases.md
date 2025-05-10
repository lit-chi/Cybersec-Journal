# SQL injection attack, listing the database contents on non-Oracle databases
<br>
<hr><br><br>
This is a practitioner level lab in SQL injection topic.
<br>
On accessing the lab it has the same layout. I also start burp.<br>
First I login as the administrator.

![alt text](<images/SQL injection attack, listing the database contents on non-Oracle databases_1.png>)
This might help me access the database contents if I don't have access.
Well after a couple of tries with different usernames and comment syntaxes i've realised that the login page doesn't seem to be weak to sql injection. I might need to find these out a different way.
<br><br>
I tried the category filter to see if that had some vulerability.<br>
![alt text](<images/SQL injection attack, listing the database contents on non-Oracle databases_2.png>)
And it did. It seems to be the same with 2 columns of varchar type.<br>
<br>
Now i got all the tables from the information_schema and filtered it by only allowing tables with "user" in their name to appear.<br>
![alt text](<images/SQL injection attack, listing the database contents on non-Oracle databases_3.png>)
<br>
Now that i've got the tables i have to iterate through each to check their columns and see if there is a password and username field in them. I've chosen pg_user first as it's the first on that list.<br>
And on getting the columns in it, there are is a field for password and username.<br>
![alt text](<images/SQL injection attack, listing the database contents on non-Oracle databases_4.png>)
<br> So on getting the data I get..
![alt text](<images/SQL injection attack, listing the database contents on non-Oracle databases_5.png>)
The password for administrator isn't there and neither are the passwords shown so i'm gonna move onto the next table.
<br><br>
The users_feyoaw table looked kinda intersting to me so I tried reading from it.
![alt text](<images/SQL injection attack, listing the database contents on non-Oracle databases_6.png>)
And it did have a username and passoword field.<br> On reading the contents of those columns in the table i get...
<br>
![alt text](<images/SQL injection attack, listing the database contents on non-Oracle databases_7.png>)
Two users carlor and administrator and their login details. Nice.<br><br>
![alt text](<images/SQL injection attack, listing the database contents on non-Oracle databases_8.png>)
And on entering the details, voila i've finally entered as administrator.
<br><br>
It seems that the lab is solved. I had thought that I would need to access some tables which i wouldn't have access to normally. But it seems I had not really understood the aim of the lab. 