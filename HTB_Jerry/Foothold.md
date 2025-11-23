![alt text](Images/MSF.png)

This exploit use force brute to find the credentials

![alt text](Images/MSF2.png)

Now we got the credentials --> tomcat:s3cret

![alt text](Images/Browser4.png)

Using this knowledge, we can exploit Tomcat with Metasploit by creating a custom malicious WAR file and deploying a new application.

![alt text](Images/MSF3.png)

After running exploit we successfully obtain a meterpreter shell on the target. Now that we have successfully compromised the target, we can spawn an interactive shell and read the flags in C:\Users\Administrator\Desktop\flags\2 for the price of 1.txt .

![alt text](Images/Flags.png)

[Back](README.md)