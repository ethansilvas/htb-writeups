# Mongod

## Introduction 

in a document-oriented nosql database the data is organized into a hierarchy like: 
- databases
- collections
- documents

databases are organized into collections which contain documents   
documents contain literal data in a JSON-like format

## Enumeration 

we can scan for ports with `nmap -p- --min-rate=1000 -sV {target IP}`

![](../Images/Pasted%20image%2020240526185505.png)

we can see on port 27017 there is a mongodb service running 

## What is MongoDB

each database contains collections which contain documents  
documents are key-value pairs   
a collection can contain multiple documents and they are schema-less, meaning that size and content can all vary 

![](../Images/Pasted%20image%2020240526185548.png)

## Connecting to MongoDB

after installing mongodb we can connect to the target's server: 

![](../Images/Pasted%20image%2020240526190117.png)

using `show dbs` we can see all of the server's databases: 

![](../Images/Pasted%20image%2020240526190146.png)

using `use` and `show` we can see any collections in a specified database, then we can use `db.{colleciton}.find().pretty()` to read the flag file:

![](../Images/Pasted%20image%2020240526190255.png)

