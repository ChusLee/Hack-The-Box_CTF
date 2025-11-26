we don't have permissions to see the flag

![alt text](Images/Perm2.png)

so we try to login as logan with our previous password

![alt text](Images/Login2.png)

But this doesn't work

If we remember, this passord is for a mysql so we try to login with user logan but in mysql

![alt text](Images/MySQL.png)

Now we navigate throw the tables

![alt text](Images/Tables.png)

![alt text](Images/Tables2.png)

![alt text](Images/Tables3.png)

To identify the password format we can do
```bash
$  hashid '$2y$10$IT4k5kmSGvHSO9d6M/1w0eYiB5Ne9XzArQRFJTGThNiy/yBtkIj12'
```
![alt text](Images/PSWD.png)

Now we can use hashcat
```bash
$ hashcat --example-hashes | grep -i “blowfish”

$ hashcat --example-hashes | grep -i “blowfish” -B 5
```
![alt text](Images/HashCat.png)

We can create a file hash
```bash
$ emacs hash
```
And paste de password in blowfish

![alt text](Images/HashCat2.png)


Now we use anothertime haschat (0 indicate brute force)
```bash
$ hashcat -m 3200 -a 0 -w 3 hash /usr/share/wordlists/rockyou.txt
```
![alt text](Images/HashCat3.png)

![alt text](Images/HashCat4.png)

And got a password for user lewis. We turn to our reverse shell connection

![alt text](Images/Login3.png)

And we logged 

![alt text](Images/Login4.png)



[Back](README.md)
