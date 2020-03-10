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

| 格式   | 描述            |
| ---- | ------------- |
| %Y   | 年，4位          |
| %y   | 年，2位          |
| %M   | 月名            |
| %m   | 月，数值(00-12)   |
| %D   | 月，数值(00-12)   |
| %d   | 月的天，数值(00-31) |

SELECT DATE_FORMAT(SYSDATE(),'%Y-%m-%d');     返回 2018-12-22

> 参考：[MySQL DATE_FORMAT() 函数](http://www.w3school.com.cn/sql/func_date_format.asp)

rand()函数

```mysql
# 生成≥a且≤b的随机数 x=a y=(b-a)+1
select floor(x+rand()*y);
```

> [mysql函数 random()](https://blog.csdn.net/sr_www/article/details/81047385)

REPLACE

limit 0,20 

## 常用操作

**表结构维护与删除**

- 修改表名

  ```mysql
  rename table 旧表名 to 新表名;
  rename table student to user;
  ```


- 添加列

  ```mysql
  alter table 表名 add 列名 类型;
  alter table user add addr varchar(50);
  ```


- 修改列类型

  ```mysql
  alter table 表名 modify 列名 新类型;
  alter table user modify servnumber varchar(20);
  ```


- 修改列名

  ```mysql
  alter table 表名 change 旧列名 新列名 类型;
  alter table user change servnumber telephone varchar(20);
  ```


- 删除列

  ```mysql
  alter table 表名 drop 列名;
  alter table user drop famliy;
  ```


- 修改字符集

  ```mysql
  alter table 表名 character set 字符集;
  alter table user character  set GBK;
  ```


- 删除表

  ```mysql
  drop table 表名；
  drop table user;
  -- 看表是否存在，若存在则删除表：
  drop table if exists 表名;
  drop table  if exists teacher;
  ```




**创建表**

- 语法

  ```mysql
  CREATE TABLE 表名 (
                    字段名1 字段类型1 约束条件1 说明1,
                    字段名2 字段类型2 约束条件2 说明2,
                    字段名3 字段类型3 约束条件3 说明3
                    );

  create table 新表名 as select * from 旧表名 where 1=2;(注意：建议这种创建表的方式用于日常测试，因  为可能索引什么的会复制不过来)

  create table 新表名 like 旧表名;
  ```


- 约束条件

  ```
  comment         ----说明解释
  not null        ----不为空
  default         ----默认值
  unsigned        ----无符号（即正数）
  auto_increment  ----自增
  zerofill        ----自动填充
  unique key      ----唯一值
  ```


- 创建sql

  ```sql
  CREATE TABLE student (
                      id tinyint(5) zerofill auto_increment  not null comment '学生学号',
                      name varchar(20) default null comment '学生姓名',
                      age  tinyint  default null comment '学生年龄',
                      class varchar(20) default null comment '学生班级',
                      sex char(5) not null comment '学生性别',
                      unique key (id)
                      )engine=innodb charset=utf8;
  ```

**创建普通索引或者唯一索引**

- 创建表的时候创建

  ```mysql
  create table test (
                          id int(7) zerofill auto_increment not null,
                          username varchar(20),
                          servnumber varchar(30),
                          password varchar(20),
                          createtime datetime,
                          unique (id)
                    )DEFAULT CHARSET=utf8;
  ```


- 直接为表添加索引

  ```mysql
  语法：alter table 表名 add index 索引名称 (字段名称);
   eg: alter table test add unique unique_username (username);
   
  注意：假如没有指定索引名称时，会以默认的字段名为索引名称
  ```


- 直接创建索引

  ```mysql
  语法：create index 索引 on 表名 (字段名);
  eg：create index index_createtime on test (createtime);
  ```


- 查看索引

  ```mysql
  语法：show index from 表名\G
  eg: show index from test\G
  ```


- 修改索引名称（mysql）

  ```mysql
  # MySQL 5.7及以上版本
  ALTER TABLE tbl_name RENAME INDEX old_index_name TO new_index_name
  # MySQL 5.7以前的版本
  ALTER TABLE tbl_name DROP INDEX old_index_name
  ALTER TABLE tbl_name ADD INDEX new_index_name(column_name)
  ```


- 删除索引

  ```mysql
  语法：drop index 索引名称 on 表名;
  eg：drop index unique_username on test;

  语法：alter table 表名 drop index 索引名;
  eg：alter table test drop index createtime;
  ```



**查看参数**

```mysql
SHOW VARIABLES LIKE 'wait_timeout'; -- 超时时间
SELECT @@join_buffer_size ; -- join线程 join_buffer内存大小
```





**cmd连接mysql连接**

```
mysql -h 主机地址 -u 用户名 -p 用户密码（注:u与root可以不用加) 
mysql -h 10.96.238.10 -P 10349 -u user_kmtest -p odgbcalehdefplbo
```

**查看MySQL配置**

```
select @@basedir;查看MySQL的安装目录，在mysql下执行
select @@datadir;查看MySQL的数据存放目录，在mysql下执行
mysql --help | grep 'my.cnf' linux 查看配置文件顺序
mysql --help | findstr my.cnf windows 查看配置文件顺序
```

**MySQL启动、停止、重启**

| 命令                    | 含义               | 备注                 |
| --------------------- | ---------------- | ------------------ |
| service mysql start   | 启动               |                    |
| service mysql stop    | 停止               |                    |
| service mysql restart | 重启               |                    |
| chkconfig mysql on    | 设置开机时自动启动mysql服务 |                    |
| chkconfig mysql off   | 关闭开机时自启          |                    |
| ntsysv                | 查看开机自启动服务        | yum install ntsysv |





## 数据类型

1、时间

```
date 		YYYY-MM-DD   它只支持date部分，如果插入了time内容，它会丢弃掉time，提示warning。

time		HH:MM:SS

datetime	占用8个字节		与时区无关		datetime类型适合用来记录数据的原始的创建时间	

timestmp	占用4个字节		时区转化 		
```

time

```sql
CREATE TABLE `linkinframe`.`test` (
  `id` INT NOT NULL,
  `a` TIME NULL,
PRIMARY KEY (`id`));
INSERT INTO `linkinframe`.`test` (`id`, `a`) VALUES ('3', '50:05');
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



3、字符串类型

```
类型           大小                用途
 CHAR          0-2^8-1字节        定长字符串
 VARCHAR       0-2^16-1字节       变长字符串
 TINYTEXT      0-2^8-1字节        短文本字符串
 TEXT          0-2^16-1字节       长文本数据
 MEDIUMTEXT    0-2^24-1字节       中等长度文本数据
 LONGTEXT      0-2^32-1字节       极大文本数据
```

char 与varchar

| 对比项    | char(16)                    | varchar(16)             |
| ------ | --------------------------- | ----------------------- |
| 长度特点   | 长度固定，存储字符                   | 度可变，存储字符                |
| 长度不足情况 | 插入的长度小于定义长度时，则用空格填充         | 小于定义长度时，按实际插人长度存储       |
| 性能     | 存取速度比varchar快得多             | 存取速度比char慢得多            |
| 使用场景   | 适合存储很短的,固定长度的字符串,如手机号，MD5值等 | 适合用在长度不固定场景，如收货地址，邮箱地址等 |



## 底层原理

### Mysql数据库引擎

**特征对比**

常见的mysql表引擎有INNODB和MyISAM，主要的区别是INNODB适合频繁写[数据库](http://www.111cn.net/database/database.html)操作，MyISAM适合读取数据库的情况多一点。

| 特征\引擎                      | Innodb                                   | MyIASM                                   |
| -------------------------- | ---------------------------------------- | ---------------------------------------- |
| 提供事务支持                     | Innodb引擎提供了对数据库ACID事务的支持。                | 不提供事务的支持                                 |
| 支持行级锁和外键                   | 提供了行级锁和外键的约束                             | 不支持行级锁和外键                                |
| Select count(*) from table | 进行扫描全表                                   | 直接的读取已经保存的值                              |
| 适用场景                       | 1、使用数据库的事务<br />2、大容量的数据集时趋向于选择Innodb。<br />3、UPDATE语句在Innodb下执行的会比较的快，尤其是在并发量大的时候。 | 1、表的读操作远远多于写操作时，<br />并且不需要事务支持<br />2、大批量的插入语句时（这里是INSERT语句） |

> 参考[mysql的常用引擎](https://www.cnblogs.com/xiaohaillong/p/6079551.html)

**操作**

修改表数据库引擎

```mysql
ALTER TABLE table_name ENGINE = MyISAM;
```

修改表注释

```sql
ALTER TABLE table_name COMMENT='最近游戏列表';
```

[MySQL 建表时给表和字段加上注释](https://blog.csdn.net/ssssSFN/article/details/88318519)

## 实践

### 1、安装MySQL

> [【MySQL】在Windows 10上安装MySQL 5.7](https://www.jianshu.com/p/bc3a060923f6)



> [阿里云Centos7上安装MySQL教程](https://www.cnblogs.com/jepson6669/p/9013652.html)



问题：

mysqldump: Got error: 1146: Table 'dbname.tbname' doesn't exist when using LOCK TABLES
http://www.edbiji.com/doccenter/showdoc/10/nav/295.html

如何彻底的卸载和删除Windows service
https://www.cnblogs.com/Wolfmanlq/p/5872043.html

安装mysql Install/Remove of the Service Denied!错误的解决办法
https://blog.csdn.net/lxpbs8851/article/details/14161935/
注：此处注意用管理员身份打开cmd窗口

MySQL出现：ERROR 2003 (HY000): Can't connect to MySQL server on 'localhost' (10061)问题解决
https://blog.csdn.net/qq_38826019/article/details/88687664
注：此处在bin目录执行`mysqld.exe -- install` 而不是 `mysql.exe -- install`

mysql5.7初始化密码报错 ERROR 1820 (HY000): You must reset your password using ALTER USER statement before
https://blog.csdn.net/memory6364/article/details/82426052

1130-host . is not allowed to connect to this MySql server,MySQL

```
grant all privileges on . to 'root'@'%%' identified by 'root' with grant option;
FLUSH   PRIVILEGES;
```



### 2、更新数据

MySQL的ON DUPLICATE KEY UPDATE用法
https://blog.csdn.net/plg17/article/details/78583692

Oracle merge into的用法，以及MySQL的相同功能语句
https://blog.csdn.net/zhijiesmile/article/details/74075267

mysql 实现merge into
https://blog.csdn.net/qq_22211217/article/details/81286311

### 3、更新字符集

```sql
-- 显示表的字符集
SHOW CREATE TABLE tablename
-- 修改库的字符集编码
ALTER DATABASE dbname DEFAULT CHARACTER SET utf8;
-- 修改表的字符集
alter table tablename character  set GBK;
-- 修改字段字符集
ALTER TABLE tablename CHANGE c1 c1 VARCHAR(50) CHARACTER SET utf8; 
```



### 4、查看mysql版本

| 操作        | 命令                 | 描述   |
| --------- | ------------------ | ---- |
| 查看mysql版本 | select version();  |      |
| 查看当前数据库   | select database(); |      |
| 查看当前登录用户  | select user();     |      |
|           |                    |      |

### 5、查看当前所有的数据库

| 操作           | 命令                     | 描述   |
| ------------ | ---------------------- | ---- |
| 查看当前有的数据库    | show databases;        |      |
| 查看指定数据库中的所有表 | show tables            |      |
| 查看数据库支持的引擎   | show engines;          |      |
| 查看当前数据的引擎    | show create table 表名\G |      |
| 查看当前库所有表的引擎  | show table status\G    |      |
| 有哪些线程在运行     | show processlist       |      |

6、查询/关闭进程

```mysql
# 查询进程
show processlist
# 杀死进程id，id就是processlist中的id的值
kill id;
```

7、查看mysql启动时读取配置文件的默认目录

```shell
# 在Linux下执行
mysql --help|grep 'my.cnf'
```

### 6、备份

```shell
# 逻辑备份
mysqldump -uroot -p xdclass-mysql account -F > xd_mysql_account_bak.sql
# 逻辑备份还原
mysql -uroot -p xdclass-mysql < /usr/local/mysqldump/xd_mysql_account_bak.sql

# 物理备份还原
mysqlbinlog mysql-bin.000002 | cat -n | grep -iw 'drop'
mysqlbinlog --no-defaults --set-charset=utf8  --stop-position="52" /var/lib/log_bin/mysql-bin.000002 | mysql -uroot -p
```

物理备份

reset master;
1、删除binlog索引文件中列出的所有binlog文件   
2、清空binlog索引文件   
3、创建一个新的binlog文件

mysqldump -uroot -proot -h112.126.63.69  lenny-personmanage  HandAccount_ThreeThings -F > /usr/local/mysqldump/backup/threethings2.sql
生成binlog



### 7、优化

mysql 索引的建立原则
https://blog.csdn.net/eaphyy/article/details/69259079

浅谈索引对数据库性能的影响
http://www.51testing.com/html/66/206966-814217.html



8、索引

索引好处
 快速定位到表的位置，减少服务器扫描的数据
 有些索引存储了实际的值，特定情况下只要使用索引就能完成查询


索引缺点
 索引会浪费磁盘空间，不要创建不必要的索引
 插入、更新、删除需要维护索引，带来额外的开销
 索引过多，修改表的时候重构索引性能差


索引优化实践
 前缀索引，特别是TEXT和BLOG类型的字段，只检索前面几个字符，提高检索速度
 尽量使用数据量少的索引，索引值过多查询速度会受到影响
 选择合适的索引列顺序
 内容变动少，且查询频繁，可以多建立几个索引
 内容变动频繁，谨慎创建索引
 根据业务创建适合的索引类型，比如某个字段常用来做查询条件，则为这个字段建立索引提高查询速度
 组合索引选择业务查询最相关的字段





## 常见问题

[Err] 1055 - Expression #1 of ORDER BY clause is not in GROUP BY clause and contains nonaggregated column 
https://blog.csdn.net/u012187452/article/details/82120345











# Oracle

## 常用操作

**取前2000条**

```sql
SELECT t.* FROM HR_STAFF_PRIMARY_INFO T WHERE rownum<2001 and t.id_number is not null;
```

**分页**

```sql
SELECT * FROM  (SELECT A.*,ROWNUM RN FROM (SELECT * FROM TABLE_NAME) A WHERE ROWNUM <= 40)  
WHERE RN >= 21  
```

Oracle中分页查询语句
https://www.cnblogs.com/zhaotiancheng/p/6262635.html

**为空**

```sql
//语法
Nvl(DATA_VALUE1,0)

//练习
DATA_VALUE1 = NVL(DECODE(TRIM(SRC_SUBJECT_NAME),'内部转入',-1 * DATA_VALUE1,DATA_VALUE1),0)
```

**删除表**

```sql
//删除表中的所有数据，并不是删除表
TRUNCATE TABLE tbale_name


//删除表的结构
DROP TABLE table_name 
```

**删除数据**

```sql
//方式2
DELETE DEPT_TRANSFER T WHERE T.UUID='DA5DD8E11204FB59E040A8C0DB006BF3';

//方式1
DELETE FROM DEPT_TRANSFER T WHERE T.UUID='DA5DD8E11206FB59E040A8C0DB006BF3';
```



**修改字段类型**

```
alter table tablename modify (fieldname varchar2(30))
```

> [oracle 如何修改 字段的长度](https://www.csdn.net/gather_2f/MtTaUgxsODUzNC1ibG9n.html)

两个日期相差天数

```sql
select TO_NUMBER(TO_DATE('2018-6-5','yyyy-mm-dd hh24:mi:ss')- TO_DATE('2018-5-31','yyyy-mm-dd hh24:mi:ss')) AS 相差天数 from dual;
```

**wm_concat**

```sql
SELECT T1.LOGIN_NAME 账号, T1.USER_NAME 姓名, wm_concat(T2.ROLE_NAME) 权限
  FROM sys_user_role T
  LEFT JOIN v_sys_user T1
    ON T.USER_ID = T1.id
  LEFT JOIN SYS_ROLE T2
    ON T.ROLE_ID = T2.ID
 where T1.LOGIN_NAME IS NOT NULL
 group by T1.LOGIN_NAME, T1.USER_NAME
```



## 常用函数

**ROW_NUMBER()**

```sql
语法：ROW_NUMBER() OVER(ORDER BY COLUMN)

select deptid,salary, row_number() OVER (PARTITION BY deptid ORDER BY salary) from employee
```

> [Oracle之ROW_NUMBER() OVER函数](https://blog.csdn.net/ericsson_liu/article/details/81391322)

**substr()**

```mysql
substr函数格式
　　格式1： substr(string string, int a, int b);
　　格式2：substr(string string, int a) ;

格式1
1、string 需要截取的字符串 
2、a 截取字符串的开始位置（注：当a等于0或1时，都是从第一位开始截取）
3、b 要截取的字符串的长度

格式2
1、string 需要截取的字符串
2、a 可以理解为从第a个字符开始截取后面所有的字符串。

substr('HelloWorld',0,3); //返回结果：Hel，截取从“H”开始3个字符 
substr('HelloWorld',0);  //返回结果：HelloWorld，截取所有字符
```

> [Oracle中的substr()函数](https://blog.csdn.net/yimixgg/article/details/89322437)

**trim()**

```mysql
select trim(leading 'x' from 'xdylan') "test_trim" from dual; -- dylan
```

> [oracle 之 trim函数](https://blog.csdn.net/indexman/article/details/7748766)

