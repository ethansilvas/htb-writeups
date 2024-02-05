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

