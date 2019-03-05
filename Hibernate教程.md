# 教程

## 配置文件

**Hibernate主配置**

```xml

<hibernate-configuration>
    <!-- 会话工厂 -->
    <session-factory>
        <!--必选配置-->
        <!-- 数据库驱动 -->
        <property name="hibernate.connection.driver_class">com.mysql.jdbc.Driver</property>
        <!-- 数据库url -->
        <property name="hibernate.connection.url">jdbc:mysql://localhost:3306/test</property>
        <!-- 数据库连接用户名 -->
        <property name="hibernate.connection.username">root</property>
        <!-- 数据库连接密码 -->
        <property name="hibernate.connection.password"></property>
        <!-- 数据库方言，根据数据库选择 -->
        <property name="hibernate.dialect">org.hibernate.dialect.MySQL5Dialect</property>

        <!--可选配置-->
        <!--为了方便调试是否在运行hibernate时在日志中输出sql语句 -->
        <property name="hibernate.show_sql">true</property>
        <!-- 是否对日志中输出的sql语句进行格式化 -->
        <property name="hibernate.format_sql">true</property>
        <!-- hibernate.hbm2ddl.auto update(推荐使用) 自动生成表.如果已经存在不会再生成.如果表有变动.自动更新表(不会删除任何数据).-->
        <property name="hibernate.hbm2ddl.auto">create</property>

        <!-- 加载映射文件 -->
        <mapping resource="ScoreEntity.hbm.xml"/>
    </session-factory>
</hibernate-configuration>

```

hibernate.hbm2ddl.auto可选值

| 可选值      | 说明                                                         |
| ----------- | ------------------------------------------------------------ |
| create      | 启动时删数据库中的表，然后创建，退出时不删除数据表           |
| create-drop | 启动时删数据库中的表，然后创建，退出时删除数据表 如果表不存在报错 |
| update      | 如果启动时表格式不一致则更新表，原有数据保留                 |
| validate    | 项目启动表结构进行校验 如果不一致则报错                      |



**ORM元数据**

```xml-dtd
<?xml version='1.0' encoding='utf-8'?>
<!DOCTYPE hibernate-mapping PUBLIC
    "-//Hibernate/Hibernate Mapping DTD 3.0//EN"
    "http://www.hibernate.org/dtd/hibernate-mapping-3.0.dtd">
<hibernate-mapping>

    <class name="ssh.entity.ScoreEntity" table="score" schema="test">
        <id name="id" column="ID"/>
        <property name="name" column="NAME"/>
        <property name="math" column="MATH"/>
        <property name="chinese" column="CHINESE"/>
        <property name="english" column="ENGLISH"/>
        <property name="pahliy" column="PAHLIY"/>
        <property name="champily" column="CHAMPILY"/>
    </class>
</hibernate-mapping>
```

> 参考：[ ORM元数据（配置详解）]( https://blog.csdn.net/Aaron357/article/details/79488223)



## API

**Configuration**



**SessionFactory**



**Session**



**Transaction**



**查询**

**Query**



**Criteria**



**SQLQuery**



# 实战