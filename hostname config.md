### 1.修改主机名
```shell
[redhat@RedHat ~]$ ls -l /etc/hostname 
-rw-r--r--. 1 root root 7 Oct 23 07:52 /etc/hostname
[redhat@RedHat ~]$ vim /etc/hostname
RedHat
```

### 2.本地映射主机名和IP
修改hosts文件，其位置：C:\Windows\System32\drivers\etc
增加IP和域名：
```shell
192.168.137.10 RedHat
```

直接通过主机名访问：
```shell
C:\Users\mi>ping RedHat

正在 Ping RedHat [192.168.137.10] 具有 32 字节的数据:
来自 192.168.137.10 的回复: 字节=32 时间<1ms TTL=64
来自 192.168.137.10 的回复: 字节=32 时间=1ms TTL=64
来自 192.168.137.10 的回复: 字节=32 时间=1ms TTL=64
```
