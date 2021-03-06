## 可以把 SQL 分为两个部分： ##

    数据操作语言 (DML) 
    
    数据定义语言 (DDL)。

SQL (结构化查询语言)是用于执行查询的语法。但是 SQL 语言也包含用于更新、插入和删除记录的语法。

## 查询和更新指令构成了 SQL 的 DML 部分： ##
    
    SELECT - 从数据库表中获取数据
    
    UPDATE - 更新数据库表中的数据
    
    DELETE - 从数据库表中删除数据
    
    INSERT INTO - 向数据库表中插入数据

SQL 的数据定义语言 (DDL) 部分使我们有能力创建或删除表格。我们也可以定义索引（键），规定表之间的链接，以及施加表间的约束。

## SQL 中最重要的 DDL 语句: ##

    CREATE DATABASE - 创建新数据库
    
    ALTER DATABASE - 修改数据库
    
    CREATE TABLE - 创建新表
    
    ALTER TABLE - 变更（改变）数据库表
    
    DROP TABLE - 删除表
    
    CREATE INDEX - 创建索引（搜索键）
    
    DROP INDEX - 删除索引

**DDL—数据定义语言(Create，Alter，Drop，DECLARE)**

**DML—数据操纵语言(Select，Delete，Update，Insert)**

**DCL—数据控制语言(GRANT，REVOKE，COMMIT，ROLLBACK)**

# MySQL中SQL语句的分类 #

 1：数据定义语言（DDL）

    用于创建、修改、和删除数据库内的数据结构，如：

	1：创建和删除数据库(CREATE DATABASE || DROP  DATABASE)；

	2：创建、修改、重命名、删除表(CREATE  TABLE || ALTER TABLE|| RENAME TABLE||DROP  TABLE)；

	3：创建和删除索引(CREATEINDEX  || DROP INDEX)

   2：数据查询语言（DQL）

    从数据库中的一个或多个表中查询数据(SELECT)

   3：数据操作语言（DML）

    修改数据库中的数据，包括插入(INSERT)、更新(UPDATE)和删除(DELETE)

   4：数据控制语言（DCL）

    用于对数据库的访问，如：

	1：给用户授予访问权限（GRANT）;

	2：取消用户访问权限（REMOKE）

## SQL SELECT 语法 ##

    SELECT 列名称 FROM 表名称

以及：

    SELECT * FROM 表名称

**注释：**SQL 语句对大小写不敏感。SELECT 等效于 select。

**提示：**星号（*）是选取所有列的快捷方式

## SQL SELECT DISTINCT 语句 ##

在表中，可能会包含重复值。这并不成问题，不过，有时您也许希望仅仅列出不同（distinct）的值。

关键词 DISTINCT 用于返回唯一不同的值。

**语法：**

    SELECT DISTINCT 列名称 FROM 表名称

#SQL TOP 实例

从 "Persons" 表中选取头两条记录。

使用下面的 SELECT 语句：

    SELECT TOP 2 * FROM Persons

前10条记录

    select top 10 * form table1 where 范围

**Top子句**

　　    TOP 子句用于规定要返回的记录的数目。对于拥有数千条记录的大型表来说，TOP 子句是非常有用的。
    
    　　在SQL Server数据库中语法为：
    
    　　　　SELECT TOP number|percent column_name(s) FROM table_name
    
    　　但是并非所有的数据库系统都支持 TOP 子句，比如Oracle和MySQL，它们有等价的语法。
    
    　　在Oracle数据库中语法为：
    
    　　　　SELECT column_name(s) FROM table_name WHERE ROWNUM <= number
    
    　　在MySQL数据库中语法为：
    
    　　　　SELECT column_name(s) FROM table_name LIMIT number

#SQL TOP PERCENT 实例

从 "Persons" 表中选取 50% 的记录。

使用下面的 SELECT 语句：

    SELECT TOP 50 PERCENT * FROM Persons

#SQL DROP TABLE 语句

DROP TABLE 语句用于删除表（表的结构、属性以及索引也会被删除）：

    DROP TABLE 表名称

