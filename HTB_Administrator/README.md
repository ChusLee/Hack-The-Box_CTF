![alt text](Images/Administrator.png)


# Scope

**Administrator** is a Windows machine of intermediate difficulty that focuses on a full Active Directory domain compromise scenario. Initial access is achieved using credentials from a low-privileged user. To escalate privileges and access the **michael** account, Access Control Lists (ACLs) on high-privilege objects are enumerated, revealing that the user **olivia** possesses **GenericAll** permissions over **michael**, which enables resetting his password.

Once logged in as **michael**, it is discovered that he has the ability to enforce a password change on the user **benjamin**, allowing his credentials to be reset. This access provides entry to an FTP service where a **backup.psafe3** file is found. After cracking this file, credentials for multiple users are obtained.

These credentials are then sprayed across the domain, resulting in valid access as the user **emily**. Further analysis shows that **emily** has **GenericWrite** permissions over the user **ethan**, making it possible to carry out a targeted Kerberoasting attack. The extracted hash is cracked, revealing valid credentials for **ethan**.

Finally, **ethan** is identified as having **DCSync** privileges, which allows the extraction of the **Administrator** account hash, leading to complete domain compromise.

# Index
- [Enumeration](Enumeration.md)
- [Foothold](Foothold.md)
- [Lateral movement](Lateral_movement.md)
- [Priv Escalation](Priv_Escalation.md)


Go back to [Hack-The-Box_CTF](https://github.com/jesuscuenca-cyber/Hack-The-Box_CTF)

