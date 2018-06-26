<<<<<<< HEAD
## Git 常见问题

一、git提交异常 fatal: LF would be replaced by..

找到 .git文件夹。修改config文件。在[core]配置项添加

autocrlf = false  

safecrlf = false


=======
## 问题

github push 提交代码时停止在writing objects怎么办

```
git config --global http.postBuffer 524288000
参考链接：https://blog.csdn.net/smart_graphics/article/details/78475735
```
>>>>>>> 8779517e1c1244ba79fc4d93c0a37dde4db48c2a



## Git 命令

 git pull <远程库名> <远程分支名>:<本地分支名> 

取回远程库中的online分支，与本地的online分支进行merge

```
git pull origin online:online
```



