### 一、初始化和安装服务

```bash
# 备注：已配置好mysql环境变量

# 删除mysql安装位置中的data文件夹，执行以下命令会初始化并打印root用户的密码
mysqld --initialize --console
# 如果服务中没有mysql server，则在管理员权限下运行一下命令，会创建服务
mysqld install
```

### 二、修改密码

```mysql
alter user 'root'@'localhost' identified '新密码';
```

### 三、数据库

```mysql
# 展示所有数据库
show databases;
# 创建数据库
create database 数据库名;
# 切换数据库
use 数据库名;
# 查看当前正在使用的数据库
select database();
# 删除数据库
drop database [if exists] 数据库名;
```

### 四、数据类型

1. 数值类型

| 类型         | 大小                                     | 范围（有符号）                                               | 范围（无符号）                                               | 用途            |
| ------------ | ---------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | --------------- |
| TINYINT      | 1 Bytes                                  | (-128，127)                                                  | (0，255)                                                     | 小整数值        |
| SMALLINT     | 2 Bytes                                  | (-32 768，32 767)                                            | (0，65 535)                                                  | 大整数值        |
| MEDIUMINT    | 3 Bytes                                  | (-8 388 608，8 388 607)                                      | (0，16 777 215)                                              | 大整数值        |
| INT或INTEGER | 4 Bytes                                  | (-2 147 483 648，2 147 483 647)                              | (0，4 294 967 295)                                           | 大整数值        |
| BIGINT       | 8 Bytes                                  | (-9,223,372,036,854,775,808，9 223 372 036 854 775 807)      | (0，18 446 744 073 709 551 615)                              | 极大整数值      |
| FLOAT        | 4 Bytes                                  | (-3.402 823 466 E+38，-1.175 494 351 E-38)，0，(1.175 494 351 E-38，3.402 823 466 351 E+38) | 0，(1.175 494 351 E-38，3.402 823 466 E+38)                  | 单精度 浮点数值 |
| DOUBLE       | 8 Bytes                                  | (-1.797 693 134 862 315 7 E+308，-2.225 073 858 507 201 4 E-308)，0，(2.225 073 858 507 201 4 E-308，1.797 693 134 862 315 7 E+308) | 0，(2.225 073 858 507 201 4 E-308，1.797 693 134 862 315 7 E+308) | 双精度 浮点数值 |
| DECIMAL      | 对DECIMAL(M,D) ，如果M>D，为M+2否则为D+2 | 依赖于M和D的值                                               | 依赖于M和D的值                                               | 小数值          |

2. 日期和时间类型

| 类型      | 大小(bytes) | 范围                                                         | 格式                | 用途                     |
| --------- | ----------- | ------------------------------------------------------------ | ------------------- | ------------------------ |
| DATE      | 3           | 1000-01-01/9999-12-31                                        | YYYY-MM-DD          | 日期值                   |
| TIME      | 3           | '-838:59:59'/'838:59:59'                                     | HH:MM:SS            | 时间值或持续时间         |
| YEAR      | 1           | 1901/2155                                                    | YYYY                | 年份值                   |
| DATETIME  | 8           | '1000-01-01 00:00:00' 到 '9999-12-31 23:59:59'               | YYYY-MM-DD hh:mm:ss | 混合日期和时间值         |
| TIMESTAMP | 4           | '1970-01-01 00:00:01' UTC 到 '2038-01-19 03:14:07' UTC结束时间是第 **2147483647** 秒，北京时间 **2038-1-19 11:14:07**，格林尼治时间 2038年1月19日 凌晨 03:14:07 | YYYY-MM-DD hh:mm:ss | 混合日期和时间值，时间戳 |

3. 字符串类型

| 类型       | 大小（bytes）   | 用途                            |
| ---------- | --------------- | ------------------------------- |
| CHAR       | 0-255           | 定长字符串                      |
| VARCHAR    | 0-65535         | 变长字符串                      |
| TINYBLOB   | 0-255           | 不超过 255 个字符的二进制字符串 |
| TINYTEXT   | 0-255           | 短文本字符串                    |
| BLOB       | 0-65 535        | 二进制形式的长文本数据          |
| TEXT       | 0-65 535        | 长文本数据                      |
| MEDIUMBLOB | 0-16 777 215    | 二进制形式的中等长度文本数据    |
| MEDIUMTEXT | 0-16 777 215    | 中等长度文本数据                |
| LONGBLOB   | 0-4 294 967 295 | 二进制形式的极大文本数据        |
| LONGTEXT   | 0-4 294 967 295 | 极大文本数据                    |

