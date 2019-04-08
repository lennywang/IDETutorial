# 教程

## 配置文件

**Hibernate主配置**

```xml
<?xml version='1.0' encoding='utf-8'?>
<!DOCTYPE hibernate-configuration PUBLIC
        "-//Hibernate/Hibernate Configuration DTD 3.0//EN"
        "http://www.hibernate.org/dtd/hibernate-configuration-3.0.dtd">

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

**HibernateUtils**

```java
package cn.itheima.utils;

import org.hibernate.Session;
import org.hibernate.SessionFactory;
import org.hibernate.cfg.Configuration;

public class HibernateUtils {
	private static SessionFactory sf;
	
	static{
		//1 创建,调用空参构造
		Configuration conf = new Configuration().configure();
		//2 根据配置信息,创建 SessionFactory对象
		 sf = conf.buildSessionFactory();
	}
	
	//获得session => 获得全新session
	public static Session openSession(){
				//3 获得session
				Session session = sf.openSession();				
				return session;		
	}
    
	//获得session => 获得与线程绑定的session
	public static Session getCurrentSession(){
		//3 获得session
		Session session = sf.getCurrentSession();		
		return session;
	}
    
	public static void main(String[] args) {
		System.out.println(HibernateUtils.openSession());
	}	
}
```



**Configuration**



**SessionFactory**



**Session**



**Transaction**



**查询**

**Query**



**Criteria**



**SQLQuery**



# 实战

1、No identifier specified for entity: DmCatalogContentnd
https://www.cnblogs.com/kingsonfu/p/9869313.html



2、java.sql.BatchUpdateException

错误描述：nested exception is org.hibernate.exception.SQLGrammarException: Could not execute JDBC batch update 

解决办法：java.sql.BatchUpdateException问题处理
https://blog.csdn.net/wan23333/article/details/78652665

拓展：java.sql.BatchUpdateException: ORA-00932: inconsistent datatypes: expected NUMBER got BINARY
java.sql.BatchUpdateException: ORA-01779: cannot modify a column which maps
ORA-01779: cannot modify a column which maps to a non key-preserved table
https://blog.csdn.net/nanaranran/article/details/19820425/

# Spring

##1.1 spring概述

**什么是Spring**
Spring 是一个分层的 JavaSE/EEfull-stack(一站式) 轻量级 开源框架。
**为什么学习Spring**
方便解耦，简化开发
Spring 就是一个大工厂，可以将所有对象创建和依赖关系维护，交给 Spring 管理 
AOP 编程的支持 
Spring 提供面向切面编程，可以方便的实现对程序进行权限拦截、运行监控等功能 
声明式事务的支持 
只需要通过配置就可以完成对事务的管理，而无需手动编程 
方便程序的测试
Spring 对 Junit4 支持，可以通过注解方便的测试 Spring 程序 
方便集成各种优秀框架
Spring 不排斥各种优秀的开源框架，其内部提供了对各种优秀框架（如：Struts、Hibernate、 MyBatis、Quartz 等）的直接支持
降低 JavaEE API 的使用难度 
Spring 对 JavaEE 开发中非常难用的一些 API（JDBC、JavaMail、远程调用等），都提供了封装， 使这些 API 应用难度大大降低 

## 1.2 IOC 与 AOP

**IOC** Inversion of Control 控制反转. 指的是 对象的创建权反转(交给)给 Spring. 作用是实现了程序的解耦合. 
**DI** Dependency Injection 依赖注入.需要有IOC的环境,Spring创建这个类的过程中,Spring将类的依 赖的属性设置进去.

## 1.3 Spring 中的工厂

**ApplicatioContext 接口有两个实现类**
ClassPathXmlApplicationContext  :加载类路径下 Spring 的配置文件. 
FileSystemXmlApplicationContext  :加载本地磁盘下 Spring 的配置文件. 
**BeanFactory 和 ApplicationContext 的区别**
BeanFactory  :是在 getBean 的时候才会生成类的实例. 
ApplicationContext :在加载 applicationContext.xml(容器启动)时候就会创建. 

## 1.4  Spring 的相关配置

**id 属性和 name 属性标签的配置**

| 特征 | id                                                           | name               |
| ---- | ------------------------------------------------------------ | ------------------ |
| id   | 在约束中采用 ID 的约束:唯一                                  | 没有采用 ID 的约束 |
| 命名 | 以字母开始，可以使用字母、数字、连字符、 下划线、句话、冒号 ，不能出现特殊字符 | 允许出现特殊字符   |

**scope 属性：Bean 的作用范围**

| 值            | 描述                                                         |      |
| ------------- | ------------------------------------------------------------ | ---- |
| singleton     | 默认值，单例的                                               |      |
| prototype     | 多例的                                                       |      |
| request       | WEB 项目中,Spring 创建一个 Bean 的对象,将对象存入到 request 域中 |      |
| session       | WEB 项目中,Spring 创建一个 Bean 的对象,将对象存入到 session 域中 |      |
| globalSession | WEB 项目中,应用在 Porlet 环境.如果没有 Porlet 环境那么 globalSession 相当 于 session |      |

**Bean 的生命周期的配置**
通过配置<bean>标签上的 init-method 作为 Bean 的初始化的时候执行的方法，配置 destroy-method 作为 Bean 的销毁的时候执行的方法。 销毁方法想要执行，需要是单例创建的 Bean 而且在工厂关闭的时候，Bean 才会被销毁. 

**Spring 的 Bean 的管理 XML 的方式**

**Spring 生成 Bean 的时候三种方式**

1、无参数的构造方法的方式

```xml
<!-- 方式一：无参数的构造方法的实例化 --> 
bean id="bean1" class="cn.itcast.spring.demo3.Bean1"></bean> 
```

2、静态工厂实例化的方式

```xml
public class Bean2Factory { 
 	public static Bean2 getBean2(){   return new Bean2();  }   
}
<!-- 方式二：静态工厂实例化 Bean --> 
<bean id="bean2" class="cn.itcast.spring.demo3.Bean2Factory" factory-method="getBean2"/>
```

3、实例工厂实例化的方式

```xml
public class Bean3Factory {    
	public Bean3 getBean3(){   return new Bean3();  } 
}
<!-- 方式三：实例工厂实例化 Bean --> 
<bean id="bean3Factory" class="cn.itcast.spring.demo3.Bean3Factory"></bean> 
<bean id="bean3" factory-bean="bean3Factory" factory-method="getBean3"></bean> 
```

**Spring 的 Bean 的属性注入**
1、构造方法的方式注入属性

```xml
<!-- 第一种：构造方法的方式 -->  
<bean id="car" class="cn.itcast.spring.demo4.Car"> 
      <constructor-arg name="name" value=" 保时捷 "/>   
      <constructor-arg name="price" value="1000000"/>  
