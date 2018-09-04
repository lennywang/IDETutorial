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

## java注解

@getMapping和@postMapping
@GetMapping是一个组合注解，是@RequestMapping(method = RequestMethod.GET)的缩写。
@PostMapping是一个组合注解，是@RequestMapping(method = RequestMethod.POST)的缩写。

@RestController
@RestController注解相当于@ResponseBody ＋ @Controller合在一起的作用。
注：如果只是使用@RestController注解Controller，则Controller中的方法无法返回jsp页面，配置的视图解析器InternalResourceViewResolver不起作用，返回的内容就是Return 里的内容。

> 参考 [@getMapping和@postMapping，@RestController](https://www.cnblogs.com/ghc666/p/8657526.html)

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


3. 文件描述、springboot描述

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

