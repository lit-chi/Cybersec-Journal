This is the first portswigger lab i'm doing. It's apprentice level.

On starting the lab we are directed to a website.
![alt text](<images/SQL injection vulenrability in WHERE clause allowing retrieval of hidden data_1.png>)

The question for the lab defines the query used in the backend. 
![alt text](<images/SQL injection vulenrability in WHERE clause allowing retrieval of hidden data_3.png>)

Therefore the 2 parameters to display the products on the site are the tag which can be all, accesories, gift etc. and value for released. I assume released implies a certain set of products which can be shown. Therefore we need to also see the product for released=0.

So we just need to modify from the category parameter and comment out the released so that it isn't checked.

we can update the category as ?category=Corporate+gifts' or 1=1--
so using this we complete the quere to check for category = corporate gifts or if it is 1=1 which is always true so this select query is true for all products. The '--' will comment the rest of the query out.

![alt text](<images/SQL injection vulenrability in WHERE clause allowing retrieval of hidden data_4.png>)

And on pressing enter we are able to see more products and the lab is solved.

![alt text](<images/SQL injection vulenrability in WHERE clause allowing retrieval of hidden data_5.png>)

