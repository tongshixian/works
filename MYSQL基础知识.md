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

#SQL TOP PERCENT 实例

从 "Persons" 表中选取 50% 的记录。

使用下面的 SELECT 语句：

    SELECT TOP 50 PERCENT * FROM Persons




