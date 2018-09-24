



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

| 命令                 | 作用 | 备注 |
| -------------------- | ---- | ---- |
| yum install -y lrzsz | 安装 |      |
| rz                   | 上传 |      |
| sz 文件名            | 下载 |      |

4、重启服务

```shell
ps -aux | grep java | grep mail
kill 命令用于杀死进程
nohup command &
```

说明：1. ps命令是Process Status

2. nohup: no hang up
3. nohup command & 使用nohup命令提交作业
   如果使用nohup命令提交作业，那么在缺省情况下该作业的所有输出都被重定向到一个名为nohup.out的文件中

### 2. Linux 系统重启、关机命令

**重启**

| 命令              | 作用                                | 备注 |
| ----------------- | ----------------------------------- | ---- |
| reboot            | 普通重启                            |      |
| shutdown -r now   | 立刻重启(root用户使用)              |      |
| shutdown -r 10    | 过10分钟自动重启(root用户使用)      |      |
| shutdown -r 20:35 | 在时间为20:35时候重启(root用户使用) |      |
| shutdown -c       | 取消重启                            |      |

**关机 **

| 命令            | 作用                   | 备注 |
| --------------- | ---------------------- | ---- |
| halt            | 立刻关机               |      |
| poweroff        | 立刻关机               |      |
| shutdown -h now | 立刻关机(root用户使用) |      |
| shutdown -h 10  | 10分钟后自动关机       |      |

### 3. Vim 编辑器

**插入**

 i

**退出**

| 命令                                              | 作用       | 备注 |
| ------------------------------------------------- | ---------- | ---- |
| 1. ESC \| : \| WQ(x) 回车<br />2. ESC \| Shift+zz | 保存退出   |      |
| ESC \| : \| q                                     | 正常退出   |      |
| ESC \| : \| q!                                    | 不保存退出 |      |
| ESC \| : \| !                                     | 强制退出   |      |









