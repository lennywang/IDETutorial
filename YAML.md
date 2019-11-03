

浏览器内核

IE浏览器				Trident； 

Chrome浏览器			以前是Webkit，现在是Blink； 

Firefox浏览器			Gecko； 

Safari浏览器			Webkit； 

Opera浏览器			最初是自己的Presto，后来是Webkit，现在是Blink； 





User Agent

中文名为用户代理，简称 UA，使得服务器能够识别客户使用的操作系统及版本、CPU 类型、浏览器及版本、浏览器渲染引擎、浏览器语言、浏览器插件等。

```java
UserAgent userAgent = UserAgent.parseUserAgentString(request.getHeader("User-Agent"));  
Browser browser = userAgent.getBrowser();  
OperatingSystem os = userAgent.getOperatingSystem();
```





Yaml

YAML是一种简洁的非标记语言 (Yaml Ain’t Markup Language) ，YAML以数据为中心，使用空白，缩进，分行组织数据，从而使得表示更加简洁易读， 常用于作为配置文件, 比json更加简洁。

语法

*大小写敏感*

使用缩进表示层级关系

*禁止使用tab缩进，只能使用空格键 , 建议使用两个空格*

缩进的空格数目不重要，只要相同层级的元素左侧对齐即可

*# 表示注释，从这个字符一直到行尾，都会被解析器忽略。*

字符串可以不用引号，也可以使用单引号或者双引号

数据结构

对象(键值表): 键值对的集合，又称为映射（mapping）/ 哈希（hashes） / 字典（dictionary）冒号分隔键值对(Key: Value), Key需要顶格写，前面不能有空格，冒号后面需要有一个空格然后再跟值, 相同的缩进属于同一个map 例如age: 12

数组(列表): 一组按次序排列的值，又称为序列（sequence） / 列表（list）

纯量scalar: 数据最小的单位，不可以再分割。

示例

### 1、换行

> a b c 
>
> d

在a b c 的c后面,**如果a b c 与d之间不空行,或者只在c后面空一格,在这个时候,按下回车的话,编辑的第二行d,会与a b c在同一行里** 要想实现换行,需要至少需要在c的后面空两个空格









