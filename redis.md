集群搭建

[通过VMware搭建分布式集群基础环境](https://blog.csdn.net/cndmss/article/details/80149952)
[VMware安装Centos7超详细过程（图文）](https://blog.csdn.net/babyxue/article/details/80970526)

redis 远程连接方法

```
1、设置redis.conf
# bind 127.0.0.1
protected-mode   no
daemonize no
2、设置防火请
防火墙放行 6379 端口
重启防火墙
3、阿里云6379添加安全组
4、重启redis
5、远程连接
redis-cli.exe -h 112.126.63.69 -p 6379
```

> [redis 远程连接方法](https://www.cnblogs.com/ipyanthony/p/9290008.html)

redis 设置密码

```powershell
# 设置密码
127.0.0.1:6379>config set requirepass "redis6379"
127.0.0.1:6379>auth redis6379
# 清除密码
127.0.0.1:6379>config set requirepass ""
```

