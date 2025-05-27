# Blind SQL injection with conditional errors
<hr><br>

### <u>Level:</u> Practioner

This lab seems to be to trigger an error to check for a condition that we give so that if the condition is true then an error comes else it doesn't or vice versa.<br><br>
On accessing the lab we are greeted by this site.<br>
![alt text](<images/Blind SQL injection with conditional errors_1.png>)
<br><br>
Initially, gotta find out where the vulnerability is there. So I try the categories parameter for vulnerability by adding a ' to the end. It ran fine, if I add another ' , it still ran fine because the backend sql engine is treating that data as a string itself and not directly using it in a query. Therefore it is not vulnerable.<br>
Now I can move onto the cookies and see if they are vulnerable. Starting with the tracking id cookie. When i put one ' it's fine but when I put two ' , it show's an error. Therefore the mismatch in quotes is causing the database to throw an error which is becuase the input isn't being sanitized. This means that the cookie is vulnerable.<br><br>
We're going to try injecting a query to purposely trip an error if the condition we specify is true. <br>
The query is going to be like: <br>
< tracking id > ' union select case<br>
&nbsp; &nbsp; &nbsp;when (username='administrator' and ascii(substr(password,1,1)) = <ascii_value>)<br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;Then to_char(1/0)<br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;else null<br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;end<br>
&nbsp; &nbsp; &nbsp;from users --<br><br>
Here the condtions inside the when paranthesis is checked and if true then it runs the condtion in the then part. The then in this case contains a to_char(1/0) which means to convert the result of the operation inside into a string. The operation inside however will return an error as it is a 1/0 operation that is 1 divided by zero which is a divisibility error.<br><br>
Testing out the query which 'a' ...<br>
![alt text](<images/Blind SQL injection with conditional errors_2.png>)
<br>There is no error so the first letter isn't 'a'.<br>
To save time i'm going to use the same logic as the previous lab and make a binary search script through which I can get the password.<br>
The logic is for a condition -> error on page then true else false<br><br>
First I will try to find out the length of the password. To do that I use the same query as above but just modify the password subtring part to length(password) = payload.<br>
![alt text](<images/Blind SQL injection with conditional errors_3.png>)
On doing that now I can run an intruder attack and check where the response is an error and in the image we can see that the response error is received at the password length = 20.<br><br>
The site will show "Internal Server Error". Therefore the checking in the python script must be if there is an error in the text got by the GET request.<br>
![alt text](<images/Blind SQL injection with conditional errors_4.png>)
<br><br>
I just edited the binary script I had made earlier. And on running it I get..<br>
![alt text](<images/Blind SQL injection with conditional errors_5.png>)
The password was generated succesfully.<br><br>
The python script I used is there in my github account. The link to it is here -> 
[Script](https://github.com/lit-chi/Portswigger-lab-python-script/blob/master/Blind_sqli_with_conditional_responses_script.py)
<br><br>
Now on entering the paasword into the login page.<br>
![alt text](<images/Blind SQL injection with conditional errors_6.png>)
<br>Succesfully completed the lab.✔️