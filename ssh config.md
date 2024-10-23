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

sshd可以使用账号密码 或 密钥登录。
为提高安全性，使用密钥登录，且不允许使用账号密码登录。


密钥形式登录的原理是：利用密钥生成器制作一对密钥——一只公钥和一只私钥。将公钥添加到服务器的某个账户上，然后在客户端利用私钥即可完成认证并登录。这样一来，没有私钥，任何人都无法通过 SSH 暴力破解你的密码来远程登录到系统。此外，如果将公钥复制到其他账户甚至主机，利用私钥也可以登录。


1.在redhat的home目录下新建.ssh目录并创建authorized_keys文件
```shell
[redhat@RedHat ~]$ mkdir -p .ssh
[redhat@RedHat ~]$ cd .ssh
[redhat@RedHat .ssh]$ touch authorized_keys
```

2.在本地生成RSA密钥对，将公钥内容复制到redhat的.ssh目录下authorized_keys文件中
```shell
[root@host ~]$ ssh-keygen -t RSA -b 4096
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

3.修改文件权限, 只要当前用户可以读取/修改其中内容
```shell
chmod 600 authorized_keys
chmod 700 ~/.ssh
```

4.修改/etc/ssh/sshd_config
```shell
RSAAuthentication yes
PubkeyAuthentication yes

# 禁止root用户登录
PermitRootLogin no

# 禁用密码登录
PasswordAuthentication no
```

5.重启sshd服务
```shell
[root@RedHat .ssh]# systemctl restart sshd
```

6.使用公钥进行ssh连接而无需输入密码


其它配置说明：
配置项	| 描述 | 示例值
-----|-------|--------
Port	| SSH服务监听的端口，默认是22	| Port 22
Protocol	| SSH协议版本，推荐使用2	| Protocol 2
ListenAddress | SSH服务监听的IP地址，默认是0.0.0.0（所有接口）	| ListenAddress 0.0.0.0
UserDNS	| 是否允许DNS反向解析用户名，默认是yes	| UserDNS no
PermitRootLogin	| 是否允许root用户登录，默认是yes |	PermitRootLogin no
PermitEmptyPasswords	 | 是否允许空密码登录，默认是yes |	PermitEmptyPasswords no
LoginGraceTime |	用户登录验证的超时时间，默认是2分钟	 | LoginGraceTime 2m
MaxAuthTries	| 用户认证尝试的最大次数，默认是6次	| MaxAuthTries 6
AllowUsers |	允许登录的用户列表，使用空格分隔 |	AllowUsers steven
DenyUsers	| 不允许登录的用户列表，使用空格分隔 |	DenyUsers steven
PasswordAuthentication |	是否启用密码认证，默认是yes	| PasswordAuthentication yes
PubkeyAuthentication	| 是否启用公钥认证，默认是yes	| PubkeyAuthentication yes
AuthorizedKeysFile	| 用户的公钥存储文件路径，默认是.ssh/authorized_keys	| AuthorizedKeysFile .ssh/authorized_keys
ClientAliveCountMax	| SSH服务器在未收到客户端响应前发送的"alive"消息的最大次数，默认是3 |	ClientAliveCountMax 3
ClientAliveInterval | 	SSH服务器等待客户端响应的时间间隔（秒），默认是0（不发送"alive"消息）|	ClientAliveInterval 0
X11Forwarding	| 是否允许X11转发，默认是yes | X11Forwarding yes
GSSAPIAuthentication |	是否启用GSSAPI认证，默认是yes |	GSSAPIAuthentication yes
