# Visible error-based SQL injection
<hr><br>

### <u>Level:</u> Practioner
<br><br>
This lab is titled visible error. Visible errors SQLis are an attack method wherein on entering a incorrect data or queries - the database returns an error. This error will contain some sensitive data of the table. <br><br>

To begin with, I try to check where the vulnerability is there and on adding a single quote to the end of the tracking id I am present with this error.<br>
![alt text](<images/Visible error-based SQL injection_1.png>)
This error itself shows the structure of the query that is running in the backend for tracking id.<br>
If we comment out the part after the single quote we include, the error will disappear.<br><br>
Now, on running a query with AND clause to check for a username in the users table and type cast it to int.
![alt text](<images/Visible error-based SQL injection_2.png>)
This shows that the input given is truncated so we can just shorten the existing cookie.<br>
![alt text](<images/Visible error-based SQL injection_3.png>)
Again an error is received because more than 1 rows are returned. We can limit that by using LIMIT which will return just the value of the first row.<br>
![alt text](<images/Visible error-based SQL injection_4.png>)
Now we get that the first row has the username administrator. If we replace username in the query with password, it should leak the password.<br>
![alt text](<images/Visible error-based SQL injection_5.png>)
<br>And it does!!<br>
<br>
And with that the lab is solved. ✔️
