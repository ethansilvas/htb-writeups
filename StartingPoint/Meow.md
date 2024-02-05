# Meow 

## Introduction 

when first starting a pen test or any security evaluation, a primary step is enumeration   
enumeration consists of documenting the current state of a target to learn as much as possible about it 

every server uses ports to serve data to other clients   
the first step of enumeration is to scan these ports to see the purpose of the target and what potential vulnerabilities might appear from the services running on it 

`nmap` is a tool that lets us quickly scan for ports 

after finding all the open ports on a target we can manually access each of them using different tools   
90% of pen testing consists of research done about the product you are testing   

key objective is not speed but meticulousness  
if a resource is missed during enumeration then you might lose a vital attack vector 

## Enumeration 

with the `ping` command we can test our connection to the target server: 

![](../Images/Pasted%20image%2020240205120238.png)

now we can scan for open ports with `nmap`, which sends requests to the target's ports to see if they reply   
some ports are used by default by certain services, others might be non-standard which is shy we can use `sV` to use service detection: 

![](../Images/Pasted%20image%2020240205120603.png)

from the service scan we can see that port 23, or telnet, is open   
since the target is running this service, it can receive telnet connections from other hosts in the network 

when using the `telnet` command we can see that we are greeted with a login prompt: 

![](../Images/Pasted%20image%2020240205120851.png)

## Foothold 

many services like the one we have found are often configured improperly and are open to authentication brute-force attacks  

trying some basic usernames we can eventually login with `root`: 

![](../Images/Pasted%20image%2020240205121234.png)

using `ls` to look around the directory we can see the flag file: 

![](../Images/Pasted%20image%2020240205121355.png)

most boxes will either have a `flag.txt`, `user.txt`, or `root.txt`   
other challenges will not contain a file but offer snippets of the flag as you solve it 
