We can use Gobuster to scan for possible vhosts that might exist on the machine.
Let's look for hidden subdomains. To construct our command, we will need to specify:

-u → The target URL to Gobuster.

-w → Wordlist of potential subdomains to test.

```bash
$ sudo gobuster dir -u http://devvortex.htb/ -w /usr/share/wordlists/dirb/common.txt
```

![alt text](Images/Gobuster.png)

We can't obtain any usefull information, so we can enumerate subdomains with wfuzz

```bash
$ wfuzz -c --hc=404,302 -t 200 -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt -H "Host: FUZZ.devvortex.htb" http://devvortex.htb
```

![alt text](Images/Fuzz.png)

We discover the subdomain dev.devvortex.htb , which we also add to our /etc/hosts file.

![alt text](Images/Dom.png)

![alt text](Images/Browser2.png)

Now, we are able to visit http://dev.devvortex.htb .

Looking around the website, we see that all its content is static. We can do a quick directory scan in order to identify any files and directories that are hosted on the server.
```bash
$ sudo gobuster dir -u http://dev.devvortex.htb/ -w /usr/share/wordlists/dirb/common.txt
```
![alt text](Images/Gobuster2.png)

Our scan reveals the /administrator endpoint, which reveals that the site is running on Joomla CMS .

![alt text](Images/Joomla.png)

Now if we visit https://github.com/joomla/joomla-cms, we can see a lot of content management sis.

![alt text](Images/Readme.png)

![alt text](Images/Code.png)

Now We know that We have in front off Joomla 4.2.6 versions. And We can search if exist any vulnerability

![alt text](Images/Joomla2.png)

Knowing the CVE we can use metasploit to search exploits

![alt text](Images/MSF.png)

If We use this exploit...

![alt text](Images/MSF2.png)


We uncover the cleartext credentials lewis:P4ntherg0t1n5r3c0n## .


[Back](README.md)