> **注意**：**char(n)** 和 **varchar(n)** 中括号中 n 代表字符的个数，并不代表字节个数，比如 CHAR(30) 就可以存储 30 个字符。

4. 枚举和集合类型
   - **ENUM**: 枚举类型，用于存储单一值，可以选择一个预定义的集合。
   - **SET**: 集合类型，用于存储多个值，可以选择多个预定义的集合。

5. 空间数据类型

   GEOMETRY, POINT, LINESTRING, POLYGON, MULTIPOINT, MULTILINESTRING, MULTIPOLYGON, GEOMETRYCOLLECTION: 用于存储空间数据（地理信息、几何图形等）。

### 五、数据表

```mysql
# 创建数据表
# table_name: 表名
# column: 列名
# dataType: 数据类型
create table table_name (
	column1 datatype,
    column2 datatype,
    ...
);

# 查询数据表列表
show tables;

# 删除数据表
drop table [if exists] 表名;
```

### 六、查询数据 

```mysql
# 查询数据表的特定列
select column1, column2, ... from 数据表名;
# 查询数据表所有数据
select * from 数据表名;
```

### 七、插入数据

```mysql
insert into 数据表名 (column1, column2, ...)
values (value1, value2, ...), (value1, value2, ...), ...;
```

### 八、where子句

```mysql
select * 数据表 where 条件; # 默认不区分大小写
select * 数据表 where binary 条件; # 区分大小写

# where子句可用于select、update、delete等命令
```

| 操作符 | 描述                                                         | 实例                 |
| ------ | ------------------------------------------------------------ | -------------------- |
| =      | 等号，检测两个值是否相等，如果相等返回true                   | (A = B) 返回false。  |
| <>, != | 不等于，检测两个值是否相等，如果不相等返回true               | (A != B) 返回 true。 |
| >      | 大于号，检测左边的值是否大于右边的值, 如果左边的值大于右边的值返回true | (A > B) 返回false。  |
| <      | 小于号，检测左边的值是否小于右边的值, 如果左边的值小于右边的值返回true | (A < B) 返回 true。  |
| >=     | 大于等于号，检测左边的值是否大于或等于右边的值, 如果左边的值大于或等于右边的值返回true | (A >= B) 返回false。 |
| <=     | 小于等于号，检测左边的值是否小于或等于右边的值, 如果左边的值小于或等于右边的值返回true | (A <= B) 返回 true。 |

```mysql
# 组合条件and、or
# 查询年龄大于等于12的男生
select * students from where age>='12' and sex='男';
# 查询年龄大于12或等于10的学生
select * students from where age>='12' or age='10';

# in
# 查询年龄等于12、13、14中任意一个的学生
select * students from where age in ('12', '13', '14');

# not
# 查询性别不是男的学生
select * students from where not sex='男';

# between
# 查询年龄在12-15之间的学生
select * students from where age between '12' and '15';

# is null
# 查询生日数据为null的学生
select * students from birthdate is null;

# is null
# 查询存在生日数据的学生
select * students from birthdate is not null;
```

### 九、更新数据

```mysql
update 数据表名
set column1=value1, column2=value2, ...
[where 条件];
```

### 十、删除数据

```mysql
delete from 数据表名 [where 条件];
```

### 十一、like子句

- **LIKE** 子句是在 MySQL 中用于在 WHERE 子句中进行模糊匹配的关键字。它通常与通配符一起使用，用于搜索符合某种模式的字符串。

- **LIKE** 子句中使用百分号 **%**字符来表示任意字符，类似于UNIX或正则表达式中的星号 *****。

- 如果没有使用百分号 **%**, LIKE 子句与等号 **=** 的效果是一样的。

- 除了**%**，还有通配符下划线**_**，表示一个字符。

```mysql
# 查询姓赵的学生
select * from students where name like '赵%';
# 查询名字中第二个字是‘子’的学生
select * from students where name like '_子%';
```

###  十二、union操作符

- **UNION**操作符用于连接两个以上的 SELECT 语句的结果组合到一个结果集合，并去除重复的行。

- **UNION**操作符必须由两个或多个 SELECT 语句组成，每个 SELECT 语句的列数和对应位置的数据类型必须相同。

- **UNION ALL**不会去除重复行。

```mysql
# 查询年龄为11或12的学生
select * from students where age='11'
union
select * from students where age='12';
```

### 十三、order by（排序）语句

**ORDER BY(排序)** 语句可以按照一个或多个列的值进行升序（**ASC**）或降序（**DESC**）排序。

```mysql
# 按年龄降序查询学生
select * from students order by age desc;
```

### 十四、group by语句

- **GROUP BY** 语句根据一个或多个列对结果集进行分组。

