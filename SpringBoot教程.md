## Spring Boot 运行流程分析

实例化SpringApplication,然后调用run

```java
SpringApplication app = new SpringApplication(App.class);
ConfigurableApplicationContext context = app.run(args);
```

1. 判断是否是web环境 
2. 加载所有calsspath下面的META-INF/spring.factories ApplicationContextInitializer
3. 加载所有calsspath下面的META-INF/spring.factories  ApplicationListener
4. 推断main方法所在的类
5. 开始执行run方法
6. 设置java.awt.headless系统变量
7. 加载所有calsspath下面的META-INF/spring.factories SpringApplicationRunListeners
8. 执行SpringApplicationRunListeners所有的starting方法
9. 实例化ApplicationArguments对象
10. 创建environment
11. 配置environment,主要是把run方法的参数配置到environment里面
12. 执行所有SpringApplicationRunListeners的environmentPrepared方法
13. 如果不是web环境,但是是web的environment,则把这个web的environment转换成标准的environment
14. 打印Banner
15. 初始化applicationContext,如果是web环境,实例化AnnotationConfigServletWebServerApplicationContext,否则实例化AnnotationConfigApplicationContext
16. 如果beanNameGenerator不为空,把beanNameGenerator注入到context里面去
17. 回调所有的ApplicationContextInitializer方法
18. 执行所有SpringApplicationRunListeners的contextPrepared方法
19. 依次往spring容器中注入springApplicationArguments对象,springBootBanner对象
20. 把所有的源加载到context里面去
21. 执行所有SpringApplicationRunListeners的contextLoaded方法
22. 执行context的refreshContext方法,并且调用context的registerShutdownHook方法
23. 回调,获取容器中所有的ApplicationRunner,CommandLineRunner接口,排序,依次调用

