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
<bean id="bean1" class="cn.itcast.spring.demo3.Bean1"></bean> 
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
      <property name="name" value="#{'奔驰'}"/>   
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

## 2.1 Spring 的 Bean 管理的中常用的注解

**@Component:组件.(作用在类上) **

Spring 中提供@Component 的三个衍生注解:(功能目前来讲是一致的)

* @Controller :WEB 层
* @Service  :业务层
*  @Repository :持久层

这三个注解是为了让标注类本身的用途清晰，Spring 在后续版本会对其增强

**属性注入的注解:(使用注解注入的方式,可以不用提供 set 方法.) **

* @Value  :用于注入普通类型. 
* @Autowired :自动装配:  1、默认按类型进行装配. 2、按名称注入: @Qualifier:强制使用名称注入.
* @Resource 相当于: @Autowired 和@Qualifier 一起使用. 

**Bean 的作用范围的注解**

@Scope:  singleton:单例 	prototype:多例

**Bean 的生命周期的配置**

* @PostConstruct :相当于 init-method 
* @PreDestroy  :相当于 destroy-method

**Spring 的 Bean 管理的方式的比较**

![spring-bean](<https://github.com/lennywang/Img/raw/master/spring-bean.png>)



XML 和注解: 

* XML :结构清晰. 
* 注解 :开发方便.(属性注入.) 

实际开发中还有一种 XML 和注解整合开发:   Bean 有 XML 配置.但是使用的属性使用注解注入. 



## 2.2 AOP的概述

**什么是AOP**

Spring 是解决实际开发中的一些问题。AOP 解决 OOP 中遇到的一些问题.是 OOP 的延续和扩展. 

**为什么学习AOP**

对程序进行增强:不修改源码的情况下. AOP 可以进行权限校验,日志记录,性能监控,事务控制. 

**Spring 的 AOP 的由来**

AOP 最早由 AOP 联盟的组织提出的,制定了一套规范.Spring 将 AOP 思想引入到框架中,必须遵守 AOP 联盟 的规范. 

**底层实现**

 Spring 的 AOP 的底层用到两种代理机制：1、JDK 的动态代理 :针对实现了接口的类产生代理。2、Cglib 的动态代理 :针对没有实现接口的类产生代理. 应用的是底层的字节码增强的技术 生成当前类 的子类对象. 

**AOP 的开发中的相关术语**

Joinpoint(连接点):所谓连接点是指那些被拦截到的点。在 spring 中,这些点指的是方法,因为 spring 只 支持方法类型的连接点. 
Pointcut(切入点):所谓切入点是指我们要对哪些 Joinpoint 进行拦截的定义. 
Advice(通知/增强):所谓通知是指拦截到 Joinpoint 之后所要做的事情就是通知.通知分为前置通知,后置 通知,异常通知,最终通知,环绕通知(切面要完成的功能) 
Introduction(引介):引介是一种特殊的通知在不修改类代码的前提下, Introduction 可以在运行期为类 动态地添加一些方法或 Field. 
Target(目标对象):代理的目标对象 
Weaving(织入):是指把增强应用到目标对象来创建新的代理对象的过程.  spring 采用动态代理织入，而 AspectJ 采用编译期织入和类装在期织入 
Proxy（代理）:一个类被 AOP 织入增强后，就产生一个结果代理类 
Aspect(切面): 是切入点和通知（引介）的结合

##3.1 Spring 使用 AspectJ 进行 AOP 的开发:注解的方式 
**开启 aop 注解的自动代理**

`< aop:aspectj-autoproxy/> `

**AspectJ 的 AOP 的注解**

```java
@Aspect:定义切面类的注解

通知类型:     
@Before   :前置通知     
@AfterReturing  :后置通知     
@Around   :环绕通知     
@After    :最终通知     
@AfterThrowing  :异常抛出通知.

@Pointcut:定义切入点的注解
```

## 3.2 事务

**什么是事务**

事务逻辑上的一组操作,组成这组操作的各个逻辑单元,要么一起成功,要么一起失败. 

**事务特性**

原子性 :强调事务的不可分割
一致性 :事务的执行的前后数据的完整性保持一致
隔离性 :一个事务执行的过程中,不应该受到其他事务的干扰
持久性 :事务一旦结束,数据就持久到数据库

**如果不考虑隔离性引发安全性问题**

脏读  :一个事务读到了另一个事务的未提交的数据 
不可重复读 :一个事务读到了另一个事务已经提交的 update 的数据导致多次查询结果不一致. 
虚幻读  :一个事务读到了另一个事务已经提交的 insert 的数据导致多次查询结果不一致. 

**解决读问题:设置事务隔离级别**

未提交读 :脏读，不可重复读，虚读都有可能发生 
已提交读 :避免脏读。但是不可重复读和虚读有可能发生 
可重复读 :避免脏读和不可重复读.但是虚读有可能发生. 
串行化的 :避免以上所有读问题. 

**Spring 进行事务管理一组 API**

PlatformTransactionManager:平台事务管理器. 
org.springframework.jdbc.datasource.DataSourceTransactionManager 使用 Spring JDBC 或 iBatis 进行持久化数据时用 org.springframework.orm.hibernate3.HibernateTransactionManager  使用 Hibernate 版本进行持久化数据时用

**TransactionDefinition:事务定义信息**

* 隔离级别 
* 传播行为 
* 超时信息 
*  是否只读 

**TransactionStatus:事务的状态**

记录事务的状态

**事务的传播行为**

保证同一个事务中

| 传播行为              | 含义                                      |
| --------------------- | ----------------------------------------- |
| PROPAGATION_REQUIRED  | 支持当前事务，如果不存在 就新建一个(默认) |
| PROPAGATION_SUPPORTS  | 支持当前事务，如果不存在，就不使用事务    |
| PROPAGATION_MANDATORY | 支持当前事务，如果不存在，抛出异常        |

保证没有在同一个事务中

| 传播行为                  | 含义                                           |
| ------------------------- | ---------------------------------------------- |
| PROPAGATION_REQUIRES_NEW  | 如果有事务存在，挂起当前事务，创建一个新的事务 |
| PROPAGATION_NOT_SUPPORTED | 以非事务方式运行，如果有事务存在，挂起当前事务 |
| PROPAGATION_NEVER         | 以非事务方式运行，如果有事务存在，抛出异常     |
| PROPAGATION_NESTED        | 如果当前事务存在，则嵌套事务执行               |



# SpringMVC

## 1.1 Springmvc是什么

Spring web mvc和Struts2都属于表现层的框架,它是Spring框架的一部分。


![springmvc](<https://github.com/lennywang/Img/raw/master/spring.png>)

## 1.2  Springmvc处理流程

![springmvc处理流程](<https://github.com/lennywang/Img/raw/master/springmvc-strcture.png>)

## 1.3 Springmvc架构

**架构流程**

1. 用户发送请求至前端控制器DispatcherServlet
2. DispatcherServlet收到请求调用HandlerMapping处理器映射器。
3. 处理器映射器根据请求url找到具体的处理器，生成处理器对象及处理器拦截器(如果有则生成)一并返回给DispatcherServlet。
4. DispatcherServlet通过HandlerAdapter处理器适配器调用处理器
5. 执行处理器(Controller，也叫后端控制器)。
6. Controller执行完成返回ModelAndView
7. HandlerAdapter将controller执行结果ModelAndView返回给DispatcherServlet
8. DispatcherServlet将ModelAndView传给ViewReslover视图解析器
9. ViewReslover解析后返回具体View
10. DispatcherServlet对View进行渲染视图（即将模型数据填充至视图中）。
11. DispatcherServlet响应用户

**组件说明**

以下组件通常使用框架提供实现：

* DispatcherServlet：前端控制器
  用户请求到达前端控制器，它就相当于mvc模式中的c，dispatcherServlet是整个流程控制的中心，由它调用其它组件处理用户的请求，dispatcherServlet的存在降低了组件之间的耦合性。

* HandlerMapping：处理器映射器

  HandlerMapping负责根据用户请求url找到Handler即处理器，springmvc提供了不同的映射器实现不同的映射方式，例如：配置文件方式，实现接口方式，注解方式等。

  Handler：处理器
  Handler 是继DispatcherServlet前端控制器的后端控制器，在DispatcherServlet的控制下Handler对具体的用户请求进行处理。

  由于Handler涉及到具体的用户业务请求，所以一般情况需要程序员根据业务需求开发Handler。

* HandlAdapter：处理器适配器

  通过HandlerAdapter对处理器进行执行，这是适配器模式的应用，通过扩展适配器可以对更多类型的处理器进行执行。

* ViewResolver：视图解析器

  View Resolver负责将处理结果生成View视图，View Resolver首先根据逻辑视图名解析成物理视图名即具体的页面地址，再生成View视图对象，最后对View进行渲染将处理结果通过页面展示给用户。 

* View：视图

  springmvc框架提供了很多的View视图类型的支持，包括：jstlView、freemarkerView、pdfView等。我们最常用的视图就是jsp。

  一般情况下需要通过页面标签或页面模版技术将模型数据通过页面展示给用户，需要由程序员根据业务需求开发具体的页面。

  ```
  说明：在springmvc的各个组件中，处理器映射器、处理器适配器、视图解析器称为springmvc的三大组件。
  需要用户开发的组件有handler、view
  ```

  **默认加载的组件**

  DispatcherServlet.properties

  **组件扫描器**

  使用组件扫描器省去在spring容器配置每个Controller类的繁琐。

  使用`<context:component-scan>`自动扫描标记@Controller的控制器类，

  在springmvc.xml配置文件中配置如下：

  ```xml
  <!-- 配置controller扫描包，多个包之间用,分隔 -->
  <context:component-scan base-package="cn.itcast.springmvc.controller" />
  ```

  **注解映射器和适配器**

  注解式处理器适配器，对标记@ResquestMapping的方法进行适配。 

  从spring3.1版本开始，废除了AnnotationMethodHandlerAdapter的使用，推荐使用RequestMappingHandlerAdapter完成注解式处理器适配。 

  在springmvc.xml配置文件中配置如下：

  ```xml
  <!-- 配置处理器适配器 --><beanclass="org.springframework.web.servlet.mvc.method.annotation.RequestMappingHandlerAdapter"/>
  ```

  **注解驱动器**

  直接配置处理器映射器和处理器适配器比较麻烦，可以使用注解驱动来加载。

  SpringMVC使用`<mvc:annotation-driven>`自动加载RequestMappingHandlerMapping和RequestMappingHandlerAdapter        

  可以在springmvc.xml配置文件中使用`<mvc:annotation-driven>`替代注解处理器和适配器的配置。

  ```xml
  <!-- 注解驱动 -->
  <mvc:annotation-driven />
  ```

  **视图解析器**

  视图解析器使用SpringMVC框架默认的InternalResourceViewResolver，这个视图解析器支持JSP视图解析

  在springmvc.xml配置文件中配置如下：

  ```xml
  	<!-- Example: prefix="/WEB-INF/jsp/", suffix=".jsp", viewname="test" -> 
  		"/WEB-INF/jsp/test.jsp" -->
  	<!-- 配置视图解析器 -->
  	<bean
  		class="org.springframework.web.servlet.view.InternalResourceViewResolver">
  		<!-- 配置逻辑视图的前缀 -->
  		<property name="prefix" value="/WEB-INF/jsp/" />
  		<!-- 配置逻辑视图的后缀 -->
  		<property name="suffix" value=".jsp" />
  	</bean>
  ```

  逻辑视图名需要在controller中返回ModelAndView指定，比如逻辑视图名为ItemList，则最终返回的jsp视图地址:

  “WEB-INF/jsp/itemList.jsp” 

  最终jsp物理地址：前缀+**逻辑视图名**+后缀