# Java MySQL

@author Leiyanfu 

@Date 2019/04/25



# 数据库的操作

| **创建**               | **create database   数据库名;**                         |
| ---------------------- | ------------------------------------------------------- |
| **指定字符集**         | **create database 数据库名   character set 字符集;**    |
|                        |                                                         |
| 删除数据库             | drop datebase 数据库名;                                 |
|                        |                                                         |
| 修改字符集             | alter database 数据库名   default character set 字符集; |
|                        |                                                         |
| **创建查询是否存在**   | **create database if   not exists 数据库名;**           |
| **查看数据库**         | **show databases;**                                     |
| **查看在使用的数据库** | **select database();**                                  |
| **使用数据库**         | **use 数据库名;**                                       |
| **查看数据库创建**     | **show create database   数据库名;**                    |

# 单表操作 增删改查

| **创建表**       |   **create table   表名(字段名 字段类型(字段长度),···);**    |
| :--------------- | :----------------------------------------------------------: |
| **创建相同的表** |            **create table 新表名 like   旧表名;**            |
| **添加字段**     |    **alter table 表名 add   字段名 字段类型(字段长度);**     |
|                  |                                                              |
| 删除表           |                       drop table 表名;                       |
| 判断存在并删除   |                 drop table if exists   表名;                 |
| 删除字段         |               alter table 表名 drop   字段名;                |
|                  |                                                              |
| **修改字段**     | **alter table 表名 change   旧字段名 新字段名 字段类型(字段长度);** |
| **修改字符集**   |         **alter table 表名   character set 字符集;**         |
| **修改表名**     |             **rename table 旧表名 to   新表名;**             |
| **修改字段类型** |    **alter table 表名 modify   字段名 新类型(类型长度);**    |
|                  |                                                              |
| 快捷修改字符集   |                      set names 字符集;                       |
| 查看数据库中的表 |                         show tables;                         |
| 查看表结构       |                          desc 表名;                          |
| 查看表的创建     |                   show create table 表名;                    |

# 数据

| **插入数据**       | **insert into   表名(字段名1,…)value(值1,…);**               |
| ------------------ | ------------------------------------------------------------ |
| **插入全部**       | **insert into   表名(字段名1,…最后字段)value(值1,…最后值);** |
| **蠕虫复制**       | **create table 表A like 被复制的表;**         **insert into 新表 select   * from 旧表;** |
| **建表时添加约束** | **create   table 表名(字段名 字段类型(字段长度) 字段约束区,···，全字段约束区(字段名));** |
| **插入全部**       | **insert into 表名   value(值1,…最后值);**                   |
|                    |                                                              |
| 有条件删除数据     | delete from 表名 where   字段名=值;                          |
| 摧毁表再创建       | truncate table 表名;                                         |
|                    |                                                              |
| **无条件修改**     | **update 表名 set 字段名=新值;**                             |
| **有条件修改**     | **update 表名 set   字段名=新值,字段名=新值 where 字段=值;** |
|                    |                                                              |
| 查询所有数据       | select * from 表名;                                          |
| 查询部分           | select 字段名1,字段名2…   from 表名;                         |
| 去重查询           | **select distinct 字段名…   from 表名;**                     |
| 结果参与运算       | **select 字段名+固定值 from   表名;**                        |
| 字段间运算         | **select 字段名1+字段名2 别名   from 表名;**                 |
| **null值运算**     | **select 字段名1   ifnull(字段名2,默认值) 别名 from 表名;**  |
| 条件查询           | select 字段名 from 表名   where 条件;  and   or   notnull    |
| **范围查询**       | **select 字段名 from 表名   where 字段名 between 值1 and 值2;** |
| 模糊查询           | select * from 表名   where 字段名 like "通配符字段";    _  % |
| **组合排序**       | **select   字段名 from 表名 where 条件 order by 字段名1 asc/desc,字段名2 asc/desc;** |
| 聚合函数           | select   聚合函数(字段名) from 表名;select 聚合函数 from 表名; |
| **聚合函数**       | count(*) 计数    ifnull (字段,替换为)     sum(*)求和      max (*)      最大值                             min(*) 最小值      avg(*)平均值             cast(avg(字段名)as decimal(5,2))保留几位小数 |
| **分组**           | **select   字段名 from 表名 where 条件 group by 字段名 having 条件;** |
| **limit分页**      | **select   字段名 from 表名 where语句 group by语句 having语句 order by语句 limit 开始条目，每页条目;** |

