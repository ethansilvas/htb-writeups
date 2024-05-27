# Explosion

## Introduction 

some services allow users to remotely connect to other hosts  
interactions with these services can either be CLI or GUI   
these services use RDP on port 3389 TCP/UDP   

## CLI - Remote Access Tools 

SSH uses public-key cryptography to verify the remote host's identity   
communication model based on client-server model   
local host uses servers public key to verify its identity before establishing the encrypted tunnel 

however, SSH only offer the user access to the remote terminal part of the host   
we can use cli tools like `xfreerdp` to view the full display projection   

## GUI - Remote Access Tools 

teamviewer is one of the most used GUI remote desktop applications   

## Enumeration 

remember `speedguide` for looking up ports: 

`https://www.speedguide.net/port.php?port=135`

using `nmap -sV` we can see port 3389 open 

connect with xfreerdp using `xfreerdp /v:{IP} /u:Administrator` and leave the password empty  
on the desktop there is a flag file with the flag contained in it 