- 在分组的列上我们可以使用 COUNT, SUM, AVG,等函数。

- **GROUP BY **语句是 SQL 查询中用于汇总和分析数据的重要工具，尤其在处理大量数据时，它能够提供有用的汇总信息。

```mysql
# 根据客户id对订单表进行分组，查询客户id和客户的总消费
select customer_id, sum(order_amount) as total_amount
from orders
group by customer_id [with rollup];

# 不使用with rollup
+-------------+--------------+
| customer_id | total_amount |
+-------------+--------------+
| 00001       |         1900 |
| 00003       |         3330 |
| 00004       |         5000 |
| 00005       |         2000 |
+-------------+--------------+

# 使用with rollup
+-------------+--------------+
| customer_id | total_amount |
+-------------+--------------+
| 00001       |         1900 |
| 00003       |         3330 |
| 00004       |         5000 |
| 00005       |         2000 |
| NULL        |        12230 |
+-------------+--------------+

# 其中with rollup会在分组统计数据的基础上再次进行相同的统计，统计列之外的其它列为null
# 注：with rollup不能和order by同时使用
# 可以使用 coalesce 来设置一个可以取代 NUll 的名称，语法如下：
select coalesce(a,b,c);
# 参数说明：如果 a==null，则选择 b；如果 b==null,则选择 c；如果 a!=null,则选择 a；如果 a b c 都为 null ，则返回为 null（没意义）。

select coalesce(customer_id, '总消费'), sum(order_amount) as total_amount
from orders
group by customer_id with rollup;

+---------------------------------+--------------+
| coalesce(customer_id, '总消费')  | total_amount |
+---------------------------------+--------------+
| 00001                           |         1900 |
| 00003                           |         3330 |
| 00004                           |         5000 |
| 00005                           |         2000 |
| 总消费                           |        12230 |
+---------------------------------+--------------+
```

### 十五、连接

- **INNER JOIN（内连接,或等值连接）**：获取两个表中字段匹配关系的记录。

- **LEFT JOIN（左连接）：**获取左表所有记录，即使右表没有对应匹配的记录。
- **RIGHT JOIN（右连接）：** 与 LEFT JOIN 相反，用于获取右表所有记录，即使左表没有对应匹配的记录。

```mysql
# orders表
+----------+-------------+------------+--------------+
| order_id | customer_id | order_date | order_amount |
+----------+-------------+------------+--------------+
|        1 | 00001       | 2020-05-23 |          500 |
|        2 | 00005       | 2018-10-05 |         2000 |
|        3 | 00003       | 2020-12-04 |          800 |
|        4 | 00001       | 2020-10-06 |         1200 |
|        5 | 00004       | 2022-08-26 |         5000 |
|        6 | 00001       | 2021-05-30 |          200 |
|        7 | 00003       | 2023-09-16 |         2530 |
+----------+-------------+------------+--------------+

# customers表
+-------------+---------------+
| customer_id | customer_name |
+-------------+-------------- +
| 00001       | 小明          |
| 00002       | 小胖          |
| 00003       | 小红          |
| 00004       | 小丽          |
| 00005       | 小文          |
| 00006       | 小亮          |
+-------------+---------------+

# INNER JOIN 返回两个表中满足连接条件的匹配行
# 查询orders表，连接customers表，根据customer_id，展示对应的customer_name
select order_id, customers.customer_name, order_date, order_amount from orders
inner join customers on customers.customer_id = orders.customer_id;
+----------+---------------+------------+--------------+
| order_id | customer_name | order_date | order_amount |
+----------+---------------+------------+--------------+
|        1 | 小明          | 2020-05-23 |          500 |
|        2 | 小文          | 2018-10-05 |         2000 |
|        3 | 小红          | 2020-12-04 |          800 |
|        4 | 小明          | 2020-10-06 |         1200 |
|        5 | 小丽          | 2022-08-26 |         5000 |
|        6 | 小明          | 2021-05-30 |          200 |
|        7 | 小红          | 2023-09-16 |         2530 |
+----------+---------------+------------+--------------+

# LEFT JOIN 返回左表的所有行，并包括右表中匹配的行，如果右表中没有匹配的行，将返回 NULL 值
select order_id, customers.customer_name, order_date, order_amount from orders
left join customers on customers.customer_id = orders.customer_id;
+----------+---------------+------------+--------------+
| order_id | customer_name | order_date | order_amount |
+----------+---------------+------------+--------------+
|        1 | 小明          | 2020-05-23 |          500 |
|        2 | 小文          | 2018-10-05 |         2000 |
|        3 | 小红          | 2020-12-04 |          800 |
|        4 | 小明          | 2020-10-06 |         1200 |
|        5 | 小丽          | 2022-08-26 |         5000 |
|        6 | 小明          | 2021-05-30 |          200 |
|        7 | 小红          | 2023-09-16 |         2530 |
+----------+---------------+------------+--------------+

# RIGHT JOIN 返回右表的所有行，并包括左表中匹配的行，如果左表中没有匹配的行，将返回 NULL 值
select order_id, customers.customer_name, order_date, order_amount from orders
right join customers on customers.customer_id = orders.customer_id;
+----------+---------------+------------+--------------+
| order_id | customer_name | order_date | order_amount |
+----------+---------------+------------+--------------+
|        6 | 小明          | 2021-05-30 |          200 |
|        4 | 小明          | 2020-10-06 |         1200 |
|        1 | 小明          | 2020-05-23 |          500 |
|     NULL | 小胖          | NULL       |         NULL |
|        7 | 小红          | 2023-09-16 |         2530 |
|        3 | 小红          | 2020-12-04 |          800 |
|        5 | 小丽          | 2022-08-26 |         5000 |
|        2 | 小文          | 2018-10-05 |         2000 |
|     NULL | 小亮          | NULL       |         NULL |
+----------+---------------+------------+--------------+
```

