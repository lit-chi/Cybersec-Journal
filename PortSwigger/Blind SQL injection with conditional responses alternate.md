# Blind SQL injection with conditional responses alternate methods
<hr><br>

This is a continuation to the previous lab -> 
[Prev lab.](<Blind SQL injection with conditional responses.md>)
<br><br>
In that lab I was able to get the password by bruteforcing using Burp. However that took a long time to do( i believe since i'm using the community version). I learnt that we could create a python script for the same, and one of the creators in the community solutions had a video on it too.<br>
I also made a similar script, I used binary search instead of a sequential search to make the searching process faster.<br>
The script is here -> https://github.com/lit-chi/Portswigger-lab-python-script
<br><br>
So I opened the lab and got the trackerid and session cookies from the cookie section in the browser inspect options.
<br>

![alt text](<images/Blind SQL injection with conditional responses_alt_1.png>)
<br><br>
Now I use the URL, TrackingID value and Session value while calling my python script<br>
![alt text](<images/Blind SQL injection with conditional responses_alt_2.png>)
<br><br>
![alt text](<images/Blind SQL injection with conditional responses_alt_3.png>)
<br>Successfully accessed the adminisitrator account.✔️

<hr>
<br>
Another option to solve this lab would be to use sqlmap.<br>
Sqlmap is a tool for disovering SQL injection vulnerabilites in Web apps.<br><br>
To use this we first get the URL and the cookie values the same way as before.<br>
Then we need to get the database name using this command<br>

    sqlmap -u < url > --cookie="cookie data"  --technique=B --level=3 --risk=3 -dbs

<br>

![alt text](<images/Blind SQL injection with conditional responses_alt_4.png>)
<br><br>
Now we use the following command to get the username and passwords of users in the users table of that database.
   
    sqlmap -u < url > --cookie="cookie data"  --technique=B --level=3 --risk=3 -d public -T users -c username,password --dump

<br>

![alt text](<images/Blind SQL injection with conditional responses_alt_5.png>)
<br><br>
And on putting the credentials into the login field we can enter the administrator account.✔️