# 多表查询

| 隐内连 | select 字段名   from 表1,表2 where 条件                      |
| ------ | ------------------------------------------------------------ |
| 显内连 | select   字段名 from 表1 join 表2 on 条件                    |
| 左外连 | select   字段名 from 表1 left join 表2 on 条件(以表1为主，表2没内容填null) |
| 右外连 | select   字段名 from 表1 right join 表2 on 条件(以表2为主，表1没内容填null) |

## 子查询

| 单列单行 | 结果作为筛选条件，放在where后面 |
| -------- | ------------------------------- |
| 单列多行 | 结果作为筛选条件，放在where后面 |
| 多列多行 | 结果作为查询的表，放在from后面  |

## 事务

| 开启     | start   transaction 开启手动事务，不提交和回滚事务不真正执行，而是放到缓存区 |
| -------- | ------------------------------------------------------------ |
| 提交     | commit将缓存区中的事务统一执行                               |
| 回滚     | rollback回到事务语句开始时的状态                             |
| 回滚点   | savepoint   回滚点名字，回到回滚点语法：rollback to 回滚点名 |
| 查询     | show   variables like "%commit%"                             |
| 关闭自动 | set   autocommit = 0,设置为1为自动                           |

## 事务的特性

| 1原子性 | 事务不可分割，一个事务中的操作要么都发生，要么都不发生       |
| ------- | ------------------------------------------------------------ |
| 2一致性 | 事务前后数据的完整性必须保持一致                             |
| 3隔离性 | 多用户并发访问数据库时，一个用户的事务不能呗其他用户的事务所干扰，多个并发事务之间要相互格力，不能互相影响 |
| 4持久性 | 一个事物一旦提交，对数据库中的改变是永久性的，接下来数据库发生故障也不会对其有任何影响 |



## 隔离级别

| 读未提交 | read   uncommitted 隔离级别最低，效率最高       |
| -------- | ----------------------------------------------- |
| 读已提交 | read   committed 避免脏读，Oracle 和 SQL Server |
| 可重复读 | repeatable   read 避免不可重复读 MySQL          |
| 串行化   | serializable   可避免一切并发访问问题，效率最低 |

| 查询 | show variables   like "%isolation%"           |
| ---- | --------------------------------------------- |
| 设置 | set   global transaction isolation level 级别 |



概念

| **一对一** | **操作多的表加外键**                                         |
| ---------- | ------------------------------------------------------------ |
| **一对多** | **多表加外键**                                               |
| **多对多** | **建立中间表，两个外键**                                     |
|            |                                                              |
| 外键约束   | 从表的某个字段引用主表的主键（外键可以重复）                 |
| **建表时** | **constraint   外键名 foreign key(外键字段） references 主表名(主表主键)** |
| **后增加** | **alter   table 从表 add constraint 外键名 foreign key(外键字段)references 主表(主表主键)** |
| 外键删除   | alter   table 从表 drop foreign key 外键名                   |
|            |                                                              |
| **第一**   | **每个字段不可再拆分**                                       |
| **第二**   | **表内有主键，一张表只描述一件事**                           |
| **第三**   | **从表的外键必须使用主表的主键**                             |
|            |                                                              |
| 产生       | 查询多个表时，会把每个表数据与另一个表数据一一对应产生新的表 |
| 消除       | 找到两个表的关联条件并进行筛选                               |



# 用户权限

| 创建用户       | create user   '用户名'@'主机名' identified by '密码';        |
| -------------- | ------------------------------------------------------------ |
| 查询权限       | show   grants for '用户名'@'主机名'                          |
| 授权用户       | grant   create,alter,drop,insert,update,delete,select on 数据库名.表名 to   '用户名'@'主机名';(可以用all代表所有权限，*.*代表所有数据库和所有表) |
| 撤销授权       | revoke   权限1,… on 数据库名.表名 from '用户名'@'主机名'(可以用all代表所有权限，*.*代表所有数据库和所有表) |
| 删除用户       | drop   user '用户名'@'主机名';                               |
| 修改普通密码   | set   password for '用户名'@'主机名' = password('新密码');   |
| 修改管理员密码 | 先退出登录，mysqladmin   -uroot -p password 新密码(没有引号)                按提示输入旧密码 |


