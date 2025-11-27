First of all we check that we have connection with IP target.

![alt text](Images/Ping.png)

This TTL value on HTB indicates that is a Linux machine.

We will start with our usual Nmap scan and find two ports open. We find OpenSSH on port 22 and http on port 80 .
```bash
$ sudo nmap -F -sC -sV -A -oX nmap.xml 10.10.11.143
$ xsltproc nmap.xml -o nmap.html
```
-F → Scans fewer ports than the default: it scans the set of "top" ports from nmap-services (roughly the top 100 most common ports).

-sC → Run the default NSE (Nmap Scripting Engine) scripts against the target(s).

-sV → Service/version detection.

-A → Performs OS Detection Scan to determinate the OS of the target.

-oX → Output option: write results in XML format to file nmap.xml.  Other formats: -oN (normal), -oG (grepable), -oA (all formats).

![alt text](Images/NMap.png)

![alt text](Images/NMap2.png)

To access the website, we must add the domain name paper to our /etc/hosts file to resolve the connection with the IP address.

![alt text](Images/Browser.png)

And now we can access to the webpage throw our browser.

![alt text](Images/Browser2.png)


[Back](README.md)