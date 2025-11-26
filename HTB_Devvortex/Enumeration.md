First of all we check that we have connection with IP target.

![alt text](Images/Ping.png)

This TTL value on HTB indicates that is a Linux machine.


We will start with our usual Nmap scan and find two ports open. We find OpenSSH on port 22 and port 80 http.

sudo nmap -F -sC -sV -A -oX nmap.xml 10.10.11.242
xsltproc nmap.xml -o nmap.html

-F → Scans fewer ports than the default: it scans the set of "top" ports from nmap-services (roughly the top 100 most common ports).

-sC → Run the default NSE (Nmap Scripting Engine) scripts against the target(s).

-sV → Service/version detection.

-A → Performs OS Detection Scan to determinate the OS of the target.

-oX → Output option: write results in XML format to file nmap.xml.  Other formats: -oN (normal), -oG (grepable), -oA (all formats).

![alt text](Images/NMap.png)

![alt text](Images/NMap2.png)

In this scan, we can see that the port 80 redirect us to http://devvortex.htb so to access the website, we must add the domain name to our /etc/hosts file to resolve the connection with the IP address.

![alt text](Images/Devvortex2.png)

Now we can navigate to the website in our browser

![alt text](Images/Browser.png)



[Back](README.md)
