# Redeemer

## Introduction 

databases are very important because they communicate information related to business operations  

many types of databases, one of them is `Redis` which is an in-memory database   
in-memory databases rely on the primary memory for data storage; database is managed in the RAM of the system, rather than store data on the disk or SSDs  
primary memory is much faster than secondary so data retrieval time is very small 

in-memory databases like redis are typically used to cache data that is frequently used   
for example, a site might check for frequently used data in the redis database first, then if it isn't there look in the traditional database like MySQL or MongoDB   
when values are loaded from traditional databases it is then held in redis for a certain amount of time 

## Enumeration 

first we `ping` the target: 

![](../Images/Pasted%20image%2020240207113247.png)

the redis port is on TCP 6379 so we need to increase our range of IPs: 

![](../Images/Pasted%20image%2020240207114028.png)

could also use `-p- --min-rate 5000` or use `-T5` to quickly look for all ports 

## What is redis? 

redis = remote dictionary server   
NoSQL key-value store used as database, cache, and message broker   
data stored in dictionary format having key-value pairs 

runs on server-side software so its core functionality is in its server component    
server listens for connections from clients, programmatically or through the cli 

cli gives access to redis' data and its functionalities 

database is stored in server's RAM   
redis will also write contents of database to disk at varying intervals to persist it as a backup 

to interact remotely with redis we will need to install `redis-cli`: 

`sudo apt install redis-tools`

could also connect to redis server with netcat 

## Enumerating Redis Server

we can use `-h` to specify the host we want to connect to: 

`redis-cli -h <target>`

![](../Images/Pasted%20image%2020240207114818.png)

`-info` will show is useful information and stats about the server: 

![](../Images/Pasted%20image%2020240207114933.png)

an important piece of info from this output is the keyspace: 

![](../Images/Pasted%20image%2020240207115016.png)

this provides stats on the main dictionary of each database  
stats include the number of keys and the number of keys with an expiration 

from the output we can see that only one database exists with an index of `0` 

we can select the database with `select 0`: 

![](../Images/Pasted%20image%2020240207115312.png)

we can then list all the keys in the database with `keys *`: 

![](../Images/Pasted%20image%2020240207115350.png)

then we can view all the values stored for each key using `get <key>`: 
