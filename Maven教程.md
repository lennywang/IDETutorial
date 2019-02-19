## 常用Maven命令

| 命令        | 作用                      | 备注                                             |
| ----------- | ------------------------- | ------------------------------------------------ |
| mvn compile | 编译源代码                |                                                  |
| mvn package | 打包                      |                                                  |
| mvn clean   | 清除产生的项目            |                                                  |
| mvn compile | 编译源代码                |                                                  |
| mvn install | 在本地Repository中安装jar | 包含mvn compile，mvn package，然后上传到本地仓库 |
| mvn deploy  | 上传到私服                | 包含mvn install,然后，上传到私服                 |

> 参考：[Maven常用命令](https://www.cnblogs.com/wkrbky/p/6352188.html)

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

### 6.查看Maven安装路径

右键 →计算机属性 →高级系统设置 →高级 →环境变量

![Maven安装路](https://github.com/lennywang/Img/raw/master/maven-install-location.png)

### 7.Idea配置Maven

> 参考：[IntellIJ IDEA 配置 Maven 以及 修改 默认 Repository](https://www.cnblogs.com/phpdragon/p/7216626.html)