> 参考：[Spring Boot运行流程分析](https://blog.csdn.net/heimabb/article/details/80419003)

## Spring MVC 常用注解

### @Controller

@Controller注解在类上，表名这个类是Spring MVC里的Controller ，将其声明为Spring 的一个Bean，Dispatcher Servlet会自动扫描注解了解次注解的类，并将Web请求映射到注解了@RequestMapping的方法上。这里特别指出，在声明普通Bean的时候，使用@Component、@Service、@Repository和@Controller是等同的，因为@Service、@Repository、@Controller都组合了@Component元注解；但在Spring MVC 声明控制器Bean的时候，只能使用@Controller。

### @RequestMapping

@RequestMapping 注解是用来映射Web请求（访问路径和参数）、处理类和方法的。

**常用属性**

**value**：     指定请求的实际地址，指定的地址可以是URI Template 模式；

```java
value="/getgoup"
```

**method**： 指定请求的method类型， GET、POST、PUT、DELETE等；

```java
method = RequestMethod.GET
```

**consumes**： 指定处理请求的提交内容类型（Content-Type），例如application/json, text/html;

```java
//方法仅处理request Content-Type为“application/json”类型的请求
@Controller  
@RequestMapping(value = "/pets", method = RequestMethod.POST, consumes="application/json")  
public void addPet(@RequestBody Pet pet, Model model) {      
    // implementation omitted  
}
```

**produces**:    指定返回的内容类型，仅当request请求头中的(Accept)类型中包含该指定类型才返回；

 ```java
//1.返回json数据，下边的代码可以省略produces属性，因为注解@responseBody就是返回值是json数据
@Controller  
@RequestMapping(value = "/pets/{petId}", method = RequestMethod.GET, produces="application/json")  
@ResponseBody
public Pet getPet(@PathVariable String petId, Model model) {         
    // implementation omitted  
} 

//2.返回json数据的字符编码为utf-8
@Controller  @RequestMapping(value = "/pets/{petId}", produces="MediaType.APPLICATION_JSON_VALUE"+";charset=utf-8")  
@ResponseBody  
public Pet getPet(@PathVariable String petId, Model model) {          
    // implementation omitted  
}
 ```

### @getMapping和@postMapping
@GetMapping是一个组合注解，是@RequestMapping(method = RequestMethod.GET)的缩写。

@PostMapping是一个组合注解，是@RequestMapping(method = RequestMethod.POST)的缩写。

> 参考 [@getMapping和@postMapping，@RestController](https://www.cnblogs.com/ghc666/p/8657526.html)

### @ResponseBody

@ResponseBody 支持将返回值放在 response 体内，而不是返回一个页面。我们在很多基于 Ajax 的程序的时候，可以以此注解返回数据而不是页面；次注解可放置在返回值前或者方法上。

```java
@RequestMapping(value = "/requestParam", produces = "text/plain;chartset=UTF-8")
public @ResponseBody  String passRequestParam(Long id, HttpServletRequest request) {
        return "url: " + request.getRequestURL() + " can access,id: " + id;
}
```

### @RequestBody

@RequestBody 允许 request 的参数在 request 体中，而不是直接链接在地址后面。次注解放置在参数前。

```java
@requestMapping("/login")
public void login(@requestBody User user){
　　System.out.println(user.userName +" : "+ user.pwd);
}
```





### @Param

```java
public interface Mapper {

  @Select("select s_id id,s_name name,class_id classid from student where  s_name= #{aaaa} and class_id = #{bbbb}") 
  public Student select(@Param("aaaa") String name,@Param("bbbb")int class_id);
  
}
```

1.@Select(....)注解的作用就是告诉mybatis框架,执行括号内的sql语句

2.s_id id,s_name name,class_id classid  格式是 字段名+属性名,例如s_id是数据库中的字段名,id是类中的属性名

这段代码的作用就是实现数据库字段名和实体类属性的一一映射,不然数据库不知道如何匹配

3.where  s_name= #{aaaa} and class_id = #{bbbb} 表示sql语句要接受2个参数,一个参数名是aaaa,一个参数名是

bbbb,如果要正确的传入参数,那么就要给参数命名,因为不用xml配置文件,那么我们就要用别的方式来给参数命名,

这个方式就是@Param注解

4.在方法参数的前面写上@Param("参数名"),表示给参数命名,名称就是括号中的内容

public Student select(@Param("aaaa") String name,@Param("bbbb")int class_id); 

给入参 String name 命名为aaaa,然后sql语句....where  s_name= #{aaaa} 中就可以根据aaaa得到参数值了

> 拓展：[@Param注解的用法解析](https://blog.csdn.net/u012031380/article/details/54924641/)

### @PathVariable

将 URL 中占位符参数绑定到控制器处理方法的入参中:URL 中的 {xxx} 占位符可以通过@PathVariable("xxx") 绑定到操作方法的入参中。

```java
@RequestMapping("/users/{username}")
@ResponseBody
public String userProfile(@PathVariable("username") String username){
	return "user" + username; 
}
```

> 參考：[SpringBoot-@PathVariable](https://www.cnblogs.com/fangpengchengbupter/p/7823493.html)

###@RequestParams

获取请求参数的值

```java
@RestControllerpublic 
class HelloController { 
    
@RequestMapping(value="/hello",method= RequestMethod.GET)    
//required=false 表示url中可以不传入id参数，此时就使用默认参数
public String sayHello(@RequestParam(value="id",required = false,defaultValue = "1") Integer id){   
    return "id:"+id;    
}}

localhost:8080/hello
id:1
```

> 参考：[SpringBoot中常用注解@ PathVaribale / @ RequestParam / @ GetMapping](https://blog.csdn.net/u010753907/article/details/75006256)



### @RestController

@RestController注解相当于@ResponseBody ＋ @Controller合在一起的作用。

注：如果只是使用@RestController注解Controller，则Controller中的方法无法返回jsp页面，配置的视图解析器

InternalResourceViewResolver不起作用，返回的内容就是Return 里的内容。

### @MapperScan

@MapperScan可以指定要扫描的Mapper类的包的路径

```java
@SpringBootApplication
@MapperScan("com.lz.water.monitor.mapper")
// 添加对mapper包扫描
public class Application {
	
}
```

@使用@MapperScan注解多个包

```java
@SpringBootApplication  
@MapperScan({"com.kfit.demo","com.kfit.user"})  
public class App {  
    public static void main(String[] args) {  
       SpringApplication.run(App.class, args);  
    }  
}
```



### Spring Boot 注解

#### @SpringBootApplication

**@SpringBootApplication** 是 Spring Boot的核心注解，它是一个组合注解，源码如下：

```java
@Target({ElementType.TYPE})
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Inherited
@SpringBootConfiguration
@EnableAutoConfiguration
@ComponentScan
public @interface SpringBootApplication {
	Class<?>[] exclude() default {};
	String[] excludeName() default {};
}
```

@SpringBootApplication 注解主要组合了 @SpringBootConfiguration、@EnableAutoConfiguration、@ComponentScan。

关闭特定的自动配置

```java

@SpringBootApplication( exclude= { CodecsAutoConfiguration.class} )
```

**实践：**关闭多个自动配置

```java
关闭多个自动配置
@SpringBootApplication( exclude= { CodecsAutoConfiguration.class, DataSourceAutoConfiguration.class } )

控制台输出
    Exclusions:
    -----------
    org.springframework.boot.autoconfigure.http.codec.CodecsAutoConfiguration
    org.springframework.boot.autoconfigure.jdbc.DataSourceAutoConfiguration
```



## 原理

###spring如何通过注解注入？

> [spring如何通过注解注入](https://blog.csdn.net/colton_null/article/details/79187414) 





## SpringBoot启动banner

**第一种方式：修改的时候，进行设置,在Application的main方法中**

关闭banner：Banner.Mode.OFF

```java
public static void main(String[] args) {
        SpringApplication application = new SpringApplication(LogbackApplication.class);
        /*
         * Banner.Mode.OFF:关闭;
         * Banner.Mode.CONSOLE:控制台输出，默认方式;
         * Banner.Mode.LOG:日志输出方式;
         */
        application.setBannerMode(Banner.Mode.OFF);
        application.run(args);
}
```

**第二种方式：修改banner.txt配置文件 (推荐)**

1. banner生成网址：http://patorjk.com/software/taag/#p=display&f=Doom&t=java

2. 修改颜色：${AnsiColor.BRIGHT_RED} 

   * 如果颜色没有变，那么还需要设置：spring.output.ansi.enabled=ALWAYS


1. 文件描述、springboot描述

   | 代码                               | 描述                    |
   | -------------------------------- | --------------------- |
   | ${application.version}           | 这个是MANIFEST.MF文件中的版本号 |
   | ${application.formatted-version} | 这个是上面的的版本号前面加v后上括号    |
   | ${spring-boot.version}           | 这个是springboot的版本号     |
   | ${spring-boot.formatted-version} | 这个是springboot的版本号     |

   ​

   [佛祖保佑 永无bug 代码注释](https://www.cnblogs.com/wangjunwei/p/6995467.html)

```
${AnsiColor.BRIGHT_RED}                    _oo0oo_
${AnsiColor.BRIGHT_RED}                   o8888888o
${AnsiColor.BRIGHT_RED}                   88" . "88
${AnsiColor.BRIGHT_RED}                   (| -_- |)
${AnsiColor.BRIGHT_RED}                   0\  =  /0
${AnsiColor.BRIGHT_RED}                 ___/`---'\___
${AnsiColor.BRIGHT_RED}               .' \\|     |// '.
${AnsiColor.BRIGHT_RED}              / \\|||  :  |||// \
${AnsiColor.BRIGHT_RED}             / _||||| -:- |||||- \
${AnsiColor.BRIGHT_RED}            |   | \\\  -  /// |   |
${AnsiColor.BRIGHT_RED}            | \_|  ''\---/''  |_/ |
${AnsiColor.BRIGHT_RED}            \  .-\__  '-'  ___/-. /
${AnsiColor.BRIGHT_RED}          ___'. .'  /--.--\  `. .'___
${AnsiColor.BRIGHT_RED}       ."" '<  `.___\_<|>_/___.' >' "".
${AnsiColor.BRIGHT_RED}      | | :  `- \`.;`\ _ /`;.`/ - ` : | |
${AnsiColor.BRIGHT_RED}      \  \ `_.   \_ __\ /__ _/   .-` /  /
${AnsiColor.BRIGHT_RED}  =====`-.____`.___ \_____/___.-`___.-'=====
${AnsiColor.BRIGHT_RED}                    `=---='
${AnsiColor.BRIGHT_RED}  ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
${AnsiColor.BRIGHT_RED}            佛祖保佑         永无BUG
${AnsiColor.BRIGHT_RED} MANIFEST.MF文件中的版本号: version:${application.version}   ${AnsiColor.BRIGHT_RED} springboot的版本号: Spring-Boot ${spring-boot.version}
```

**第三种方式：重写接口Banner实现**

SpringBoot提供了一个接口org.springframework.boot.Banner，他的实例可以被传给SpringApplication的setBanner(banner)方法。如果你闲得不行非要着重美化这个命令行输出的话，可以重写Banner接口的printBanner方法。

**第四种方式：在application.properties进行配置**

在application.proerpties进行banner的显示和关闭：spring.main.banner-mode=off

> 适用于Spring-Boot 2.0.4.RELEASE

## SpringBoot自定义favicon.ico

**自定义Favicon**

将favicon.ico放置在src/main/resources/static下

**关闭Favicon**

在application.properties中设置关闭Favicon，默认为开启。

```
spring.mvc.favicon.enabled=false
```

## SpringBoo实践

**conflicts with existing, non-compatible bean definition of same name and class 的解决办法**

**原因：**spring管理bean大概类似把bean实例化放到map中，而当中的键，默认是用的是类名，这样，如果项目中

两个Contoller/Service 重名的话，就会导致管理bean的map中的key重复。本例中didi-km-x-service中有两个

MailService.java文件。

**解决办法：**重命名键值。给其中一个文件添加``@Service("mailsend")`` 注解

**场景还原：**

MailService.java

```java
package com.didi.km.x.service;
@Service("mailsend")
public class MailService {
  
}
```

MailService.java

```java
package com.didi.km.x.service.mail;
@Service
public class MailService {
  
}
```

> 参考：[SpringMVC conflicts with existing, non-compatible bean definition of same name and class 的解决办法](https://www.cnblogs.com/a2211009/p/4534215.html)

**springboot 启动报错Field XXX required a bean of type XXX that could not be found.**

原因：service类上面没有@service注解

解决办法：sp添加@Service注解。

场景还原：

```java
package com.didi.km.x.service;
@Service("mailsend")
public class MailService {
  
}
```

> 参考：[springboot 启动报错Field XXX required a bean of type XXX that could not be found.](https://blog.csdn.net/Julycaka/article/details/80622754)

**“No 'Access-Control-Allow-Origin' header is present on the requested resource.”**

**同源策略**(Same origin Policy)
浏览器出于安全方面的考虑，只允许与同域下的接口交互。同域指的是？
同协议：如都是http或者https
同域名：如都是<http://jirengu.com/a> 和<http://jirengu.com/b> 
同端口：如都是80端口

**解决方案**
**1.代理服务器** 					**2.JSONP** 				**3.CORS**

**CORS**全称Cross-Origin Resource Sharing

**JSONP**(JSON with padding)
通过 script 标签加载数据的方式去获取数据当做 JS 代码来执行

```javascript
showData({“city”: “hangzhou”, “weather”: “晴天”})

function showData(ret){ 
	console.log(ret); 
}
```

**示例代码**

```
@ResponseBody
@RequestMapping("/getMySeat")
public String getMySeatSuccess(@RequestParam("callback") String callback){
        Gson gson=new Gson();
        Map<String,String> map=new HashMap<>();
        map.put("seat","1_2_06_12");
        logger.info(callback);
        return callback+"("+gson.toJson(map)+")";
}

$.ajax({
        type:"GET",
        url:"http://www.deardull.com:9090/getMySeat", //访问的链接
        dataType:"jsonp",  //数据格式设置为jsonp
        jsonp:"callback",  //Jquery生成验证参数的名称
        success:function(data){  //成功的回调函数
            alert(data);
        },
        error: function (e) {
            alert("error");
        }
});
```

> 參考：[前端人员必须会的jsonp!](https://blog.csdn.net/Summer_water/article/details/52740953)

