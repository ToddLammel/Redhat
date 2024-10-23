### 1."permissions are too open"
我在windows下生成的RSA密钥对，使用公钥ssh到远程主机时，提示“permissions are too open”。


原因：
公钥文件的安全属性权限有多个用户控制。


解决：
删除其它用户的控制权限，仅保留当前用户的控制权限。


### 2."Load key "XXX.pub": invalid format"
我在windows下生成的RSA密钥对，使用公钥ssh到远程主机时，提示“Load key "XXX.pub": invalid format”。


原因：
Windows换行符 CR LF；Linux换行符 LF；MAC OS换行符 CR；
我在Windows下生成的RSA密钥对，复制黏贴公钥到.ssh/authorized_keys时，格式发生了变化

未解决：
无语，看不出格式有啥差别，直接从linux下把文件拷贝过来了。