### 十六、null值处理

- **IS NULL:** 当列的值是 NULL,此运算符返回 true。
- **IS NOT NULL:** 当列的值不为 NULL, 运算符返回 true。
- **<=>:** 比较操作符（不同于 = 运算符），当比较的的两个值相等或者都为 NULL 时返回 true。

### 十七、正则表达式

| 模式       | 描述                                                         |
| ---------- | ------------------------------------------------------------ |
| ^          | 匹配输入字符串的开始位置。如果设置了 RegExp 对象的 Multiline 属性，^ 也匹配 '\n' 或 '\r' 之后的位置。 |
| $          | 匹配输入字符串的结束位置。如果设置了RegExp 对象的 Multiline 属性，$ 也匹配 '\n' 或 '\r' 之前的位置。 |
| .          | 匹配除 "\n" 之外的任何单个字符。要匹配包括 '\n' 在内的任何字符，请使用像 '[.\n]' 的模式。 |
| [...]      | 字符集合。匹配所包含的任意一个字符。例如， '[abc]' 可以匹配 "plain" 中的 'a'。 |
| [^...]     | 负值字符集合。匹配未包含的任意字符。例如， '[^abc]' 可以匹配 "plain" 中的'p'。 |
| p1\|p2\|p3 | 匹配 p1 或 p2 或 p3。例如，'z\|food' 能匹配 "z" 或 "food"。'(z\|f)ood' 则匹配 "zood" 或 "food"。 |
| *          | 匹配前面的子表达式零次或多次。例如，zo* 能匹配 "z" 以及 "zoo"。* 等价于{0,}。 |
| +          | 匹配前面的子表达式一次或多次。例如，'zo+' 能匹配 "zo" 以及 "zoo"，但不能匹配 "z"。+ 等价于 {1,}。 |
| ?          | 匹配零个或一个前面的元素。                                   |
| {n}        | n 是一个非负整数。匹配确定的 n 次。例如，'o{2}' 不能匹配 "Bob" 中的 'o'，但是能匹配 "food" 中的两个 o。 |
| {n,m}      | m 和 n 均为非负整数，其中n <= m。最少匹配 n 次且最多匹配 m 次。 |
| \w         | 匹配一个字母数字字符（包括下划线）。                         |
| \s         | 匹配一个空白字符。                                           |

```mysql
# user表
+----+----------+--------------------+------------+-----------+
| id | username | email              | birthdate  | is_active |
+----+----------+--------------------+------------+-----------+
|  1 | xiaoming | xiaoming@qq.com    | 2000-06-10 |         1 |
|  2 | xiaohong | xiaohong@gmail.com | NULL       |         0 |
|  3 | xiaogang | xiaogang@qq.com    | 2001-10-05 |         1 |
+----+----------+--------------------+------------+-----------+

select * from user where email regexp '@qq.com$';
+----+----------+-----------------+------------+-----------+
| id | username | email           | birthdate  | is_active |
+----+----------+-----------------+------------+-----------+
|  1 | xiaoming | xiaoming@qq.com | 2000-06-10 |         1 |
|  3 | xiaogang | xiaogang@qq.com | 2001-10-05 |         1 |
+----+----------+-----------------+------------+-----------+
```

### 十八、事务

