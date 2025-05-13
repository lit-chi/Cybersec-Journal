# SQL injection UNION attack, determining the number of columns returned by the query
<hr>
<br>
This is a practioner level lab.
<br>
On accessing the lab we are led to this page.<br>

![alt text](<images/SQL injection UNION attack, determining the number of columns returned by the query_1.png>)
<br><br>
The aim is to find out the number of columns returned by the query. I assume this refers to the query when we see the products on clicking on the category filter.<br>
To do this we use UNION to attach a select NULL statement and keep increasing the number of NULL till we get a postive error response code.<br><br>
In case we can't use UNION we can simply use the order by clause and increment the number till we get our exact number of columns that is returned.<br>
format of 'order by' is 'order by < column > < asc or desc > ' but instead of specifying the column name we can also specify the column number i.e 1,2,3,4. That's how that method works.
<br><br>
We need to use method 1 so on first trying with 1 NULL we get an error code.<br>
![alt text](<images/SQL injection UNION attack, determining the number of columns returned by the query_2.png>)
On trying 2 more times we can see that with three NULL we get a 200 OK code signifying that the number of columns is 3.<br>
![alt text](<images/SQL injection UNION attack, determining the number of columns returned by the query_3.png>)<br><br>
And with that this lab is solved.