# pwd命令概述
`pwd`是`Print Working Directory`的缩写，其功能是显示当前所在工作目录的全路径。主要用在当不确定当前所在位置时，通过`pwd`来查看当前目录的绝对路径。

# pwd命令语法
`pwd [选项]`  
参数：  
`-L`：`--logical`，显示当前的路径，有连接文件时，直接显示连接文件的路径，(不加参数时默认此方式)，[参考示例1](#exp1)。  
`-p`：`--physical`，显示当前的路径，有连接文件时，不使用连接路径，直接显示连接文件所指向的文件，[参考示例2](#exp2)。  当包含多层连接文件时，显示连接文件最终指向的文件，[参考示例3](#exp3)。  
`--help`：显示帮助信息。  
`--version`：显示版本信息。  

# pwd命令示例
## <span id="exp1"> </span>示例1:查看当前所在路径
```
[root@localhost var]# pwd
/var
```

## <span id="exp2"> </span>示例2:查看当前所在路径，不使用连接路径
```
[root@localhost ~]# cd /var/   #进入/var目录，该目录下有个mail连接文件，方便对比查看
[root@localhost var]# ll
total 164
...
drwxr-xr-x 12 root root 4096 Apr 22 19:56 log
lrwxrwxrwx  1 root root   10 Oct 17  2015 mail -> spool/mail
drwxr-xr-x  2 root root 4096 May 11  2011 nis
...

[root@localhost var]# cd mail/   #进入mail目录，mail为连接文件。
[root@localhost mail]# pwd     #默认，使用连接文件，直接显示连接文件全路径。
/var/mail

[root@localhost mail]# pwd -P    #不使用逻辑路径，连接文件最终指向的文件
/var/spool/mail

```

## <span id="exp3"> </span>示例3:多层连接文件时，显示所有连接文件最终指向的文件全路径
```
[root@localhost ~]# ll      # /root目录下面有个dir1目录，test连接文件指向dir1目录
total 12
drwxr-xr-x 2 root root 4096 Apr 24 05:51 dir1
lrwxrwxrwx 1 root root    5 Apr 24 05:54 test -> dir1/
[root@localhost ~]# ll /home/   #/home目录下面有一个test连接文件，指向/root/test连接文件 
total 20
drwx------ 16 sgl  sgl  4096 Oct 17  2015 sgl
lrwxrwxrwx  1 root root   10 Apr 24 05:55 test -> /root/test


[root@localhost ~]# cd /home/test/   #通过cd命令进入/home/test
[root@localhost test]# pwd      #默认，只显示连接文件的全路径
/home/test
[root@localhost test]# pwd -P   # 显示连接文件最终指向的文件的全路径。注意这里不是/root/test。
/root/dir1

```




<br><br><br><br>
注：本系列内容主要参考《鸟哥的linux私房菜》和CentOS系统自带的帮助文档以及网上相关资料，示例都是基于CentOS。






















