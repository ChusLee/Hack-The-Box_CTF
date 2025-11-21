Now we can move on to final privilege escalation. To start our enumeration, we will check all active listening ports on the machine with netstat . More specifically, we will use the following parameters to show:

-t → TCP connections.

-u → UDP connections.

-l  → Only listening sockets (ports that are waiting for connections).

-n → Numeric addresses/ports (instead of resolving hostnames or service names).

-p → PID and process name of the program bound to each socket.

![alt text](Images/Netstat.png)

Let's find the service running on port 8000 by port forwarding it to our machine.

![alt text](Images/Server.png)

We can try to access it locally from our browser.

![alt text](Images/Browser4.png)

We are required to sign in, but none of the credentials we have thus far have been successful. So we will have to keep enumerating.
In the /opt directory we find an interesting folder crontabs that we can read.
Inside it we find crontab.db which we can read as well.

![alt text](Images/image3.png)

We found another plaintext password.

Password: P4ssw0rdS0pRi0T3c

User: we supose that is “root”

We can log in and see the custom interface. We can view the current .db file and also create a new one.

![alt text](Images/image4.png)

Knowing that these tasks run as root, we can create a new cron job to execute any command with elevated privileges.

To take advantage of this, we’ll modify the permissions of the /bin/bash binary and set the SUID bit, allowing us to run commands with root privileges directly from our SSH session as the enzo user.
```bash
$ cp /bin/bash /tmp/bash & chmod u+s /tmp/bash

$ cp /bin/bash /tmp/bash: Copies the system’s Bash binary into /tmp.
$ chmod u+s /tmp/bash: Applies the SetUID bit, ensuring that anyone who runs /tmp/bash executes it with root privileges.
```
![alt text](Images/image5.png)

Then press “Save” and after that, press “Run now” button.

![alt text](Images/image6.png)

Then, check the /tmp directory

![alt text](Images/image7.png)

We can see that permissions corfirmed that the SetUID bit wass successfully applied.

Finally, we executed  /tmp/bash -p to gain root shell. (The -p flag ensure that the privileged UIS is preserved)

![alt text](Images/image8.png)

With this, we obtain the second flag and fully compromise the machine.

[Back](README.md)