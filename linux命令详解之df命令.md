# df命令概述

`df`命令作用是列出文件系统的整体磁盘空间使用情况。可以用来查看磁盘已被使用多少空间和还剩余多少空间。  
`df`命令显示系统中包含每个文件名参数的磁盘使用情况，如果没有文件名参数，则显示所有当前已挂载文件系统的磁盘空间使用情况，[参考示例1](#exp1)。  
在默认情况下，磁盘空间是以**1KB**为单位进行显示的，但是，如果**POSIXLY_CORRECT**环境变量被设置为true，这种情况下默认使用**512字节**为单位显示，[参考示例9](#exp9)。


# df命令语法

`df [选项] [文件名]`  
参数：    
`-a`：`--all`，显示所有的文件系统，包括虚拟文件系统，[参考示例2](#exp2)。  
`-B`：`--block-size`，指定单位大小。比如1k，1m等，[参考示例3](#exp3)。  
`-h`：`--human-readable`，以人们易读的GB、MB、KB等格式显示，[参考示例4](#exp4)。  
`-H`：`--si`，和`-h`参数一样，但是不是以1024，而是1000，即1k=1000，而不是1k=1024。  
`-i`：`--inodes`，不用硬盘容量，而是以inode的数量来显示，[参考示例5](#exp5)。  
`-k`：以KB的容量显示各文件系统，相当于`--block-size=1k`。  
`-m`：以KB的容量显示各文件系统，相当于`--block-size=1m`。  
`-l`：`--local`，只显示本地文件系统。  
`--no-sync`：在统计使用信息之前不调用sync命令(默认)。  
`-sync`：在统计使用信息之前调用sync命令。  
`-P`：`--portability`，使用POSIX格式显示，[参考示例6](#exp6)。  
`-t`：`--type=TYPE`，只显示指定类型的文件系统，[参考示例7](#exp7)。  
`-T`：`--print-type`，显示文件系统类型，[参考示例8](#exp8)。  
`-x`：`--exclude-type=TYPE`，不显示指定类型的文件系统。  
`--help`：显示帮助信息。  
`--version`：显示版本信息。  


# df命令示例

## <span id="exp1"> </span>示例1:查看包含给定文件磁盘空间使用情况
```
[root@localhost ~]# df /home   #指定一个文件夹，查看该文件夹所在磁盘的使用情况
Filesystem           1K-blocks      Used Available Use% Mounted on
/dev/sda2             16036224   2749160  12459316  19% /

[root@localhost ~]# df /bin/ls   #指定一个文件
Filesystem           1K-blocks      Used Available Use% Mounted on
/dev/sda2             16036224   2749160  12459316  19% /

[root@localhost ~]# df /bin/ls /home  #指定多个文件或文件夹
Filesystem           1K-blocks      Used Available Use% Mounted on
/dev/sda2             16036224   2749160  12459316  19% /
/dev/sda2             16036224   2749160  12459316  19% /

[root@localhost ~]# df /bin/ls /home /usr/  #指定多个文件或文件夹
Filesystem           1K-blocks      Used Available Use% Mounted on
/dev/sda2             16036224   2749160  12459316  19% /
/dev/sda2             16036224   2749160  12459316  19% /
/dev/sda2             16036224   2749160  12459316  19% /

[root@localhost ~]# df   # 默认情况
Filesystem           1K-blocks      Used Available Use% Mounted on
/dev/sda2             16036224   2750464  12458012  19% /
/dev/sda1               295561     16911    263390   7% /boot
tmpfs                  1028272         0   1028272   0% /dev/shm
```
输出结果列说明： 

- Filesystem：代表该文件系统时哪个分区，所以列出的是设备名称。  
- 1K-blocks：说明下面的数字单位是1KB，可利用`-h`或`-m`来改变单位大小，也可以用`-B`来设置。  
- Used：已经使用的空间大小。  
- Available：剩余的空间大小。  
- Use%：磁盘使用率。如果使用率在90%以上时，就需要注意了，避免磁盘容量不足出现系统问题，尤其是对于文件内容增加较快的情况(如/home、/var/spool/mail等)。  
- Mounted on：磁盘挂载的目录，即该磁盘挂载到了哪个目录下面。  


## <span id="exp2"> </span>示例2:查看所有文件系统
```
[root@localhost ~]# df -a    #包括虚拟文件系统
Filesystem           1K-blocks      Used Available Use% Mounted on
/dev/sda2             16036224   2749160  12459316  19% /
proc                         0         0         0   -  /proc
sysfs                        0         0         0   -  /sys
devpts                       0         0         0   -  /dev/pts
/dev/sda1               295561     16911    263390   7% /boot
tmpfs                  1028272         0   1028272   0% /dev/shm
none                         0         0         0   -  /proc/sys/fs/binfmt_misc
none                         0         0         0   -  /proc/fs/vmblock/mountPoint
sunrpc                       0         0         0   -  /var/lib/nfs/rpc_pipefs

[root@localhost ~]# df     # 默认
Filesystem           1K-blocks      Used Available Use% Mounted on
/dev/sda2             16036224   2749160  12459316  19% /
/dev/sda1               295561     16911    263390   7% /boot
tmpfs                  1028272         0   1028272   0% /dev/shm
```
说明：系统里面存在很多特殊的文件系统，这些比较特殊的文件系统几乎都是在内存当中，（如/proc挂载点），所以，这些特殊文件系统都不会占据硬盘空间。


## <span id="exp3"> </span>示例3:指定单位大小
```
[root@localhost ~]# df -B 1k    #1k为单位
Filesystem           1K-blocks      Used Available Use% Mounted on
/dev/sda2             16036224   2749160  12459316  19% /
/dev/sda1               295561     16911    263390   7% /boot
tmpfs                  1028272         0   1028272   0% /dev/shm

[root@localhost ~]# df --block-size 1m   #1M为单位
Filesystem           1M-blocks      Used Available Use% Mounted on
/dev/sda2                15661      2685     12168  19% /
/dev/sda1                  289        17       258   7% /boot
tmpfs                     1005         0      1005   0% /dev/shm
```

## <span id="exp4"> </span>示例4:以人们易读的方式显示
```
[root@localhost ~]# df -h
Filesystem            Size  Used Avail Use% Mounted on
/dev/sda2              16G  2.7G   12G  19% /
/dev/sda1             289M   17M  258M   7% /boot
tmpfs                1005M     0 1005M   0% /dev/shm
```

## <span id="exp5"> </span>示例5:以inode的数量显示
```
[root@localhost ~]# df -i
Filesystem            Inodes   IUsed   IFree IUse% Mounted on
/dev/sda2            4141216  101279 4039937    3% /
/dev/sda1              76304      35   76269    1% /boot
tmpfs                 257068       1  257067    1% /dev/shm
```

## <span id="exp6"> </span>示例6:使用POSIX格式显示
```
[root@localhost ~]# df -P  #使用POSIX格式显示
Filesystem         1024-blocks      Used Available Capacity Mounted on
/dev/sda2             16036224   2750464  12458012      19% /
/dev/sda1               295561     16911    263390       7% /boot
tmpfs                  1028272         0   1028272       0% /dev/shm

[root@localhost ~]# df 
Filesystem           1K-blocks      Used Available Use% Mounted on
/dev/sda2             16036224   2750464  12458012  19% /
/dev/sda1               295561     16911    263390   7% /boot
tmpfs                  1028272         0   1028272   0% /dev/shm
```

## <span id="exp7"> </span>示例7:只显示类型为ext3的文件系统
```
[root@localhost ~]# df -t ext3
Filesystem           1K-blocks      Used Available Use% Mounted on
/dev/sda2             16036224   2750464  12458012  19% /
/dev/sda1               295561     16911    263390   7% /boot
```

## <span id="exp8"> </span>示例8:显示出每个文件系统的类型
```
[root@localhost ~]# df -T
Filesystem    Type   1K-blocks      Used Available Use% Mounted on
/dev/sda2     ext3    16036224   2750464  12458012  19% /
/dev/sda1     ext3      295561     16911    263390   7% /boot
tmpfs        tmpfs     1028272         0   1028272   0% /dev/shm
```

## <span id="exp9">&nbsp; </span>示例9:显示出每个文件系统的类型
```
[root@localhost ~]# df   #默认情况是1024
Filesystem           1K-blocks      Used Available Use% Mounted on
/dev/sda2             16036224   2750464  12458012  19% /
/dev/sda1               295561     16911    263390   7% /boot
tmpfs                  1028272         0   1028272   0% /dev/shm

[root@localhost ~]# export POSIXLY_CORRECT=true   #设置POSIXLY_CORRECT为true

[root@localhost ~]# df    #POSIXLY_CORRECT为true时默认512
Filesystem         512B-blocks      Used Available Use% Mounted on
/dev/sda2             32072448   5500928  24916024  19% /
/dev/sda1               591122     33822    526780   7% /boot
tmpfs                  2056544         0   2056544   0% /dev/shm

[root@localhost ~]# unset POSIXLY_CORRECT   #取消设置POSIXLY_CORRECT
[root@localhost ~]# df 
Filesystem           1K-blocks      Used Available Use% Mounted on
/dev/sda2             16036224   2750464  12458012  19% /
/dev/sda1               295561     16911    263390   7% /boot
tmpfs                  1028272         0   1028272   0% /dev/shm
```



<br><br><br><br>
注：本系列内容主要参考《鸟哥的linux私房菜》和CentOS系统自带的帮助文档以及网上相关资料，示例都是基于CentOS。

















