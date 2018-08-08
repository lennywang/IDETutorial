### git 基础

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







### git 常见问题

一、git提交异常 fatal: LF would be replaced by..

```
找到 .git文件夹，修改config文件。在[core]配置项添加

autocrlf = false   

safecrlf = false

```

附：CR(Carriage Return) 回车  LF(Line Feed) 换行









