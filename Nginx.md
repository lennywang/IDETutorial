Nginx 配置文件

\# 运行用户
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

