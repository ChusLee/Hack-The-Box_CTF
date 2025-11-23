With nmap we will try to find a vulneravility.
```bash
$ nmap --script vuln 10.10.10.95 -p8080
```

![alt text](Images/Vuln.png)

We found that our Tomcat versions is vulnerable to CVE-2007-6750 (Slowloris DOS attack)

![alt text](Images/CVE.png)

Navigate throw the web page, in the “Manager App” options, returns a login.

![alt text](Images/Browser3.png)

We don't find to do this attack, so we will know the credentials, so we use Metasploit tool to find some exploit to login.

[Back](README.md)