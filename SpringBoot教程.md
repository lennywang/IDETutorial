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



