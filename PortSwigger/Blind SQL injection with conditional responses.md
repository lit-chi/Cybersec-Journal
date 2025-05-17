# Blind SQL injection with conditional responses
<hr><br>

### Level: Practioner
<br>
As we enter the lab, we are directed to this page.<br>
![alt text](<images/Blind SQL injection with conditional responses_1.png>)
<br>
This lab is to demonstrate a blind SQL injection vulnerability. So we cannot see the changes/outputs like we've been doing in the previous labs. Normally you'd see the results of the SQL query on the page but in this you won't see it directly. However you'll have to infer it based on the application behaviour. So things such as UNION attacks aren't valid here. <br>
In this lab we have to utilize a tracking cookie to exploit vulnerability.<br>
This means that the application uses in this case a cookie to track the analysis about usage. In the site we can see a "welcome back! " message. That means the site checks if the tracking id contained in the cookie already exists in the DB. If it does then it shows welcome back!. We can inject an SQL query along with the tracking ID so that when the SQL query runs in the backend to check if it exists, instead of the standard query, our malicious query will run.<br><br>
First we inspect site and go to the storage header and under cookies we can see a cookie called "trackingid"<br>
![alt text](<images/Blind SQL injection with conditional responses_2.png>)
<br><br>
Instead of doing it directly in the browser i'm gonna move to Burp and then do it over there.<br>
In Burp I just forward the GET request in the dashboard to the repeater and over there I can make changes to the cookie value.<br>
![alt text](<images/Blind SQL injection with conditional responses_3.png>)
<br><br>
Now, just to check if the cookie is vulnerable to SQLi we add a condition to the cookie so that if it is true the the query will return a true value and the site will show "welcome back" else it won't show "welcome back".
<br>
The condition is 1=1 which is always true.<br>
![alt text](<images/Blind SQL injection with conditional responses_4.png>)
<br>We can see the Welcome back is displayed and if we true with 1=2 [which is false].<br>
![alt text](<images/Blind SQL injection with conditional responses_5.png>)
There is no "Welcome Back" displayed.<br><br>
SO we now know that we can add a boolean value to the query so that if the value is false then "welcome back" is not shown and if it's true, then "welcome back" is shown.
<br>
Now to confirm that the table given exists we will again add a boolean to the end of the query.<br>
select 'a value' from users; is a query to select that value from users table. If it's the name of a column in the user's table, then it returns the data in that column from the users table. We can also put a string instead there like -> select "string" from users; . This will display the value "string" for the number of rows in the table.<br>
we can equate that string to it's own value by doing (select statement)=string-value.<br>
So if the table exists, then the select works and then the value of this is true. If it doesn't exist then the select doesn't work and the value is false. However we do need to keep in mind that the number of times the "string" is returned is the number of row's in that table. So we need to limit it to one by using the limit clause.<br>
So the statement becomes -> (select "string" from table_name limit 1)="string"<br>
![alt text](<images/Blind SQL injection with conditional responses_6.png>)<br>
So the 'users' table does exist.<br><br>
Now to check if the 'administrator' username exists within this table.<br>
![alt text](<images/Blind SQL injection with conditional responses_7.png>)
So an 'administrator' username does exist.<br><br>
Now onto finding out the length of the password for this username.<br>
The way to find password is to add another condition in our select query such that it only returns 'string' if username is administrator and the length(password)= "a value". We need to replace this value with 1,2,3,.... till we get the length. Now i'm going to use Burp intruder isntead of doing it  manually.<br>
So in intruder I mark that length(password)=1 and mark 1 as payload. So 1 keeps getting replaced by values in my payload list. In the payload list i've added numbers from 1 to 30 and intruder will replace these and give me the responses.<br>
![alt text](<images/Blind SQL injection with conditional responses_8.png>)<br><br>
On starting the attack I get the responses. I'll keep going through till I see a welcome back message.<br>
![alt text](<images/Blind SQL injection with conditional responses_9.png>)
And the message is got at length = 20.<br>
Now that i know the length i can try to find the values the same way.<br><br>

> **Note:** I realised that instead of doing it like , I could have done it an easier way by putting the payload type as number and then specifying a range and it would substitute within that range.

Now to check the password we will have to check each individual character of the 20 length password for possible values from a to z or 0 - 9. We can do this in intruder itself.<br>
we modify the query to be <br>
select (substring(password,'number',1) from users where username= 'administrator')='character'<br>
Now the number in the substring refers to the character index in the password and the character we are equating to will be to check whihc character is being replaced. <br>
the number will be replaced from payload from 1-20 and can be done using the number type payload and giving the range there.<br>
The character can be replaced using brutefore from a list of character which will be 'qwertyuiopasdfghjklzxcvbnm1234567890' . Basically, all the alphanumeric characters. And we'll check the responses for these where each alphabet shows a welcome back and then we know which is where.<br><br>
![alt text](<images/Blind SQL injection with conditional responses_10.png>)
<br><br>
![alt text](<images/Blind SQL injection with conditional responses_11.png>)
<br>Now we can start the intruder and wait for it to get the results. This will take a long time on community version, so I waited for long. Finally I got the answer. Portswigger did mention that experts use some form of binary search or somethign to shorten the time. So i'll try seeing how that goes about and using that soon.<br>
![alt text](<images/Blind SQL injection with conditional responses_12.png>)
<br>Once the resutls are out, take the one's with different length as those are the one's where the welcome back is there..to find those i just sorted based on length and at the bottom all those were gathered together. Then i wrote down the ones at different indices joined the charcter and got the password.<br>
Just enter that password into the login page and the lab is solved.✔️<br><br>
> This lab took very long. So sometime the session for the lab did expire which is why i've got a different cookie somewhere in between.