First of all we check that we have connection with IP target.
```bash
$ ping -c 1 10.10.11.41
```
![alt text](Images/ping.png)

This TTL value on HTB indicates that is a Windows machine.

We observe that SMB (port 445), LDAP (port 389), and Kerberos (port 88) are running. Therefore, this system can be identified as a Domain Controller.
```bash
$ sudo nmap -p- --open -sS -sC -sV --min-rate 5000 -n -Pn -A 10.10.11.11  -oX nmap.xml
$ xsltproc nmap.xml -o nmap.html
```
-p- → Scans all 65,535 TCP ports, not just the most common ones. All 65,535 TCP ports, not just the most common ones, not just the most common ones. 

--open → Shows only ports that are open, filtering out closed or filtered ones.

-sS → Performs a TCP SYN scan (half-open scan), which is fast and stealthy and requires root privileges.

-sC → Runs default NSE (Nmap Scripting Engine) scripts to gather additional information such as common vulnerabilities and service details.

-sV → Attempts to detect service versions running on open ports.

--min-rate 5000 → Forces Nmap to send at least 5000 packets per second, speeding up the scan but increasing the chance of detection or packet loss. 

-n →  Disables DNS resolution to make the scan faster.

-Pn → Skips host discovery and assumes the target is alive, useful when ICMP is blocked.

-A → Enables aggressive scan options, including OS detection, version detection, script scanning, and traceroute.

-oX → Output option: write results in XML format to file nmap.xml.  Other formats: -oN (normal), -oG (grepable), -oA (all formats).

![alt text](Images/Nmap.png)
![alt text](Images/Nmap2.png)

Consequently, we add both the domain name and the DNS name to the /etc/hosts file.

![alt text](Images/Browser.png)

Using **rpcclient** and the obtained credentials, we attempt to connect to the machine and we will enumerate users inside the machine that we have access;
```bash
$ rpcclient -U  "judith.mader%judith09" 10.10.11.41 -c 'enumdomusers'
```
![alt text](Images/RCPclient.png)

We will use **netexec** to attempt to enumerate the SMB service on the provided IP address. We will check the **shares** directory to see what we can do, what we have access to, and which permissions are assigned.
```bash
$ netexec smb 10.10.11.41 -u 'judith.mader' -p 'judith09' --shares
```
![alt text](Images/Netexec.png)

Using the provided credentials judith.mader:judith09 , we enumerate the Domain Controller using bloodhound .
```bash
$ bloodhound-python -d certified.htb -u 'judith.mader' -p 'judith09' -dc 'dc01.certified.htb' -c all -ns 10.10.11.41
```
 bloodhound-python →  Launches the Python-based BloodHound ingestor.

 -d certified.htb →  Specifies the Active Directory domain to target.

 -u 'judith.mader' →  The username used to authenticate to the domain.

 -p 'judith09' →  The password for the specified user account.

 -dc 'dc01.certified.htb' →  The domain controller to query for information.

 -c all →  Enables all collection methods, including users, groups, computers, sessions, ACLs, trusts, etc.

 -ns 10.10.11.41 → Specifies the DNS server IP address for resolving domain names.
 
 Running this command generates one or more .json / .zip output files containing AD relationship data. These files can be uploaded to the Bloodhound GUI connected to a Neo4j database for anaysis.


![alt text](Images/Bloodhound.png)

To install Bloodhound we need follow the following → https://bloodhound.specterops.io/get-started/quickstart/community-edition-quickstart.

Once you have all like the guide, then:
```bash
$ docker-compose pull && docker-compose up
```
And wait

![alt text](Images/Bloodhound2.png)

You need to save your password to later authenticate yourself on Bloodhound.

![alt text](Images/Bloodhound3.png)

Initial Password Set To:    nlLEdLMGP3mnfU6NEA0xypdT6wOz7ug_

When the proccess ended, you will see in your terminal

![alt text](Images/Bloodhound4.png)

Then you can go to your browser → http://localhost:8080/

![alt text](Images/Bloodhound5.png)
```bash
The user is: admin
Password : nlLEdLMGP3mnfU6NEA0xypdT6wOz7ug_ (provided in previous step)
```
And then you need to change your password

![alt text](Images/Bloodhound6.png)

After change the password, you need to upload the data

![alt text](Images/Data.png)

And we wait until the file status will be “Complete”

![alt text](Images/Data2.png)

Then we will go to Explore, and there we will go to the section that shows the image.

![alt text](Images/Data3.png)

Now we look for the user Judith, who is the user that was provided to us.

![alt text](Images/Data4.png)

We right-click and select 'Owned' to add the user and in the right menu choose “Outbound Object Control”  to see what can do. In the Pathfinding section once you know all the line , this options show you the way to follow.

![alt text](Images/Path.png)

Here we see 3 things:
1. The judith.mader user has WriteOwner ACL over the management group.

2. The management group has GenericWrite ACL over the management_svc user.

3. The management_svc has CanPSRenote attribute set, which means that the user can log in to the target (via WinRM )


[Back](README.md)