MySQL 事务主要用于处理操作量大，复杂度高的数据。比如说，在人员管理系统中，你删除一个人员，你既需要删除人员的基本资料，也要删除和该人员相关的信息，如信箱，文章等等，这样，这些数据库操作语句就构成一个事务！

在 MySQL 中，事务是一组SQL语句的执行，它们被视为一个单独的工作单元。

- 在 MySQL 中只有使用了 Innodb 数据库引擎的数据库或表才支持事务。
- 事务处理可以用来维护数据库的完整性，保证成批的 SQL 语句要么全部执行，要么全部不执行。
- 事务用来管理 **insert、update、delete** 语句

一般来说，事务是必须满足4个条件（ACID）：：原子性（**A**tomicity，或称不可分割性）、一致性（**C**onsistency）、隔离性（**I**solation，又称独立性）、持久性（**D**urability）。

- **原子性：**一个事务（transaction）中的所有操作，要么全部完成，要么全部不完成，不会结束在中间某个环节。事务在执行过程中发生错误，会被回滚（Rollback）到事务开始前的状态，就像这个事务从来没有执行过一样。
- **一致性：**在事务开始之前和事务结束以后，数据库的完整性没有被破坏。这表示写入的资料必须完全符合所有的预设规则，这包含资料的精确度、串联性以及后续数据库可以自发性地完成预定的工作。
- **隔离性：**数据库允许多个并发事务同时对其数据进行读写和修改的能力，隔离性可以防止多个事务并发执行时由于交叉执行而导致数据的不一致。事务隔离分为不同级别，包括读未提交（Read uncommitted）、读提交（read committed）、可重复读（repeatable read）和串行化（Serializable）。
- **持久性：**事务处理结束后，对数据的修改就是永久的，即便系统故障也不会丢失。

> *在 MySQL 命令行的默认设置下，事务都是自动提交的，即执行 SQL 语句后就会马上执行 COMMIT 操作。因此要显式地开启一个事务务须使用命令 BEGIN 或 START TRANSACTION，或者执行命令 SET AUTOCOMMIT=0，用来禁止使用当前会话的自动提交*



**事务控制语句：**

- BEGIN 或 START TRANSACTION 显式地开启一个事务；
- COMMIT 也可以使用 COMMIT WORK，不过二者是等价的。COMMIT 会提交事务，并使已对数据库进行的所有修改成为永久性的；
- ROLLBACK 也可以使用 ROLLBACK WORK，不过二者是等价的。回滚会结束用户的事务，并撤销正在进行的所有未提交的修改；
- SAVEPOINT identifier，SAVEPOINT 允许在事务中创建一个保存点，一个事务中可以有多个 SAVEPOINT；
- RELEASE SAVEPOINT identifier 删除一个事务的保存点，当没有指定的保存点时，执行该语句会抛出一个异常；
- ROLLBACK TO identifier 把事务回滚到标记点；
- SET TRANSACTION 用来设置事务的隔离级别。InnoDB 存储引擎提供事务的隔离级别有READ UNCOMMITTED、READ COMMITTED、REPEATABLE READ 和 SERIALIZABLE。



```mysql
# customers表
+-------------+---------------+
| customer_id | customer_name |
+-------------+---------------+
| 00001       | 小明          |
| 00002       | 小胖          |
| 00003       | 小红          |
| 00004       | 小丽          |
| 00005       | 小文          |
| 00006       | 小亮          |
+-------------+---------------+

begin;
insert into customers (customer_id, customer_name) values('00007', '小雨');
update customers set customer_name='小明_update' where customer_id='00001';
rollback;
select * from customers;
+-------------+---------------+
| customer_id | customer_name |
+-------------+---------------+
| 00001       | 小明          |
| 00002       | 小胖          |
| 00003       | 小红          |
| 00004       | 小丽          |
| 00005       | 小文          |
| 00006       | 小亮          |
+-------------+---------------+

begin;
insert into customers (customer_id, customer_name) values('00007', '小雨');
update customers set customer_name='小明_update' where customer_id='00001';
commit;
select * from customers;
+-------------+---------------+
| customer_id | customer_name |
+-------------+---------------+
| 00001       | 小明_update   |
| 00002       | 小胖          |
| 00003       | 小红          |
| 00004       | 小丽          |
| 00005       | 小文          |
| 00006       | 小亮          |
| 00007       | 小雨          |
+-------------+---------------+
```

### 十九、alter

MySQL 的 **ALTER** 命令用于修改数据库、表和索引等对象的结构。

**ALTER** 命令允许你添加、修改或删除数据库对象，并且可以用于更改表的列定义、添加约束、创建和删除索引等操作。

