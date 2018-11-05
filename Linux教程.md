### 1. 目录操作

#### 1.1 目录结构

![Linux目录结构](https://github.com/lennywang/Img/raw/master/linux.png)

* home:创建admin用户，就会在home目录下对应admin目录。创建vsftp用户，就会在home目录下对应vsftp目录


* usr：通常将软件安装在/usr/local目录下面。安装jdk   /usr/local/jdk/….（安装的jdk）

#### 1.2 目录切换

| 操作                 | 命令      | 说明                    |
| :------------------- | :-------- | ----------------------- |
| 打印当前目录         | pwd       | print working directory |
| 进入某个目录         | cd 目录名 |                         |
| 回到上一层目录       | cd ..     |                         |
| 切换到系统根目录     | cd /      |                         |
| 切换到用户主目录     | cd ~      |                         |
| 切换到上一个所在目录 | cd -      |                         |

####1.3 目录操作

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

#### 2.3 修改文件内容

#### 2.4 删除文件

#### 2.5 压缩文件 

### 3.其他命令

###4.权限命令



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
nohup command &
```

说明：1. ps命令是Process Status

1. nohup: no hang up
2. nohup command & 使用nohup命令提交作业
   如果使用nohup命令提交作业，那么在缺省情况下该作业的所有输出都被重定向到一个名为nohup.out的文件中

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

### 3. Vim 编辑器

**插入**

 i

**退出**

| 命令                                       | 作用    | 备注               |
| ---------------------------------------- | ----- | ---------------- |
| 1. ESC \| : \| WQ(x) 回车<br />2. ESC \| Shift+zz | 保存退出  | w:write   q:quit |
| ESC \| : \| q                            | 正常退出  |                  |
| ESC \| : \| q!                           | 不保存退出 |                  |
| ESC \| : \| !                            | 强制退出  |                  |

### 4.ps -ef | grep nginx

解释：ps -ef的意思是以长格式显示所有进程；“|”是管道，意思是前面ps的输出做为后面的输入，即—grep命令所检索的文本源；grep tomcat是在所有进程里查找与字符nginx有关的进程，并显示出来。
<font face="微软雅黑" color="red" size="5">ps</font>命令：某个进程显示出来。ps 全称是 Process Status 。
<font face="微软雅黑" color="red" size="5">grep</font>命令是一种强大的文本搜索工具，它能使用正则表达式搜索文本，并把匹 配的行打印出来。grep全称是Global Regular Expression Print，表示全局正则表达式版本。

ps[选项]

| 选项 | 含义                                    |
| ---- | --------------------------------------- |
| -e   | 显示所有进程,环境变量                   |
| -f   | 全格式                                  |
| -h   | 不显示标题                              |
| -l   | 长格式                                  |
| -w   | 宽输出                                  |
| -a   | 显示终端上地所有进程,包括其他用户地进程 |
| -r   | 只显示正在运行地进程                    |
| -x   | 显示没有控制终端地进程                  |

结果说明

![查询结果(网络配图)](https://github.com/lennywang/Img/raw/master/psparameterexplain.png)







