swagger2 常用注解

> [swagger2常用注解说明](https://blog.csdn.net/u014231523/article/details/76522486)



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

