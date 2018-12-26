MySql



1、查询日期

select date_format(birthday,'%Y-%m-%d')  from score;

SELECT SUBSTR('123' FROM 1 FOR 2);

SELECT * FROM websites WHERE url REGEXP '[f]';

## 常用函数

### IFNULL

IFNULL(expression_1,expression_2);

expression_1不为NULL，则IFNULL函数返回expression_1; 否则返回expression_2的结果。

SELECT IFNULL(NULL,'IFNULL function');	返回IFNULL function

### DATE_FORMAT()

DATE_FORMAT(date,format)

*date* 参数是合法的日期。*format* 规定日期/时间的输出格式。

| 格式 | 描述                |
| ---- | ------------------- |
| %Y   | 年，4位             |
| %y   | 年，2位             |
| %M   | 月名                |
| %m   | 月，数值(00-12)     |
| %D   | 月，数值(00-12)     |
| %d   | 月的天，数值(00-31) |

SELECT DATE_FORMAT(SYSDATE(),'%Y-%m-%d');     返回 2018-12-22

> 参考：[MySQL DATE_FORMAT() 函数](http://www.w3school.com.cn/sql/func_date_format.asp)





REPLACE

limit 0,20 

## 常用操作

**cmd连接mysql连接**

```
mysql -h 主机地址 -u 用户名 -p 用户密码（注:u与root可以不用加) 
mysql -h 10.96.238.10 -P 10349 -u user_kmtest -p odgbcalehdefplbo
```







## 数据类型

1、时间

```
date 		YYYY-MM-DD   它只支持date部分，如果插入了time内容，它会丢弃掉time，提示warning。

time		HH:MM:SS

datetime	占用8个字节		与时区无关		datetime类型适合用来记录数据的原始的创建时间	

timestmp	占用4个字节		时区转化 		
```

2、数字

```
类型            大小         范围（有符号）            范围（无符号）       用途
TINYINT         1字节        (-2^6，2^6 -1)           (0，2^6)        小整数值 
SMALLINT        2 字节       (-2^15，2^15-1)          (0，2^15-1)     大整数值 
MEDIUMINT       3 字节       (-2^22，2^22-1)  		   (0，2^22-1) 	 大整数值 
INT或INTEGER    4 字节       (-2^31，2^31-1) 		  (0，2^31-1) 	大整数值 
BIGINT         8 字节        (-2^63，2^63-1) 		   (0，2^63-1)    极大整数值
```

## 底层原理

### Mysql数据库引擎

**特征对比**

常见的mysql表引擎有INNODB和MyISAM，主要的区别是INNODB适合频繁写[数据库](http://www.111cn.net/database/database.html)操作，MyISAM适合读取数据库的情况多一点。

| 特征\引擎                  | Innodb                                                       | MyIASM                                                       |
| -------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 提供事务支持               | Innodb引擎提供了对数据库ACID事务的支持。                     | 不提供事务的支持                                             |
| 支持行级锁和外键           | 提供了行级锁和外键的约束                                     | 不支持行级锁和外键                                           |
| Select count(*) from table | 进行扫描全表                                                 | 直接的读取已经保存的值                                       |
| 适用场景                   | 1、使用数据库的事务<br />2、大容量的数据集时趋向于选择Innodb。<br />3、UPDATE语句在Innodb下执行的会比较的快，尤其是在并发量大的时候。 | 1、表的读操作远远多于写操作时，<br />并且不需要事务支持<br />2、大批量的插入语句时（这里是INSERT语句） |

> 参考[mysql的常用引擎](https://www.cnblogs.com/xiaohaillong/p/6079551.html)

**操作**

修改表数据库引擎

```mysql
ALTER TABLE table_name ENGINE = MyISAM;
```

