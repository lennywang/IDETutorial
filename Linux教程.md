## 常用操作

### 1. 目录操作

#### 1.1 目录结构

![Linux目录结构](https://github.com/lennywang/Img/raw/master/linux.png)

* home:创建admin用户，就会在home目录下对应admin目录。创建vsftp用户，就会在home目录下对应vsftp目录


* usr：通常将软件安装在/usr/local目录下面。安装jdk   /usr/local/jdk/….（安装的jdk）

#### 1.2 目录切换

| 操作         | 命令     | 说明                      |
| :--------- | :----- | ----------------------- |
| 打印当前目录     | pwd    | print working directory |
| 进入某个目录     | cd 目录名 |                         |
| 回到上一层目录    | cd ..  |                         |
| 切换到系统根目录   | cd /   |                         |
| 切换到用户主目录   | cd ~   |                         |
| 切换到上一个所在目录 | cd -   |                         |

#### 1.3 目录操作

**增加目录**
命令：mkdir 目录名称
示例：在根目录 / 下 mkdir test，就会在根目录 / 下产生一个test目录
![增加目录](https://github.com/lennywang/Img/raw/master/linux-content-add.png)

**查看目录**
命令：ls [-al] 父目录
示例：在根目录 / 下使用ls，可以看到该目录下的所有的目录和文件
![查看目录](https://github.com/lennywang/Img/raw/master/linux-content-list.png)

示例：在根目录 / 下使用ls -a，可以看到该目录下的所有文件和目录，包括隐藏的
![查看目录包括隐藏的](https://github.com/lennywang/Img/raw/master/linux-content-list-2.png)

示例：在根目录 / 下使用ls -l，可以看到该目录下的所有目录和文件的详细信息
![查看目录,该目录下的所有目录和文件的详细信息](https://github.com/lennywang/Img/raw/master/linux-content-list-3.png)

**寻找目录**
命令：find 目录 参数
示例：查找/root下的与test相关的目录(文件)  find /root -name ‘test*’

**修改目录的名称**
命令：mv 目录名称 新目录名称
示例：test目录下有一个oldTest目录，使用mv oldTest newTest命令修改
![修改目录的名称](https://github.com/lennywang/Img/raw/master/linux-content-modify.png)
**注意：mv的语法不仅可以对目录进行重命名而且也可以对各种文件，压缩包等进行    重命名的操作**

**移动目录的位置---剪切**
命令：mv 目录名称 目录的新位置
示例：在test下将newTest目录剪切到 /usr下面，使用mv newTest /usr
![移动目录的位置](https://github.com/lennywang/Img/raw/master/linux-content-move.png)
**注意：mv语法不仅可以对目录进行剪切操作，对文件和压缩包等都可执行剪切操作**

**拷贝目录**
命令：cp -r 目录名称 目录拷贝的目标位置 -----r代表递归拷贝
示例：将/usr下的newTest拷贝到根目录下的test中，使用cp -r /usr/newTest /test
![拷贝目录](https://github.com/lennywang/Img/raw/master/linux-content-copy.png)
**注意：cp命令不仅可以拷贝目录还可以拷贝文件，压缩包等，拷贝文件和压缩包时不  用写-r递归**

**删除目录**
命令：rm [-rf] 目录
示例：删除/usr下的newTest，进入/usr下使用rm -r newTest
![删除目录](https://github.com/lennywang/Img/raw/master/linux-content-delete.png)

示例：删除/test下的newTest而不需要询问强制删除，在/test下使用rm -rf newTest
![删除目录，无询问](https://github.com/lennywang/Img/raw/master/linux-content-delete-2.png)
**注意：rm不仅可以删除目录，也可以删除其他文件或压缩包，为了增强大家的记忆， 无论删除任何目录或文件，都直接使用rm -rf 目录/文件/压缩包**

### 2. 文件操作

> [linux文件操作命令](https://blog.csdn.net/hardworkingzy/article/details/54835913)

#### 2.1 新建文件

【命令格式】：touch [option] filename

【命令参数】：该命令会创建以参数filename为名称的文件，因此参数filename     应该遵循文件命名规则。

【示例】： (1) 创建空文件：文件名是ab    				# touch ab

​		   (2) 创建并修改文件的时间戳记：使用选项 d          touch -d "6/20/10 18:32" ab

#### 2.2 查看文件

命令：cat/more/less/tail 文件
示例：使用cat查看/etc/sudo.conf文件，只能显示最后一屏内容![查看文件](https://github.com/lennywang/Img/raw/master/linux-file-cat-1.png)

示例：使用more查看/etc/sudo.conf文件，可以显示百分比，回车可以向下一行，    空格可以向下一页，q可以退出查看
![more](https://github.com/lennywang/Img/raw/master/linux-file-cat-2.png)

示例：使用less查看/etc/sudo.conf文件，可以使用键盘上的PgUp和PgDn向上 和向下翻页，q结束查看
![less](https://github.com/lennywang/Img/raw/master/linux-file-cat-3.png)

示例：使用tail -10 查看/etc/sudo.conf文件的后10行，Ctrl+C结束
![tail](https://github.com/lennywang/Img/raw/master/linux-file-cat-4.png)

**注意：命令 tail -f 文件 可以对某个文件进行动态监控，例如tomcat的日志文件，    会随着程序的运行，日志会变化，可以使用tail -f catalina-2016-11-11.log 监控文件的变化**

#### 2.3 修改文件内容

命令：vim 文件
示例：编辑/test下的aaa.txt文件，使用vim aaa.txt
![vim](https://github.com/lennywang/Img/raw/master/linux-file-modify-1.png)

但此时并不能编辑，因为此时处于命令模式，点击键盘i/a/o进入编辑模式，可以编辑文件
![i](https://github.com/lennywang/Img/raw/master/linux-file-modify-2.png)

编辑完成后，按下Esc，退回命令模式
![i](https://github.com/lennywang/Img/raw/master/linux-file-modify-3.png)

此时文件虽然已经编辑完成，但是没有保存，需输入冒号：进入底行模式，在底行模    式下输入wq代表写入内容并退出，即保存；输入q!代表强制退出不保存。
![wq](https://github.com/lennywang/Img/raw/master/linux-file-modify-4.png)

#### 2.4 删除文件

同目录删除：熟记 rm -rf 文件 即可
 -f, --force    忽略不存在的文件，从不给出提示。
-r, --recursive   指示rm将参数中列出的全部目录和子目录均递归地删除。

#### 2.5 压缩文件 

**(1)打包并压缩文件**

Linux中的打包文件一般是以.tar结尾的，压缩的命令一般是以.gz结尾的。而一般情况下打包和压缩是一起进行的，打包并压缩后的文件的后缀名一般.tar.gz。

命令：tar -zcvf 打包压缩后的文件名 要打包压缩的文件
其中：z：调用gzip压缩命令进行压缩
​	  c：打包文件
​	  v：显示运行过程
​	  f：指定文件名
示例：打包并压缩/test下的所有文件 压缩后的压缩包指定名称为xxx.tar.gz
​	  tar -zcvf xxx.tar.gz aaa.txt bbb.txt ccc.txt  	或：tar -zcvf xxx.tar.gz /test/*
![tar](https://github.com/lennywang/Img/raw/master/linux-tar-1.png)

**(2)解压压缩包（重点）**

命令：tar [-xvf] 压缩文件
其中：x：代表解压
示例：将/test下的xxx.tar.gz解压到当前目录下
​	  tar -xvf xxx.tar.gz
![tar](https://github.com/lennywang/Img/raw/master/linux-tar-2.png)

示例：将/test下的xxx.tar.gz解压到根目录/usr下
![tar](https://github.com/lennywang/Img/raw/master/linux-tar-3.png)

<font color="red">tar -xvf xxx.tar.gz -C /usr------C代表指定解压的位置</font>

### 3.其他命令

| 命令                  | 示例                        | 含义                                   |
| ------------------- | ------------------------- | ------------------------------------ |
| grep 要搜索的字符串 要搜索的文件 | grep to sudo.conf --color | 搜索/usr/sudu.conf文件中包含字符串to的行 to要高亮显示 |
| \|                  |                           | 将前一个命令的输出作为本次目录的输入                   |
| ps -ef              | ps -ef \| grep system     | 查看当前系统中所有的进程中包括system字符串的进程          |
| kill -9 进程的pid      |                           | 杀死进程                                 |
| ifconfig            |                           | 查看当前系统的网卡信息                          |
| ping                |                           | 查看与某台机器的连接情况                         |
| netstat -an         |                           | 查看当前系统的端口使用                          |



### 4.权限命令

权限是Linux中的重要概念，每个文件/目录等都具有权限，通过ls -l命令我们可以	查看某个目录下的文件或目录的权限
示例：在随意某个目录下ls -l
![](https://github.com/lennywang/Img/raw/master/priviledge-1.png))

第一列的内容的信息解释如下：
![](https://github.com/lennywang/Img/raw/master/priviledge-2.png)

文件的类型：
d：代表目录
-：代表文件
l：代表链接（可以认为是window中的快捷方式）
后面的9位分为3组，每3位置一组，分别代表属主的权限，与当前用户同组的	用户的权限，其他用户的权限
r：代表权限是可读，r也可以用数字4表示
w：代表权限是可写，w也可以用数字2表示
x：代表权限是可执行，x也可以用数字1表示



修改文件/目录的权限的命令：chmod
示例：修改/test下的aaa.txt的权限为属主有全部权限，属主所在的组有读写权限，
其他用户只有读的权限
chmod u=rwx,g=rw,o=r aaa.txt

![](https://github.com/lennywang/Img/raw/master/priviledge-3.png)

上述示例还可使用数字表示：
chmod 764 aaa.txt



## 实践

### 1. 重启邮件服务

1、查找要替换的文件

```shell
cat mail.txt
```

2、备份文件

```shell
move a.txt b.bak.txt
```

3、上传文件

```shell
rz
```

备注：Linux上传文件和下载文件

| 命令                   | 作用   | 备注   |
| -------------------- | ---- | ---- |
| yum install -y lrzsz | 安装   |      |
| rz                   | 上传   |      |
| sz 文件名               | 下载   |      |

4、重启服务

```shell
ps -aux | grep java | grep mail
kill 命令用于杀死进程

nohup java -Xdebug -Xrunjdwp:transport=dt_socket,server=y,suspend=n,address=5354 -jar -Dspring.profiles.active=prod ./didi-km-mail/target/didi-km-mail-0.0.1-SNAPSHOT.jar & 
```

说明：1. ps命令是Process Status

2.nohup command &
nohup: no hang up
nohup command &   用途：不挂断地运行命令 语法：nohup Command  Arg & 
如果使用nohup命令提交作业，那么在缺省情况下该作业的所有输出都被重定向到一个名为nohup.out的文件中

3.java –jar 
运行Jar包

4.-Xdebug -Xrunjdwp:transport=dt_socket,server=y,suspend=n,address=5354
-Xdebug ：启用调试
Xrunjdwp ：通知JVM使用(java debug wire protocol)来运行调试环境
Xrunjdwp 调试选项

| 选项        | 含义                       | 取值                                       |
| :-------- | :----------------------- | ---------------------------------------- |
| transport | 指定调试数据的传送方式              | dt_socket是指用SOCKET模式                               <br/> dt_shmem指用共享内存方式，dt_shmem只适用于Windows平台 |
| server    | 是否支持在server模式的VM         |                                          |
| suspend   | 是否在调试客户端建立起来后，再执行JVM     |                                          |
| address   | 调试服务器的端口号，客户端用来连接服务器的端口号 |                                          |

> 参考：[-Xdebug 启动命令](https://blog.csdn.net/benben683280/article/details/78716397)

5.Dspring.profiles.active=prod
-D<name>=<value> set a system property  设置系统属性





### 2. Linux 系统重启、关机命令

**重启**

| 命令                | 作用                      | 备注   |
| ----------------- | ----------------------- | ---- |
| reboot            | 普通重启                    |      |
| shutdown -r now   | 立刻重启(root用户使用)          |      |
| shutdown -r 10    | 过10分钟自动重启(root用户使用)     |      |
| shutdown -r 20:35 | 在时间为20:35时候重启(root用户使用) |      |
| shutdown -c       | 取消重启                    |      |

**关机**

| 命令              | 作用             | 备注   |
| --------------- | -------------- | ---- |
| halt            | 立刻关机           |      |
| poweroff        | 立刻关机           |      |
| shutdown -h now | 立刻关机(root用户使用) |      |
| shutdown -h 10  | 10分钟后自动关机      |      |

**常规**

| 命令                         | 作用            | 备注                                       |
| -------------------------- | ------------- | ---------------------------------------- |
| date                       | 查看时间和日期       |                                          |
| du -sh catalina-daemon.out | 查看文件占用空间大小    | -h 表示「Human-readable」输出，使用 GB、MB 等格式     |
| ls \| wc -w                | 查看当前目录有多少文件   |                                          |
| ll -rt                     | 按时间排序显示文件     | ll －t 是降序， ll －t ｜ tac 是升序               |
| ll -Sh                     | 按大小排序(单位：k,M) | -r, --reverse   reverse order while sorting<br />-t                   sort by modification time<br />-S                  sort by file size<br />-h,                  --human-readable  <br />with -l, print sizes in human readable format |
|                            |               |                                          |

怎么查看linux文件夹下有多少个文件
https://jingyan.baidu.com/article/77b8dc7fa4efc46174eab6b9.html

LINUX中LS对文件进行按大小排序和按时间排序,设置LS时间格式
https://www.cnblogs.com/sien6/p/8056315.html



### 3. Vim 编辑器

**插入**

 i

**退出**

| 命令                                       | 作用     | 备注               |
| ---------------------------------------- | ------ | ---------------- |
| 1. ESC \| : \| WQ(x) 回车<br />2. ESC \| Shift+zz | 保存退出   | w:write   q:quit |
| ESC \| : \| q                            | 正常退出   |                  |
| ESC \| : \| q!                           | 不保存退出  |                  |
| ESC \| : \| !                            | 强制退出   |                  |
| :n                                       | 跳转到第n行 | :79，就跳转到第79行     |
| :set nu                                  | 显示行数   |                  |
| :set nu!                                 | 取消行号   |                  |
|                                          |        |                  |
|                                          |        |                  |

Linux获取日志指定行数范围内的内容
https://www.cnblogs.com/xxiong1031/p/6884362.html

Linux---vi/vim复制剪切粘贴以及常用命令小结
https://blog.csdn.net/netdxy/article/details/50553543

linux 下 vi 复制一行粘贴删除一行数据
https://blog.csdn.net/xieganyu3460/article/details/82229091

### 4.查看文件

查看文件指定行信息 (前n行，后n行)

* 查看文件所有内容（如果太长一般只显示后面一部分）  cat filename.txt

* 查看文件前100行  cat filename.txt | head -n 100

* 查看文件后50行   cat filename.txt | tail -n 50

* 从1000行开始显示，也就是显示1000行以后的   tail -n +1000

* 显示1000行到3000行内容   cat filename.txt |head -n 3000 | tail -n +1000

* 从第3000行开始，显示1000行，也就是3000~3999   cat filename.txt | tail -n +3000 | head -n 1000

* 直接用sed命令：  sed -n '5,10p' filename.txt   只查看文件的第5行到第10行



| 命令                         | 作用           | 备注                      |
| -------------------------- | ------------ | ----------------------- |
| ls -Sl                     | 按文件大小倒序      |                         |
| ls -Slr                    | 按文件大小倒序      | -h，表示"--human-readable" |
| ls -lt                     | 按时间倒序        |                         |
| ls -lrt                    | 按时间正序        |                         |
| ll                         | 按文件名正序       |                         |
| ll \| grep '^-'  \| wc -l  | 统计当前目录下文件总数  | wc：Word Count  -l 统计行数  |
| \|\| \| grep '^d' \| wc -l | 统计当前目录下文件夹总数 |                         |
|                            |              |                         |
|                            |              |                         |



> [linux下ls -l命令（即ll命令）查看文件的显示结果分析](https://blog.csdn.net/LEON1741/article/details/82386520)
>
> [linux中wc命令用法](https://www.cnblogs.com/newcaoguo/p/5896491.html)



### 5.ps -ef | grep nginx

解释：ps -ef的意思是以长格式显示所有进程；“|”是管道，意思是前面ps的输出做为后面的输入，即—grep命令所检索的文本源；grep tomcat是在所有进程里查找与字符nginx有关的进程，并显示出来。
<font face="微软雅黑" color="red" size="5">ps</font>命令：某个进程显示出来。ps 全称是 Process Status 。
<font face="微软雅黑" color="red" size="5">grep</font>命令是一种强大的文本搜索工具，它能使用正则表达式搜索文本，并把匹 配的行打印出来。grep全称是Global Regular Expression Print，表示全局正则表达式版本。

ps[选项]

| 选项   | 含义                   |
| ---- | -------------------- |
| -e   | 显示所有进程,环境变量          |
| -f   | 全格式                  |
| -h   | 不显示标题                |
| -l   | 长格式                  |
| -w   | 宽输出                  |
| -a   | 显示终端上地所有进程,包括其他用户地进程 |
| -r   | 只显示正在运行地进程           |
| -x   | 显示没有控制终端地进程          |

grep [选项]

| 选项   | 含义         | 备注   |
| ---- | ---------- | ---- |
| -v   | 反转查找       |      |
| -n   | 对提取的内容显示行号 |      |
| -w   | 精确匹配       |      |
| -i   | 忽略大小写      |      |
| ^    | 匹配开头行首     |      |
| -E   | 正则匹配       |      |



结果说明

![查询结果(网络配图)](https://github.com/lennywang/Img/raw/master/psparameterexplain.png)

5.1 ps

在Linux中查看所有正在运行的进程
https://www.cnblogs.com/zwgblog/p/5971455.html

5.2 grep

grep应用场景：通常对数据进行 行的提取
语法：grep [选项]...[内容]...[file]

```shell
-v 	#对内容进行取反提取
-n 	#对提取的内容显示行号
-w 	#精确匹配
-i 	#忽略大小写
^ 	#匹配开头行首
-E 	#正则匹配
```

grep高亮显示匹配项

设置步骤：

1. 编辑vi ~/.bashrc
2. 添加如下一行内容：export GREP_OPTIONS='--color=always' GREP_COLOR='1;33'
3. source ~/.bashrc //使配置生效

参数说明：

`export GREP_OPTIONS='--color=XXX'`

color有三个值供选择: never always auto ;

always和auto的区别: always会在任何情况下都给匹配字段加上颜色标记; auto 只给最后一个管道符匹配项加亮显示；

`export GREP_COLOR='a;b'` #默认是1;31，即高亮的红色; 您可以根据自己的喜好设置不同的颜色； 

a 可以选择：【0，1，4，5，7，8】

| 选项   | 含义     |
| ---- | ------ |
| 0    | 关闭所有属性 |
| 1    | 设置高亮度  |
| 4    | 下划线    |
| 5    | 闪烁     |
| 7    | 反显     |
| 8    | 消隐     |

b 可以选择：【30-37 或 40-47】

| 选项    | 含义     |
| ----- | ------ |
| 30    | black  |
| 31    | red    |
| 32    | green  |
| 33    | yellow |
| 34    | blue   |
| 35    | purple |
| 36    | cyan   |
| 37    | white  |
| 30-37 | 设置前景色  |
| 40-47 | 设置背景色  |

> 参考：[设置grep高亮显示匹配项](https://www.linuxidc.com/Linux/2014-09/106871.htm)

grep与egrep
https://blog.csdn.net/qq_41201816/article/details/80767308

5.centos 界面切换

| 命令                        | 作用                    | 备注   |
| ------------------------- | --------------------- | ---- |
| Ctr+Alt+Fn(n=1,2,3,4,5,6) | 图形界面到控制台              |      |
| Alt+F7                    | 控制台到图形界面              |      |
| Alt+Fn(n=1,2,3,4,5,6)     | Alt+Fn(n=1,2,3,4,5,6) |      |
| startx                    | 控制台到图形界面              |      |

### 6.centos 中搭建开发环境

6.1安装linux运行容器

> [VMware下载与安装](https://www.baidu.com/s?wd=VMware&tn=24004469_oem_dg&rsv_dl=gh_pl_sl_csd)

6.2 安装linux

>  [Linux环境搭建-在虚拟机中安装Centos7.0](https://www.cnblogs.com/lynn-li/p/6077944.html)

6.3 联网

linux设置静态ip
https://jingyan.baidu.com/album/39810a23baf9dab637fda64f.html?picindex=2

VMware下Linux配置局域网和外网访问
https://www.linuxidc.com/Linux/2017-11/148771.htm

vmware下设置host-only方式上网
https://jingyan.baidu.com/album/d8072ac497452aec95cefda5.html?picindex=1



| 命令                          | 作用   | 备注   |
| --------------------------- | ---- | ---- |
| systemctl start firewalld   | 启动   |      |
| systemctl stop firewalld    | 关闭   |      |
| systemctl status firewalld  | 查看状态 |      |
| systemctl disable firewalld | 开机禁用 |      |
| systemctl enable firewalld  | 开机启用 |      |

CentOS7使用firewalld打开关闭防火墙与端口
https://www.cnblogs.com/moxiaoan/p/5683743.html



VMware下Linux配置局域网和外网访问
https://www.linuxidc.com/Linux/2017-11/148771.htm



systemctl restart network

linux系统下怎么连接网络
https://zhidao.baidu.com/question/498565331.html

LINUX下网卡激活失败时解决方法（已实践）
https://blog.csdn.net/grace_yoyo/article/details/46501685

6.4 安装JDK

Linux安装JDK完整步骤
https://www.cnblogs.com/Dylansuns/p/6974272.html

6.5 安装Tomcat

[Linux下安装Tomcat服务器和部署Web应用](https://www.cnblogs.com/xdp-gacl/p/4097608.html)

6.6 安装Nginx

[CentOS 7 下安装Nginx](https://www.cnblogs.com/zhoading/p/8514050.html)

6.7 安装XShell

利用Xshell5从本机上向Linux（虚拟机中）上传文件
https://www.cnblogs.com/xdjun/p/7115303.html

6.8 问题

解决VMware主窗口中的虚拟机窗口太小的方法
https://blog.csdn.net/u014337397/article/details/80753056

Centos7更改默认启动桌面（或命令行）模式
https://www.cnblogs.com/justuntil/p/7851604.html

Linux 系统下用户之间的切换
https://blog.csdn.net/u013118258/article/details/79300450

name is not in the sudoers file. This incident will be reported. 不在sudoers文件中,此事将被报告.
https://blog.csdn.net/liguangxianbin/article/details/80818231

CentOS7设置终端快捷键一键打开终端
https://jingyan.baidu.com/article/f7ff0bfc1e2a322e26bb13d5.html

### 7.rpm -qa | grep java

RPM：(RedHat Package Manger RedHat 软件管理工具)：是一种用于打包及安装工具
qa：q代表query，a代表all
grep(global search rgular expression(RE) and print out the line):是一种强大的文本搜索工具

### 8.find  /etc -name  *init 

模糊搜索，etc目录以 init 结尾的文件或目录名

find . -name "mail*" 				在当前目录下查找mail开头文件

>  参考：[Linux常用命令之文件搜索命令](https://www.cnblogs.com/ysocean/p/7712417.html)

### 9.常用目录

| 目录地址                           | 目录说明   | 备注   |
| ------------------------------ | ------ | ---- |
| /etc/sysconfig/network-scripts | 网卡配置目录 |      |
| /usr/local                     | 软件安装目录 |      |

### 10.crontab

查看crontab服务状态：service crond status
手动启动crontab服务：service crond start
基础命令：
-e 表示编辑当前的crontab
-l  表示列表显示当前的crontab任务
-r  表示删除当前用户的crontab
-i  表示删除crontab时给予提示信息
使用：crontab -l  * * * * * /usr/local/davecron.sh
参考：https://blog.csdn.net/qq_37050329/article/details/89093960

### 11.Linux统计文件夹中文件个数以及目录个数

https://blog.csdn.net/sganchang/article/details/91432435
ll | wc -l 
wc [-lwm] 参数:-l 仅列出行数;

### 12.lsof -i:port作用

lsof -i :22 知道22端口被哪个进程占用
netstat -lnp|grep 7000 查看7000端口被哪个进程占用
lsof -p 10075 查看指定进程ID已打开的内容

> [Linux 命令神器：lsof](https://www.jianshu.com/p/a3aa6b01b2e1)

### 13. sudo su -

sudo su -：切换到root登录，使用用户密码。

[su;su -;sudo;sudo -i;sudo su;sudo su - 之间的区别](https://www.cnblogs.com/GaoYuan_cnblogs/p/9986036.html)

| 操作        | 命令     | 描述   |
| --------- | ------ | ---- |
| 查看当前登录用户名 | whoami |      |





### 14、防火墙

| 命令                                 | 含义      | 备注   |
| ---------------------------------- | ------- | ---- |
| systemctl restart iptables.service | 重启防火墙   |      |
| systemctl start iptables.service   | 开启防火墙   |      |
| systemctl stop iptables.service    | 关闭防火墙   |      |
| systemctl status iptables.service  | 查看防火墙状态 |      |



### 15、内存占用

| 命令                | 含义     | 备注   |
| ----------------- | ------ | ---- |
| top               | 系统整体负载 |      |
| free              | 查看内存占用 |      |
| cat /proc/meminfo |        |      |

> [Linux查看系统资源占用](https://www.cnblogs.com/jiangshiguo/p/9160454.html)

### 16、sed

sed的应用场景：主要对数据进行处理（选取，新增，替换，删除，搜索）

sed语法：sed [选项][动作] 文件名

| 选项                | 含义                           | 例子                                       |
| ----------------- | ---------------------------- | ---------------------------------------- |
| -n                | 把匹配到的行输出打印到屏幕                |                                          |
| p                 | 以行为单位进行查询，通常与-n一起使用          | eg：df -h \| sed -n '2p'                  |
| d                 | 删除                           |                                          |
| a                 | 在行的下面插入新的内容                  | sed '2a 1234567890' df.txt               |
| i                 | 在行的上面插入新的内容                  | sed '2i 1234567890' df.txt               |
| c                 | 替换                           | sed '2c 1234567890' df.txt               |
| s/要被取代的内容/新的字符串/g | 指定内容进行替换                     | sed 's/0%/100%/g' df.txt                 |
| -e                | 表示可以执行多条动作                   | cat -n df.txt  \| sed -n -e 's/100%/100%-----100%/g' -e '/100%-----100%/p' |
| -i                | 对源文件进行修改(高危操作，慎用，用之前需要备份源文件) |                                          |





### 15. 其他

chmod 775 文件名

bash 命令

！/bin/bash    
/etc/sysconfig/network-scripts
/usr/lib/jvm
vim /etc/profile
source /etc/profile

Linux下查找进程id并强制停止进程的脚本
https://www.cnblogs.com/zeng1994/p/13a2c5a28e55dd3abc2c75a4fb80371a.html

指定日期显示格式

临时更改显示格式

```
export TIME_STYLE='+%Y-%m-%d %H:%M:%S' 
```

永久改变日期显示格式

```
vi /etc/profile
export TIME_STYLE='+%Y-%m-%d %H:%M:%S'
```

LINUX 设置LL的时候显示日期的格式
https://www.jianshu.com/p/ba927b40a3fd

lsof

```
显示特定端口并查找连接/进程
lsof -i:port_number
```

> [linux怎样使用lsof查看被占用的文件](https://jingyan.baidu.com/album/6b182309fdd969ba59e1597e.html?picindex=2)

netstat

```
列出所有监听和非监听状态的连接
netstat -a|grep 6379
```

> [netstat](https://www.cnblogs.com/kcxg/p/11242567.html)

## Shell

Shell：定义和使用变量
https://www.cnblogs.com/xuejianbest/p/10285180.html

Shell获取格式化日期
https://www.cnblogs.com/zhzhang/p/7646443.html

Shell中判断文件,目录是否存在
https://www.cnblogs.com/DreamDrive/p/7706585.html

shell脚本中判断上一个命令是否执行成功
https://blog.csdn.net/laobai1015/article/details/94010186