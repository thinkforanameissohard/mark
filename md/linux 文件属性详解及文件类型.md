> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [www.cnblogs.com](https://www.cnblogs.com/654321cc/p/9102035.html)

**一** 

 **drwxr-xr-x 的意思解释：**

[![](http://common.cnblogs.com/images/copycode.gif)](javascript:void(0); "复制代码")

```
ls -al

得到如下列表：
drwxr-xr-x   4 oracle dba       4096 May 20 11:47 oralog1
drwxr-x---  18 root   root      4096 May 20 13:51 root

解释：
d ：第一位表示文件类型，d是目录文件、l是链接文件、-是普通文件、p是管道

rwx ：第2-4位表示这个文件的属主拥有的权限。r是读、w是写、x是执行

r-x ：第5-7位表示和这个文件属主所在同一个组的用户所具有的权限

r-x ：第8-10位表示其他用户所具有的权限

比如：
drwxr-xr-x   4 oracle dba       4096 May 20 11:47 oralog1

表示oralog1是个目录，oracle拥有读写执行的权限，和oracle所在同一个dba组里的用户拥有只读和执行权限，剩下其他用户拥有只读和执行权限！
```

[![](http://common.cnblogs.com/images/copycode.gif)](javascript:void(0); "复制代码")

**ls -al 的各段含义：**

[![](http://common.cnblogs.com/images/copycode.gif)](javascript:void(0); "复制代码")

```
第1字段:  文件属性字段
文件属性字段总共有10个字母组成，第一个字母表示文件类型，如果这个字母是一个减号”-”，则说明该文件是一个普通文件。字母”d”表示该文件是一个目录，字母”d”，是dirtectory(目录)的缩写。
请注意，一个目录或者说一个文件夹是一个特殊文件，这个特殊文件存放的是其他文件和文件夹的相关信息。

第2字段
文件硬链接数或目录子目录数

第3字段:
文件拥有者

第4字段:
文件拥有者所在的组

第5字段:
文件文件大小（以字节为单位）

第6字段:
文件创建月份

第7字段:
文件创建日期

第8字段:
文件创建时间

第9字段:
文件名 （如果是一个符号链接，那么会有一个 “->”箭头符号，后面根一个它指向的文件）
```

[![](http://common.cnblogs.com/images/copycode.gif)](javascript:void(0); "复制代码")

**rwxrwxrwx=777 的解释：**

**针对字母的操作比较臃肿，可以简化为数字的写法，如超级权限 777。其实就是数字相加得出的结果。**

[![](http://common.cnblogs.com/images/copycode.gif)](javascript:void(0); "复制代码")

```
r:read就是读权限     --数字4表示
w:write就是写权限    --数字2表示
x:excute就是执行权限 --数字1表示

读、写、运行三项权限可以用数字表示，就是r=4,w=2,x=1。所以，-rw-r--r--用数字表示成644。
这里总共会有10个“-”，第一个表示文件类型，如该文件是文件(-表示)，文件夹(d表示),连接文件(l表示)，后面9个按照三个一组分。
如:rwxrwx--- 770
表示此文件(文件夹)的拥有着和同组用户有读写及执行权限，其他用户组没任何权限。
也就是前面三个表示所有者权限，中间三个表示同组用户权限，最后一组表示其他用户权限。
注意：以上的其他用户，不包括root这个super user。
```

[![](http://common.cnblogs.com/images/copycode.gif)](javascript:void(0); "复制代码")

现在下面这张图就能看懂了吧

[![](http://common.cnblogs.com/images/copycode.gif)](javascript:void(0); "复制代码")

```
[root@VM_0_11_centos /]# ls -l
total 72
lrwxrwxrwx.  1 root root     7 Apr 21  2016 bin -> usr/bin
dr-xr-xr-x.  4 root root  4096 May 27 16:47 boot
drwxr-xr-x   2 root root  4096 Apr 21  2016 data
drwxr-xr-x  19 root root  3000 May 27 16:47 dev
drwxr-xr-x. 88 root root 12288 May 27 22:56 etc
drwxr-xr-x.  4 root root  4096 May 27 22:31 home
lrwxrwxrwx.  1 root root     7 Apr 21  2016 lib -> usr/lib
lrwxrwxrwx.  1 root root     9 Apr 21  2016 lib64 -> usr/lib64
drwx------.  2 root root 16384 Apr 21  2016 lost+found
drwxr-xr-x.  2 root root  4096 Aug 12  2015 media
drwxr-xr-x.  2 root root  4096 Aug 12  2015 mnt
drwxr-xr-x.  3 root root  4096 Apr 21  2016 opt
dr-xr-xr-x  89 root root     0 May 27 16:47 proc
dr-xr-x---.  6 root root  4096 May 28 18:19 root
drwxr-xr-x  24 root root   840 May 28 19:15 run
lrwxrwxrwx.  1 root root     8 Apr 21  2016 sbin -> usr/sbin
drwxr-xr-x.  2 root root  4096 Aug 12  2015 srv
dr-xr-xr-x  13 root root     0 May 27 16:47 sys
drwxrwxrwt.  8 root root  4096 May 28 19:33 tmp
drwxr-xr-x. 13 root root  4096 Apr 21  2016 usr
drwxr-xr-x. 19 root root  4096 May 27 16:47 var
```

[![](http://common.cnblogs.com/images/copycode.gif)](javascript:void(0); "复制代码")

二 文件类型

　　LINUX 中的七种文件类型。

　　　　d  目录文件

　　　　l  符号链接 (指向另一个文件, 类似于瘟下的快捷方式)

　　　　s  套接字文件

　　　　b  块设备文件，二进制文件。

　　　　c  字符设备文件

　　　　p  命名管道文件

　　　　-  普通文件，或更准确地说，不属于以上几种类型的文件