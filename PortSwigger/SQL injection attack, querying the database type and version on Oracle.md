This is the third lab under SQL injection and this is Practitioner difficulty.

Here, on starting the lab we are led to a page kind off similar to the previous labs but the difference is that the products are now displayed by text only and not images too.
![alt text](<images/SQL injection attack, querying the database type and version on Oracle_1.png>)

We can try to inject some query along with the URL when we are browsing through category.
The data that is returned is known to be in string, so we need to find the number of columns that are returned so we can use UNION operator to return the version of sql.
to do that we initially test for one column by doing adding -> ' union select 'abcd' from dual--<br>
![alt text](<images/SQL injection attack, querying the database type and version on Oracle_2.png>)
It returns an error, so we try with two strings now.
![alt text](<images/SQL injection attack, querying the database type and version on Oracle_3.png>)
The two strings are also displayed along with the product descriptions. So now instead of the strings, we can put select statements for the version.
we add the to the statment-> ' union select a.*,b.* from v$version a, v$version b-- <br>
![alt text](<images/SQL injection attack, querying the database type and version on Oracle_4.png>)
And with that we get the version and the lab is solved.