</bean>
```

2、set 方法的方式注入属性

```xml
<!-- 第二种：set 方法的方式 -->  
<bean id="car2" class="cn.itcast.spring.demo4.Car2"> 
      <property name="name" value=" 奇瑞 QQ"/>   
      <property name="price" value="40000"/>  
</bean>
```

**Spring 的属性注入：对象类型的注入**

```xml
<!-- 注入对象类型的属性 -->  
<bean id="person" class="cn.itcast.spring.demo4.Person"> 
      <property name="name" value=" 会希 "/>   
      <!-- ref 属性：引用另一个 bean 的 id 或 name -->   
      <property name="car2" ref="car2"/>
</bean> 
```

**名称空间 p 的属性注入的方式:Spring2.x 版本后提供的方式**

```xml
第一步:引入 p 名称空间 
<beans xmlns="http://www.springframework.org/schema/beans"     			  		xmlns:p="http://www.springframework.org/schema/p" 
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"     
xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd"> 	
 
第二步:使用 p 名称空间.     
* 普通属性:      p:属性名称=""    
* 对象类型属性: p:属性名称-ref=""
<!-- p 名称空间的属性注入的方式 -->  
<bean id="car2" class="cn.itcast.spring.demo4.Car2" p:name=" 宝马7" p:price="1200000"/> 
<bean id="person" class="cn.itcast.spring.demo4.Person" p:name=" 思聪" p:car2-ref="car2"/> 
```

**SpEL 的方式的属性注入:Spring3.x 版本后提供的方式**

```xml
SpEL：Spring Expression Language. 语法:#{ SpEL } 
 
 <!-- SpEL 的注入的方式 -->  
 <bean id="car2" class="cn.itcast.spring.demo4.Car2"> 
      <property name="name" value="#{' 奔驰 '}"/>   
      <property name="price" value="#{800000}"/>  
 </bean> 
 
 <bean id="person" class="cn.itcast.spring.demo4.Person"> 
     <property name="name" value="#{'冠希'}"/>      
     <property name="car2" value="#{car2}"/>     
 </bean> 
 
 <bean id="carInfo" class="cn.itcast.spring.demo4.CarInfo"></bean>   
  <!--引用了另一个类的属性-->  
  <bean id="car2" class="cn.itcast.spring.demo4.Car2"> 
      <property name="name" value="#{carInfo.carName}"/>   
      <property name="price" value="#{carInfo.calculatePrice()}"/> 
 </bean>
```



**注入复杂类型**

```xml
<!-- Spring 的复杂类型的注入===================== -->  
<bean id="collectionBean" class="cn.itcast.spring.demo5.CollectionBean"> 
  <!-- 数组类型的属性 -->   
  <property name="arrs">    
      <list> 
            <value>会希</value>     
            <value>冠希</value>     
            <value>天一</value>    
      </list> 
  </property>    
  <!-- 注入 List 集合的数据 -->   
  <property name="list">    
      <list> 
            <value>芙蓉</value>
            <value>如花</value>
            <value>凤姐</value>
      </list>   
  </property>   
  <!-- 注入 Map 集合 -->   
  <property name="map">    
      <map> 
            <entry key="aaa" value="111"/>
            <entry key="bbb" value="222"/>
            <entry key="ccc" value="333"/>
       </map>   
   </property>    
  <!-- Properties 的注入 -->   
  <property name="properties">    
      <props> 
            <prop key="username">root</prop>     
            <prop key="password">123</prop>    
      </props>   
  </property>  
</bean> 
```

**Spring 的分配置文件的开发**

```xml
一种:创建工厂的时候加载多个配置文件: 
ApplicationContext applicationContext = new ClassPathXmlApplicationContext("applicationContext.xml","applicationContext2.xml"); 
 
二种:在一个配置文件中包含另一个配置文件： <import resource="applicationContext2.xml"></import>
```

