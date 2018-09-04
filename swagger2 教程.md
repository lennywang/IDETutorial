# swagger2 教程

> [swagger2常用注解说明](https://blog.csdn.net/u014231523/article/details/76522486)

## Swagger2 常见注解

### Api

**@Api()** 
用于类；表示标识这个类是swagger的资源 
tags–表示说明 
value–也是说明，可以使用tags替代 
**但是tags如果有多个值，会生成多个list**

```java
@Api(value="用户controller",tags={"用户操作接口"})
@RestController
public class UserController {

}
```

### ApiOperation

**@ApiOperation()** 用于方法；表示一个http请求的操作 
value用于方法描述 
notes用于提示内容 
tags可以重新分组（视情况而用） 
**@ApiParam()** 用于方法，参数，字段说明；表示对参数的添加元数据（说明或是否必填等） 
name–参数名 
value–参数说明 
required–是否必填

```java
@Api(value="用户controller",tags={"用户操作接口"})
@RestController
public class UserController {
@ApiOperation(value="获取用户信息",tags={"获取用户信息copy"},notes="注意问题点")
@GetMapping("/getUserInfo")
public User getUserInfo(@ApiParam(name="id",value="用户id",required=true) Long id,@ApiParam(name="username",value="用户名") String username) {
     // userService可忽略，是业务逻辑
      User user = userService.getUserInfo();

      return user;
  }
}
```



## Swagger 常见问题

### no response from server错误

```java
 public Docket init() {
        Docket docket = new Docket(DocumentationType.SWAGGER_2)
                .apiInfo(apiInfo())
                .select()
                .apis(RequestHandlerSelectors.basePackage("com.didi.km.x.api.controller"))
                .paths(PathSelectors.any())
                .build();
        docket.host("localhost:8080");
        return docket;
    }
```

> 参考：[swagger出现no response from server错误的解决办法](https://blog.csdn.net/razeSpirit/article/details/78908366)







