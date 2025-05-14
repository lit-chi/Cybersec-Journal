# It's Oops PM
<hr><br>
In the CTF Try out this is my first attempt at a CTF.<br>
To start off with I chose a very easy difficulty CTF called It's Oops PM.<br>
To begin with I connect to the machine through netcat.<br>
I could also download a couple of .vhdl files and a particular png as well. It seemed to be of some sort of machine that when given the key to, would trigger a backdoor and allow access.<br>
The input was a 16 bit binary and the output was another 16 bit binary so i tested out some binary numbers.<br><br>
I don't know much about this VHDL code but on simple analysis it seemed that the backdoor code needed a particular key which was given in it itself.

![alt text](<images/It's Oops pm_1.png>)
<br><br>
On analyzing the other files given it seemed to perform a few xor and also set some digits as something, but i've really not understood most of it.I am just going to try putting the key value into the terminal.<br><br>
![alt text](<images/It's Oops pm_2.png>)<br>
Oh! I've just got the key!!<br><br>
And with that, this challenge was solved. It was much much more straightforward than I thought.