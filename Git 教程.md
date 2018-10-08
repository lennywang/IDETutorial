## Git 基础

用命令git add告诉Git，把文件添加到仓库：
 $ git add 文件名（加入参数-A推送所以修改文件） 


命令git commit告诉Git，文件提交到仓库： 
$ git commit -m '添加readme.txt' 

推送至服务器
git push -u 仓库别名 分支（例：$ git push -u origin master）

git push --set-upstream origin feature_v4.0_wanglulu_1

Git比较两个分支间所有变更的文件列表
git diff branch1 branch2 --stat
加上 --stat 是显示文件列表, 否则是文件内容diff

Updates were rejected because the tip of your current branch is behind
https://blog.csdn.net/michael10001/article/details/51371715

git 提交到远程分支的诡异错误
https://segmentfault.com/q/1010000000257571

git获取远程服务器的指定分支
https://www.cnblogs.com/phpper/p/7136048.html

Git:代码冲突常见解决方法
https://blog.csdn.net/iefreer/article/details/7679631

Error when changing to master branch: my local changes would be overwritten by checkout
https://stackoverflow.com/questions/22424142/error-when-changing-to-master-branch-my-local-changes-would-be-overwritten-by-c

git diff 四种比较方式	
https://blog.csdn.net/catchertherye/article/details/49834705







## Git 命令

 git pull <远程库名> <远程分支名>:<本地分支名> 

取回远程库中的online分支，与本地的online分支进行merge

    git pull origin online:online



git log 命令显示从最近到最远的提交日志

    git log --pretty=oneline


## Git 实战

### **1. 拉取远程指定分支**

    git checkout -b feature_v4-0_zouzhili_1 origin/feature_v4-0_zouzhili_1 

解析：

1. git checkout -b 本地分支名 origin/远程分支名，在本地自动创建一个新分支，并与指定的远程分支关联起
   来。
2. git checkout --track origin/special    在本地创建一个special分支用于跟踪远端的special分支。

参考：git 拉取远程指定分支

### **2. 推送本地分支到远程仓库**

```
git branch –-set-upstream feature_v4-0_wll_1 origin/feature_v4-0_wanglulu_v_1
```

### **3. 提交并创建CR**

    git push origin feature_v4-0_wanglulu_v_1:refs/for/feature_v4-0_wanglulu_v_1

说明：此命令只适用于 Didi

### **4. 使用git push**

    1、git push -u origin master#如果当前分支和多个主机之间存在追踪关系，使用这个命令来设置默认的主机
    2、git push

### **5. git回滚到指定版本**

    git reset --hard 版本号                                       # git log -3 看3次提交

### 6.比较两个提交之间的差异

```shell
git diff commit1 commit2 
```

> 参考：[git diff 四种比较方式](https://blog.csdn.net/catchertherye/article/details/49834705)




## Git 常见问题

一、git提交异常 fatal: LF would be replaced by..

```
找到 .git文件夹，修改config文件。在[core]配置项添加

autocrlf = false   

safecrlf = false

```

附：CR(Carriage Return) 回车  LF(Line Feed) 换行
