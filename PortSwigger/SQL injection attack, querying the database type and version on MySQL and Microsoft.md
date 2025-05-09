# <u> SQL injection attack, querying the database type and version on MySQL and Microsoft  </u>
<br>
<hr>
<br>
This lab is at practitioner level.<br>
By the description it seems to be similar to the previous lab, just that the previous lab database was in oracle and this seems to be in MYSQL.

<br>
On entering the site, 
<br><br>

![alt text](<images/SQL injection attack, querying the database type and version on MySQL and Microsoft_1.png>)
The site is pretty similar image to the previous lab. I'm going to try solving this lab using burpsuite this time.<br><br>
So i've opened up Burp in the background and on inspecting it we can find the category filter.
![alt text](<images/SQL injection attack, querying the database type and version on MySQL and Microsoft_2.png>)
<br><br>
To resend the request, that particular request needs to be sent to the repeater. 
![alt text](<images/SQL injection attack, querying the database type and version on MySQL and Microsoft_3.png>)
<br>
Now the URL can be modified and resent.<br><br>
I don't know if this site has all similar paramters to the previous one so i'm going to check for number of columns again.<br>
i'll add the order by clause so "order by < a number >" to the end and keep incrementing the number so that when it returns a error code, I know that the previous number is the number of columns present.<br>
Order by 1:Successful<br>
![alt text](<images/SQL injection attack, querying the database type and version on MySQL and Microsoft_4.png>)
Order by 2:Successful<br>
![alt text](<images/SQL injection attack, querying the database type and version on MySQL and Microsoft_5.png>)
Order by 3:Error<br>
![alt text](<images/SQL injection attack, querying the database type and version on MySQL and Microsoft_6.png>)
<br>So the number of Columns is '2'.
    
> **note:** The Query initially returned an error even at 'order by 1'. This was because I had put the comment using -- and not # .         
![alt text](<images/SQL injection attack, querying the database type and version on MySQL and Microsoft_7.png>)

<br><br>
2 Columns are there in the image and are of string datatype. This is known from the value they show on the website.  But if unsure we can do it by adding " union select 'some string value' " and adjut this query based on the number of columns and status code returned to check which combination gives us a valid status code.<br><br>
Now to get the version value. The syntax for version in MySQL is " select version(); " <br>
So that is appended to the query using UNION operation.<br>
![alt text](<images/SQL injection attack, querying the database type and version on MySQL and Microsoft_8.png>)
And that returns the version number and the lab is solved.
<br><hr>