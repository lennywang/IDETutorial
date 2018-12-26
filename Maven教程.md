## 常用Maven命令

### 1. 编译源代码

```java
mvn compile
```

### 2.打包

```
mvn package
```

### 3.清除产生的项目 

```
mvn clean
```



> 参考：[Maven常用命令]((https://www.cnblogs.com/wkrbky/p/6352188.html))

## 实践

### 1.maven打包加时间戳

```xml
<properties>
	<maven.build.timestamp.format>yyyyMMddHHmmss</maven.build.timestamp.format>
</properties>
<build>
    <finalName>
      	${project.artifactId}-${project.version}_${maven.build.timestamp}
    </finalName>
</build>	
```

> 参考：[maven打包加时间戳](https://blog.csdn.net/z410970953/article/details/50680603)

### 2.maven打包时跳过测试

```shell
mvn clean package -Dmaven.test.skip=true
```

### 3.查看本地maven仓库地址

```shell
mvn help:effective-settings
```

默认地址为 ${user.home}/ .m2 /repository

### 4.修改Maven镜像源

1、maven安装目录下conf文件夹settings.xml
2、把镜像源改为阿里云的

```xml
<mirror>  
  <id>alimaven</id>  
  <mirrorOf>central</mirrorOf>    
  <name>aliyun maven</name>  
  <url>http://maven.aliyun.com/nexus/content/groups/public/</url>        
</mirror>
```

### 5.[Maven安装与配置](https://www.cnblogs.com/eagle6688/p/7838224.html)

