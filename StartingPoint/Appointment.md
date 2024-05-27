# Appointment

## Introduction 

sql injections will ignore any separation between the tables of a backend system   

a good example of how a sql service typically operates is a login system   
usernames and password are matched to an entry in database   
on successful login the user is given an auth token   

## Enumeration 

run a service and script scan to see that there is an apache server on port 80: 

![](../Images/Pasted%20image%2020240527113819.png)

usually a good idea is to lookup the version number for any known vulnerabilities but this version does not have any  

we are greeted with a login page: 

![](../Images/Pasted%20image%2020240527114027.png)

use dirbuster to look for any hidden directories: 

```
gobuster dir --url http://{ip} --wordlist {wordlist}
```

![](../Images/Pasted%20image%2020240527120516.png)

we could then try various default login credentials but this wont seem to work either

however, using a sql injection payload like `admin'# ` will allow you to successfully login because the backend code will be terminated after looking for an account named admin   