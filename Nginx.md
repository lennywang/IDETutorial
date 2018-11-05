## Nginx 安装

**操作教程**

> 参考：[CentOS 7 下安装Nginx](https://www.cnblogs.com/zhoading/p/8514050.html)

**启动、停止nginx**

```shell
#启动
/usr/local/nginx/sbin/nginx -c /usr/local/nginx/conf/nginx.conf
#停止
./nginx -s stop #此方式停止步骤是待nginx进程处理任务完毕进行停止。
./nginx -s quit #此方式相当于先查出nginx进程id再使用kill命令强制杀掉进程。
#重启
./nginx -s reload
#查询nginx进程
ps -ef | grep nginx
```



##Nginx 配置文件

运行用户

user		nobody;

\# 全局错误日志
error_log		logs/error.log;
error_log		logs/error.log		notice;
error_log		logs/error.log		info;

\# 启动进程,通常设置成和cpu的数量相等
worker_processes		1;

\# PID文件
pid		logs/nginx.pid;

\# 连接数上限
events {
​	\# 单个后台worker process进程的最大并发链接数	
​	worker_connections 	1024;
}

\# 开启gzip压缩
gzip  on;

\# 虚拟主机配置

```
server{
	#监听端口
    listen 80;
    
    #域名可以有多个，用空格隔开
    server_name www.ha97.com ha97.com;
    
	#定义服务器的默认网站根目录位置
    root /data/www/ha97;
    
	#默认请求
    location / {
          root   /root;      			#定义服务器的默认网站根目录位置
          index index.html index.htm;    #定义首页索引文件的名称
    }
    
    #图片缓存时间设置
    location ~ .*\.(gif|jpg|jpeg|png|bmp|swf)$
    {
        expires 10d;
    }
    
    #JS和CSS缓存时间设置
    location ~ .*\.(js|css)?$
    {
        expires 1h;
    }
    
    #日志格式设定
    log_format access '$remote_addr - $remote_user [$time_local] "$request" '
    '$status $body_bytes_sent "$http_referer" '
    '"$http_user_agent" $http_x_forwarded_for';
    
    #定义本虚拟主机的访问日志
    access_log /var/log/nginx/ha97access.log access;
}
```



> 参考：[Nginx配置文件详细说明](https://www.cnblogs.com/Joans/p/4386556.html)

> 参考：[Nginx 配置文件nginx.conf 中文详解](http://www.ha97.com/5194.html)

## Nginx 虚拟主机配置

虚拟主机配置步骤：

1.配置IP地址

2.绑定IP地址与虚拟主机

**配置IP地址**

1、查看本机IP

```shell
ifconfig
```

1、配置主设备IP

```shell
ifconfig ens33 192.168.1.9 netmask 255.255.255.0
```

2、配置分设备1的IP地址

```shell
ifconfig ens33:1 192.168.1.7 broadcast 192.168.1.255 netmask 255.255.255.0
```

3、配置分设备2的IP地址

```shell
ifconfig ens33:2 192.168.1.17 broadcast 192.168.1.255 netmask 255.255.255.0
```

**绑定IP地址与虚拟主机**

1、在/usr/local/nginx/conf目录下创建xnzj.conf

```
touch xnzj.conf
```

2、绑定IP地址与虚拟主机

```shell
user nobody;
worker_processes 4;
events{
    worker_connections 1024;
}
http{
    server{
        listen 192.168.1.7:80;
        server_name 192.168.1.7;
        access_log logs/server1.access.log combined;
        location /{
            index index.html index.htm;
            root  html/server1;
        }
    }
    
    server{
        listen 192.168.1.7:80;
        server_name 192.168.1.17;
        access_log logs/server2.access.log combined;
        location /{
            index index.html index.htm;
            root  html/server2;
        }
    }
}
```

**使用xnzj.conf启动nginx**

```shell
/usr/local/nginx/sbin/nginx -c /usr/local/nginx/conf/xnzj.conf
```

**访问测试**

```shell
curl 192.168.1.7
server1
curl 192.168.1.17
server2
cat /usr/local/nginx/html/server1/index.html
server1
cat /usr/local/nginx/html/server2/index.html
server2
```

## Nginx 日志文件配置

**格式配置**

log_format  #用来定义记录日志的格式（可以定义多种日志格式，取不同名字即可）

log_format的默认值：

```shell
log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                  '$status $body_bytes_sent "$http_referer" '
				 '"$http_user_agent" "$http_x_forwarded_for"';
```

log_format语法格式及参数语法说明如下:

 ```shell
log_format   <NAME>  <string>;
关键字        格式标签 日志格式

关键字：其中关键字error_log不能改变
格式标签：格式标签是给一套日志格式设置一个独特的名字
日志格式：给日志设置格式

log_format格式变量：
    $remote_addr  #记录访问网站的客户端地址
    $remote_user  #远程客户端用户名
    $time_local  #记录访问时间与时区
    $request  #用户的http请求起始行信息
    $status  #http状态码，记录请求返回的状态码，例如：200、301、404等
    $body_bytes_sent  #服务器发送给客户端的响应body字节数
    $http_referer  #记录此次请求是从哪个连接访问过来的，可以根据该参数进行防盗链设置。
    $http_user_agent  #记录客户端访问信息，例如：浏览器、手机客户端等
    $http_x_forwarded_for  #当前端有代理服务器时，设置web节点记录客户端地址的配置，此参数生效的前提是代理服务器也要进行相关的x_forwarded_for设置
 ```

**存储路径配置**

access_log  #用来指定日至文件的路径及使用的何种日志格式记录日志

access_log的默认值：

```
access_log  logs/access.log  main;
```

access_log语法格式及参数语法说明如下:

```shell
access_log    <FILE>    <NAME>;
关键字         日志文件   格式标签

关键字：其中关键字error_log不能改变
日志文件：可以指定任意存放日志的目录
格式标签：给日志文件套用指定的日志格式

其他语法：
    access_log    off;  	#关闭access_log，即不记录访问日志
```

> 参考：[Nginx访问日志（access_log）配置及信息详解](https://www.cnblogs.com/czlun/articles/7010591.html)



**切割**

手动切割

```

```

自动切割

```

```



##实践

### 1.安装Nginx

**操作教程**

> 参考：[CentOS 7 下安装Nginx](https://www.cnblogs.com/zhoading/p/8514050.html)

**查找文件**

find / -name *文件名*

**移动文件**

mv 文件名 另一个目录

**查看虚拟机里的Centos7的IP**

 ip addr

> 参考：[查看虚拟机里的Centos7的IP](https://blog.csdn.net/dancheren/article/details/73611878)

**centos 如何查看操作系统版本**

cat /etc/redhat-release

**防火墙**

| 操作名         | 命令                                         | 说明                                           |
| -------------- | -------------------------------------------- | ---------------------------------------------- |
| 允许某端口放行 | firewall-cmd --permanent --add-port=3389/tcp | 命令：--permanent 永久添加端口，去除则表示临时 |
| 查看防火墙状态 | firewall-cmd --state                         |                                                |
| 重新加载       | firewall-cmd --reload                        |                                                |
| 关闭防火墙     | service iptables stop                        |                                                |

**问题**

**1.nginx公网IP无法访问浏览器**
https://blog.csdn.net/LJFPHP/article/details/78670459?utm_source=blogxgwz0

**2.command not found**
yum -y install wget