
# cd命令概述
`cd`是`Change Directory`的缩写，这是用来切换工作目录的命令。`cd`命令是一个内置命令，可以通过`type`命令查看，如下：
```
[root@localhost ~]# type cd
cd is a shell builtin
```


# cd命令语法
`cd [相对路径或绝对路径或特殊符号]`
说明：
不加参数时，默认切换到用户主目录，即环境变量`HOME`指定的目录，如`root`用户的`HOME`变量为`/root`，那么`cd`命令不带参数时便切换到`/root`目录下。
绝对路径是从跟目录开始的，如`/root`或`/home/sgl`，相对路径是相对于当前路径来说的，假如当前目录在`/home/guo`下面，那么前面的`/home/sgl`的相对路径就是`../sgl`，即当前目录的上级目录下的sgl目录。

特殊符号包括`~`、`-`、`..`等。
`~`表示用户主目录，即HOME变量指定的目录，如root用户的主目录为/root。
`-`表示前一个工作目录。
`..`表示上级目录。
`.`表示当前目录。


# cd命令示例
```
[root@localhost ~]# pwd   #查看当前目录。
/root
[root@localhost ~]# cd /home  #参数为绝对路径。
[root@localhost home]# pwd
/home
[root@localhost home]# cd    #不加参数，默认切换到HOME变量指定的目录。
[root@localhost ~]# pwd
/root
[root@localhost ~]# cd -   	 # - 中划线，表示前一个工作目录，这里的前一个目录是/home。
/home
[root@localhost home]# pwd
/home
[root@localhost home]# cd ~   # ~ 波浪线表示用户主目录，和不加参数时类似。
[root@localhost ~]# pwd
/root
[root@localhost ~]# cd ../var/spool/mail/   #参数为相对路径，这里是相对于/root目录。
[root@localhost mail]# pwd
/var/spool/mail
```




<br><br><br><br>
注：本系列内容主要参考《鸟哥的linux私房菜》和CentOS系统自带的帮助文档以及网上相关资料，示例都是基于CentOS。




