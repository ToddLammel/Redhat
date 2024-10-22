查看Redhat发行版本
```shell
[redhat@RedHat ~]$ cat /etc/redhat-release 
Red Hat Enterprise Linux release 8.0 (Ootpa)
```

Redhat中已经自带sshd服务
```shell
[redhat@RedHat ~]$ service sshd status
Redirecting to /bin/systemctl status sshd.service
● sshd.service - OpenSSH server daemon
   Loaded: loaded (/usr/lib/systemd/system/sshd.service; enabled; vendor preset>
   Active: active (running) since Wed 2024-10-23 07:56:53 CST; 25min ago
     Docs: man:sshd(8)
           man:sshd_config(5)
 Main PID: 1105 (sshd)
    Tasks: 1 (limit: 12390)
   Memory: 1.9M
   CGroup: /system.slice/sshd.service
           └─1105 /usr/sbin/sshd -D -oCiphers=aes256-gcm@openssh.com,chacha20-p>
lines 1-10/10 (END)

```

sshd可以使用账号密码 或 密钥登录
为提高安全性，使用密钥登录，且不允许使用账号密码登录
1.在redhat的home目录下新建.ssh目录并创建authorized_keys文件
```shell
[redhat@RedHat ~]$ mkdir -p .ssh
[redhat@RedHat ~]$ cd .ssh
[redhat@RedHat .ssh]$ touch authorized_keys
```

2.在本地生成RSA密钥对，将公钥内容复制到redhat的.ssh目录下authorized_keys文件中
```ssh
[root@host ~]$ ssh-keygen -t RSA
Generating public/private RSA key pair.
Enter file in which to save the key (/root/.ssh/id_rsa): <== 按 Enter
Created directory '/root/.ssh'.
Enter passphrase (empty for no passphrase): <== 输入密钥锁码，或直接按 Enter 留空
Enter same passphrase again: <== 再输入一遍密钥锁码
Your identification has been saved in /root/.ssh/id_rsa. <== 私钥
Your public key has been saved in /root/.ssh/id_rsa.pub. <== 公钥
The key fingerprint is:
0f:d3:e7:1a:1c:bd:5c:03:f1:19:f1:22:df:9b:cc:08 root@host
```

3.修改

