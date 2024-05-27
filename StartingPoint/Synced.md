# Synced

FTP is very slow and old  
`rsync` can be used instead, especially for cases for when you don't need to transfer every line of a file   

the changes in a file that need to be transferred are called `deltas`   

main stages of an rsync transfer are: 
- rsync creates connection to remote host and spawns another rsync receiver process
- sender and receiver processes compare what files have changed 
- what has changed gets updated to the remote host 

## Enumeration

doing a port scan we can see that port 873 is open: 

![](../Images/Pasted%20image%2020240526192825.png)

## Connecting to Rsync 

src = file or directory to copy from   
dest = directory to copy to  

we can try to see all the available directories to an anonymous user with `--list-only`: 

![](../Images/Pasted%20image%2020240526193053.png)

then we can select the public share and list its files: 

![](../Images/Pasted%20image%2020240526193136.png)

now we can copy the flag file to our host machine with `public/flag.txt flag.txt`: 

![](../Images/Pasted%20image%2020240526193228.png)

