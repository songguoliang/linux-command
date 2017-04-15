# ls命令概述

`ls`命令用于显示文件目录列表，和`Windows`系统下`DOS`命令`dir`类似。当执行`ls`命令时，默认显示的只有**非隐藏文件**的文件名、以文件名进行排序及文件名代表的颜色显示。当不加参数时，默认列出当前目录的列表信息。`ls`命令使用频率非常高，参数也非常多，多达四五十个，本文只介绍一部分常用的参数，其他参数可以通过`man`命令查看帮助手册。

说明：在linux下，文件名以点`.`开头表示该文件为隐藏文件，如`.bashrc`。

# ls命令语法
`ls [选项] [目录或文件名]`  
参数：  
`-a`：`--all`的缩写，显示所有的文件，包括隐藏文件(以`.`开头的文件)，[参考示例1](#exp1)。(常用)   
`-A`：`--almost-all`的缩写，显示所有的文件，包括隐藏文件，但不包括表示当前目录`.`和上级目录`..`这两个文件，[参考示例2](#exp2)。  
`-c`：和`-lt`一起使用：显示列表并且以ctime(文件状态最后改变时间)排序。和`-l`一起使用：显示ctime并且以文件名排序。其他情况，以ctime排序。[参考示例3](#exp3)。  
`-d`：`--directory`的缩写，仅列出目录本身，而不是列出目录里的内容列表，[参考示例4](#exp4)。(常用)  
`-f`：直接列出结果，而不进行排序(ls默认会以文件名排序)  
`--color[=WHEN]`：是否根据文件类型显示颜色，WHEN可以为`never`、`always`或者`auto`  
`--full-time`：以完整的实际模式显示(包含年月日时分)，类似与`ls -l --time-style=full-iso`，[参考示例5](#exp5)。  
`-g`：列表显示结果，和-l类似，但是不显示文件所属者。  
`-h`：将文件内容大小以GB、KB等易读的方式显示，[参考示例6](#exp6)。  
`-i`：结合`-l`参数，列出每个文件的inode，[参考示例7](#exp7)。  
`-l`：列出长数据串，显示出文件的属性与权限等数据信息(常用)  
`-n`：和-l类似，只是显示的所属用户和组不是名称而是对应的id，[参考示例8](#exp8)。  
`-r`：`--reverse`，将排序结果以倒序方式显示，[参考示例9](#exp9)。  
`-S`：以文件大小排序，[参考示例9](#exp9)。  
`-t`：以修改时间排序  
`--help`：显示帮助信息  

# ls命令示例

<span id="exp1"></span>示例1：列出所有文件(注意和`-A`参数的区别，结果里面包括表示当前目录`.`和上级目录`..`这两个文件)。
```
[root@localhost ~]# ls -a    #列出所有文件
.  ..  .bash_history  .bash_logout  .bash_profile  .bashrc   install.log  install.log.syslog
[root@localhost ~]# ls --all
.  ..  .bash_history  .bash_logout  .bash_profile  .bashrc   install.log  install.log.syslog
```

<span id="exp2"></span>示例2：列出所有的文件，但不包括表示当前目录`.`和上级目录`..`这两个文件。
```
[root@localhost ~]# ls -A
.bash_history  .bash_logout  .bash_profile  .bashrc  install.log  install.log.syslog  
[root@localhost ~]# ls --almost-all
.bash_history  .bash_logout  .bash_profile  .bashrc  install.log  install.log.syslog
```

<span id="exp3"></span>示例3：显示列表并且以ctime排序
```
[root@localhost /]# ls -clt   #和 -lt参数一起使用，以时间排序
total 146
drwxrwxrwt   7 root root  4096 Apr 13 06:23 tmp
drwxr-xr-x  12 root root  4440 Apr 13 05:18 dev
drwxr-xr-x  93 root root 12288 Apr 13 05:18 etc
drwxr-xr-x   2 root root     0 Apr 13 05:18 net
drwxr-xr-x   2 root root     0 Apr 13 05:18 misc
drwxr-xr-x   4 root root     0 Apr 13 05:16 selinux
drwxr-xr-x  11 root root     0 Apr 13 05:16 sys
dr-xr-xr-x 150 root root     0 Apr 13 05:16 proc
drwxr-xr-x   2 root root 12288 Mar 28 06:34 sbin
drwxr-xr-x   2 root root  4096 Mar 28 06:33 bin
drwxr-xr-x   8 root root  4096 Mar 28 06:33 lib64
drwxr-x---   4 root root  4096 Nov 19 06:52 root
drwxr-xr-x   4 root root  4096 Nov 18 22:05 home
drwxr-xr-x  11 root root  4096 Nov 14 06:13 lib
drwxr-xr-x   3 root root  4096 Oct 17  2015 mnt
drwxr-xr-x  22 root root  4096 Oct 17  2015 var
drwxr-xr-x   4 root root  1024 Oct 17  2015 boot
drwxr-xr-x  15 root root  4096 Oct 17  2015 usr
drwxr-xr-x   2 root root  4096 Oct 17  2015 media
drwxr-xr-x   2 root root  4096 Oct 17  2015 srv
drwx------   2 root root 16384 Oct 17  2015 lost+found
drwxr-xr-x   3 root root  4096 Oct 17  2015 opt
[root@localhost /]# ls -cl   #和-l参数一起使用，以文件名排序并显示时间
total 146
drwxr-xr-x   2 root root  4096 Mar 28 06:33 bin
drwxr-xr-x   4 root root  1024 Oct 17  2015 boot
drwxr-xr-x  12 root root  4440 Apr 13 05:18 dev
drwxr-xr-x  93 root root 12288 Apr 13 05:18 etc
drwxr-xr-x   4 root root  4096 Nov 18 22:05 home
drwxr-xr-x  11 root root  4096 Nov 14 06:13 lib
drwxr-xr-x   8 root root  4096 Mar 28 06:33 lib64
drwx------   2 root root 16384 Oct 17  2015 lost+found
drwxr-xr-x   2 root root  4096 Oct 17  2015 media
drwxr-xr-x   2 root root     0 Apr 13 05:18 misc
drwxr-xr-x   3 root root  4096 Oct 17  2015 mnt
drwxr-xr-x   2 root root     0 Apr 13 05:18 net
drwxr-xr-x   3 root root  4096 Oct 17  2015 opt
dr-xr-xr-x 150 root root     0 Apr 13 05:16 proc
drwxr-x---   4 root root  4096 Nov 19 06:52 root
drwxr-xr-x   2 root root 12288 Mar 28 06:34 sbin
drwxr-xr-x   4 root root     0 Apr 13 05:16 selinux
drwxr-xr-x   2 root root  4096 Oct 17  2015 srv
drwxr-xr-x  11 root root     0 Apr 13 05:16 sys
drwxrwxrwt   7 root root  4096 Apr 13 06:23 tmp
drwxr-xr-x  15 root root  4096 Oct 17  2015 usr
drwxr-xr-x  22 root root  4096 Oct 17  2015 var
[root@localhost /]# ls -c   #单独使用，以时间排序，但不显示时间
tmp  dev  etc  net  misc  selinux  sys  proc  sbin  bin  lib64  root  home  lib  mnt  var  boot  usr  media  srv  lost+found  opt
```

<span id="exp4"></span>示例4：仅仅列出目录本身，不需要列出目录里的内容
```
[root@localhost /]# ls -d /home   #仅列出/home目录本身
/home
[root@localhost /]# ls /home   #列出/home目录里的内容
sgl  software

# 加上-l参数，比较的更清楚一些：
[root@localhost /]# ls -ld /home
drwxr-xr-x 4 root root 4096 Nov 18 22:05 /home
[root@localhost /]# ls -l /home
total 16
drwx------ 16 sgl  sgl  4096 Oct 17  2015 sgl
drwxr-xr-x  3 root root 4096 Nov 14 05:13 software

```

<span id="exp5"></span>示例5：显示完整时间
```
[root@localhost ~]# ls --full-time /
total 146
drwxr-xr-x   2 root root  4096 2017-03-28 06:33:59.000000000 -0700 bin
drwxr-xr-x   4 root root  1024 2015-10-17 08:08:24.000000000 -0700 boot
drwxr-xr-x  12 root root  4440 2017-04-14 21:22:27.241239736 -0700 dev
drwxr-xr-x  93 root root 12288 2017-04-14 21:22:24.000000000 -0700 etc
drwxr-xr-x   4 root root  4096 2016-11-18 22:05:32.000000000 -0800 home
drwxr-xr-x  11 root root  4096 2016-11-14 06:13:35.000000000 -0800 lib
drwxr-xr-x   8 root root  4096 2017-03-28 06:33:33.000000000 -0700 lib64
drwx------   2 root root 16384 2015-10-17 08:01:52.000000000 -0700 lost+found
drwxr-xr-x   2 root root  4096 2011-05-11 04:58:23.000000000 -0700 media
drwxr-xr-x   2 root root     0 2017-04-14 21:22:23.789239736 -0700 misc
drwxr-xr-x   3 root root  4096 2015-10-17 08:16:39.000000000 -0700 mnt
drwxr-xr-x   2 root root     0 2017-04-14 21:22:23.839239736 -0700 net
drwxr-xr-x   3 root root  4096 2015-10-17 00:17:25.000000000 -0700 opt
dr-xr-xr-x 147 root root     0 2017-04-14 21:21:02.005999666 -0700 proc
drwxr-x---   4 root root  4096 2016-11-19 06:52:09.000000000 -0800 root
drwxr-xr-x   2 root root 12288 2017-03-28 06:34:07.000000000 -0700 sbin
drwxr-xr-x   4 root root     0 2017-04-14 21:21:02.671999847 -0700 selinux
drwxr-xr-x   2 root root  4096 2011-05-11 04:58:23.000000000 -0700 srv
drwxr-xr-x  11 root root     0 2017-04-14 21:21:02.657999847 -0700 sys
drwxrwxrwt   7 root root  4096 2017-04-14 21:24:24.000000000 -0700 tmp
drwxr-xr-x  15 root root  4096 2015-10-17 08:04:13.000000000 -0700 usr
drwxr-xr-x  22 root root  4096 2015-10-17 08:11:05.000000000 -0700 var
```

<span id="exp6"></span>示例6：以易读方式显示列表
```
[root@localhost ~]# ls -lh /   #注意列表容量大小列的单位
total 146K
drwxr-xr-x   2 root root 4.0K Mar 28 06:33 bin
drwxr-xr-x   4 root root 1.0K Oct 17  2015 boot
drwxr-xr-x  12 root root 4.4K Apr 14 21:22 dev
drwxr-xr-x  93 root root  12K Apr 14 21:22 etc
drwxr-xr-x   4 root root 4.0K Nov 18 22:05 home
drwxr-xr-x  11 root root 4.0K Nov 14 06:13 lib
drwxr-xr-x   8 root root 4.0K Mar 28 06:33 lib64
drwx------   2 root root  16K Oct 17  2015 lost+found
drwxr-xr-x   2 root root 4.0K May 11  2011 media
drwxr-xr-x   2 root root    0 Apr 14 21:22 misc
drwxr-xr-x   3 root root 4.0K Oct 17  2015 mnt
drwxr-xr-x   2 root root    0 Apr 14 21:22 net
drwxr-xr-x   3 root root 4.0K Oct 17  2015 opt
dr-xr-xr-x 147 root root    0 Apr 14 21:21 proc
drwxr-x---   4 root root 4.0K Nov 19 06:52 root
drwxr-xr-x   2 root root  12K Mar 28 06:34 sbin
drwxr-xr-x   4 root root    0 Apr 14 21:21 selinux
drwxr-xr-x   2 root root 4.0K May 11  2011 srv
drwxr-xr-x  11 root root    0 Apr 14 21:21 sys
drwxrwxrwt   7 root root 4.0K Apr 14 21:24 tmp
drwxr-xr-x  15 root root 4.0K Oct 17  2015 usr
drwxr-xr-x  22 root root 4.0K Oct 17  2015 var

[root@localhost ~]# ls -l /   #默认方式，以字节为单位显示
total 146
drwxr-xr-x   2 root root  4096 Mar 28 06:33 bin
drwxr-xr-x   4 root root  1024 Oct 17  2015 boot
drwxr-xr-x  12 root root  4440 Apr 14 21:22 dev
drwxr-xr-x  93 root root 12288 Apr 14 21:22 etc
drwxr-xr-x   4 root root  4096 Nov 18 22:05 home
drwxr-xr-x  11 root root  4096 Nov 14 06:13 lib
drwxr-xr-x   8 root root  4096 Mar 28 06:33 lib64
drwx------   2 root root 16384 Oct 17  2015 lost+found
drwxr-xr-x   2 root root  4096 May 11  2011 media
drwxr-xr-x   2 root root     0 Apr 14 21:22 misc
drwxr-xr-x   3 root root  4096 Oct 17  2015 mnt
drwxr-xr-x   2 root root     0 Apr 14 21:22 net
drwxr-xr-x   3 root root  4096 Oct 17  2015 opt
dr-xr-xr-x 147 root root     0 Apr 14 21:21 proc
drwxr-x---   4 root root  4096 Nov 19 06:52 root
drwxr-xr-x   2 root root 12288 Mar 28 06:34 sbin
drwxr-xr-x   4 root root     0 Apr 14 21:21 selinux
drwxr-xr-x   2 root root  4096 May 11  2011 srv
drwxr-xr-x  11 root root     0 Apr 14 21:21 sys
drwxrwxrwt   7 root root  4096 Apr 14 21:24 tmp
drwxr-xr-x  15 root root  4096 Oct 17  2015 usr
drwxr-xr-x  22 root root  4096 Oct 17  2015 var
```
<span id="exp7"></span>示例7：显示inode
```
[root@localhost ~]# ls -li /
total 146
3717313 drwxr-xr-x   2 root root  4096 Mar 28 06:33 bin
      2 drwxr-xr-x   4 root root  1024 Oct 17  2015 boot
   1071 drwxr-xr-x  12 root root  4440 Apr 14 21:22 dev
1369537 drwxr-xr-x  93 root root 12288 Apr 14 21:22 etc
1402145 drwxr-xr-x   4 root root  4096 Nov 18 22:05 home
2380385 drwxr-xr-x  11 root root  4096 Nov 14 06:13 lib
2184737 drwxr-xr-x   8 root root  4096 Mar 28 06:33 lib64
     11 drwx------   2 root root 16384 Oct 17  2015 lost+found
 195649 drwxr-xr-x   2 root root  4096 May 11  2011 media
  14244 drwxr-xr-x   2 root root     0 Apr 14 21:22 misc
1434753 drwxr-xr-x   3 root root  4096 Oct 17  2015 mnt
  14249 drwxr-xr-x   2 root root     0 Apr 14 21:22 net
 391297 drwxr-xr-x   3 root root  4096 Oct 17  2015 opt
      1 dr-xr-xr-x 147 root root     0 Apr 14 21:21 proc
  65217 drwxr-x---   4 root root  4096 Nov 19 06:52 root
3554273 drwxr-xr-x   2 root root 12288 Mar 28 06:34 sbin
    591 drwxr-xr-x   4 root root     0 Apr 14 21:21 selinux
1956481 drwxr-xr-x   2 root root  4096 May 11  2011 srv
      1 drwxr-xr-x  11 root root     0 Apr 14 21:21 sys
3815137 drwxrwxrwt   7 root root  4096 Apr 14 21:24 tmp
3456449 drwxr-xr-x  15 root root  4096 Oct 17  2015 usr
2576033 drwxr-xr-x  22 root root  4096 Oct 17  2015 var
```

<span id="exp8"></span>示例8：列出文件夹内容，并显示出文件所属用户和组的id
```
[root@localhost ~]# ls -ln /
total 146
drwxr-xr-x   2 0 0  4096 Mar 28 06:33 bin
drwxr-xr-x   4 0 0  1024 Oct 17  2015 boot
drwxr-xr-x  12 0 0  4440 Apr 14 21:22 dev
drwxr-xr-x  93 0 0 12288 Apr 14 21:22 etc
drwxr-xr-x   4 0 0  4096 Nov 18 22:05 home
drwxr-xr-x  11 0 0  4096 Nov 14 06:13 lib
drwxr-xr-x   8 0 0  4096 Mar 28 06:33 lib64
drwx------   2 0 0 16384 Oct 17  2015 lost+found
drwxr-xr-x   2 0 0  4096 May 11  2011 media
drwxr-xr-x   2 0 0     0 Apr 14 21:22 misc
drwxr-xr-x   3 0 0  4096 Oct 17  2015 mnt
drwxr-xr-x   2 0 0     0 Apr 14 21:22 net
drwxr-xr-x   3 0 0  4096 Oct 17  2015 opt
dr-xr-xr-x 147 0 0     0 Apr 14 21:21 proc
drwxr-x---   4 0 0  4096 Nov 19 06:52 root
drwxr-xr-x   2 0 0 12288 Mar 28 06:34 sbin
drwxr-xr-x   4 0 0     0 Apr 14 21:21 selinux
drwxr-xr-x   2 0 0  4096 May 11  2011 srv
drwxr-xr-x  11 0 0     0 Apr 14 21:21 sys
drwxrwxrwt   7 0 0  4096 Apr 14 21:24 tmp
drwxr-xr-x  15 0 0  4096 Oct 17  2015 usr
drwxr-xr-x  22 0 0  4096 Oct 17  2015 var
```
<span id="exp9"></span>示例9：以文件大小排序(升序和降序)
```
[root@localhost ~]# ls -lS /    #默认降序排序
total 146
drwx------   2 root root 16384 Oct 17  2015 lost+found
drwxr-xr-x  93 root root 12288 Apr 14 21:22 etc
drwxr-xr-x   2 root root 12288 Mar 28 06:34 sbin
drwxr-xr-x  12 root root  4440 Apr 14 21:22 dev
drwxr-xr-x   2 root root  4096 Mar 28 06:33 bin
drwxr-xr-x   4 root root  4096 Nov 18 22:05 home
drwxr-xr-x  11 root root  4096 Nov 14 06:13 lib
drwxr-xr-x   8 root root  4096 Mar 28 06:33 lib64
drwxr-xr-x   2 root root  4096 May 11  2011 media
drwxr-xr-x   3 root root  4096 Oct 17  2015 mnt
drwxr-xr-x   3 root root  4096 Oct 17  2015 opt
drwxr-x---   4 root root  4096 Nov 19 06:52 root
drwxr-xr-x   2 root root  4096 May 11  2011 srv
drwxrwxrwt   7 root root  4096 Apr 14 21:24 tmp
drwxr-xr-x  15 root root  4096 Oct 17  2015 usr
drwxr-xr-x  22 root root  4096 Oct 17  2015 var
drwxr-xr-x   4 root root  1024 Oct 17  2015 boot
drwxr-xr-x   2 root root     0 Apr 14 21:22 misc
drwxr-xr-x   2 root root     0 Apr 14 21:22 net
dr-xr-xr-x 147 root root     0 Apr 14 21:21 proc
drwxr-xr-x   4 root root     0 Apr 14 21:21 selinux
drwxr-xr-x  11 root root     0 Apr 14 21:21 sys
[root@localhost ~]# ls -lSr /  #通过-r参数实现升序排列
total 146
drwxr-xr-x  11 root root     0 Apr 14 21:21 sys
drwxr-xr-x   4 root root     0 Apr 14 21:21 selinux
dr-xr-xr-x 147 root root     0 Apr 14 21:21 proc
drwxr-xr-x   2 root root     0 Apr 14 21:22 net
drwxr-xr-x   2 root root     0 Apr 14 21:22 misc
drwxr-xr-x   4 root root  1024 Oct 17  2015 boot
drwxr-xr-x  22 root root  4096 Oct 17  2015 var
drwxr-xr-x  15 root root  4096 Oct 17  2015 usr
drwxrwxrwt   7 root root  4096 Apr 14 21:24 tmp
drwxr-xr-x   2 root root  4096 May 11  2011 srv
drwxr-x---   4 root root  4096 Nov 19 06:52 root
drwxr-xr-x   3 root root  4096 Oct 17  2015 opt
drwxr-xr-x   3 root root  4096 Oct 17  2015 mnt
drwxr-xr-x   2 root root  4096 May 11  2011 media
drwxr-xr-x   8 root root  4096 Mar 28 06:33 lib64
drwxr-xr-x  11 root root  4096 Nov 14 06:13 lib
drwxr-xr-x   4 root root  4096 Nov 18 22:05 home
drwxr-xr-x   2 root root  4096 Mar 28 06:33 bin
drwxr-xr-x  12 root root  4440 Apr 14 21:22 dev
drwxr-xr-x   2 root root 12288 Mar 28 06:34 sbin
drwxr-xr-x  93 root root 12288 Apr 14 21:22 etc
drwx------   2 root root 16384 Oct 17  2015 lost+found
```





<br><br><br><br>
注：本系列内容主要参考《鸟哥的linux私房菜》和CentOS系统自带的帮助文档以及网上相关资料，示例都是基于CentOS。