#SQL DROP DATABASE 语句

DROP DATABASE 语句用于删除数据库：

    DROP DATABASE 数据库名称

#SQL TRUNCATE TABLE 语句

TRUNCATE TABLE 命令（仅仅删除表格中的数据）：

    TRUNCATE TABLE 表名称

# SQL Date 数据类型 #

MySQL 使用下列数据类型在数据库中存储日期或日期/时间值：

    DATE - 格式 YYYY-MM-DD
    
    DATETIME - 格式: YYYY-MM-DD HH:MM:SS
    
    TIMESTAMP - 格式: YYYY-MM-DD HH:MM:SS
    
    YEAR - 格式 YYYY 或 YY
# 子查询(表名1：a 表名2：b) #

    select a,b,c from a where a IN (select d from b ) 或者: select a,b,c from a where a IN (1,2,3)

# 什么是子查询？ #

把一个查询的结果在另一个查询中使用就叫做子查询

## 单行子查询 ##
    select s.s_id , s.s_name , avg(score)
    from t_student s join t_grade g on s.s_id = g.s_id
    group by s.s_id , s.s_name
    having avg(score) > (select avg(score)
     from t_student s join t_grade g on s.s_id = g.s_id
     where s.s_name = '王五'
     group by s.s_id)  

## 多行子查询 ##

    select s.s_id , s_name , c.c_id , c_name , score
    from t_grade g join t_student s on g.s_id = s.s_id
       join t_course c on g.c_id = c.c_id
    having c.c_id != 400004 and score > all (
    select score
    from t_grade 
    where c_id = 400004
    )
    group by c.c_id , s.s_id , s.s_name , c_name ,score

# 在线视图查询(表名1：a ) #

    select * from (SELECT a,b,c FROM a) T where t.a > 1;

# between的用法,between限制查询数据范围时包括了边界值,not between不包括 #

    select * from table1 where time between time1 and time2
    
    select a,b,c, from table1 where a not between 数值1 and 数值2

# 两张关联表，删除主表中已经在副表中没有的信息 #


exists （sql 返回结果集为真）
  
