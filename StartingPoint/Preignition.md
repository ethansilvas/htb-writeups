# Preignition

web servers play a big part in the infrastructure of many orgs  
for the most part, web servers are managed by admin panels locked behind a log-in page   

## Enumeration 

using nmap we can see port 80 has an open nginx service: 

![](../Images/Pasted%20image%2020240526182035.png)

visiting the port in our browser we can see it is set to the default nginx page: 

![](../Images/Pasted%20image%2020240526182145.png)

we can use gobuster to see that there is an open `/admin.php` page: 

![](../Images/Pasted%20image%2020240526184042.png)

visiting the page we are greeted to a login form:

![](../Images/Pasted%20image%2020240526184018.png)

using the credentials admin:admin we can get the flag

