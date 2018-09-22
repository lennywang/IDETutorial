



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