not exists (sql 不返回结果集为真）
 
    delete from table1 where not exists ( select * from table2 where table1.field1=table2.field1 )

#  sql group by 实例 #

**查询选修了3门课程以上（含3门）的学生学号和选修课程数。**

    select Sno as 学号 ,count(course.Cno) as 选修课程数
    
    From SC,course
    
    Where course.Cno=SC.Cno
    
    Group by Sno
    
    Having Count(course.Cno)>=3;

在 SQL 中增加 HAVING 子句原因是，WHERE 关键字无法与合计函数一起使用。

**检索至少选修两门课程的学生学号**

    SELECT sno FROM sc  
    
    GROUP BY sno HAVING (count(*)>=2);  

根据表：members(id,username,posts,pass,email),写出发帖数最多的十个人名字的sql

    select username,count(username) as 数量 from members group by  username having count(username)>2 order by count(username) desc limit 5;

# sql in子查询 #

    select *
    
    from student
    
    where Sdept in (
     select Sdept
     from student
     where Sname='王敏'
    );

# sql union实例 #

**UNION 操作符用于合并两个或多个 SELECT 语句的结果集。**

**请注意**，UNION 内部的 SELECT 语句必须拥有相同数量的列。列也必须拥有相似的数据类型。同时，每条 SELECT 语句中的列的顺序必须相同。

 **查询计算机系的学生及年龄不大于19岁的学生详细信息。**

    select *
    
    from student
    
    where student.Sdept='CS'
    
    union
    
    select *
    
    from student
    
    where student.Sage<=19;

# sql INTERSECT 交集 #

查询选修了1号课程的与年龄不大于19岁的 学生 详细信息 的交集。

    Select *
    
    from student,SC
    
    where student.Sno=SC.Sno and SC.Cno=1
    
    INTERSECT
    
    Select *
    
    from student
    
    where student.Sage<=19;

# sql EXCEPT 差集 #

查询计算机科学系的学生与年龄不大于19岁的学生详细信息的差集。

    select *

    from student

    where student.Sdept='SC'

    EXCEPT

    select *

    from student

    where student.Sage<=19;


## 引用两个表 ##

    SELECT Persons.LastName, Persons.FirstName, Orders.OrderNo
    FROM Persons, Orders
    WHERE Persons.Id_P = Orders.Id_P 

## SQL JOIN - 使用 Join ##

    SELECT Persons.LastName, Persons.FirstName, Orders.OrderNo
    FROM Persons
    INNER JOIN Orders
    ON Persons.Id_P = Orders.Id_P
    ORDER BY Persons.LastName

## 不同的 SQL JOIN ##

下面列出了您可以使用的 JOIN 类型，以及它们之间的差异。
- 
- JOIN: 如果表中有至少一个匹配，则返回行
- LEFT JOIN: 即使右表中没有匹配，也从左表返回所有的行
- RIGHT JOIN: 即使左表中没有匹配，也从右表返回所有的行
- FULL JOIN: 只要其中一个表中存在匹配，就返回行

## SQL INNER JOIN 关键字 ##

在表中存在至少一个匹配时，INNER JOIN 关键字返回行。

**INNER JOIN 关键字语法**

    SELECT column_name(s)
    FROM table_name1
    INNER JOIN table_name2 
    ON table_name1.column_name=table_name2.column_name

**注释：**INNER JOIN 与 JOIN 是相同的。

## SQL LEFT JOIN 关键字 ##

LEFT JOIN 关键字会从左表 (table_name1) 那里返回所有的行，即使在右表 (table_name2) 中没有匹配的行。

**LEFT JOIN 关键字语法**

    SELECT column_name(s)
    FROM table_name1
    LEFT JOIN table_name2 
    ON table_name1.column_name=table_name2.column_name

**注释**：在某些数据库中， LEFT JOIN 称为 LEFT OUTER JOIN。

## SQL RIGHT JOIN 关键字 ##

RIGHT JOIN 关键字会右表 (table_name2) 那里返回所有的行，即使在左表 (table_name1) 中没有匹配的行。

**RIGHT JOIN 关键字语法**

    SELECT column_name(s)
    FROM table_name1
    RIGHT JOIN table_name2 
    ON table_name1.column_name=table_name2.column_name

**注释**：在某些数据库中， RIGHT JOIN 称为 RIGHT OUTER JOIN。

## SQL FULL JOIN 关键字 ##

只要其中某个表存在匹配，FULL JOIN 关键字就会返回行。

**FULL JOIN 关键字语法(全连接)**

    SELECT column_name(s)
    FROM table_name1
    FULL JOIN table_name2 
    ON table_name1.column_name=table_name2.column_name

**注释**：在某些数据库中， FULL JOIN 称为 FULL OUTER JOIN。

## 聚合函数： ##

- –COUNT：统计行数量
- –SUM：获取单个列的合计值
- –AVG：计算某个列的平均值
- –MAX：计算列的最大值
- –MIN：计算列的最小值

## SQL的执行顺序： ##

- –第一步：执行FROM
- –第二步：WHERE条件过滤
- –第三步：GROUP BY分组
- –第四步：执行SELECT投影列
- –第五步：HAVING条件过滤
- –第六步：执行ORDER BY 排序

# SQL 添加索引 #

    使用CREATE 语句创建索引
    
    CREATE INDEX index_name ON table_name(column_name,column_name) include(score)
    
    普通索引
    
    CREATE UNIQUE INDEX index_name ON table_name (column_name) ;
    
    非空索引
    
    CREATE PRIMARY KEY INDEX index_name ON table_name (column_name) ;
    
    主键索引
     
    使用ALTER TABLE语句创建索引
    
    alter table table_name add index index_name (column_list) ;
    alter table table_name add unique (column_list) ;
    alter table table_name add primary key (column_list) ;
    

    全文索引添加FULLTEXT
    ALTER TABLE `table_name` ADD FULLTEXT ( `column`)
    
    如何添加多列索引
    ALTER TABLE `table_name` ADD INDEX index_name ( `column1`, `column2`, `column3` )
    
    
    删除索引
    
    drop index index_name on table_name ;
    alter table table_name drop index index_name ;
    alter table table_name drop primary key ;

    建表：
    DROP TABLE IF EXISTS bulletin;
    CREATE TABLE bulletin(
     id INT NOT NULL PRIMARY KEY AUTO_INCREMENT, # 主键
     uid INT(11) NOT NULL DEFAULT 0, # 创建者id
     context VARCHAR(600) NOT NULL DEFAULT '', # 公告详细内容（300字）
     begintime DEC(20) NOT NULL DEFAULT 0, # 公告开始时间
     endtime DEC(20) NOT NULL DEFAULT 0, # 公告结束时间
     createtime DEC(20) NOT NULL DEFAULT 0, # 创建时间
     modifytime DEC(20) NOT NULL DEFAULT 0 # 修改时间
     PRIMARY KEY (`Id`),
    )DEFAULT CHARSET=UTF8 TYPE=INNODB;

    修改原有字段名称及类型：
    ALTER TABLE bulletin CHANGE uid username VARCHAR(50) NOT NULL DEFAULT '';

    添加新字段：
    alter table bulletin add citycode varchar(6) not null default 0; # 城市代码

    1.创建数据库时设置编码
    create database test character set utf8;

    2.创建表时设置编码
    create table test(id int primary key)DEFAULT charset=utf8;

    3.修改数据库编码
    alter database test character set utf8;

    4.修改表默认编码
    alter table test character set utf8;

    5.修改字段编码
    alter table test modify col_name varchar(50) CHARACTER SET utf8;

select username，count(username) as 数量 from members group by username order by count(username) limit 10;

# 联合查询，关联查询，聚合函数 左连接、右链接，子查询 ，建表sql和添加索引sql #

![](images/5d60c55074326f1d7e2a3f8a7bbe2927.jpg)

![](images/04.gif)

# MySQL中字段类型的取值范围 #

数值类型

|    数据类型    |  字节  |    最小值    |    最大值    |
| ------------- |  ----- | ------------| ------------|
|   tinyint     |    1   |无符号 0     |无符号 255    |
|smallint|2|无符号 0|无符号65535|
|mediumint|3|无符号0|无符号1677215|
|int、integer|4|无符号0|无符号4294967295|
|bigint|8|无符号 0|无符号18446744073709551615|
|浮点数类型|字节|最小值|最大值|
|float|4|(正负)1.175494351E-38|（正负）3.402823466E+38|
|double|8|(正负)2.225073858507214E-308|（正负）1.7976931348623157E+308|

时间日期类型


|    日期和时间类型    |  字节  |    最小值    |    最大值    |
| ------------- |  ----- | ------------| ------------|
|   data  | 4 |1000-01-01|9999-12-31|
|   datatime  | 8 |1000-01-01 00:00:00|9999-12-31 23:59:59|
|timestamp  |4 |1970101080001|2038年的某个时刻|
|time| 3 |-838:59:59|838:59:59|
|year| 1 |1901|2155|

字符类型

| 字符串类型 |  字节  | 描述及存储需求  |
| ------------- |  ----- | ------------|
|char(M)|M|M为0~255之间的整数|
|varchar(M)||M为0~65535之间的整数，值的长度+1个字节|
|tinyblob||允许长度0~255字节，值的长度+1个字节|
|blob||允许长度0~65535字节，值的长度+2个字节|
|mediumblob||允许长度0~1677772150字节，值的长度+3个字节|
|longblob||允许长度0~4294967295字节，值的长度+4个字节|
|tinytext||允许长度0~255字节，值的长度+2个字节|
|text||允许长度0~65535字节，值的长度+2个字节|
|mediumtext||允许长度0~167772150字节，值的长度+3个字节|
|longtext||允许长度0~4294967295字节，值的长度+4个字节|
|varbinary|M|允许长度0~M个字节的变长字节字符串，值的长度+1个字节|
|binary(M)|M|允许长度0~M个字节的定长字节字符串|



**索引失效原因总结**

1. 随着表的增长，where条件出来的数据太多，大于15%，使得索引失效（会导致CBO计算走索引花费大于走全表）

2. 统计信息失效      需要重新搜集统计信息

3. 索引本身失效      需要重建索引

下面是一些不会使用到索引的原因

索引失效 

1) 没有查询条件，或者查询条件没有建立索引 

