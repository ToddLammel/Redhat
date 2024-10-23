### 1.RWX权限对文件和目录的作用
|R|W|X|
|---|---|---|
|对目录：读取目录结构列表，查看目录下的文件名字和子目录名字|对目录：具有更改该目录结构列表的权限（新建/删除/重命名/移动文件或子目录）|对目录：具有进入该目录的权限，查询该目录下的文件的内容|
|对文件：读取文件的内容|对文件：编辑、追加或替换文件内容（如果上级目录没有w权限，则无法修改目录结构列表，即无法删除文件） |对文件：具有可以被系统执行的权限|


### 2.文件和目录的默认权限：
Umask（User File Creation Mode Mask）是一个在类Unix系统中用于设置新创建文件和目录默认权限的命令。


Umask 的值通常以八进制数表示，它的作用是从默认的文件权限中去除相应的权限。默认情况下，新建文件的权限是0666（即所有用户都有读和写权限），新建目录的权限是0777（即所有用户都有读、写和执行权限）。Umask 的值从这些默认权限中减去，以确定最终的文件和目录权限。

查看umask
```shell
[redhat@RedHat ~]$ umask
0002
```


新建文件
```shell
[redhat@RedHat ~]$ touch test
[redhat@RedHat ~]$ ls -l test
-rw-rw-r--. 1 redhat redhat 0 Oct 24 04:46 test
```
0666 - 002 = 0664 即 RW-RW-R--


新建目录
```shell
[redhat@RedHat ~]$ mkdir dirs
drwxrwxr-x.  2 redhat redhat     6 Oct 24 04:47 dirs
```
0777 - 002 = 0775 即 RWXRWXR-X
