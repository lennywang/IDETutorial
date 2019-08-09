final

对于一个final变量，如果是基本数据类型的变量，则其数值一旦在初始化之后便不能更改；如果是引用类型的变量，则在对其初始化之后便不能再让其指向另一个对象。



SimpleDateFormat

```java
SimpleDateFormat df = new SimpleDateFormat("yyyy-mm-dd");
Date birth =df.parse("1983-11-22");

String strBirth =df.format(list.get(i).getBirth());
```



将GB2312编码的字符串转换为ISO-8859-1编码的字符串

```java
String s1 = "你好";
String s2 = newString(s1.getBytes("GB2312"), "ISO-8859-1");
```



 打印异常

```java
Exception e;
e.printStackTrace(System.out);
```







JAVA-null或空值的判断处理
https://blog.csdn.net/qq_41214527/article/details/81145645

JAVA学习(十)__MessageFormat用法
https://blog.csdn.net/zhiweianran/article/details/8666992

Java MessageFormat.format 特殊符号、单引号
https://blog.csdn.net/a258831020/article/details/46820855

EnumUtil根据值获取枚举对象
https://blog.csdn.net/albertfly/article/details/77073039

带你认识Java中的枚举对象—Enum
https://baijiahao.baidu.com/s?id=1595377225273101054&wfr=spider&for=pc

EnumUtil根据值获取枚举对象
https://blog.csdn.net/albertfly/article/details/77073039





Jackson快速入门
https://blog.csdn.net/u011054333/article/details/80504154

mybatis foreach list

operateTags.size()

Lists.newArrayList

Lists.newArrayListWithExpectedSize(src.size());

result.addAll(operateTags);

java hashmap的使用
https://www.cnblogs.com/liujinhong/p/6113183.html

java中，一个类实现某个接口，必须重写接口中的所有方法吗？



## Java 虚拟机

### Java内存管理之Xms、-Xmx 

**堆内存分配**
JVM 初始分配的内存由**-Xms** 指定，默认是物理内存的 1/64；
JVM 最大分配的内存由**-Xmx** 指定，默认是物理内存的 1/4；
默认空余堆内存小于 40% 时，JVM 就会增大堆直到-Xmx 的最大限制；空余堆内存大于 70% 时，JVM 会减少堆直到 -Xms 的最小限制；
因此服务器一般设置-Xms、-Xmx 相等以避免在每次 GC 后调整堆的大小。对象的堆内存由称为垃圾回收器的自动内存管理系统回收。

**非堆内存分配**
JVM 使用**-XX:PermSize** 设置非堆内存初始值，默认是物理内存的 1/64；
由 XX:MaxPermSize 设置最大非堆内存的大小，默认是物理内存的 1/4；
-Xmn2G：设置年轻代大小为 2G；
-XX：SurvivorRatio，设置年轻代中Eden区与Survivor区的比值。

参考：[Java内存管理之类似-Xms、-Xmx 这些参数的含义是什么？](<https://blog.csdn.net/baidu_34122324/article/details/83472951>)