2) 在查询条件上没有使用引导列 

3) 查询的数量是大表的大部分，应该是30％以上。 

4) 索引本身失效 

5) 查询条件使用函数在索引列上（见12） 

6) 对小表查询 

7) 提示不使用索引 

8) 统计数据不真实 

9) CBO计算走索引花费过大的情况。其实也包含了上面的情况，这里指的是表占有的block要比索引小。 

10)隐式转换导致索引失效.这一点应当引起重视.也是开发中经常会犯的错误. 由于表的字段tu_mdn定义为varchar2(20), 

但在查询时把该字段作为number类型以where条件传给Oracle,这样会导致索引失效. 

错误的例子：select * from test where tu_mdn=13333333333; 

正确的例子：select * from test where tu_mdn='13333333333'; 

11)对索引列进行运算导致索引失效,我所指的对索引列进行运算包括(+，-，*，/，! 等) 

错误的例子：select * from test where id-1=9; 

正确的例子：select * from test where id=10; 

12)使用Oracle内部函数导致索引失效.对于这样情况应当创建基于函数的索引. 

错误的例子：select * from test where round(id)=10; 

说明，此时id的索引已经不起作用了 正确的例子：首先建立函数索引， 

create index test_id_fbi_idx on test(round(id)); 

然后 select * from test where round(id)=10; 这时函数索引起作用了 1,<> 2,单独的>,<,(有时会用到，有时不会) 

