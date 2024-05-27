# Sequel

## Enumeration 

do another nmap scan to see that a mariaDB sql server is being used on port 3306: 

![](../Images/Pasted%20image%2020240527132230.png)

connecting to the database with the username `root` we can see the open `htb` table: 

![](../Images/Pasted%20image%2020240527132425.png)

using `SELECT * FROM config;` we can see the flag