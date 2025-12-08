The webapage states that the MFP Firmware Update Center conducts various tests on printer firmwares and drivers. Let's navigate to Firmware Updates and check what options we have.

![alt text](Images/Browser4.png)

Since each file is reviewed manually and it is uploaded to an SMB share we could potentially upload a file that, when executed, makes a connection back to our local machine using SMB, thus allowing us to grab an NTLM hash. Since every file is opened for review purposes we can upload a Shell Command File (.scf) with a simple command to grab a single file from our local machine.
To this we can do a search in google to fing a malicious SCF file.

https://pentestlab.blog/2017/12/13/smb-share-scf-file-attacks/

![alt text](Images/SCF_File.png)

In this webpage tell us how to do a SCF file attack throw SMB Share. So let's follow the steps.

SCF file creation. We oppen nanto to create the file and save this file as SCF.

![alt text](Images/SCF_File2.png)

![alt text](Images/SCF_File3.png)

Saving the pentestlab.txt file as SCF file will make the file to be executed when the user will browse the file.

Responder needs to be executed with the following parameters to capture the hashes of the users that will browse the share.
```bash
$ sudo responder -w -I tun0
```
![alt text](Images/Responder.png)

![alt text](Images/Responder2.png)

Then we upload a .scf file

![alt text](Images/SCF_File4.png)

And then in our responder we received a hash for the “tony” user

![alt text](Images/Responder3.png)

Then, we save the hash and use John to crack it and retrieve the plaintext password.

![alt text](Images/Hash.png)

```bash
$ john TonyHash --wordlist=/usr/share/wordlists/rockyou.txt
```
![alt text](Images/John.png)

The has is successfully cracked and we get the credentials tony / liltony . Using these credentials we can attempt to login to the remote machine using WinRM.
```bash
$ evil-winrm -i 10.10.11.106 -u tony -p liltony
```
![alt text](Images/Shell.png)

![alt text](Images/Shell2.png)

![alt text](Images/Shell3.png)

Searching trhow the directories we can find the user flag

![alt text](Images/UserFlag.png)
```bash
User flag → a427e7b097781c3d150bfc231c8164a5
```

[Back](README.md)