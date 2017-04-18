# du命令概述
`du`命令作用是估计文件系统的磁盘已使用量，常用于查看文件或目录所占磁盘容量。  
`du`命令与`df`命令不同，df命令是统计磁盘使用情况，详见[linux命令详解之df命令](http://blog.csdn.net/gnail_oug/article/details/70217446)。
`du`命令会直接到文件系统内查找所有文件数据，所以命令执行时会耗费一点儿时间。  
在默认情况下，输出结果大小是以`KB`为单位的。如果想以`MB`为单位，使用`-m`参数即可，如果只想知道目录占了多少容量，使用`-s`参数即可。  

# du命令语法
`du [选项] [文件或目录名称]`  
参数：  
`-a`：`--all`， 列出所有的文件和目录容量大小而不仅仅列出目录容量大小，默认情况只是统计目录的容量大小，[参考示例1](#exp1)。  
`-B`：`--block-size=SIZE`，指定单位大小。  
`-b`：`--bytes`，以字节为单位列出文件和目录的容量大小。  
`-c`：`--total`，除了列出文件和目录的容量大小外，列出总的容量大小，[参考示例2](#exp2)。  
`-h`：`--human-readable`，以人们易读的方式(KB,MB,GB)显示容量大小，[参考示例3](#exp3)。  
`--si`：和`-h`参数类似，但是单位换算时是以1000进行换算，而不是1024。  
`-k`：和`--block-size=1k`类似，以KB为单位。  
`-m`：和`--block-size=1m`类似，以MB为单位。  
`-s`：`--summarize`，仅列出总量，而不列出每个目录和文件的大小，[参考示例4](#exp4)。  
`-S`：`--separate-dirs`，和`-s`参数类似，但是统计时不包含子目录的容量大小。  
`--max-depth=N`：类似于默认情况的du，但是，递归显示时的递归深度小于等于N。如果`--max-depth=0`，就相当于`-s`参数，只统计总量而已，[参考示例4](#exp4)。如果`--max-depth=1`，就相当于`du -s 目录/*`，[参考示例5](#exp5)。


# du命令示例
test目录里的内容如下：
```
test/dir1
		/dir1-dira
			/dir1-dira-file1
		/dir1-file1
		/dir1-file2
	/dir2
	/file1
	/file2
[root@localhost test]# ll -R    # test目录下所有文件
.:
total 216
drwxr-xr-x 3 root root  4096 Apr 18 05:47 dir1
drwxr-xr-x 2 root root  4096 Apr 18 05:44 dir2
-rwxr-xr-x 1 root root 91272 Apr 18 05:45 file1
-rwxr-xr-x 1 root root 91272 Apr 18 05:46 file2

./dir1:
total 864
drwxr-xr-x 2 root root   4096 Apr 18 05:48 dir1-dira
-rwxr-xr-x 1 root root  55472 Apr 18 05:46 dir1-file1
-rwxr-xr-x 1 root root 801528 Apr 18 05:47 dir1-file2

./dir1/dir1-dira:
total 4
-rw-r--r-- 1 root root 0 Apr 18 05:48 dir1-dira-file1

./dir2:
total 0
```
## <span id="exp1"> </span>示例1:列出目录下所有文件和目录的容量大小
```
[root@localhost test]# du  #默认情况下，只统计目录的容量大小。
8       ./dir2
12      ./dir1/dir1-dira
876     ./dir1
1092    .
[root@localhost test]# du -a   #统计目录和文件的容量大小。
100     ./file2
8       ./dir2
100     ./file1
4       ./dir1/dir1-dira/dir1-dira-file1
12      ./dir1/dir1-dira
792     ./dir1/dir1-file2
64      ./dir1/dir1-file1
876     ./dir1
1092    .
```

## <span id="exp2"> </span>示例2:统计各文件的大小，并显示总大小
```
[root@localhost test]# du  /home/test/    # 默认，不显示总大小
8       /home/test/dir2
12      /home/test/dir1/dir1-dira
876     /home/test/dir1
1092    /home/test/
[root@localhost test]# du -c /home/test/   #最下面显示总大小total
8       /home/test/dir2
12      /home/test/dir1/dir1-dira
876     /home/test/dir1
1092    /home/test/
1092    total
```
## <span id="exp3"> </span>示例3:以易读的方式显示容量大小
```
[root@localhost test]# du -h /home/test
8.0K    /home/test/dir2
12K     /home/test/dir1/dir1-dira
876K    /home/test/dir1
1.1M    /home/test
```  
## <span id="exp4"> </span>示例4:仅显示目录的总大小
```
[root@localhost test]# du -s /home   #通过-s参数只统计总量
3208    /home

[root@localhost test]# du --max-depth=0 /home  #通过指定递归深度方式
3208    /home
```
## <span id="exp5"> </span>示例5:显示指定目录下每个文件或目录的容量大小
```
[root@localhost test]# du -s /*   #使用-s参数
8320    /bin
6659    /boot
152     /dev
170328  /etc
3208    /home
142868  /lib
25868   /lib64
16      /lost+found
8       /media
0       /misc
16      /mnt
0       /net
16      /opt
0       /proc
200     /root
36680   /sbin
0       /selinux
8       /srv
0       /sys
436     /tmp
2498560 /usr
72792   /var

[root@localhost test]# du --max-depth=1 /   #使用指定递归深度方式
436     /tmp
142868  /lib
0       /net
16      /opt
6659    /boot
0       /sys
8       /srv
8       /media
16      /mnt
25868   /lib64
36680   /sbin
2498560 /usr
170328  /etc
16      /lost+found
72792   /var
0       /selinux
8320    /bin
0       /proc
0       /misc
200     /root
3208    /home
152     /dev
2966147 /
```

## <span id="exp6"> </span>示例6:显示指定目录下每个文件或目录的容量大小，并且以易读方式显示(常用)。
```
[root@localhost test]# du -sh /*
8.2M    /bin
6.6M    /boot
152K    /dev
167M    /etc
3.2M    /home
140M    /lib
26M     /lib64
16K     /lost+found
8.0K    /media
0       /misc
16K     /mnt
0       /net
16K     /opt
0       /proc
200K    /root
36M     /sbin
0       /selinux
8.0K    /srv
0       /sys
436K    /tmp
2.4G    /usr
72M     /var
```




<br><br><br><br>
注：本系列内容主要参考《鸟哥的linux私房菜》和CentOS系统自带的帮助文档以及网上相关资料，示例都是基于CentOS。






















