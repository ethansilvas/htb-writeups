# Dancing

## Introduction  

there are multiple ways to transfer a file between hosts on the same network   

SMB (server message block) is a communication protocol that provides shared access to files, printers, and serial ports between endpoints on a network   
mostly see on windows machines 

usually see TCP port 445 open on the target for SMB    
SMB runs on application and presentation layers, so it relies on lower-level protocols for transport   
transport layers most often used with is NetBIOS over TCP/IP (NBT), which is why we will typically see both protocols open and running on the target 

using SMB, an app or user of the app can access files at a remote server, and other resources like printers   
client app can read, create, and update files on remote server   
can also communicate with any server program that is set up to receive an SMB client request 

![](../Images/Pasted%20image%2020240206124732.png)

an SMB-enabled storage on the network is called a `share`   
these can be accessed by any client that has the address of the server and the proper credentials   
SMB requires some security layers like authentication because it allows clients to create, edit, retrieve, and remove files on a share   
SMB clients required to provide username/password combo to see or interact with the contents of a share 

still, admins of SMB can always misconfigure or accidentally allow logins without valid creds or using `guest accounts` or `anonymous log-ons` 

## Enumeration 

doing our service scan shows the following open ports: 

![](../Images/Pasted%20image%2020240206125231.png)

we see that port 445 is open which means that we have an active share that we could potentially explore; think of this share as a folder that can be accessed over the internet  

`smbclient` = a script that will allow us to enumerate share content on the remote system   
can install with `sudo apt-get install smbclient`

running `smbclient` will attempt to connect to the remote host and check if there is authentication required   
remember that if we do not specify a username to smbclient then it will just use your local machine's username 

![](../Images/Pasted%20image%2020240206130038.png)

for now though, lets use our local machine's username since we don't know any remote usernames at the moment   
we also need a password which we don't know but for now we will be trying either: 
- guest authentication 
- anonymous authentication 

using `smbclient -L` will list the shares of the specified host: 

![](../Images/Pasted%20image%2020240206130700.png)

from the output we can see 4 separate shares: 
- `ADMIN$` - admin shares are hidden network shares created by the windows NT family of OS that allow sysadmin to have remote access to every disk volume. These may not be permanently deleted but may be disabled 
- `C$` - admin share for the `C:\` disk volume, which is where the OS is hosted 
- `IPC$` - inter-process communication share; used for inter-process communication via named pipes and is not part of the file system 
- `WorkShares` - custom share 

## Foothold 

we can try to connect to each of the shares except for the `IPC$` share because it is not browsable as any regular directory would be, and doesn't contain any files that we could use (in this stage of our learning process)   

to begin trying to connect to the shares we can try the same tactic as before by attempting to login without the proper creds to find improperly configured permissions: 

![](../Images/Pasted%20image%2020240206132955.png)

we can see that the `WorkShares` share is open for us to connect to

we can use the `help` command like in FTP: 

![](../Images/Pasted%20image%2020240206133154.png)

using `ls` we can see two directories for people: 

![](../Images/Pasted%20image%2020240206133322.png)

then going to the `Amy.J` directory we can download the `worknotes.txt` file: 

![](../Images/Pasted%20image%2020240206133423.png)