```mysql
# 添加列
alter table table_name
add column new_column_name datatype;

# 修改列的数据类型
alter table table_name
modify column column_name new_datatype;

# 修改列名、同时修改数据类型
alter table table_name
change column old_column_name new_column_name datetype;

# 删除列
alter table table_name
drop column column_name;

# 添加主键
alter table table_name
add primary key (column);

# 添加外键，为table_name添加列column_name作为外键，外键名为fk_name，与表table_name2的列column_name2进行关联
alter table table_name
add constraint fk_name
foreign key column_name
references table_name2 (column_name2);

# 修改表名
alter table table_name
rename to new_table_name;
```

### 二十、索引

MySQL 索引是一种数据结构，用于加快数据库查询的速度和性能。

MySQL 索引的建立对于 MySQL 的高效运行是很重要的，索引可以大大提高 MySQL 的检索速度。

> MySQL 索引类似于书籍的索引，通过存储指向数据行的指针，可以快速定位和访问表中的特定数据。
>
> 打个比方，如果合理的设计且使用索引的 MySQL 是一辆兰博基尼的话，那么没有设计和使用索引的 MySQL 就是一个人力三轮车。
>
> 拿汉语字典的目录页（索引）打比方，我们可以按拼音、笔画、偏旁部首等排序的目录（索引）快速查找到需要的字。

索引分单列索引和组合索引：

- 单列索引，即一个索引只包含单个列，一个表可以有多个单列索引。
- 组合索引，即一个索引包含多个列。

创建索引时，你需要确保该索引是应用在 SQL 查询语句的条件(一般作为 WHERE 子句的条件)。

实际上，索引也是一张表，该表保存了主键与索引字段，并指向实体表的记录。

索引虽然能够提高查询性能，但也需要注意以下几点：

- 索引需要占用额外的存储空间。
- 对表进行插入、更新和删除操作时，索引需要维护，可能会影响性能。
- 过多或不合理的索引可能会导致性能下降，因此需要谨慎选择和规划索引。

**1. 普通索引**

索引能够显著提高查询的速度，尤其是在大型表中进行搜索时。通过使用索引，MySQL 可以直接定位到满足查询条件的数据行，而无需逐行扫描整个表。

```mysql
# 创建索引
create index index_name
on table_name (column1 [asc|desc], column2 [asc|desc], ...);

# 使用alter修改表结构创建索引
alter table table_name
add index index_name (column1 [asc|desc], column2 [asc|desc], ...);

# 创建表时直接指定
create table table_name(
	column1 datetype,
    column2 datatype,
    ...,
    index index_name (column1 [asc|desc], column2 [asc|desc], ...);
);

# 删除索引
drop index index_name on table_name;
alter table table_name drop index index_name;
```

**2. 唯一索引**

在 MySQL 中，你可以使用 **CREATE UNIQUE INDEX** 语句来创建唯一索引。

唯一索引确保索引中的值是唯一的，不允许有重复值（除了null外，null可能会出现多次）。

```mysql
# 创建索引
create unique index index_name
on table_name (column1 [asc|desc], column2 [asc|desc], ...);

# 使用alter创建唯一索引
alter table table_name
add constraint index_name unique (column1 [asc|desc], column2 [asc|desc], ...);

alter table table_name
add unique index_name (column1 [asc|desc], column2 [asc|desc], ...);

# 创建表时直接指定
create table table_name(
	column1 datetype,
    column2 datatype,
    ...,
    constraint index_name unique (column1 [asc|desc], column2 [asc|desc], ...);
);

# 添加主键，索引值唯一，且不能为null
alter table table_name add primary key (column1 [asc|desc], column2 [asc|desc], ...);
```

**3. 补充**

```mysql
# 全文索引，仅限char、varchar、text等类型
alter table table_name add fulltext index_name (column1 [asc|desc], column2 [asc|desc], ...);

# 查看索引信息
# \g为格式化输出信息，显示索引名称（Key_name）、索引列（Column_name）、是否是唯一索引（Non_unique，0唯一，1不唯一）、排序方式（Collation）、索引的基数（Cardinality）等
show index from table_name\g;
```

### 二十一、临时表

临时表是一种在当前会话中存在的表，它在会话结束时会自动被销毁。

```mysql
# 创建临时表
create temporary table teble_name(
	column1 datatype,
    column2 datatype,
    ...
);

# 根据查询结果生成临时表
create temporary table teble_name as
select语句;

# 当临时表和普通表名称相同时，只能查看和操作临时表，删除临时表，普通表可见
# 临时表的查询、插入、更新、删除等表操作与普通表相同

# 手动删除临时表
drop temporary table table_name;
```

### 二十二、复制表

1. 获取数据表的创建语句

