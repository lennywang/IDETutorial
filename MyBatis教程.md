# MyBatis教程

## **1.MyBatis架构**

![MyBatis架构](https://github.com/lennywang/Img/raw/master/mybatis-structure.gif)

1. mybatis配置SqlMapConfig.xml，此文件作为mybatis的全局配置文件，配置了mybatis的运行环境等信息。mapper.xml文件即sql映射文件，文件中配置了操作数据库的sql语句。此文件需要在SqlMapConfig.xml中加载。
2. 通过mybatis环境等配置信息构造SqlSessionFactory即会话工厂
3. 由会话工厂创建sqlSession即会话，操作数据库需要通过sqlSession进行。
4. mybatis底层自定义了Executor执行器接口操作数据库，Executor接口有两个实现，一个是基本执行器、一个是缓存执行器。
5. MappedStatement也是mybatis一个底层封装对象，它包装了mybatis配置信息及sql映射信息等。mapper.xml文件中一个sql对应一个Mapped Statement对象，sql的id即是Mapped statement的id。
6. MappedStatement对sql执行输入参数进行定义，包括HashMap、基本类型、pojo，Executor通过Mapped Statement在执行sql前将输入的java对象映射至sql中，输入参数映射就是jdbc编程中对preparedStatement设置参数。
7. Mapped Statement对sql执行输出结果进行定义，包括HashMap、基本类型、pojo，Executor通过Mapped Statement在执行sql后将输出结果映射至java对象中，输出结果映射过程相当于jdbc编程中对结果的解析处理过程。

## 2.SqlMapConfig.xml配置文件

2.1 配置内容

SqlMapConfig.xml中配置的内容和顺序如下：

| 序号 | 属性               | 配置内容         |
| ---- | ------------------ | ---------------- |
| 1    | properties         | 属性             |
| 2    | settings           | 全局配置参数     |
| 3    | typeAliases        | 类型别名         |
| 4    | typeHandlers       | 类型处理器       |
| 5    | objectFactory      | 对象工厂         |
| 6    | plugins            | 插件             |
| 7    | environments       | 环境集合属性对象 |
| 8    | environment        | 环境子属性对象   |
| 9    | transactionManager | 事务管理         |
| 10   | dataSource         | 数据源           |
| 11   | mappers            | 映射器           |

2.2 typeAliases

```xml
	<typeAliases>
		<!-- 单个别名定义 -->
		<typeAlias alias="user" type="cn.itcast.mybatis.pojo.User" />
		<!-- 批量别名定义，扫描整个包下的类，别名为类名（大小写不敏感） -->
		<package name="cn.itcast.mybatis.pojo" />
		<package name="其它包" />
	</typeAliases>mappers（映射器）
```

2.3 Mapper配置的几种方法：

2.3.1. <mapper resource=" " />

使用相对于类路径的资源（现在的使用方式）

如：<mapper resource="sqlmap/User.xml" />



 2.3.2. <mapper class=" " />

使用mapper接口类路径

如：<mapper class="cn.itcast.mybatis.mapper.UserMapper"/>

 注意：此种方法要求mapper接口名称和mapper映射文件名称相同，且放在同一个目录中。

 

2.3.3<package name=""/>

注册指定包下的所有mapper接口

如：<package name="cn.itcast.mybatis.mapper"/>

注意：此种方法要求mapper接口名称和mapper映射文件名称相同，且放在同一个目录中。

## **3.输入映射和输出映射**

```xml
<mapper namespace="com.mybatis.mapper.UserMapper">
    <select id="queryUserById" parameterType="int" resultType="com.mybatis.pojo.User">
        SELECT * FROM `user` where id =#{id};
    </select>
</mapper>
```

## 4.Mapper动态代理方式   

**开发规范**

​        Mapper接口开发方法只需要程序员编写Mapper接口（相当于Dao接口），由Mybatis框架根据接口定义创建接口的动态代理对象，代理对象的方法体同上边Dao接口实现类方法。

 Mapper接口开发需要遵循以下规范：

1、  Mapper.xml文件中的namespace与mapper接口的类路径相同。

2、  Mapper接口方法名和Mapper.xml中定义的每个statement的id相同 

3、  Mapper接口方法的输入参数类型和mapper.xml中定义的每个sql 的parameterType的类型相同

4、  Mapper接口方法的输出参数类型和mapper.xml中定义的每个sql的resultType的类型相同

## 5. Mybatis解决jdbc编程的问题

1、数据库连接创建、释放频繁造成系统资源浪费从而影响系统性能，如果使用数据库连接池可解决此问题。

解决：在SqlMapConfig.xml中配置数据连接池，使用连接池管理数据库链接。

2、Sql语句写在代码中造成代码不易维护，实际应用sql变化的可能较大，sql变动需要改变java代码。

解决：将Sql语句配置在XXXXmapper.xml文件中与java代码分离。

3、向sql语句传参数麻烦，因为sql语句的where条件不一定，可能多也可能少，占位符需要和参数一一对应。

解决：Mybatis自动将java对象映射至sql语句，通过statement中的parameterType定义输入参数的类型。

4、对结果集解析麻烦，sql变化导致解析代码变化，且解析前需要遍历，如果能将数据库记录封装成pojo对象解析比较方便。

解决：Mybatis自动将sql执行结果映射至java对象，通过statement中的resultType定义输出结果的类型。

## 6. mybatis与hibernate不同

Mybatis和hibernate不同，它不完全是一个ORM框架，因为MyBatis需要程序员自己编写Sql语句。mybatis可以通过XML或注解方式灵活配置要运行的sql语句，并将java对象和sql语句映射生成最终执行的sql，最后将sql执行的结果再映射生成java对象。

Mybatis学习门槛低，简单易学，程序员直接编写原生态sql，可严格控制sql执行性能，灵活度高，非常适合对关系数据模型要求不高的软件开发，例如互联网软件、企业运营类软件等，因为这类软件需求变化频繁，一但需求变化要求成果输出迅速。但是灵活的前提是mybatis无法做到数据库无关性，如果需要实现支持多种数据库的软件则需要自定义多套sql映射文件，工作量大。

Hibernate对象/关系映射能力强，数据库无关性好，对于关系模型要求高的软件（例如需求固定的定制化软件）如果用hibernate开发可以节省很多代码，提高效率。但是Hibernate的学习门槛高，要精通门槛更高，而且怎么设计O/R映射，在性能和对象模型之间如何权衡，以及怎样用好Hibernate需要具有很强的经验和能力才行。

总之，按照用户的需求在有限的资源环境下只要能做出维护性、扩展性良好的软件架构都是好架构，所以框架只有适合才是最好。 

