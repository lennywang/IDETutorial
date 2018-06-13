## Git 常见问题

一、git提交异常 fatal: LF would be replaced by..

找到 .git文件夹。修改config文件。在[core]配置项添加

autocrlf = false  

safecrlf = false



