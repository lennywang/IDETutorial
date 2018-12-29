## Git 基础

**git add 文件名**
把文件添加到仓库：

**git commit -m 'commit log**
把文件提交到仓库

**git push -u 仓库别名 分支** （例：$ git push -u origin master）
推送至服务器

## Git 命令

 git pull <远程库名> <远程分支名>:<本地分支名> 

取回远程库中的online分支，与本地的online分支进行merge

    git pull origin online:online

> 参考：[git获取远程服务器的指定分支](https://www.cnblogs.com/phpper/p/7136048.html)

git log 命令显示从最近到最远的提交日志

    git log --pretty=oneline

git push --set-upstream origin feature_v4.0_wanglulu_1

Git比较两个分支间所有变更的文件列表
git diff branch1 branch2 --stat
加上 --stat 是显示文件列表, 否则是文件内容diff

Git删除暂存区或版本库中的文件
https://www.cnblogs.com/cposture/p/git.html

## Git常用

```
git init
git add README.md
git commit -m "first commit"
git remote add origin https://github.com/lennywang/JDBC.git
git push -u origin master
```

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

> [Git恢复之前版本的两种方法reset、revert](https://blog.csdn.net/yxlshk/article/details/79944535)

### 6.比较两个提交之间的差异

```shell
git diff commit1 commit2 
```

> 参考：[git diff 四种比较方式](https://blog.csdn.net/catchertherye/article/details/49834705)

### 7.git stash储藏

```powershell
git stash save "stash save log" # 储藏当前修改
git stash pop #重新应用储藏
```

> 参考：[git-stash用法小结](https://www.cnblogs.com/tocy/p/git-stash-reference.html)

### 8.git 解决冲突

1.编辑解决冲突
2.删掉冲突标识符

```powershell
<<<<<<< HEAD:file.txt # 冲突标识符
Hello world！
=======
Hello wolld！		# 冲突
>>>>>>> 77976da35a11db4580b80ae27e8d65caf5208086:file.txt
```



##Git 命令比较

### 1.git commit -am "commit log"

将文件提交到本地的分支并且推送到远程服务器，方式一：

```powershell
git add .		# 将本地修改过的文件且已经追踪的文件添加到本地的暂存区
git commit -m "commit log" # 将暂存区的代码提交到本地仓库
git push 		# 将本地仓库的代码推送到远程服务器端
```

方式二：

```powershell
git commit -am "commit log" # 相当于git add . 和 git commit -m "commit log"
git push
```

**<font size="4" color="red">git commit -am 'commit log' 命令只能提交已经追踪过且修改了的文件，新增文件必须使用第一步的命令（git add）</font>**

### 2.git pull

**`git fetch + git merge` ** 等价于  **`git pull`**

推荐使用 **`git fetch + git merge`**

### 3.git revert 与 git reset

git reset 是把HEAD向后移动了一下，而git revert是HEAD继续前进

> [Git恢复之前版本的两种方法reset、revert](https://blog.csdn.net/yxlshk/article/details/79944535)

### 4.git add -A和git add .

| 命令       | 作用                                                         | 备注                   |
| ---------- | ------------------------------------------------------------ | ---------------------- |
| git add -A | 提交所有变化                                                 | git add --all的缩写    |
| git add -u | 提交被修改(modified)和被删除(deleted)文件，不包括新文件(new) | git add --update的缩写 |
| git add .  | 提交新文件(new)和被修改(modified)文件，不包括被删除(deleted)文件 |                        |







##原理

###1.git  工作区、版本库

![git  工作区、版本库](https://github.com/lennywang/Img/raw/master/git-theory-repository.jpg)

往Git版本库里添加的时候，是分两步执行的：
第一步是用`git add`把文件添加进去，实际上就是把文件修改添加到暂存区；
第二步是用`git commit`提交更改，实际上就是把暂存区的所有内容提交到当前分支。

###2.git 常用操作图解

> [git原理图解](https://www.cnblogs.com/cb0327/p/5066685.html)



##Git 常见问题

一、git提交异常 fatal: LF would be replaced by..

```
找到 .git文件夹，修改config文件。在[core]配置项添加

autocrlf = false   

safecrlf = false

```

附：CR(Carriage Return) 回车  LF(Line Feed) 换行

二、Updates were rejected because the tip of your current branch is behind
https://blog.csdn.net/michael10001/article/details/51371715

三、git 提交到远程分支的诡异错误
https://segmentfault.com/q/1010000000257571

四、Git:代码冲突常见解决方法
https://blog.csdn.net/iefreer/article/details/7679631

五、Error when changing to master branch: my local changes would be overwritten by checkout
https://stackoverflow.com/questions/22424142/error-when-changing-to-master-branch-my-local-changes-would-be-overwritten-by-c