# SQL injection UNION attack, finding a column containing text
<hr><br>

This is a practioner level lab.
<br>
The aim in this lab is to reveal the column with text and make the databse return 'oQBNIe'.<br><br>
To do this lab I will add a select statement to the existing query using UNION and then forward it to the server.<br> The new query will be similar to the select statement using NULL for finding the number of columns but instead of null it will have strings.<br> In this case -> 'oQBNIe'<br><br>

On entering the lab i'm greeted with the same website as last lab,<br>
![alt text](<images/SQL injection UNION attack, finding a column containing text_1.png>)
<br><br>
To being I first select a category filter from the given ones and then in Burp, forward that particular request to the repeater. <br>
I'm just checking if the number of columns remain the same as last time by adding the order by clause to the query and the sending that request.<br>
![alt text](<images/SQL injection UNION attack, finding a column containing text_2.png>)
And yes the request show's OK so there's 3 columns returned. <br><br>
Now i'm just going to add select 'oQBNIe',null,null to the query. If i wanted to check if the other columns are also text or if column 1 is of another data type i can shift the string to the side or use more strings instead of null.<br>
Initially i've put the text in column 1.<br>
![alt text](<images/SQL injection UNION attack, finding a column containing text_3.png>)<br>
It returns an error. So it seems that the column 1 is not varchar. I'm going to shift the text to column 2 and set column1 as null.<br><br>
![alt text](<images/SQL injection UNION attack, finding a column containing text_4.png>)
Now i've successfuly got the text displayed on the site and the Lab is solved.✔️