3,like "%_" 百分号在前. 

4,表没分析. 

5,单独引用复合索引里非第一位置的索引列. 

6,字符型字段为数字时在where条件里不添加引号. 

7,对索引列进行运算.需要建立函数索引. 

8,not in ,not exist. 

9,当变量采用的是times变量，而表的字段采用的是date变量时.或相反情况。 

10, 索引失效。 

11,基于cost成本分析(oracle因为走全表成本会更小)：查询小表,或者返回值大概在10%以上 

12,有时都考虑到了 但就是不走索引,drop了从建试试在 

13,B-tree索引 is null不会走,is not null会走,位图索引 is null,is not null 都会走 

14,联合索引 is not null 只要在建立的索引列（不分先后）都会走, 

in null时 必须要和建立索引第一列一起使用,当建立索引第一位置条件是is null 时, 

其他建立索引的列可以是is null（但必须在所有列 都满足is null的时候）, 

或者=一个值；当建立索引的第一位置是=一个值时,其他索引列可以是任何情况（包括is null =一个值）, gv

以上两种情况索引都会走。其他情况不会走。


**1.mysql都有什么锁**

MySQL有三种锁的级别：页级、表级、行级。

表级锁：开销小，加锁快；不会出现死锁；锁定粒度大，发生锁冲突的概率最高,并发度最低。

行级锁：开销大，加锁慢；会出现死锁；锁定粒度最小，发生锁冲突的概率最低,并发度也最高。

页面锁：开销和加锁时间界于表锁和行锁之间；会出现死锁；锁定粒度界于表锁和行锁之间，并发度一般

**2.什么情况下会造成死锁**

所谓死锁<DeadLock>: 是指两个或两个以上的进程在执行过程中,
因争夺资源而造成的一种互相等待的现象,若无外力作用,它们都将无法推进下去.
此时称系统处于死锁状态或系统产生了死锁,这些永远在互相等竺的进程称为死锁进程.
表级锁不会产生死锁.所以解决死锁主要还是针对于最常用的InnoDB.

死锁的关键在于：两个(或以上)的Session加锁的顺序不一致。

那么对应的解决死锁问题的关键就是：让不同的session加锁有次序




