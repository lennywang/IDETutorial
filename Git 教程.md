## 问题

github push 提交代码时停止在writing objects怎么办

```
git config --global http.postBuffer 524288000
参考链接：https://blog.csdn.net/smart_graphics/article/details/78475735
```



## Git 命令

 git pull <远程库名> <远程分支名>:<本地分支名> 

取回远程库中的online分支，与本地的online分支进行merge

```
git pull origin online:online
```



