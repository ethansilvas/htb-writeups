# Fawn

## Introduction 

sometimes when we enumerate services of hosts we can find file transfer services that are poorly configured   

FTP is a native protocol to all host OS and has been used for a long time for simple file transfer tasks   
FTP can easily be misconfigured if not fully understood   
can also be used to transfer log files from one network device to another or a log collection server, attacker could gain leverage of the logs and extract all info from them to later use to map out network, enumerate usernames, detect active services, etc. 

FTP is part of the client-server model   
sends authentication credentials in cleartext but if encryption is then FTPS (SSL/TLS) or SFTP (SSH) can be used   

clients can browse the available files on the server when using FTP 

a port running an active service is a reserved space for the IP address of the target to receive requests and send results from   
if we only had IP addresses and hostnames then we would only be able to do 1 task at a time on our computer 

![](../Images/Pasted%20image%2020240205123031.png)

since it is considered non-standard to use FTP without encryption due to MitM attacks, FTP is often moved to other ports for SFTP or FTPS: 

![](../Images/Pasted%20image%2020240205123302.png)

## Enumeration 

performing a service scan with `nmap` we can see that the target is running telnet on an open port 21: 

![](../Images/Pasted%20image%2020240205123828.png)

## Foothold 

first lets make sure that our FTP version is up to date and installed properly: 

![](../Images/Pasted%20image%2020240205124212.png)

now we can connect to the target using FTP and it prompts us to login: 

![](../Images/Pasted%20image%2020240205124559.png)

a typical misconfigured FTP server allows an `anonymous` account to access the service like any other authenticated user  

logging in with the username `anonymous` and no password lets us access the service with a 230 successful response code: 

![](../Images/Pasted%20image%2020240205124819.png)

we can use `help` to see what commands are available to us: 

![](../Images/Pasted%20image%2020240205125045.png)

additionally we can use `man <command>` to learn about how to use each of these 

using `ls` we can see the flag file: 

![](../Images/Pasted%20image%2020240205125156.png)

to download the flag file to our host machine we can use the `get` command: 

![](../Images/Pasted%20image%2020240205125327.png)

now the file will be downloaded to the directory we were in before we connected to the FTP server: 

![](../Images/Pasted%20image%2020240205125419.png)



