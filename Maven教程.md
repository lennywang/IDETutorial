## 常用Maven命令

| 命令          | 作用                  | 备注                                  |
| ----------- | ------------------- | ----------------------------------- |
| mvn compile | 编译源代码               |                                     |
| mvn package | 打包                  |                                     |
| mvn clean   | 清除产生的项目             |                                     |
| mvn compile | 编译源代码               |                                     |
| mvn install | 在本地Repository中安装jar | 包含mvn compile，mvn package，然后上传到本地仓库 |
| mvn deploy  | 上传到私服               | 包含mvn install,然后，上传到私服              |

> 参考：[Maven常用命令](https://www.cnblogs.com/wkrbky/p/6352188.html)

## 常用Maven标签

### 1、build

```xml
<build>
    <finalName>com_dubbo_config</finalName>

    <resources>
        <resource>
            <!-- 指定resources插件处理哪个目录下的资源文件 -->
            <directory>src/main/resources</directory>
            <!-- 打包后放在什么位置 -->
            <targetPath>${project.build.directory}/classes</targetPath>
            <!-- 不包含directory指定目录下的以下文件 -->
            <excludes>
                <exclude>pro/*</exclude>
                <exclude>dev/*</exclude>
                <exclude>test/*</exclude>
            </excludes>
            <!-- 只（这个字很重要）包含directory指定目录下的以下文件 
                 <include>和<exclude>都存在的话，那就发生冲突了，这时会以<exclude>为准 -->
            <includes>
                <include></include>
            </includes>
            <!-- filtering为true的时候，这时只会把过滤的文件（<excludes>）打到classpath下，
                 filtering为false的时候，会把不需要过滤的文件（<includes>）打到classpath下 -->
            <filtering>true</filtering>
        </resource>

        <resource>
            <directory>src/main/resources/${profiles.active}</directory>
            <targetPath>${project.build.directory}/classes</targetPath>
        </resource>
    </resources>
  </build>
```

> 参考：[Maven中标签详解](<https://blog.csdn.net/newbie_907486852/article/details/81205532>)

### 2、profiles

```xml
<profiles>
    <profile>
        <!-- 声明这个profile的id身份 -->
        <id>dev</id>
        <!-- 默认激活：比如当知心mvn package命令是，没有传入参数，默认使用这个
                                    当使用mvn package -P dev 传入参数时，表示使用这个id的profile -->
        <activation>
            <activeByDefault>true</activeByDefault>
        </activation>
        <!-- 该标签下配置对应的key  value -->
        <properties>
            <!-- 这里的标签名任意，在 项目的 properties、xml等配置文件中可以使用${profiles.active}取出dev这个值-->
            <profiles.active>dev</profiles.active>
        </properties>
    </profile>
    <profile>
        <id>test</id>
        <properties>
            <profiles.active>test</profiles.active>
        </properties>
    </profile>
    <profile>
        <id>pro</id>
        <properties>
            <profiles.active>pro</profiles.active>
        </properties>
    </profile>
  </profiles>
```

> 参考：[Maven中标签详解](<https://blog.csdn.net/newbie_907486852/article/details/81205532>)

### 3、build

```xml
<build>
      <resources>
        <resource>
          <directory>src/main/java</directory>
          <includes>
            <include>**/*.xml</include>
          </includes>
          <filtering>false</filtering>
        </resource>
      </resources>
</build>
```



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

1、修改Maven镜像源
1）、maven安装目录下conf文件夹settings.xml
2）、把镜像源改为阿里云的

```xml
<mirror>  
  <id>alimaven</id>  
  <mirrorOf>central</mirrorOf>    
  <name>aliyun maven</name>  
  <url>http://maven.aliyun.com/nexus/content/groups/public/</url>        
</mirror>
```

2、修改当前项目的maven仓库地址

```xml
    <repositories>
            <repository>
                <id>nexus-aliyun</id>
                <name>Nexus aliyun</name>
                <layout>default</layout>
                <url>http://maven.aliyun.com/nexus/content/groups/public</url>
                <snapshots>
                    <enabled>false</enabled>
                </snapshots>
                <releases>
                    <enabled>true</enabled>
                </releases>
            </repository>
    </repositories>
```



### 5.[Maven安装与配置](https://www.cnblogs.com/eagle6688/p/7838224.html)

### 6.查看Maven安装路径

右键 →计算机属性 →高级系统设置 →高级 →环境变量

![Maven安装路](https://github.com/lennywang/Img/raw/master/maven-install-location.png)

### 7.Idea配置Maven

> 参考：[IntellIJ IDEA 配置 Maven 以及 修改 默认 Repository](https://www.cnblogs.com/phpdragon/p/7216626.html)

### 8.IDEA 设置 MAVEN 默认仓库

> 参考：https://blog.csdn.net/qq_36483951/article/details/105669474

