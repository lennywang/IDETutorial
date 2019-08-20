# logback教程

## logback简介

**slf4j**：全拼为Simple Logging Facade for Java，即“为java提供的简单日志门面”，slf4j并不是一个具体的日志解决方案，实际上，它提供的核心api只是一个名为Logger的接口（里面封装了你可能需要的各种日志方法）和一个名为LoggerFactory工厂类。
**logback**： logback是log4j创始人设计的另一个开源日志组件。logback被设计成了原生支持slf4j，也就是说调用slf4j接口时，似乎会自动调用logback，而不需要你做任何配置。
logback当前分成三个模块：logback-core,logback-classic和logback-access。logback-core是其它两个模块的基础模块。logback-classic是log4j的一个改良版本。

## logback使用

1、maven 配置

```xml
<dependencies>
  
    <dependency>
        <groupId>org.slf4j</groupId>
        <artifactId>slf4j-api</artifactId>
        <version>1.7.22</version>
    </dependency>
  
    <dependency>
        <groupId>ch.qos.logback</groupId>
        <artifactId>logback-classic</artifactId>
        <version>1.1.6</version>
    </dependency>
  
</dependencies>
```



2、logback.xml 配置

```xml
<configuration>
    <!-- 上下文变量设置,用来定义变量值,其中name的值是变量的名称，value的值时变量定义的值。
        通过<property>定义的值会被插入到logger上下文中。定义变量后，可以使“${}”来使用变量。 -->    
    <property name="encoding" value="UTF-8"/>
    <property name="access-pattern" value="%d{yyyy-MM-dd HH:mm:ss.SSS}|%msg%n"/>
    <property name="normal-pattern"
              value="%d{HH:mm:ss.SSS}[%thread] %highlight(%-5level) %cyan(%logger{15}) - %msg %c:%L%n"/>
    <property name="LOG_PATH" value="./logs"/>

    <!--控制台日志-->
    <appender name="console" class="ch.qos.logback.core.ConsoleAppender">
        <encoder>
            <pattern>${normal-pattern}</pattern>
            <charset>${encoding}</charset>
        </encoder>
    </appender>

    <!--访问日志文件-->
    <!-- <appender>是<configuration>的子节点，是负责写日志的组件。
        有两个必要属性name和class。
        name指定appender名称，
        class指定appender的实现类。 -->  
    <appender name="access-appender" class="ch.qos.logback.core.rolling.RollingFileAppender">
        <!-- 被写入的文件名，可以是相对目录，也可以是绝对目录，如果上级目录不存在会自动创建，没有默认值。 -->
        <file>${LOG_PATH}/km-access.log</file>
        <prudent>true</prudent>
        <Append>true</Append>
        <!-- 对日志进行格式化。 -->
        <encoder>
            <pattern>${access-pattern}</pattern>
            <charset>${encoding}</charset>
        </encoder>
        <!-- 当发生滚动时的行为  -->
        <rollingPolicy class="ch.qos.logback.core.rolling.TimeBasedRollingPolicy">
            <fileNamePattern>${LOG_PATH}/km-access.%d{yyyy-MM-dd}.log</fileNamePattern>
            <MaxHistory>90</MaxHistory>
        </rollingPolicy>
    </appender>


    <appender name="api" class="ch.qos.logback.core.rolling.RollingFileAppender">
        <File>${LOG_PATH}/api.log</File>
        <encoder>
            <pattern>${normal-pattern}</pattern>
        </encoder>
        <rollingPolicy class="ch.qos.logback.core.rolling.TimeBasedRollingPolicy">
            <fileNamePattern>${LOG_PATH}/api.log.%d{yyyy-MM-dd}</fileNamePattern>
        </rollingPolicy>
    </appender>
	<!-- 用来设置某一个 包 或者具体的某一个 类 的日志打印级别、以及指定<appender>
		name:用来指定受此logger约束的某一个包或者具体的某一个类。
        level:用来设置打印级别，大小写无关：TRACE, DEBUG, INFO, WARN, ERROR, ALL 和 OFF，还有一个特俗值INHERITED或者同义词NULL，代表强制执行上级的级别。如果未设置此属性，那么当前loger将会继承上级的级别。 
        additivity:是否向上级logger传递打印信息。默认是true。(这个logger的上级就是上面的root)
        <logger>可以包含零个或多个<appender-ref>元素，标识这个appender将会添加到这个logger。-->
    <logger name="xuyihao.logback.test" level="DEBUG" additivity="true">
        <appender-ref ref="access-appender"/>
    </logger>
  
	<!-- 特殊的<logger>元素，是根logger。只有一个level属性，应为已经被命名为"root".
         level:设置打印级别，大小写无关：TRACE, DEBUG, INFO, WARN, ERROR, ALL 和 OFF，不能设置为INHERITED或者同义词NULL。默认是DEBUG。
        <root>可以包含零个或多个<appender-ref>元素，标识这个appender将会添加到这个loger。 -->
    <root>
        <appender-ref ref="console"/>
        <appender-ref ref="file-default"/>
        <appender-ref ref="file-error"/>
    </root>
</configuration>
```



1、<pattern>%d{HH:mm:ss.SSS}[%thread] %highlight(%-5level) %cyan(%logger{15}) - %msg %c:%L%n</pattern> 

| 格式字符             | 含义                             |
| ---------------- | ------------------------------ |
| %d               | 时间日期格式                         |
| %thread          | 调用的线程                          |
| %-5level         | 日志界别                           |
| %logger          | 调用对象                           |
| %msg             | 日志信息                           |
| %n               | 换行                             |
| %highlight、%cyan | 高亮 ；语法：%highlight(sub-pattern) |

> 参考：[Chapter 6: Layouts](https://logback.qos.ch/manual/layouts.html#conversionWord)

2、打印方法与基本的选择规则

记录请求级别为 p，其 logger的有效级别为 q，只有则当 p>=q时，该请求才会被执行。该规则是 logback 的核心。

级别排序为： TRACE < DEBUG < INFO < WARN < ERROR

> 参考：[logback的使用和logback.xml详解](https://www.cnblogs.com/warking/p/5710303.html)

3、创建logger对象

```java
private Logger logger = LoggerFactory.getLogger(MethodHandles.lookup().lookupClass());
```