```mysql
# 查询表的创建语句
show create table user \g;
# 表的创建语句
| Table | Create Table
| user  | CREATE TABLE `user` (
  `id` int NOT NULL AUTO_INCREMENT,
  `username` varchar(50) NOT NULL,
  `email` varchar(100) NOT NULL,
  `birthdate` date DEFAULT NULL,
  `is_active` tinyint(1) DEFAULT '1',
  PRIMARY KEY (`id`),
  KEY `idx_name` (`username`,`email`)
) ENGINE=InnoDB AUTO_INCREMENT=6 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci |
```

2. 修改SQL语句中的数据表名，执行SQL，创建数据表

```mysql
CREATE TABLE `clone_user` (
  `id` int NOT NULL AUTO_INCREMENT,
  `username` varchar(50) NOT NULL,
  `email` varchar(100) NOT NULL,
  `birthdate` date DEFAULT NULL,
  `is_active` tinyint(1) DEFAULT '1',
  PRIMARY KEY (`id`),
  KEY `idx_name` (`username`,`email`)
) ENGINE=InnoDB AUTO_INCREMENT=6 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
```

3. 通过insert into ... select语句克隆表的数据

```mysql
insert into clone_user (id, username, email, birthdate, is_active)
select id, username, email, birthdate, is_active from user;
```

### 二十三、元数据

元数据是关于数据库和其对象（如表、列、索引等）的信息。

元数据存储在系统表中，这些表位于 MySQL 数据库的 information_schema 数据库中，通过查询这些系统表，你可以获取关于数据库结构、对象和其他相关信息的详细信息。

**常用元数据查询：**

```mysql
# 查看所有数据库
show databases;

# 选择数据库
use database_name;

# 查看数据库中所有的表
show tables;

# 查看表的结构
desc table_name;
show columns from table_name;

# 查看表的索引
show index from table_name;

# 查看表的创建语句
show create table table_name;

# 查看表的行数
select count(*) from table_name;

# 查看列的信息
select COLUMN_NAME, DATA_TYPE, IS_NULLABLE, COLUMN_KEY
from INFORMATION_SCHEMA.COLUMNS
where TABLE_SCHEMA = 'your_database_name'
and TABLE_NAME = 'your_table_name';

# 查看外键信息
select
    TABLE_NAME,
    COLUMN_NAME,
    CONSTRAINT_NAME,
    REFERENCED_TABLE_NAME,
    REFERENCED_COLUMN_NAME
from
    INFORMATION_SCHEMA.KEY_COLUMN_USAGE
where
    TABLE_SCHEMA = 'your_database_name'
    and TABLE_NAME = 'your_table_name'
    and REFERENCED_TABLE_NAME is not NULL;
```



**information_schema 数据库**

information_schema 是 MySQL 数据库中的一个系统数据库，它包含有关数据库服务器的元数据信息，这些信息以表的形式存储在information_schema 数据库中。

1. **SCHEMATA 表**

存储有关数据库的信息，如数据库名、字符集、排序规则等。

```mysql
SELECT * FROM information_schema.SCHEMATA;
```

2. **TABLES 表**

包含有关数据库中所有表的信息，如表名、数据库名、引擎、行数等。

```mysql
SELECT * FROM information_schema.TABLES WHERE TABLE_SCHEMA = 'your_database_name';
```

3. **COLUMNS 表**

包含有关表中列的信息，如列名、数据类型、是否允许 NULL 等。

```mysql
SELECT * FROM information_schema.COLUMNS
WHERE TABLE_SCHEMA = 'your_database_name' AND TABLE_NAME = 'your_table_name';
```

4. **STATISTICS 表**

提供有关表索引的统计信息，如索引名、列名、唯一性等。

```mysql
SELECT * FROM information_schema.STATISTICS
WHERE TABLE_SCHEMA = 'your_database_name' AND TABLE_NAME = 'your_table_name';
```

5. **KEY_COLUMN_USAGE 表**

包含有关表中外键的信息，如外键名、列名、关联表等。

```mysql
SELECT * FROM information_schema.KEY_COLUMN_USAGE
WHERE TABLE_SCHEMA = 'your_database_name' AND TABLE_NAME = 'your_table_name';
```

6. **REFERENTIAL_CONSTRAINTS 表**

存储有关外键约束的信息，如约束名、关联表等。

```mysql
SELECT * FROM information_schema.REFERENTIAL_CONSTRAINTS
WHERE CONSTRAINT_SCHEMA = 'your_database_name' AND TABLE_NAME = 'your_table_name';
```

### 二十四、序列

