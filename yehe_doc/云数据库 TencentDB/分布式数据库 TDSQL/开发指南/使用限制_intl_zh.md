
TDSQL 是部署在腾讯云上的一种支持自动水平拆分的 Shared Nothing 架构的分布式数据库。用户只需在创建表时指定一个分表字段，由 TDSQL 系统负责数据的路由以及汇总，应用层可以对数据库进行透明操作。

## 软件版本
本开发指南对应的内核版本为：1.13.21-M-V2R501D002，可通过`/*Proxy*/show status`语句查询。

>TDSQL 不支持4.0以下版本以及压缩协议，建议在客户端使用时增加`-c`选项，以便使用注释透传功能。

## 功能特性
TDSQL 提供水平扩容能力，适用于海量数据的场景。具有如下功能特性：
- 支持创建分表、单表、广播表
- 提供灵活的读写分离模式
- 支持全局 Order by、Group by、Limit 操作
- 支持 Sum、Count、Avg、Min、Max 五种聚合函数
- 支持跨 Set 的 JOIN、子查询功能
- 支持预处理协议
- 支持全局唯一字段，支持 Sequence
- 支持分布式事务
- 支持二级分区
- 提供特定的 SQL 查询整个集群的配置和状态


## 使用限制
TDSQL 分布式实例高度兼容 MySQL 协议和语法，由于分布式数据库和单机数据库存在较大的架构差异，对 MySQL 的部分功能和小语法有使用限制。

### TDSQL 大类限制
- 暂不支持自定义函数、事件、表空间
- 暂不支持视图、存储过程、触发器、游标
- 暂不支持外键、自建分区、临时表
- 暂不支持复合语句，例如，BEGIN END、LOOP、UNION 的语句
- 暂不支持主备同步相关的 SQL 语言

### TDSQL 小语法限制
TDSQL 实例暂不支持 DDL、DML、管理 SQL 语言的部分语法，具体限制如下：

#### DDL
- 暂不支持 CREATE TABLE ... SELECT 
- 暂不支持 CREATE TEMPORARY TABLE 
- 暂不支持 CREATE/DROP/ALTER SERVER/LOGFILE GROUP/
- 暂不支持 ALTER 对分表键（shardkey）进行改名，但可以修改类型
- 暂不支持 RENAME

#### DML
- 暂不支持 SELECT INTO OUTFILE/INTO DUMPFILE/INTO var_name
- 暂不支持 query_expression_options，如，HIGH_PRIORITY/STRAIGHT_JOIN/SQL_SMALL_RESULT/ 					SQL_BIG_RESULT/SQL_BUFFER_RESULT/SQL_CACHE/SQL_NO_CACHE/SQL_CALC_FOUND_ROWS
- 暂不支持非 SELECT 的子查询
- 暂不支持不带列名的 INSERT/REPLACE
- 暂不支持全局的 DELETE/UPDATE 使用 ORDER BY/LIMIT
- 暂不支持不带 WHERE 条件的 UPDATE/DELETE
- 暂不支持 LOAD DATA/XML
- 暂不支持 SQL 中使用 DELAYED 和 LOW_PRIORITY
- 暂不支持 SQL 中对于变量的引用和操作，例如 SET @c=1, @d=@c+1; SELECT @c, @d
- 暂不支持 index_hint
- 暂不支持 HANDLER/DO

#### 管理 SQL 语句
- 暂不支持 ANALYZE/CHECK/CHECKSUM/OPTIMIZE/REPAIR TABLE，需要用透传语法
- 暂不支持 CACHE INDEX
- 暂不支持 FLUSH
- 暂不支持 KILL（非跨城版本数据库支持）
- 暂不支持 LOAD INDEX INTO CACHE
- 暂不支持 RESET
- 暂不支持 SHUTDOWN
- 暂不支持 SHOW BINARY LOGS/BINLOG EVENTS
- 暂不支持 SHOW WARNINGS/ERRORS 和 LIMIT/COUNT 的组合


## 系统连接方式
TDSQL 通过 Proxy 接口提供和 MySQL 兼容的连接方式，用户可以通过 IP 地址、端口号、用户名以及密码连接 TDSQL 系统，连接语句如下：
```
mysql -h10.10.10.10 -P3306 -utest12 -ptest123 -c
```
