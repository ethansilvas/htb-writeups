# Crocodile

## Enumeration 

nmap results show FTP and http ports open: 

![](../Images/Pasted%20image%2020240527134704.png)

logging in as `anonymous` in the ftp server we can see a couple files: 

![](../Images/Pasted%20image%2020240527134812.png)

we can download both of these files using `get`: 

![](../Images/Pasted%20image%2020240527134926.png)

then we can view them on our local machine: 

![](../Images/Pasted%20image%2020240527134956.png)

trying to login to the ftp server with these usernames and passwords will not work, however we can now also try them on the found HTTP port: 

![](../Images/Pasted%20image%2020240527135109.png)

lets use gobuster to enumerate any directories: 

```
gobuster dir --url http://10.129.57.72:80/ --wordlist /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt -x php,html
```

![](../Images/Pasted%20image%2020240527135253.png)

we can see a login page which we can visit: 

![](../Images/Pasted%20image%2020240527135317.png)

using `admin` and `rKXM59ESxesUFHAd` we can successfully login and view the flag