在 MySQL 中，序列是一种自增生成数字序列的对象，是一组整数 **1、2、3、...**，由于一张数据表只能有一个字段自增主键。

尽管 MySQL 本身并没有内建的序列类型，但可以使用 AUTO_INCREMENT 属性来模拟序列的行为，通常 **AUTO_INCREMENT** 属性用于指定表中某一列的自增性。

```mysql
CREATE TABLE example_table (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(50)
);
```

以上例子中，id 列被定义为 INT AUTO_INCREMENT，这表示每次插入一行数据时，id 列的值会自动增加。主键约束保证了 id 列的唯一性。

当你插入一行数据时，可以不指定 id 列的值，数据库会自动为其分配一个唯一的、自增的值：

```mysql
INSERT INTO example_table (name) VALUES ('John');
```

你也可以使用 LAST_INSERT_ID() 函数来获取刚刚插入的行的自增值：

```mysql
SELECT LAST_INSERT_ID();
```

如果你需要获取表的当前自增值，可以使用以下语句：

```mysql
SHOW TABLE STATUS LIKE 'example_table';
```

在结果集中，Auto_increment 列的值即为当前表的自增值。

> *请注意，使用 AUTO_INCREMENT 属性的列只能是整数类型（通常是 INT 或 BIGINT）。此外，如果你删除表中的某一行，其自增值不会被重新使用，而是会继续递增。如果你希望手动设置自增值，可以使用 SET 语句，但这不是一种常规的做法，因为可能引起唯一性冲突。*



一般情况下序列的开始值为 1，但如果你需要指定一个开始值 100，那我们可以通过以下语句来实现：

```mysql
CREATE TABLE insect (
	id INT UNSIGNED NOT NULL AUTO_INCREMENT,
	PRIMARY KEY (id),
	name VARCHAR(30) NOT NULL, 
	date DATE NOT NULL,
	origin VARCHAR(30) NOT NULL
) engine=innodb auto_increment=100 charset=utf8;
```

或者你也可以在表创建成功后，通过以下语句来实现：

```mysql
ALTER TABLE t AUTO_INCREMENT = 100;
```

### 二十五、处理重复数据

```mysql
# 可以通过设置primary key(主键)或unique(唯一)来保证数据的唯一性
# 设置唯一索引后，插入重复数据会报错
# 表people结构
+------------+---------------+------+-----+---------+-------+
| Field      | Type          | Null | Key | Default | Extra |
+------------+---------------+------+-----+---------+-------+
| first_name | varchar(10)   | NO   | PRI | NULL    |       |
| last_name  | varchar(10)   | NO   | PRI | NULL    |       |
| sex        | enum('0','1') | YES  |     | 1       |       |
+------------+---------------+------+-----+---------+-------+
# 表people数据
+------------+-----------+------+
| first_name | last_name | sex  |
+------------+-----------+------+
| li         | ming      | 0    |
+------------+-----------+------+

# 插入重复数据
insert into people (first_name, last_name, sex) values('li', 'ming', '0');
ERROR 1062 (23000): Duplicate entry 'li-ming' for key 'people.first_name'

# 设置了唯一性后，使用insert ignore into插入数据时，存在重复数据，则跳过该数据,不报错，但提示警告
insert ignore into people (first_name, last_name, sex) values('li', 'ming', '1');
Query OK, 0 rows affected, 1 warning (0.00 sec)

# replace into会删除重复数据，再插入新数据
replace into people (first_name, last_name, sex) values('li', 'ming', '1');
Query OK, 2 rows affected (0.03 sec)
+------------+-----------+------+
| first_name | last_name | sex  |
+------------+-----------+------+
| li         | ming      | 1    |
+------------+-----------+------+


# 表people2数据
+------------+-----------+
| first_name | last_name |
+------------+-----------+
| xiao       | hong      |
| xiao       | hong      |
| xiao       | yu        |
| cheng      | long      |
| xiao       | yu        |
+------------+-----------+

# 统计重复数据
select count(*) as repetitions, first_name, last_name from people2
group by first_name, last_name
having repetitions > 1;
+-------------+------------+-----------+
| repetitions | first_name | last_name |
+-------------+------------+-----------+
|           2 | xiao       | hong      |
|           2 | xiao       | yu        |
+-------------+------------+-----------+

# 过滤重复数据
# 通过distinct过滤
select distinct first_name, last_name from people2;
# 通过group by过滤
select first_name, last_name
from people2
group by first_name, last_name;

# 删除重复数据
# 1.根据过滤数据创建表
create table temp select distinct first_name, last_name from people2;
# 2.删除原来的表
drop table people2;
# 3.修改表名
alter table temp rename to people2;
# 
```

