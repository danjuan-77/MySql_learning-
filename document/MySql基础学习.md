# SQL（相关术语）

### 数据库database

> 有组织的存储数据的容器，通常是一个文件或者一组文件

### 表table

> 存储数据的文件称为表，表是某种特定数据的结构化清单。
> 
> 表可以保存顾客清单、产品目录，或者其他信息清单。

要注意的是，数据库中，每个表都具有唯一的名称来标识自己。

### 模式schema

> 关于数据库和表的布局及特性信息

### 列colum，数据类型datatype

所有的表都是由一个或者多个列组成的，每个列中存储的是特定的数据类型，特定的数据类型表示特定类型的信息。也被称为字段

### 行 row

表中的数据是按行存储的，而一行就代表一个记录。

比如说顾客表中，每一列分别代表着顾客的姓名，年龄等特定类型的信息，而每一行则代表着一个顾客的信息，行数就代表着记录的总数。

### 主键primary key

主键是一列数据中的值，这列数据中没有重复的数据出现，他的值是区分每一行数据的唯一标识，我们通过主键就能保证每一行的数据的唯一性。

### 外键 foreign key

通过外键来关联两个表

### 复合键composite key

复合键（组合键）将多个列作为一个索引键，一般用于复合索引。

### 索引 index

使用索引可快速访问数据库表中的特定信息。索引是对数据库表中一列或多列的值进行排序的一种结构。<u>类似于书籍的目录</u>。

### 表头header

每一列的名称

### 值 value

行的具体信息，每个值都应该与自己所在列的数据类型相同

### 键 key

键的值在当前列具有唯一值

# MySQL

## 常用命令

==注意在mysql中使用的命令需要用英文分号结尾（启动/关闭mysql服务不需要带分号）==

* `net start mysql` 启动mysql服务（需要管理员启动cmd）

* `net stop mysql`关闭mysql服务（需要管理员启动cmd）

* `mysql -u root -p 123456` 登录mysql

* `exit `退出mysql

* `show databases` 查看数据库

* `use database_name` 使用某个数据库

* `create database database_name` 创建一个数据库

* `show tables` 查看数据库中的表

* `select version()` 查看MySql版本号

* `select database()` 查看当前是使用哪个数据库

## SQL语言分类

SQL语言有很多类：

* `DQL` 数据查询语言（带有select的语句）

* `DML` 数据操作语言
  
  * insert 增加数据
  * delete 删除数据
  * update 修改数据

* `DDL` 数据定义语言
  
  * create 新建
  * drop 删除
  * alter 修改
  
  **<u>DDL的增删改和DML的增删改不一样，DDL的增删改是对表的结构进行增删改，而DML的增删改是对表中的数据进行增删改。</u>**

* `TCL `事务控制语言
  
  * commit 事务提交
  * rollback 事务回滚

* `DCL` 数据控制语言
  
  * grant 授权
  * revoke 撤销权限

# DQL

## 导入数据

首先使用`use database`进入数据库中，然后使用命令

```mysql
source D:\mysql_learning\mysql_learning\document\bjpowernode.sql
```

注意文件名不能有双引号，命令结尾没有分号。

## SQL脚本

`.sql`文件是SQL脚本文件，它里面的内容都是SQL语句，当调用这个文件的时候就会执行文件里面的所有语句。

批量的执行SQL语句，可以使用sql脚本文件。

在mysql当中怎么执行sql脚本呢？

```mysql
sourse 脚本路径
```

你在实际的工作中，第一天到了公司，项目经理会给你一个xxx.sql文件，你执行这个脚本文件，你电脑上的数据库数据就有了！

## 查看表结构

```mysql
mysql> show tables;
+------------------------+
| Tables_in_bjpowernnode |
+------------------------+
| dept                   |
| emp                    |
| salgrade               |
+------------------------+
```

### 查看表中的数据

```mysql
select * from 表名;
```

```mysql
mysql> select * from emp;
+-------+--------+-----------+------+------------+---------+---------+--------+
| EMPNO | ENAME  | JOB       | MGR  | HIREDATE   | SAL     | COMM    | DEPTNO |
+-------+--------+-----------+------+------------+---------+---------+--------+
|  7369 | SMITH  | CLERK     | 7902 | 1980-12-17 |  800.00 |    NULL |     20 |
|  7499 | ALLEN  | SALESMAN  | 7698 | 1981-02-20 | 1600.00 |  300.00 |     30 |
|  7521 | WARD   | SALESMAN  | 7698 | 1981-02-22 | 1250.00 |  500.00 |     30 |
|  7566 | JONES  | MANAGER   | 7839 | 1981-04-02 | 2975.00 |    NULL |     20 |
|  7654 | MARTIN | SALESMAN  | 7698 | 1981-09-28 | 1250.00 | 1400.00 |     30 |
|  7698 | BLAKE  | MANAGER   | 7839 | 1981-05-01 | 2850.00 |    NULL |     30 |
|  7782 | CLARK  | MANAGER   | 7839 | 1981-06-09 | 2450.00 |    NULL |     10 |
|  7788 | SCOTT  | ANALYST   | 7566 | 1987-04-19 | 3000.00 |    NULL |     20 |
|  7839 | KING   | PRESIDENT | NULL | 1981-11-17 | 5000.00 |    NULL |     10 |
|  7844 | TURNER | SALESMAN  | 7698 | 1981-09-08 | 1500.00 |    0.00 |     30 |
|  7876 | ADAMS  | CLERK     | 7788 | 1987-05-23 | 1100.00 |    NULL |     20 |
|  7900 | JAMES  | CLERK     | 7698 | 1981-12-03 |  950.00 |    NULL |     30 |
|  7902 | FORD   | ANALYST   | 7566 | 1981-12-03 | 3000.00 |    NULL |     20 |
|  7934 | MILLER | CLERK     | 7782 | 1982-01-23 | 1300.00 |    NULL |     10 |
+-------+--------+-----------+------+------------+---------+---------+--------+
```

### 不看表中的数据，只看表中的结构

```mysql
desc 表名;
```

```mysql
mysql> desc emp;
+----------+-------------+------+-----+---------+-------+
| Field    | Type        | Null | Key | Default | Extra |
+----------+-------------+------+-----+---------+-------+
| EMPNO    | int         | NO   | PRI | NULL    |       |  # varchar就是string
| ENAME    | varchar(10) | YES  |     | NULL    |       |
| JOB      | varchar(9)  | YES  |     | NULL    |       |
| MGR      | int         | YES  |     | NULL    |       |
| HIREDATE | date        | YES  |     | NULL    |       |
| SAL      | double(7,2) | YES  |     | NULL    |       |
| COMM     | double(7,2) | YES  |     | NULL    |       |
| DEPTNO   | int         | YES  |     | NULL    |       |
+----------+-------------+------+-----+---------+-------+
```

## 简单查询

> 简单查询都是和`select`相关的操作，只要是和`select`相关的操作都不会对原表中的数据进行修改，只会进行查询操作。

### 查询一个字段

```mysql
select 字段名 from 表名;
```

### 查询多个字段

```mysql
select 字段名1，字段名2... from 表名;# 用逗号将多个字段名分隔开
```

### 查询所有字段

```mysql
# 一种方式是
select a,b,c,d.... from 表名;
#另外一种方式是
select * from 表名;
```

但是第二种方式一般效率较低，不是很推荐。

```mysql
mysql> select * from emp;
+-------+--------+-----------+------+------------+---------+---------+--------+
| EMPNO | ENAME  | JOB       | MGR  | HIREDATE   | SAL     | COMM    | DEPTNO |
+-------+--------+-----------+------+------------+---------+---------+--------+
|  7369 | SMITH  | CLERK     | 7902 | 1980-12-17 |  800.00 |    NULL |     20 |
|  7499 | ALLEN  | SALESMAN  | 7698 | 1981-02-20 | 1600.00 |  300.00 |     30 |
|  7521 | WARD   | SALESMAN  | 7698 | 1981-02-22 | 1250.00 |  500.00 |     30 |
|  7566 | JONES  | MANAGER   | 7839 | 1981-04-02 | 2975.00 |    NULL |     20 |
|  7654 | MARTIN | SALESMAN  | 7698 | 1981-09-28 | 1250.00 | 1400.00 |     30 |
|  7698 | BLAKE  | MANAGER   | 7839 | 1981-05-01 | 2850.00 |    NULL |     30 |
|  7782 | CLARK  | MANAGER   | 7839 | 1981-06-09 | 2450.00 |    NULL |     10 |
|  7788 | SCOTT  | ANALYST   | 7566 | 1987-04-19 | 3000.00 |    NULL |     20 |
|  7839 | KING   | PRESIDENT | NULL | 1981-11-17 | 5000.00 |    NULL |     10 |
|  7844 | TURNER | SALESMAN  | 7698 | 1981-09-08 | 1500.00 |    0.00 |     30 |
|  7876 | ADAMS  | CLERK     | 7788 | 1987-05-23 | 1100.00 |    NULL |     20 |
|  7900 | JAMES  | CLERK     | 7698 | 1981-12-03 |  950.00 |    NULL |     30 |
|  7902 | FORD   | ANALYST   | 7566 | 1981-12-03 | 3000.00 |    NULL |     20 |
|  7934 | MILLER | CLERK     | 7782 | 1982-01-23 | 1300.00 |    NULL |     10 |
+-------+--------+-----------+------+------------+---------+---------+--------+
14 rows in set (0.00 sec)

mysql> select Job,Sal from emp;
+-----------+---------+
| Job       | Sal     |
+-----------+---------+
| CLERK     |  800.00 |
| SALESMAN  | 1600.00 |
| SALESMAN  | 1250.00 |
| MANAGER   | 2975.00 |
| SALESMAN  | 1250.00 |
| MANAGER   | 2850.00 |
| MANAGER   | 2450.00 |
| ANALYST   | 3000.00 |
| PRESIDENT | 5000.00 |
| SALESMAN  | 1500.00 |
| CLERK     | 1100.00 |
| CLERK     |  950.00 |
| ANALYST   | 3000.00 |
| CLERK     | 1300.00 |
+-----------+---------+
14 rows in set (0.00 sec)
```

### 给查询的列取别名，按照别名来进行显示

```mysql
select 字段名 as 别名 from 表名;
```

```mysql
mysql> select Job,Sal as salary from emp;
+-----------+---------+
| Job       | salary  |
+-----------+---------+
| CLERK     |  800.00 |
| SALESMAN  | 1600.00 |
| SALESMAN  | 1250.00 |
| MANAGER   | 2975.00 |
| SALESMAN  | 1250.00 |
| MANAGER   | 2850.00 |
| MANAGER   | 2450.00 |
| ANALYST   | 3000.00 |
| PRESIDENT | 5000.00 |
| SALESMAN  | 1500.00 |
| CLERK     | 1100.00 |
| CLERK     |  950.00 |
| ANALYST   | 3000.00 |
| CLERK     | 1300.00 |
+-----------+---------+
14 rows in set (0.00 sec)
```

注意，这里的取别名只会对显示的列显示别名的效果，不会对原本的表中的列名进行修改。

同时，`as`关键字是可以被省略的，用空格代替，如果别名中的含有空格，需要用单引号将别名括起来，当然，使用双引号也行，但是`oracle`中不支持双引号进行这样的操作，因此还是统一使用单引号。

### 列参进行数学运算

字段是支持直接进行数学运算的，例如：

```mysql
mysql> select ename, sal * 12 as "year's salary" from emp;
+--------+---------------+
| ename  | year's salary |
+--------+---------------+
| SMITH  |       9600.00 |
| ALLEN  |      19200.00 |
| WARD   |      15000.00 |
| JONES  |      35700.00 |
| MARTIN |      15000.00 |
| BLAKE  |      34200.00 |
| CLARK  |      29400.00 |
| SCOTT  |      36000.00 |
| KING   |      60000.00 |
| TURNER |      18000.00 |
| ADAMS  |      13200.00 |
| JAMES  |      11400.00 |
| FORD   |      36000.00 |
| MILLER |      15600.00 |
+--------+---------------+
14 rows in set (0.01 sec)
```

这样久能实现查看到年薪是多少了，同时还取了个别名。

## 条件查询

> 查询出符合条件的内容

```mysql
select 字段名1，字段名2...
    from 表名 
        where 条件;
```

主要使用的一些条件

* `等于=`

```mysql
mysql> select ename,job,sal from emp where sal=1250;# 找到工资为1250的人
+--------+----------+---------+
| ename  | job      | sal     |
+--------+----------+---------+
| WARD   | SALESMAN | 1250.00 |
| MARTIN | SALESMAN | 1250.00 |
+--------+----------+---------+
2 rows in set (0.00 sec)

# 当然也支持数学运算
mysql> select ename,job,sal from emp where sal*8=10000;
+--------+----------+---------+
| ename  | job      | sal     |
+--------+----------+---------+
| WARD   | SALESMAN | 1250.00 |
| MARTIN | SALESMAN | 1250.00 |
+--------+----------+---------+
2 rows in set (0.00 sec)

#也是支持查找字符串的
mysql> select ename,job,sal from emp where ename='SMITH';
+-------+-------+--------+
| ename | job   | sal    |
+-------+-------+--------+
| SMITH | CLERK | 800.00 |
+-------+-------+--------+
1 row in set (0.00 sec)
```

* `不等于!=或者<>`

```mysql
mysql> select ename,job,sal from emp where sal!=1250;
+--------+-----------+---------+
| ename  | job       | sal     |
+--------+-----------+---------+
| SMITH  | CLERK     |  800.00 |
| ALLEN  | SALESMAN  | 1600.00 |
| JONES  | MANAGER   | 2975.00 |
| BLAKE  | MANAGER   | 2850.00 |
| CLARK  | MANAGER   | 2450.00 |
| SCOTT  | ANALYST   | 3000.00 |
| KING   | PRESIDENT | 5000.00 |
| TURNER | SALESMAN  | 1500.00 |
| ADAMS  | CLERK     | 1100.00 |
| JAMES  | CLERK     |  950.00 |
| FORD   | ANALYST   | 3000.00 |
| MILLER | CLERK     | 1300.00 |
+--------+-----------+---------+
12 rows in set (0.00 sec)
```

* `小于<`
* `大于>`
* `大于等于>=`
* `小于等于<=`

==上面的都是类似的==

* 区间 
  * `between...and... ` 严格的要求左小右大，同时between...and...是闭区间，包括两端的值
  * `() and ()`

```mysql
mysql> select ename,job,sal from emp where sal>=950 and sal<3000;
+--------+----------+---------+
| ename  | job      | sal     |
+--------+----------+---------+
| ALLEN  | SALESMAN | 1600.00 |
| WARD   | SALESMAN | 1250.00 |
| JONES  | MANAGER  | 2975.00 |
| MARTIN | SALESMAN | 1250.00 |
| BLAKE  | MANAGER  | 2850.00 |
| CLARK  | MANAGER  | 2450.00 |
| TURNER | SALESMAN | 1500.00 |
| ADAMS  | CLERK    | 1100.00 |
| JAMES  | CLERK    |  950.00 |
| MILLER | CLERK    | 1300.00 |
+--------+----------+---------+
10 rows in set (0.01 sec)
```

* `is null /is not null`

null在mysql中表示没有，如果用=或者！=表示查找为值为空的，那样是找不到null元素的

```mysql
# is not null
mysql> select ename,job,comm from emp where COMM is not null;
+--------+----------+---------+
| ename  | job      | comm    |
+--------+----------+---------+
| ALLEN  | SALESMAN |  300.00 |
| WARD   | SALESMAN |  500.00 |
| MARTIN | SALESMAN | 1400.00 |
| TURNER | SALESMAN |    0.00 |
+--------+----------+---------+
4 rows in set (0.00 sec)

# is null
mysql> select ename,job,comm from emp where COMM is null;
+--------+-----------+------+
| ename  | job       | comm |
+--------+-----------+------+
| SMITH  | CLERK     | NULL |
| JONES  | MANAGER   | NULL |
| BLAKE  | MANAGER   | NULL |
| CLARK  | MANAGER   | NULL |
| SCOTT  | ANALYST   | NULL |
| KING   | PRESIDENT | NULL |
| ADAMS  | CLERK     | NULL |
| JAMES  | CLERK     | NULL |
| FORD   | ANALYST   | NULL |
| MILLER | CLERK     | NULL |
+--------+-----------+------+
10 rows in set (0.00 sec)
```

* `and/or/not`

and表示并且，or表示或者，and和or同时出现的时候会有优先级问题，and的优先级更高，如果想优先使用or，就用小括号括起来，not 就是表示否，一般和is 和 in 一起用 ，is not null / not in

```mysql
mysql> select ename,job,sal from emp where job='MANAGER' or job='SALESMAN';
+--------+----------+---------+
| ename  | job      | sal     |
+--------+----------+---------+
| ALLEN  | SALESMAN | 1600.00 |
| WARD   | SALESMAN | 1250.00 |
| JONES  | MANAGER  | 2975.00 |
| MARTIN | SALESMAN | 1250.00 |
| BLAKE  | MANAGER  | 2850.00 |
| CLARK  | MANAGER  | 2450.00 |
| TURNER | SALESMAN | 1500.00 |
+--------+----------+---------+
7 rows in set (0.00 sec)
```

* `in`

in就是多个or的集合 ，（not in 不在这个范围中）

```mysql
mysql> select empno,ename,job from emp where job in('MANAGER', 'SALESMAN');
+-------+--------+----------+
| empno | ename  | job      |
+-------+--------+----------+
|  7499 | ALLEN  | SALESMAN |
|  7521 | WARD   | SALESMAN |
|  7566 | JONES  | MANAGER  |
|  7654 | MARTIN | SALESMAN |
|  7698 | BLAKE  | MANAGER  |
|  7782 | CLARK  | MANAGER  |
|  7844 | TURNER | SALESMAN |
+-------+--------+----------+
7 rows in set (0.00 sec)
```

```mysql
mysql> select ename,sal from emp where sal in(800, 5000);# 只会找到sal=500和sal=5000的信息
+-------+---------+
| ename | sal     |
+-------+---------+
| SMITH |  800.00 |
| KING  | 5000.00 |
+-------+---------+
2 rows in set (0.00 sec)
```

括号里面的值不能理解成区间范围，只能理解成可选项。

* `like % _`

模糊查找

`%`表示若干个字符，`_`表示一个字符，如果查找的字符串中含有这两个关键字符，需要用转义字符`\`

例如：查找名字以T结尾的成员信息

```mysql
mysql> select ename from emp where ename like '%T';
+-------+
| ename |
+-------+
| SCOTT |
+-------+
1 row in set (0.00 sec)
```

## 排序

查询所有员工薪资，排序？

### 按照一个字段排序

```mysql
select 字段名1，字段名2，...
from 表名
order by 字段名;
```

```mysql
mysql> select ename,sal from emp order by sal;
+--------+---------+
| ename  | sal     |
+--------+---------+
| SMITH  |  800.00 |
| JAMES  |  950.00 |
| ADAMS  | 1100.00 |
| WARD   | 1250.00 |
| MARTIN | 1250.00 |
| MILLER | 1300.00 |
| TURNER | 1500.00 |
| ALLEN  | 1600.00 |
| CLARK  | 2450.00 |
| BLAKE  | 2850.00 |
| JONES  | 2975.00 |
| SCOTT  | 3000.00 |
| FORD   | 3000.00 |
| KING   | 5000.00 |
+--------+---------+
14 rows in set (0.00 sec)
```

通过发现可以知道默认是从上到下，==升序==排列

### 指定降序和升序排列

* 降序

```mysql
select 字段名1，字段名2，...
from 表名
order by 字段名 desc;
```

* 升序

```mysql
select 字段名1，字段名2，...
from 表名
order by 字段名 asc;
```

关键字`asc`和`desc`分别代表`ascend`和`descend`，帮助记忆。

### 按照多个字段排序

```mysql
select 字段名1，字段名2，...
from 表名
order by 字段名1 asc/desc,字段名2 asc/desc ...;
# 如果按照字段名1进行排序遇到相等的情况，就按照字段名2进行排序
```

比如说：

> 查询员工名字和薪资，要求按照薪资升序，如果薪资一样的话，再按照名字升序排列。

```mysql
mysql> select
    ->          ename,sal
    ->  from
    ->          emp
    ->  order by
    ->          sal asc, ename asc;
+--------+---------+
| ename  | sal     |
+--------+---------+
| SMITH  |  800.00 |
| JAMES  |  950.00 |
| ADAMS  | 1100.00 |
| MARTIN | 1250.00 |
| WARD   | 1250.00 |
| MILLER | 1300.00 |
| TURNER | 1500.00 |
| ALLEN  | 1600.00 |
| CLARK  | 2450.00 |
| BLAKE  | 2850.00 |
| JONES  | 2975.00 |
| FORD   | 3000.00 |
| SCOTT  | 3000.00 |
| KING   | 5000.00 |
+--------+---------+
14 rows in set (0.00 sec)
```

```mysql
mysql> select
    ->          ename,sal
    ->  from
    ->          emp
    ->  order by
    ->          sal asc, ename asc;# sal在前，起主导，只有sal相等的时候，才会考虑启用ename排序。
```

综合测试：找出工资在1250到3000之间的员工信息，要求按照薪资降序排列。

```mysql
mysql> select ename,sal
    -> from emp
    -> where sal>=1250 and sal<=3000
    -> order by
    -> sal desc;
+--------+---------+
| ename  | sal     |
+--------+---------+
| SCOTT  | 3000.00 |
| FORD   | 3000.00 |
| JONES  | 2975.00 |
| BLAKE  | 2850.00 |
| CLARK  | 2450.00 |
| ALLEN  | 1600.00 |
| TURNER | 1500.00 |
| MILLER | 1300.00 |
| WARD   | 1250.00 |
| MARTIN | 1250.00 |
+--------+---------+
10 rows in set (0.01 sec)
```

注意：

```mysql
关键字顺序不能变：
        select
            ...
        from
            ...
        where
            ...
        order by
            ... ;
```

以上语句的执行顺序必须掌握：
            第一步：from
            第二步：where
            第三步：select
            第四步：order by（排序总是在最后执行！）

## 数据处理函数/单行处理函数

也被称为单行处理函数：**一个输入对应一个输出。**

### lower转小写

```mysql
mysql> select lower(ename) from emp;
# 这里也可以取别名
# select lower(ename) as ename from emp;
+--------------+
| lower(ename) |
+--------------+
| smith        |
| allen        |
| ward         |
| jones        |
| martin       |
| blake        |
| clark        |
| scott        |
| king         |
| turner       |
| adams        |
| james        |
| ford         |
| miller       |
+--------------+
14 rows in set (0.01 sec)

--------------------------------
mysql> select lower(ename) as ename,lower(Job) as job from emp;# 也可以处理多列
+--------+-----------+
| ename  | job       |
+--------+-----------+
| smith  | clerk     |
| allen  | salesman  |
| ward   | salesman  |
| jones  | manager   |
| martin | salesman  |
| blake  | manager   |
| clark  | manager   |
| scott  | analyst   |
| king   | president |
| turner | salesman  |
| adams  | clerk     |
| james  | clerk     |
| ford   | analyst   |
| miller | clerk     |
+--------+-----------+
14 rows in set (0.00 sec)
```

### upper转大写

和小写一个用法

### substr提取子串

```mysql
substr(被截取的字符串，起始下标，截取的长度)
```

注意，SQL语句中的下标是从`1`开始的

例如，我们用substr提取出字符串中的首字母来判断首字母是不是‘A’,并且将相关信息提取出来。

```mysql
mysql> select ename ,job,sal from emp where substr(ename,1,1)='A';
+-------+----------+---------+
| ename | job      | sal     |
+-------+----------+---------+
| ALLEN | SALESMAN | 1600.00 |
| ADAMS | CLERK    | 1100.00 |
+-------+----------+---------+
2 rows in set (0.01 sec)
```

### concat拼接字符串

```mysql
mysql> select concat(empno,ename,job) from emp;# 这里发现是可以拼接多个字符串的
+-------------------------+
| concat(empno,ename,job) |
+-------------------------+
| 7369SMITHCLERK          |
| 7499ALLENSALESMAN       |
| 7521WARDSALESMAN        |
| 7566JONESMANAGER        |
| 7654MARTINSALESMAN      |
| 7698BLAKEMANAGER        |
| 7782CLARKMANAGER        |
| 7788SCOTTANALYST        |
| 7839KINGPRESIDENT       |
| 7844TURNERSALESMAN      |
| 7876ADAMSCLERK          |
| 7900JAMESCLERK          |
| 7902FORDANALYST         |
| 7934MILLERCLERK         |
+-------------------------+
14 rows in set (0.00 sec)
```

### length取长度

```mysql
mysql> select length(ename) enamelength from emp;
+-------------+
| enamelength |
+-------------+
|           5 |
|           5 |
|           4 |
|           5 |
|           6 |
|           5 |
|           5 |
|           5 |
|           4 |
|           6 |
|           5 |
|           5 |
|           4 |
|           6 |
+-------------+
14 rows in set (0.00 sec)
```

### trim去空格

也是去除字符串的前后空白

```mysql
mysql> select * from emp where ename=trim('  KING ');
+-------+-------+-----------+------+------------+---------+------+--------+
| EMPNO | ENAME | JOB       | MGR  | HIREDATE   | SAL     | COMM | DEPTNO |
+-------+-------+-----------+------+------------+---------+------+--------+
|  7839 | KING  | PRESIDENT | NULL | 1981-11-17 | 5000.00 | NULL |     10 |
+-------+-------+-----------+------+------------+---------+------+--------+
1 row in set (0.00 sec)
```

但是

```mysql
mysql> select * from emp where ename=trim('  K I NG ');
Empty set (0.00 sec)
```

这样是查询不到的。

### round四舍五入

```mysql
select 'abc' from emp; // select后面直接跟“字面量/字面值”
mysql> select 'abc' from emp;
+-----+
| abc |
+-----+
| abc |
| abc |
| abc |
| abc |
| abc |
| abc |
| abc |
| abc |
| abc |
| abc |
| abc |
| abc |
| abc |
| abc |
+-----+

mysql> select abc from emp;
        ERROR 1054 (42S22): Unknown column 'abc' in 'field list'
        这样肯定报错，因为会把abc当做一个字段的名字，去emp表中找abc字段去了。

select 1000 as num from emp; // 1000 也是被当做一个字面量/字面值。
        +------+
        | num  |
        +------+
        | 1000 |
        | 1000 |
        | 1000 |
        | 1000 |
        | 1000 |
        | 1000 |
        | 1000 |
        | 1000 |
        | 1000 |
        | 1000 |
        | 1000 |
        | 1000 |
        | 1000 |
        | 1000 |
        +------+
```

> **结论：select后面可以跟某个表的字段名（可以等同看做变量名），也可以跟字面量/字面值（数据）。**

```mysql
select round(1245.6735,0) as num from emp;# 将1245.6735保留到整数位
+------+
| num  |
+------+
| 1246 |
| 1246 |
| 1246 |
| 1246 |
| 1246 |
| 1246 |
| 1246 |
| 1246 |
| 1246 |
| 1246 |
| 1246 |
| 1246 |
| 1246 |
| 1246 |
+------+
select round(1245.6735,1) as num from emp;# 保留一位小数
+--------+
| num    |
+--------+
| 1245.7 |
| 1245.7 |
| 1245.7 |
| 1245.7 |
| 1245.7 |
| 1245.7 |
| 1245.7 |
| 1245.7 |
| 1245.7 |
| 1245.7 |
| 1245.7 |
| 1245.7 |
| 1245.7 |
| 1245.7 |
+--------+
依次类推
select round(1245.6735,-1) as num from emp;# -1那么就是保留到十位
+------+
| num  |
+------+
| 1250 |
| 1250 |
| 1250 |
| 1250 |
| 1250 |
| 1250 |
| 1250 |
| 1250 |
| 1250 |
| 1250 |
| 1250 |
| 1250 |
| 1250 |
| 1250 |
+------+
```

### rand生成随机数

```mysql
mysql> select rand() as random from emp;
+---------------------+
| random              |
+---------------------+
|  0.6779789288323176 |
| 0.03282456009911798 |
| 0.13018604473228199 |
|   0.552456574097701 |
|  0.3717247670253038 |
| 0.20125414356706117 |
|  0.8910964474930395 |
|  0.8517198374976589 |
|  0.5853098757428209 |
|  0.3713898969547729 |
| 0.10101988827904676 |
|  0.3909297812645601 |
|  0.6515892722193052 |
| 0.08515704803649062 |
+---------------------+
```

可以结合round函数生成整数随机数

```mysql
mysql> select round(rand()*100,0) as random from emp;# 生成100以内的随机数
+--------+
| random |
+--------+
|     47 |
|     10 |
|      9 |
|     13 |
|     38 |
|     50 |
|     39 |
|     42 |
|     95 |
|     47 |
|     52 |
|     20 |
|     43 |
|     53 |
+--------+
```

### ifnull 处理null值

在SQL语句中规定，所有数据与null进行数学运算之后的结果只能是null

```mysql
mysql> select * from emp;
+-------+--------+-----------+------+------------+---------+---------+--------+
| EMPNO | ENAME  | JOB       | MGR  | HIREDATE   | SAL     | COMM    | DEPTNO |
+-------+--------+-----------+------+------------+---------+---------+--------+
|  7369 | SMITH  | CLERK     | 7902 | 1980-12-17 |  800.00 |    NULL |     20 |
|  7499 | ALLEN  | SALESMAN  | 7698 | 1981-02-20 | 1600.00 |  300.00 |     30 |
|  7521 | WARD   | SALESMAN  | 7698 | 1981-02-22 | 1250.00 |  500.00 |     30 |
|  7566 | JONES  | MANAGER   | 7839 | 1981-04-02 | 2975.00 |    NULL |     20 |
|  7654 | MARTIN | SALESMAN  | 7698 | 1981-09-28 | 1250.00 | 1400.00 |     30 |
|  7698 | BLAKE  | MANAGER   | 7839 | 1981-05-01 | 2850.00 |    NULL |     30 |
|  7782 | CLARK  | MANAGER   | 7839 | 1981-06-09 | 2450.00 |    NULL |     10 |
|  7788 | SCOTT  | ANALYST   | 7566 | 1987-04-19 | 3000.00 |    NULL |     20 |
|  7839 | KING   | PRESIDENT | NULL | 1981-11-17 | 5000.00 |    NULL |     10 |
|  7844 | TURNER | SALESMAN  | 7698 | 1981-09-08 | 1500.00 |    0.00 |     30 |
|  7876 | ADAMS  | CLERK     | 7788 | 1987-05-23 | 1100.00 |    NULL |     20 |
|  7900 | JAMES  | CLERK     | 7698 | 1981-12-03 |  950.00 |    NULL |     30 |
|  7902 | FORD   | ANALYST   | 7566 | 1981-12-03 | 3000.00 |    NULL |     20 |
|  7934 | MILLER | CLERK     | 7782 | 1982-01-23 | 1300.00 |    NULL |     10 |
+-------+--------+-----------+------+------------+---------+---------+--------+
14 rows in set (0.00 sec)

mysql> select ename,sal+comm as salcomm from emp;# 会发现所有sal中的数据加上null都变成了null；
+--------+---------+
| ename  | salcomm |
+--------+---------+
| SMITH  |    NULL |
| ALLEN  | 1900.00 |
| WARD   | 1750.00 |
| JONES  |    NULL |
| MARTIN | 2650.00 |
| BLAKE  |    NULL |
| CLARK  |    NULL |
| SCOTT  |    NULL |
| KING   |    NULL |
| TURNER | 1500.00 |
| ADAMS  |    NULL |
| JAMES  |    NULL |
| FORD   |    NULL |
| MILLER |    NULL |
+--------+---------+
```

但是有时候我们并不想这么做，我们认为有时候null代表着0，那么这个时候该怎么做呢？

使用`ifnull`函数`ifnull（数据，null被当作哪个值）`

```mysql
mysql> select ename,sal+ifnull(comm,0) as salcomm from emp;# 这里我们将null当作0
+--------+---------+
| ename  | salcomm |
+--------+---------+
| SMITH  |  800.00 |
| ALLEN  | 1900.00 |
| WARD   | 1750.00 |
| JONES  | 2975.00 |
| MARTIN | 2650.00 |
| BLAKE  | 2850.00 |
| CLARK  | 2450.00 |
| SCOTT  | 3000.00 |
| KING   | 5000.00 |
| TURNER | 1500.00 |
| ADAMS  | 1100.00 |
| JAMES  |  950.00 |
| FORD   | 3000.00 |
| MILLER | 1300.00 |
+--------+---------+
```

### case...when...then...when...then...else...end模拟if-else语句

当员工的工作岗位是MANAGER的时候，工资上调10%，当工作岗位是SALESMAN的时候，工资上调50%,其它正常。
        （注意：不修改数据库，只是将查询结果显示为工资上调）

`case(变量)when(变量满足条件1)then(如果满足条件1后的执行)when(变量满足条件2)then...else...end`

```mysql
select ename,
        job,
        sal as oldsal,
        (case job when 'MANAGER' then sal*1.1 when 'SALESMAN' then sal*1.5 else sal end) as newsal
        from emp;
+--------+-----------+---------+---------+
| ename  | job       | oldsal  | newsal  |
+--------+-----------+---------+---------+
| SMITH  | CLERK     |  800.00 |  800.00 |
| ALLEN  | SALESMAN  | 1600.00 | 2400.00 |
| WARD   | SALESMAN  | 1250.00 | 1875.00 |
| JONES  | MANAGER   | 2975.00 | 3272.50 |
| MARTIN | SALESMAN  | 1250.00 | 1875.00 |
| BLAKE  | MANAGER   | 2850.00 | 3135.00 |
| CLARK  | MANAGER   | 2450.00 | 2695.00 |
| SCOTT  | ANALYST   | 3000.00 | 3000.00 |
| KING   | PRESIDENT | 5000.00 | 5000.00 |
| TURNER | SALESMAN  | 1500.00 | 2250.00 |
| ADAMS  | CLERK     | 1100.00 | 1100.00 |
| JAMES  | CLERK     |  950.00 |  950.00 |
| FORD   | ANALYST   | 3000.00 | 3000.00 |
| MILLER | CLERK     | 1300.00 | 1300.00 |
+--------+-----------+---------+---------+
14 rows in set (0.00 sec)        
```

### str_to_date

将字符串varchar类型转换成date类型。

### date_format

将date类型转换成具有一定格式的varchar字符串类型。

## 分组函数/多行处理函数

**输入多行，输出一行。**

* count 计数
* sum 求和
* avg 平均值
* max 最大值
* min 最小值

> 注意：
>         分组函数在使用的时候必须先进行分组，然后才能用。
>         如果你没有对数据进行分组，整张表默认为一组。

```mysql
mysql> select max(sal) from emp;# 求最大值
+----------+
| max(sal) |
+----------+
|  5000.00 |
+----------+
1 row in set (0.01 sec)

mysql> select min(sal) from emp;# 求最小值
+----------+
| min(sal) |
+----------+
|   800.00 |
+----------+
1 row in set (0.01 sec)

mysql> select avg(sal) from emp;# 求平均值
+-------------+
| avg(sal)    |
+-------------+
| 2073.214286 |
+-------------+
1 row in set (0.00 sec)

mysql> select sum(sal) from emp;# 求总和
+----------+
| sum(sal) |
+----------+
| 29025.00 |
+----------+
1 row in set (0.00 sec)

mysql> select count(sal) from emp;# 求个数
+------------+
| count(sal) |
+------------+
|         14 |
+------------+
1 row in set (0.00 sec)
```

值得注意的是分组函数有几个注意事项

* 分组函数自动忽略掉`null`值，我们不需要提前对`null`值进行处理，例如：

```mysql
mysql> select count(comm) from emp;
+-------------+
| count(comm) |
+-------------+
|           4 |
+-------------+
```

* 分组函数中`count(*)`与`count(具体字段)`的区别

`count(*)`会统计表中的总行数。

`count(具体字段)`会忽略字段中的`null`。

因为每一行记录不可能都为NULL，一行数据中有一列不为NULL，则这行数据就是有效的。

* 分组函数不能用在`where`子句中（分组查询中会解释）

```mysql
select ename,job,sal from emp where max(sal);
ERROR 1111 (HY000): Invalid use of group function
```

* 所有的分组函数可以组合在一起用

```mysql
mysql> select sum(sal),min(sal),max(sal),avg(sal),count(*) from emp;
+----------+----------+----------+-------------+----------+
| sum(sal) | min(sal) | max(sal) | avg(sal)    | count(*) |
+----------+----------+----------+-------------+----------+
| 29025.00 |   800.00 |  5000.00 | 2073.214286 |       14 |
+----------+----------+----------+-------------+----------+
1 row in set (0.00 sec)
```

## 分组查询

在实际的应用中，可能有这样的需求，需要先进行分组，然后对每一组的数据进行操作。

例如我们要计算每个部门的薪资和，每个工作岗位的平均薪资，这都是要进行分组，分组之后才能计算

```mysql
select
    ...
    from
    ...
    group by
    ...
```

结合已经学到的关键字，可以知道有代码顺序：

```mysql
select
...
from 
...
where
...
group by
...
order by
...
```

上面的执行顺序应该是

1. from 
2. where
3. group by
4. select
5. order by

结合分组函数的使用注意事项**分组函数必须先分组，才能执行**，那么`where`子句中如果有分组函数，但是`group by`是在`where`语句执行完之后才会执行的，因此执行`where`语句中的分组函数，那个时候是还没有完成分组的，于是就会报错。

### 单个分组

找出每个工作岗位的工资和。

```mysql
select 
    job,sum(sal)
from
    emp
group by
    job;

+-----------+----------+
| job       | sum(sal) |
+-----------+----------+
| CLERK     |  4150.00 |
| SALESMAN  |  5600.00 |
| MANAGER   |  8275.00 |
| ANALYST   |  6000.00 |
| PRESIDENT |  5000.00 |
+-----------+----------+
```

那么上面的代码中`select`后面还能加上别的字段名吗？

答案是不可以的，那样会报错。如果想要找出每个工作岗位的工资最高的人是谁，显示名字啥的，需要结合后面学习到的知识才能运行。

> 在有的时候，上面说的情况不会报错，但是那样是没有意义的。
> 
> 重点结论：
> 在一条select语句当中，如果有group by语句的话，
> select后面只能跟：参加分组的字段，以及分组函数。
> 其它的一律不能跟。

### 多个分组

找出“每个部门，不同工作岗位”的最高薪资

```mysql
mysql> select
    ->      deptno,job,max(sal)
    -> from
    ->      emp
    -> group by
    ->      deptno,job# 根据多个选项进行分组
    -> order by
    ->      deptno;
+--------+-----------+----------+
| deptno | job       | max(sal) |
+--------+-----------+----------+
|     10 | CLERK     |  1300.00 |
|     10 | MANAGER   |  2450.00 |
|     10 | PRESIDENT |  5000.00 |
|     20 | ANALYST   |  3000.00 |
|     20 | CLERK     |  1100.00 |
|     20 | MANAGER   |  2975.00 |
|     30 | CLERK     |   950.00 |
|     30 | MANAGER   |  2850.00 |
|     30 | SALESMAN  |  1600.00 |
+--------+-----------+----------+
9 rows in set (0.00 sec)
```

### having语句进行进一步过滤

找出每个部门最高薪资，要求显示最高薪资大于3000的？

首先我们找到每个部门的最高薪资

```mysql
mysql> select 
            deptno,max(sal) 
        from 
            emp 
        group by 
            deptno;
+--------+----------+
| deptno | max(sal) |
+--------+----------+
|     20 |  3000.00 |
|     30 |  2850.00 |
|     10 |  5000.00 |
+--------+----------+
```

然后我们再对最高薪资进行过滤

```mysql
mysql> select 
            deptno,max(sal) 
        from 
            emp 
        group by 
            deptno 
        having 
            max(sal)>3000;
+--------+----------+
| deptno | max(sal) |
+--------+----------+
|     10 |  5000.00 |
+--------+----------+
```

思考：这样做效率是不是很低？

实际上我们可以先把所有大于3000的人找出来再分组

```mysql
mysql> select 
            deptno,max(sal) 
        from 
            emp 
        where 
            sal>3000 
        group by 
            deptno;
+--------+----------+
| deptno | max(sal) |
+--------+----------+
|     10 |  5000.00 |
+--------+----------+
```

但是有的时候也会存在where无法过滤的情况

找出每个部门平均薪资，要求显示平均薪资高于2500的。

这个例子中，我们就必须先找出平均薪资了，是无法用where过滤的

```mysql
mysql> select 
            deptno,avg(sal) 
        from 
            emp 
        group by 
            deptno 
        having 
            avg(sal)>2500;
+--------+-------------+
| deptno | avg(sal)    |
+--------+-------------+
|     10 | 2916.666667 |
+--------+-------------+
```

### distinct关键字

`distinct`关键字是用来对查询记录进行重复处理

```mysql
mysql> select job from emp;
+-----------+
| job       |
+-----------+
| CLERK     |
| SALESMAN  |
| SALESMAN  |
| MANAGER   |
| SALESMAN  |
| MANAGER   |
| MANAGER   |
| ANALYST   |
| PRESIDENT |
| SALESMAN  |
| CLERK     |
| CLERK     |
| ANALYST   |
| CLERK     |
+-----------+
```

例如这里查询`job`字段，会有重复的job出现，这个时候可以用`distinct`关键字进行去重

```mysql
mysql> select distinct job from emp;
+-----------+
| job       |
+-----------+
| CLERK     |
| SALESMAN  |
| MANAGER   |
| ANALYST   |
| PRESIDENT |
+-----------+
```

注意：`distinct`关键字只能出现在字段名之前，不能夹在字段名中间。

```mysql
mysql> select ename,distinct job from emp;
```

这样是错误的。

当`distinct`关键字后面有多个字段名的时候，它会实现联合这多个字段名进行查询结果的去重。

```mysql
mysql> select deptno,job from emp;
+--------+-----------+
| deptno | job       |
+--------+-----------+
|     20 | CLERK     |
|     30 | SALESMAN  |
|     30 | SALESMAN  |
|     20 | MANAGER   |
|     30 | SALESMAN  |
|     30 | MANAGER   |
|     10 | MANAGER   |
|     20 | ANALYST   |
|     10 | PRESIDENT |
|     30 | SALESMAN  |
|     20 | CLERK     |
|     30 | CLERK     |
|     20 | ANALYST   |
|     10 | CLERK     |
+--------+-----------+
```

```mysql
mysql> select distinct deptno,job from emp;
+--------+-----------+
| deptno | job       |
+--------+-----------+
|     20 | CLERK     |
|     30 | SALESMAN  |
|     20 | MANAGER   |
|     30 | MANAGER   |
|     10 | MANAGER   |
|     20 | ANALYST   |
|     10 | PRESIDENT |
|     30 | CLERK     |
|     10 | CLERK     |
+--------+-----------+
```

统计job的种类数量：

```mysql
mysql> select count(distinct job) from emp;
+---------------------+
| count(distinct job) |
+---------------------+
|                   5 |
+---------------------+
```

### 小结

```mysql
select 
        ...
    from
        ...
    where
        ...
    group by
        ...
    having
        ...
    order by
        ...
```

上面是已经学到的整个框架，顺序是不能变的。

执行顺序大概是：

1. `from` 从某张表中查询数据
2. `where` 先经过where条件筛选出有价值的数据。
3. `group by `对这些有价值的数据进行分组。
4. `having `分组之后可以使用having继续筛选。
5. `select` 使用select查询出来。
6. `order by` 最后排序输出！

找出每个岗位的平均薪资，要求显示平均薪资大于1500的，除MANAGER岗位之外，要求按照平均薪资降序排。

```mysql
mysql> select 
            job ,avg(sal) as avgsal
        from 
            emp
        where 
            job!='MANAGER'
        group by 
            job
        having
            avg(sal)>1500
        order by     
            avgsal desc;
+-----------+-------------+
| job       | avgsal      |
+-----------+-------------+
| PRESIDENT | 5000.000000 |
| ANALYST   | 3000.000000 |
+-----------+-------------+
```

## 连接查询

> 从一张表中单独查询，称为单表查询。
> emp表和dept表联合起来查询数据，从emp表中取员工名字，从dept表中取部门名字。
> 这种跨表查询，多张表联合起来查询数据，被称为连接查询。

> 根据表连接的方式分类：
>         内连接：
>             等值连接
>             非等值连接
>             自连接
> 
> ​        外连接：
> ​            左外连接（左连接）
> ​            右外连接（右连接）
> 
> ​        全连接

### 笛卡尔积现象

```mysql
mysql> select * from emp;
+-------+--------+-----------+------+------------+---------+---------+--------+
| EMPNO | ENAME  | JOB       | MGR  | HIREDATE   | SAL     | COMM    | DEPTNO |
+-------+--------+-----------+------+------------+---------+---------+--------+
|  7369 | SMITH  | CLERK     | 7902 | 1980-12-17 |  800.00 |    NULL |     20 |
|  7499 | ALLEN  | SALESMAN  | 7698 | 1981-02-20 | 1600.00 |  300.00 |     30 |
|  7521 | WARD   | SALESMAN  | 7698 | 1981-02-22 | 1250.00 |  500.00 |     30 |
|  7566 | JONES  | MANAGER   | 7839 | 1981-04-02 | 2975.00 |    NULL |     20 |
|  7654 | MARTIN | SALESMAN  | 7698 | 1981-09-28 | 1250.00 | 1400.00 |     30 |
|  7698 | BLAKE  | MANAGER   | 7839 | 1981-05-01 | 2850.00 |    NULL |     30 |
|  7782 | CLARK  | MANAGER   | 7839 | 1981-06-09 | 2450.00 |    NULL |     10 |
|  7788 | SCOTT  | ANALYST   | 7566 | 1987-04-19 | 3000.00 |    NULL |     20 |
|  7839 | KING   | PRESIDENT | NULL | 1981-11-17 | 5000.00 |    NULL |     10 |
|  7844 | TURNER | SALESMAN  | 7698 | 1981-09-08 | 1500.00 |    0.00 |     30 |
|  7876 | ADAMS  | CLERK     | 7788 | 1987-05-23 | 1100.00 |    NULL |     20 |
|  7900 | JAMES  | CLERK     | 7698 | 1981-12-03 |  950.00 |    NULL |     30 |
|  7902 | FORD   | ANALYST   | 7566 | 1981-12-03 | 3000.00 |    NULL |     20 |
|  7934 | MILLER | CLERK     | 7782 | 1982-01-23 | 1300.00 |    NULL |     10 |
+-------+--------+-----------+------+------------+---------+---------+--------+
14 rows in set (0.00 sec)

mysql> select * from dept;
+--------+------------+----------+
| DEPTNO | DNAME      | LOC      |
+--------+------------+----------+
|     10 | ACCOUNTING | NEW YORK |
|     20 | RESEARCH   | DALLAS   |
|     30 | SALES      | CHICAGO  |
|     40 | OPERATIONS | BOSTON   |
+--------+------------+----------+
4 rows in set (0.00 sec)
```

当两张表进行无条件的连接查询：

```mysql
mysql> select ename,dname from emp,dept;
+--------+------------+
| ename  | dname      |
+--------+------------+
| SMITH  | OPERATIONS |
| SMITH  | SALES      |
| SMITH  | RESEARCH   |
| SMITH  | ACCOUNTING |
| ALLEN  | OPERATIONS |
| ALLEN  | SALES      |
| ALLEN  | RESEARCH   |
| ALLEN  | ACCOUNTING |
| WARD   | OPERATIONS |
| WARD   | SALES      |
| WARD   | RESEARCH   |
| WARD   | ACCOUNTING |
| JONES  | OPERATIONS |
| JONES  | SALES      |
| JONES  | RESEARCH   |
| JONES  | ACCOUNTING |
| MARTIN | OPERATIONS |
| MARTIN | SALES      |
| MARTIN | RESEARCH   |
| MARTIN | ACCOUNTING |
| BLAKE  | OPERATIONS |
| BLAKE  | SALES      |
| BLAKE  | RESEARCH   |
| BLAKE  | ACCOUNTING |
| CLARK  | OPERATIONS |
| CLARK  | SALES      |
| CLARK  | RESEARCH   |
| CLARK  | ACCOUNTING |
| SCOTT  | OPERATIONS |
| SCOTT  | SALES      |
| SCOTT  | RESEARCH   |
| SCOTT  | ACCOUNTING |
| KING   | OPERATIONS |
| KING   | SALES      |
| KING   | RESEARCH   |
| KING   | ACCOUNTING |
| TURNER | OPERATIONS |
| TURNER | SALES      |
| TURNER | RESEARCH   |
| TURNER | ACCOUNTING |
| ADAMS  | OPERATIONS |
| ADAMS  | SALES      |
| ADAMS  | RESEARCH   |
| ADAMS  | ACCOUNTING |
| JAMES  | OPERATIONS |
| JAMES  | SALES      |
| JAMES  | RESEARCH   |
| JAMES  | ACCOUNTING |
| FORD   | OPERATIONS |
| FORD   | SALES      |
| FORD   | RESEARCH   |
| FORD   | ACCOUNTING |
| MILLER | OPERATIONS |
| MILLER | SALES      |
| MILLER | RESEARCH   |
| MILLER | ACCOUNTING |
+--------+------------+
56 rows in set (0.01 sec)
```

我们发现，他其实是拿emp表中的每个成员分别和dept中的四个成员连接，最终也就是有了`4*14`行的数据了，但是这里面有一些数据是没有意义的，因为我们连接两个表进行查询是为了通过两个表具有相同的元素进行关联查询，即通过`deptno`关联起来两个表，但是结果是具有冗余数据的，这种现象就是笛卡尔积现象。

![image-20220716104818495](https://raw.githubusercontent.com/danjuan-77/picgo/main/202207161048601.png)

### 避免笛卡尔积现象

**连接时加条件，满足这个条件的记录被筛选出来！**

```mysql
select
    ename,dname# 它既会去emp中找ename也会去dept中找ename（dname）同理，因此效率并不是很高
    # 提高效率可以这样写：emp.ename,dept.dname
from 
    emp,dept
where 
    emp.deptno=dept.deptno;

+--------+------------+
| ename  | dname      |
+--------+------------+
| SMITH  | RESEARCH   |
| ALLEN  | SALES      |
| WARD   | SALES      |
| JONES  | RESEARCH   |
| MARTIN | SALES      |
| BLAKE  | SALES      |
| CLARK  | ACCOUNTING |
| SCOTT  | RESEARCH   |
| KING   | ACCOUNTING |
| TURNER | SALES      |
| ADAMS  | RESEARCH   |
| JAMES  | SALES      |
| FORD   | RESEARCH   |
| MILLER | ACCOUNTING |
+--------+------------+
```

这样就能实现两个表通过deptno产生关联，连接之后再进行查询。

> 最终查询的结果条数是14条，但是匹配的过程中，匹配的次数减少了吗？
> 还是56次，只不过进行了四选一。次数没有减少。
> 
> 注意：通过笛卡尔积现象得出，表的连接次数越多效率越低，尽量避免表的
> 连接次数。

同时一种书写习惯是，给表取别名

```mysql
# 表起别名。很重要。效率问题。
    select 
        e.ename,d.dname 
    from 
        emp e, dept d
    where
        e.deptno = d.deptno; //SQL92语法。
```

### 内连接与等值连接

**条件是等量关系，所以被称为等值连接。**

```mysql
# SQL92语法。
select 
        e.ename,d.dname 
    from 
        emp e, dept d
    where
        e.deptno = d.deptno;
```

sql92的缺点：结构不清晰，表的连接条件，和后期进一步筛选的条件，都放到了where后面。

```mysql
# SQL99语法
select 
        e.ename,d.dname
    from
        emp e
    inner join #inner可以省略（带着inner可读性更好！！！一眼就能看出来是内连接）
        dept d
    on
        e.deptno = d.deptno;# 条件是等量关系，所以被称为等值连接。
```

sql99优点：表连接的条件是独立的，连接之后，如果还需要进一步筛选，再往后继续添加where。

```mysql
# SQL99语法：
        select 
            ...
        from
            a
        join
            b
        on
            a和b的连接条件
        where
            筛选条件
```

### 内连接与非等值连接

 **条件不是一个等量关系，称为非等值连接。**

案例：找出每个员工的薪资等级，要求显示员工名、薪资、薪资等级？

```mysql
mysql> select * from salgrade;
+-------+-------+-------+
| GRADE | LOSAL | HISAL |
+-------+-------+-------+
|     1 |   700 |  1200 |
|     2 |  1201 |  1400 |
|     3 |  1401 |  2000 |
|     4 |  2001 |  3000 |
|     5 |  3001 |  9999 |
+-------+-------+-------+
```

```mysql
mysql> select
    ->   e.ename,e.sal,s.grade
    -> from
    ->   emp e
    -> join
    ->   salgrade s
    -> on
    ->   e.sal >= s.losal and e.sal <=s.hisal;# emp表中的薪资在salgrade表中的区间范围之内的
                                                 # 条件不是一个等量关系，称为非等值连接。
+--------+---------+-------+
| ename  | sal     | grade |
+--------+---------+-------+
| SMITH  |  800.00 |     1 |
| ALLEN  | 1600.00 |     3 |
| WARD   | 1250.00 |     2 |
| JONES  | 2975.00 |     4 |
| MARTIN | 1250.00 |     2 |
| BLAKE  | 2850.00 |     4 |
| CLARK  | 2450.00 |     4 |
| SCOTT  | 3000.00 |     4 |
| KING   | 5000.00 |     5 |
| TURNER | 1500.00 |     3 |
| ADAMS  | 1100.00 |     1 |
| JAMES  |  950.00 |     1 |
| FORD   | 3000.00 |     4 |
| MILLER | 1300.00 |     2 |
+--------+---------+-------+
```

### 内连接与自连接

案例：查询员工的上级领导，要求显示员工名和对应的领导名？

员工名和领导名的相关信息都是在同一个表中，技巧就是将emp a看作员工表，将emp b看作领导表，然后将这两个表进行等值连接

```mysql
mysql> select empno,ename,mgr from emp;
+-------+--------+------+
| empno | ename  | mgr  |
+-------+--------+------+
|  7369 | SMITH  | 7902 |
|  7499 | ALLEN  | 7698 |
|  7521 | WARD   | 7698 |
|  7566 | JONES  | 7839 |
|  7654 | MARTIN | 7698 |
|  7698 | BLAKE  | 7839 |
|  7782 | CLARK  | 7839 |
|  7788 | SCOTT  | 7566 |
|  7839 | KING   | NULL |
|  7844 | TURNER | 7698 |
|  7876 | ADAMS  | 7788 |
|  7900 | JAMES  | 7698 |
|  7902 | FORD   | 7566 |
|  7934 | MILLER | 7782 |
+-------+--------+------+
```

`empno`是员工编号，`mgt`是员工对应的领导的编号。

```mysql
select 
    a.ename as '员工',b.ename as '领导'
from
    emp a
join 
    emp b
on
    a.mgr=b.empno;# 员工的领导编号 = 领导的员工编号
+--------+--------+
| 员工   | 领导   |
+--------+--------+
| SMITH  | FORD   |
| ALLEN  | BLAKE  |
| WARD   | BLAKE  |
| JONES  | KING   |
| MARTIN | BLAKE  |
| BLAKE  | KING   |
| CLARK  | KING   |
| SCOTT  | JONES  |
| TURNER | BLAKE  |
| ADAMS  | SCOTT  |
| JAMES  | BLAKE  |
| FORD   | JONES  |
| MILLER | CLARK  |
+--------+--------+
13 rows in set (0.00 sec)
```

由于`KING`没有领导，因此没有这个人的数据，一共只有13行数据。

==技巧：一张表看做两张表。==

### 外连接与左外连接右外连接

内连接所连接查询的表没有主次关系，不能全部都匹配出来（比如上方的那个`KING`案例，就没有匹配到他的领导）

外连接是具有主次关系的，关键字：`right/left`

右外连接

```mysql
select 
    e.ename,d.dname
from
    emp e 
right outer join # outer是可以省略的，带着可读性强。
    dept d
on
    e.deptno = d.deptno;# 完全根据这个条件进行匹配
+--------+------------+
| ename  | dname      |
+--------+------------+
| MILLER | ACCOUNTING |
| KING   | ACCOUNTING |
| CLARK  | ACCOUNTING |
| FORD   | RESEARCH   |
| ADAMS  | RESEARCH   |
| SCOTT  | RESEARCH   |
| JONES  | RESEARCH   |
| SMITH  | RESEARCH   |
| JAMES  | SALES      |
| TURNER | SALES      |
| BLAKE  | SALES      |
| MARTIN | SALES      |
| WARD   | SALES      |
| ALLEN  | SALES      |
| NULL   | OPERATIONS |
+--------+------------+
```

会发现最底下会有NULL，这是因为d表中有的值在e表中是无法匹配到相关数据的。

`right`表示在`join`右边的这张表看作主表，主表中的所有数据都要在另一个表中关于on中的条件进行查询，如果没有找到可以匹配的，就用`NULL`代替。

左外连接

```mysql
select 
    e.ename,d.dname
from
    dept d 
left join 
    emp e
on
    e.deptno = d.deptno;
+--------+------------+
| ename  | dname      |
+--------+------------+
| MILLER | ACCOUNTING |
| KING   | ACCOUNTING |
| CLARK  | ACCOUNTING |
| FORD   | RESEARCH   |
| ADAMS  | RESEARCH   |
| SCOTT  | RESEARCH   |
| JONES  | RESEARCH   |
| SMITH  | RESEARCH   |
| JAMES  | SALES      |
| TURNER | SALES      |
| BLAKE  | SALES      |
| MARTIN | SALES      |
| WARD   | SALES      |
| ALLEN  | SALES      |
| NULL   | OPERATIONS |
+--------+------------+
```

在`join`关键字左边的表作为主表，将主表中的所有数据进行查询

> 带有right的是右外连接，又叫做右连接。
> 带有left的是左外连接，又叫做左连接。
> 任何一个右连接都有左连接的写法。
> 任何一个左连接都有右连接的写法。

内连接与外连接主要区别在于：

内连接所关联的的表之间是没有主次关系的，当一个表中的数据在另一个表中的没有相关联的，就不会进行查询匹配。

外连接所关联的表之间是有主次关系的，关键字`right/left`用来标记关键字`join`旁的哪个表作为主表，主表中的所有数据都必须进行查询，若没有相关联的匹配项就用null代替。

```mysql
mysql> select
            a.ename as '员工',b.ename as '领导'
     from
              emp a
     left join
              emp b
     on
              a.mgr=b.empno;
+--------+--------+
| 员工   | 领导   |
+--------+--------+
| SMITH  | FORD   |
| ALLEN  | BLAKE  |
| WARD   | BLAKE  |
| JONES  | KING   |
| MARTIN | BLAKE  |
| BLAKE  | KING   |
| CLARK  | KING   |
| SCOTT  | JONES  |
| KING   | NULL   |
| TURNER | BLAKE  |
| ADAMS  | SCOTT  |
| JAMES  | BLAKE  |
| FORD   | JONES  |
| MILLER | CLARK  |
+--------+--------+
```

### 多表连接

```mysql
语法：
        select 
            ...
        from
            a
        join
            b
        on
            a和b的连接条件
        join
            c
        on
            a和c的连接条件
        right join
            d
        on
            a和d的连接条件
```

**一个SQL语句中内连接和外连接可以混合使用。**

案例：找出每个员工的部门名称以及工资等级，要求显示员工名、部门名、薪资、薪资等级？

```mysql
select
    e.ename,d.dname,e.sal,s.grade
from
    emp e
join
    dept d
on
    e.deptno=d.deptno
join
    salgrade s
on 
    e.sal between s.losal and hisal
order by
    e.sal;
+--------+------------+---------+-------+
| ename  | dname      | sal     | grade |
+--------+------------+---------+-------+
| SMITH  | RESEARCH   |  800.00 |     1 |
| JAMES  | SALES      |  950.00 |     1 |
| ADAMS  | RESEARCH   | 1100.00 |     1 |
| WARD   | SALES      | 1250.00 |     2 |
| MARTIN | SALES      | 1250.00 |     2 |
| MILLER | ACCOUNTING | 1300.00 |     2 |
| TURNER | SALES      | 1500.00 |     3 |
| ALLEN  | SALES      | 1600.00 |     3 |
| CLARK  | ACCOUNTING | 2450.00 |     4 |
| BLAKE  | SALES      | 2850.00 |     4 |
| JONES  | RESEARCH   | 2975.00 |     4 |
| SCOTT  | RESEARCH   | 3000.00 |     4 |
| FORD   | RESEARCH   | 3000.00 |     4 |
| KING   | ACCOUNTING | 5000.00 |     5 |
+--------+------------+---------+-------+
14 rows in set (0.00 sec)
```

结合外连接，将每个员工的上司也输出

```mysql
select
    e.ename '员工',d.dname,m.ename '上司',e.sal,s.grade
from
    emp e
join
    dept d
on
    e.deptno=d.deptno
join
    salgrade s
on 
    e.sal between s.losal and hisal
left join
    emp m
on
    e.mgr=m.empno
order by
    e.sal;
+--------+------------+--------+---------+-------+
| 员工    | dname      | 上司   | sal     | grade |
+--------+------------+--------+---------+-------+
| SMITH  | RESEARCH   | FORD   |  800.00 |     1 |
| JAMES  | SALES      | BLAKE  |  950.00 |     1 |
| ADAMS  | RESEARCH   | SCOTT  | 1100.00 |     1 |
| MARTIN | SALES      | BLAKE  | 1250.00 |     2 |
| WARD   | SALES      | BLAKE  | 1250.00 |     2 |
| MILLER | ACCOUNTING | CLARK  | 1300.00 |     2 |
| TURNER | SALES      | BLAKE  | 1500.00 |     3 |
| ALLEN  | SALES      | BLAKE  | 1600.00 |     3 |
| CLARK  | ACCOUNTING | KING   | 2450.00 |     4 |
| BLAKE  | SALES      | KING   | 2850.00 |     4 |
| JONES  | RESEARCH   | KING   | 2975.00 |     4 |
| FORD   | RESEARCH   | JONES  | 3000.00 |     4 |
| SCOTT  | RESEARCH   | JONES  | 3000.00 |     4 |
| KING   | ACCOUNTING | NULL   | 5000.00 |     5 |
+--------+------------+--------+---------+-------+
14 rows in set (0.00 sec)
```

## 子查询

**select语句中嵌套select语句，被嵌套的select语句称为子查询。**

```mysql
    select
        ..(select).
    from
        ..(select).
    where
        ..(select).
```

### where子查询

案例：找出比最低工资高的员工姓名和工资？

```mysql
select ename,sal from emp where sal>min(sal);
```

这个句子是错误的，因为分组函数不能出现在`where`之中。

第一步：查询最低工资是多少

```mysql
mysql> select min(sal) from emp;
+----------+
| min(sal) |
+----------+
|   800.00 |
+----------+
```

第二步：找到>800的人

```mysql
mysql> select ename,sal from emp where sal>800;
+--------+---------+
| ename  | sal     |
+--------+---------+
| ALLEN  | 1600.00 |
| WARD   | 1250.00 |
| JONES  | 2975.00 |
| MARTIN | 1250.00 |
| BLAKE  | 2850.00 |
| CLARK  | 2450.00 |
| SCOTT  | 3000.00 |
| KING   | 5000.00 |
| TURNER | 1500.00 |
| ADAMS  | 1100.00 |
| JAMES  |  950.00 |
| FORD   | 3000.00 |
| MILLER | 1300.00 |
+--------+---------+
```

第三步：合并

```mysql
select 
    ename,sal
from 
    emp
where
    sal>(select min(sal) from emp);
```

执行到`where`会先去执行子查询，得到最小值，然后执行`where`中的判断语句。

### from子查询

在from后面的子查询所得到的结果可以看作一张临时表。

案例：找出每个岗位的平均工资的薪资等级。

第一步：找到每个岗位的平均薪资（分组查询）

```mysql
mysql> select job,avg(sal) from emp group by job;
+-----------+-------------+
| job       | avg(sal)    |
+-----------+-------------+
| CLERK     | 1037.500000 |
| SALESMAN  | 1400.000000 |
| MANAGER   | 2758.333333 |
| ANALYST   | 3000.000000 |
| PRESIDENT | 5000.000000 |
+-----------+-------------+
```

第二步：将上述表看作一张临时表，与工资等级表进行连接

```mysql
select 
    t.job,t.avgsal,s.grade
from 
    (select job,avg(sal) as avgsal from emp group by job) t
join
    salgrade s
on
    t.avgsal between s.losal and s.hisal;
+-----------+-------------+-------+
| job       | avgsal      | grade |
+-----------+-------------+-------+
| CLERK     | 1037.500000 |     1 |
| SALESMAN  | 1400.000000 |     2 |
| MANAGER   | 2758.333333 |     4 |
| ANALYST   | 3000.000000 |     4 |
| PRESIDENT | 5000.000000 |     5 |
+-----------+-------------+-------+
```

### select子查询

```mysql
mysql> select
          e.ename,e.deptno,(select d.dname from dept d where e.deptno = d.deptno) as dname
         from
          emp e;
+--------+--------+------------+
| ename  | deptno | dname      |
+--------+--------+------------+
| SMITH  |     20 | RESEARCH   |
| ALLEN  |     30 | SALES      |
| WARD   |     30 | SALES      |
| JONES  |     20 | RESEARCH   |
| MARTIN |     30 | SALES      |
| BLAKE  |     30 | SALES      |
| CLARK  |     10 | ACCOUNTING |
| SCOTT  |     20 | RESEARCH   |
| KING   |     10 | ACCOUNTING |
| TURNER |     30 | SALES      |
| ADAMS  |     20 | RESEARCH   |
| JAMES  |     30 | SALES      |
| FORD   |     20 | RESEARCH   |
| MILLER |     10 | ACCOUNTING |
+--------+--------+------------+
14 rows in set (0.00 sec)
```

### union合并查询结果集

```mysql
select ename,job from emp where job = 'MANAGER'
union
select ename,job from emp where job = 'SALESMAN';
+--------+----------+
| ename  | job      |
+--------+----------+
| JONES  | MANAGER  |
| BLAKE  | MANAGER  |
| CLARK  | MANAGER  |
| ALLEN  | SALESMAN |
| WARD   | SALESMAN |
| MARTIN | SALESMAN |
| TURNER | SALESMAN |
+--------+----------+
```

union主要体现在合并表的效率很高，在表连接中，每次连接一次新的表，匹配的次数就会乘以新表的行数

但是使用union可以减少匹配的次数，并且完成表的拼接

a 连接 b 连接 c
a 10条记录
b 10条记录
c 10条记录
匹配次数是：1000=10*10\*10

使用union的话是：

```mysql
a连接b：10*10

union

a连接c：10*10

100次 + 100次 = 200次。
```

使用`union`的一写注意事项：

* 要求合并的两个表的列数相同

* 要求合并的两个表的列与列之间的数据类型一致

* 注释：UNION 结果集中的列名总是等于 UNION 中第一个 SELECT 语句中的列名。

### limit分页

```mysql
limit startIndex, length
```

通过limit去除表中的一部分数据，提高用户的的体验

`startIndex`默认是从0开始的

省缺用法：

```mysql
limit 5;
```

取出前5条数据。

```mysql
select
    ename,sal
from 
    emp
order by
    sal desc
limit 5;
+-------+---------+
| ename | sal     |
+-------+---------+
| KING  | 5000.00 |
| SCOTT | 3000.00 |
| FORD  | 3000.00 |
| JONES | 2975.00 |
| BLAKE | 2850.00 |
+-------+---------+
```

这样就找到了前5条

```mysql
limit 2，3;# 表示从下标2开始，也就是第三条数据开始，取出3条数据，也就是第3，4，5
```

公式：

每页显示`pageSize`条记录：
                第`pageNo`页：**limit (pageNo - 1) * pageSize  , pageSize**

# DDL

## 建表语法

建表属于DDL语句，DDL语句包括`create` `drop` `alter`

```mysql
create table 表名(
    字段名1 数据类型,
    字段名2 数据类型,
    字段名3 数据类型,
    ..
);
```

表名一般建议使用`t_`开头，可读性更强。

## Mysql数据类型

* `varchar`

可变长度的字符串，最长为255，会根据实际的数据长度来动态分配存储空间，能够节省空间，但是由于需要动态分配空间，因此速度较慢，效率较低。

* `char`

定长字符串，最长为255，不管实际字符串的长度是多少，只会分配固定的长度空间去存储数据，可能会导致空间的浪费，但是不需要动态申请空间，因此速度快。

> varchar和char我们应该怎么选择？
> 性别字段你选什么？因为性别是固定长度的字符串，所以选择char。
> 姓名字段你选什么？每一个人的名字长度不同，所以选择varchar。

* `int`

最长为11位数字，整数类型。

* `bigint`

长整型，相当于long。

* `float`

单精度浮点型数据。

* `double`

双精度浮点型数据。

* `date`

短日期类型。

* `datetime`

长日期类型。

* `clob`

字符大对象，最多存储4G的字符串，可以用来存储一篇文章的数据，超过255个字符的字符串都用clob来存储。

* `blob`

二进制大对象，专门用来存储图片，声音，视频等流媒体数据。

## 创建一个学生表

```mysql
create table t_student(
    no int,
    name varchar(32),
    sex char(1),
    age int(3),
    email varchar(255)
);
```

注意最后右括号左边没有逗号。

![image-20220717091201005](https://raw.githubusercontent.com/danjuan-77/picgo/main/202207170912055.png)

## 删除一个表

```mysql
drop table t_student;# 如果这个表不存在就会报错
```

```mysql
drop table if exists t_student;# 如果这张表存在的话就会删除
```

## 为什么不需要掌握DDL的具体操作

`DDL`语句适用于对表的结构进行增删改——添加一个字段，删除一个字段，修改一个字段！！！

但是在实际开发中很少用到这些操作，并且在之后的开发中，用图形化操作工具(Navicat)更容易进行可视化的对表的结构进行的操作，因此是不需要掌握这些操作的命令。

# DML

## 插入数据insert

```mysql
insert into 表名(字段名1，字段名2，字段名3...)values(值1，值2，值3)；
```

字段名和值要一一对应（顺序对应，数据类型对应）

```mysql
insert into t_student(no,name,sex,age,email) values(1,'Jack','b',12,'123456@123.com');
+------+------+------+------+----------------+
| no   | name | sex  | age  | email          |
+------+------+------+------+----------------+
|    1 | Jack | b    |   12 | 123456@123.com |
+------+------+------+------+----------------+
insert into t_student(email,name,sex,age,no) values('lisi@123.com','lisi','f',20,2);
+------+------+------+------+----------------+
| no   | name | sex  | age  | email          |
+------+------+------+------+----------------+
|    1 | Jack | b    |   12 | 123456@123.com |
|    2 | lisi | f    |   20 | lisi@123.com   |
+------+------+------+------+----------------+
insert into t_student(no) values(3);
+------+------+------+------+----------------+
| no   | name | sex  | age  | email          |
+------+------+------+------+----------------+
|    1 | Jack | b    |   12 | 123456@123.com |
|    2 | lisi | f    |   20 | lisi@123.com   |
|    3 | NULL | NULL | NULL | NULL           |
+------+------+------+------+----------------+
```

`insert`语句只负责插入数据，不负责修改数据。

没有给其它字段指定值的话，默认值是NULL。

通过关键字`default`可以设置字段的默认值，例如：

```mysql
sex char(1) default 'm',
```

`insert`语句中的字段名可以省略，但是`values`中的值就必须全部写上，并且一一对应。

## insert插入时间

```mysql
create table t_user(
    id int(11),
    name varchar(32),
    birth date
);
```

```mysql
 insert into t_user values(123,'Jack',str_to_date('01-10-1990','%d-%m-%Y'));
```

使用`str_to_date`函数将字符串类型转换成`data`类型。

```mysql
str_to_date('字符串日期','日期格式')；
```

MySQL日期格式：

```mysql
%Y    年// 注意这里Y大写
%m  月
%d  日
%h    时
%i    分
%s    秒
```

通常使用在插入`insert`方面，因为插入的时候需要一个日期类型的数据，需要通过该函数将字符串转换成`date`。

如果你提供的日期字符串是`%Y-%m-%d`这个格式，`str_to_date`函数就不需要了！！！

查询的时候可以使用`date-format`函数将日期类型转化成特定格式的字符串。

```mysql
date_format('日期类型数据', '日期格式')
```

```mysql
mysql> select * from t_user;
+------+------+------------+
| id   | name | birth      |
+------+------+------------+
|  123 | Jack | 1990-10-01 |
|  124 | Lili | 1991-06-21 |
+------+------+------------+
```

默认的日期显示格式是`%Y-%m-%d`

自定义显示格式：

```mysql
mysql> select id,name,date_format(birth,'%Y/%m/%d') as birth from t_user;
+------+------+------------+
| id   | name | birth      |
+------+------+------------+
|  123 | Jack | 1990/10/01 |
|  124 | Lili | 1991/06/21 |
+------+------+------------+
```

### date和datetime之间的区别

`date`是短日期，只包括年月日

`datetime`是长日期，包括年月日，时分秒

mysql短日期默认格式：`%Y-%m-%d`
mysql长日期默认格式：`%Y-%m-%d %h:%i:%s`

```mysql
create table t_user(
    id int,
    name varchar(32),
    birth date,
    create_time datetime
);

insert into t_user(id,name,birth,create_time) values(123,'Tim','1990-10-01','2021-06-21 12:12:52');
mysql> select * from t_user;
+------+------+------------+---------------------+
| id   | name | birth      | create_time         |
+------+------+------------+---------------------+
|  123 | Tim  | 1990-10-01 | 2021-06-21 12:12:52 |
+------+------+------------+---------------------+
```

`now()`函数可以获取系统的时间，并且是**datetime**类型的。

```mysql
insert into t_user (id,name,birth,create_time) values(122,'Jan','2012-12-23',now());
mysql> select * from t_user;
+------+------+------------+---------------------+
| id   | name | birth      | create_time         |
+------+------+------------+---------------------+
|  123 | Tim  | 1990-10-01 | 2021-06-21 12:12:52 |
|  122 | Jan  | 2012-12-23 | 2022-07-17 12:28:10 |
|  111 | Nik  | 2011-06-23 | 2022-07-17 12:28:34 |
+------+------+------------+---------------------+
```

当然了，`datetime`也是支持函数`date_format`进行格式化显示的

```mysql
mysql> select id,name,birth,date_format(create_time,'%h/%i/%s %Y-%m-%d')as create_time from t_user;
+------+------+------------+---------------------+
| id   | name | birth      | create_time         |
+------+------+------------+---------------------+
|  123 | Tim  | 1990-10-01 | 12/12/52 2021-06-21 |
|  122 | Jan  | 2012-12-23 | 12/28/10 2022-07-17 |
|  111 | Nik  | 2011-06-23 | 12/28/34 2022-07-17 |
+------+------+------------+---------------------+
```

## 修改表中数据update

```mysql
update 表名 set 字段名1=新值1，字段名2=新值2，字段名3=新值3...where 条件
```

这里的where条件是用来判断修改哪一行的数据。

```mysql
mysql> select * from t_user;
+------+------+------------+---------------------+
| id   | name | birth      | create_time         |
+------+------+------------+---------------------+
|  123 | Tim  | 1990-10-01 | 2021-06-21 12:12:52 |
|  122 | Jan  | 2012-12-23 | 2022-07-17 12:28:10 |
|  111 | Nik  | 2011-06-23 | 2022-07-17 12:28:34 |
+------+------+------------+---------------------+
```

```mysql
update t_user set birth='2013-12-01',create_time=now() where id=123;
mysql> select * from t_user;
+------+------+------------+---------------------+
| id   | name | birth      | create_time         |
+------+------+------------+---------------------+
|  123 | Tim  | 2013-12-01 | 2022-07-17 12:58:55 |
|  122 | Jan  | 2012-12-23 | 2022-07-17 12:28:10 |
|  111 | Nik  | 2011-06-23 | 2022-07-17 12:28:34 |
+------+------+------------+---------------------+
```

如果没有了where条件，就是更新了所有。

```mysql
 update t_user set create_time=now();
 mysql> select * from t_user;
+------+------+------------+---------------------+
| id   | name | birth      | create_time         |
+------+------+------------+---------------------+
|  123 | Tim  | 2013-12-01 | 2022-07-17 13:00:18 |
|  122 | Jan  | 2012-12-23 | 2022-07-17 13:00:18 |
|  111 | Nik  | 2011-06-23 | 2022-07-17 13:00:18 |
+------+------+------------+---------------------+
```

## 删除表中数据delete

```mysql
delete from 表名 where 条件;
```

如果没有条件，整个表都会被删除！！

```mysql
delete from t_user where id=111;
mysql> select * from t_user;
+------+------+------------+---------------------+
| id   | name | birth      | create_time         |
+------+------+------------+---------------------+
|  123 | Tim  | 2013-12-01 | 2022-07-17 13:00:18 |
|  122 | Jan  | 2012-12-23 | 2022-07-17 13:00:18 |
+------+------+------------+---------------------+
```

## insert插入多条数据

```mysql
insert into t_user (id,name,birth,create_time) values
(1,'zs','1980-10-11',now()), 
(2,'lisi','1981-10-11',now()),
(3,'wangwu','1982-10-11',now());
mysql> select * from t_user;
+------+--------+------------+---------------------+
| id   | name   | birth      | create_time         |
+------+--------+------------+---------------------+
|    1 | zs     | 1980-10-11 | 2022-07-17 13:41:43 |
|    2 | lisi   | 1981-10-11 | 2022-07-17 13:41:43 |
|    3 | wangwu | 1982-10-11 | 2022-07-17 13:41:43 |
+------+--------+------------+---------------------+
```

语法：

```mysql
insert into t_user(字段名1,字段名2...) values
(),
(),
(),
();
```

## 快速创建表(复制表)

```mysql
create table emp2 as select * from emp;
mysql> show tables;
+------------------------+
| Tables_in_bjpowernnode |
+------------------------+
| dept                   |
| emp                    |
| emp2                   |
| salgrade               |
| t_student              |
| t_user                 |
+------------------------+
mysql> select * from emp2;
+-------+--------+-----------+------+------------+---------+---------+--------+
| EMPNO | ENAME  | JOB       | MGR  | HIREDATE   | SAL     | COMM    | DEPTNO |
+-------+--------+-----------+------+------------+---------+---------+--------+
|  7369 | SMITH  | CLERK     | 7902 | 1980-12-17 |  800.00 |    NULL |     20 |
|  7499 | ALLEN  | SALESMAN  | 7698 | 1981-02-20 | 1600.00 |  300.00 |     30 |
|  7521 | WARD   | SALESMAN  | 7698 | 1981-02-22 | 1250.00 |  500.00 |     30 |
|  7566 | JONES  | MANAGER   | 7839 | 1981-04-02 | 2975.00 |    NULL |     20 |
|  7654 | MARTIN | SALESMAN  | 7698 | 1981-09-28 | 1250.00 | 1400.00 |     30 |
|  7698 | BLAKE  | MANAGER   | 7839 | 1981-05-01 | 2850.00 |    NULL |     30 |
|  7782 | CLARK  | MANAGER   | 7839 | 1981-06-09 | 2450.00 |    NULL |     10 |
|  7788 | SCOTT  | ANALYST   | 7566 | 1987-04-19 | 3000.00 |    NULL |     20 |
|  7839 | KING   | PRESIDENT | NULL | 1981-11-17 | 5000.00 |    NULL |     10 |
|  7844 | TURNER | SALESMAN  | 7698 | 1981-09-08 | 1500.00 |    0.00 |     30 |
|  7876 | ADAMS  | CLERK     | 7788 | 1987-05-23 | 1100.00 |    NULL |     20 |
|  7900 | JAMES  | CLERK     | 7698 | 1981-12-03 |  950.00 |    NULL |     30 |
|  7902 | FORD   | ANALYST   | 7566 | 1981-12-03 | 3000.00 |    NULL |     20 |
|  7934 | MILLER | CLERK     | 7782 | 1982-01-23 | 1300.00 |    NULL |     10 |
+-------+--------+-----------+------+------------+---------+---------+--------+
```

原理是将一个查询结果当作一张新表，实现快速表的复制

```mysql
create table mytable as select empno,ename from emp where job = 'MANAGER';
mysql> select * from mytable;
+-------+-------+
| empno | ename |
+-------+-------+
|  7566 | JONES |
|  7698 | BLAKE |
|  7782 | CLARK |
+-------+-------+
```

## 将查询结果插入到表中

用的不多，了解就行了。

```mysql
create table dept_bak as select * from dept;
mysql> select * from dept_bak;
+--------+------------+----------+
| DEPTNO | DNAME      | LOC      |
+--------+------------+----------+
|     10 | ACCOUNTING | NEW YORK |
|     20 | RESEARCH   | DALLAS   |
|     30 | SALES      | CHICAGO  |
|     40 | OPERATIONS | BOSTON   |
+--------+------------+----------+
insert into dept_bak select * from dept;
mysql> select * from dept_bak;
+--------+------------+----------+
| DEPTNO | DNAME      | LOC      |
+--------+------------+----------+
|     10 | ACCOUNTING | NEW YORK |
|     20 | RESEARCH   | DALLAS   |
|     30 | SALES      | CHICAGO  |
|     40 | OPERATIONS | BOSTON   |
|     10 | ACCOUNTING | NEW YORK |
|     20 | RESEARCH   | DALLAS   |
|     30 | SALES      | CHICAGO  |
|     40 | OPERATIONS | BOSTON   |
+--------+------------+----------+
```

## 快速删除表中所有数据

使用`delete`不增加`where`条件也能删除表中所有数据

```mysql
delete from dept_bak;
mysql> select * from dept_bak;
Empty set (0.00 sec)
```

但是它可以回滚数据：

```mysql
mysql> start transaction;
Query OK, 0 rows affected (0.00 sec)
mysql> rollback;
Query OK, 0 rows affected (0.00 sec)

mysql> select * from dept_bak;
+--------+------------+----------+
| DEPTNO | DNAME      | LOC      |
+--------+------------+----------+
|     10 | ACCOUNTING | NEW YORK |
|     20 | RESEARCH   | DALLAS   |
|     30 | SALES      | CHICAGO  |
|     40 | OPERATIONS | BOSTON   |
|     10 | ACCOUNTING | NEW YORK |
|     20 | RESEARCH   | DALLAS   |
|     30 | SALES      | CHICAGO  |
|     40 | OPERATIONS | BOSTON   |
+--------+------------+----------+
8 rows in set (0.00 sec)
```

但是从底层逻辑上来说，delete是一个个来删除表中的数据，效率比较低。

另外一个快速删除表中所有数据的方法是`truncate`

```mysql
truncate table 表名;
```

这个操作属于`DDL`中的操作。

使用`truncate`可以快速删除表中的所有数据，但是不支持数据回滚，因此要考虑再三再去使用它。

> delete语句删除数据的原理？（delete属于DML语句！！！）
>             表中的数据被删除了，但是这个数据在硬盘上的真实存储空间不会被释放！！！
>             这种删除缺点是：删除效率比较低。
>             这种删除优点是：支持回滚，后悔了可以再恢复数据！！！
> truncate语句删除数据的原理？
>             这种删除效率比较高，表被一次截断，物理删除。
>             这种删除缺点：不支持回滚。
>             这种删除优点：快速。

在`DDL`中也有删除表的操作`drop`，但是`drop`是删除整个表，表和表的数据全部删除，`truncate`删除的仅仅只是表中的所有数据，表的结构还在。

# 约束

## 什么是约束？

约束对应的英语单词：constraint
在创建表的时候，我们可以给表中的字段加上一些约束，来保证这个表中数据的完整性、有效性！！！约束的作用就是为了保证：表中的数据有效！！

## 约束的分类

* 非空约束 `not null`
* 唯一性约束 `unique`
* 主键约束`primary key`
* 外键约束 `foreign key`
* 检查约束 `check`（mysql不支持，oracle支持）

使用语法：

在创建表的时候

```mysql
create table 表名(
    字段名1 类型1 约束，
    字段名2 类型2 约束，
    字段名3 类型3 约束
);
```

## 非空约束

```mysql
drop table if exists t_vip;
create table t_vip(
    id int,
    name varchar(255) not null
);
insert into t_vip(id,name) values(1,'zhangsan');
insert into t_vip(id,name) values(2,'lisi');
```

对于批量化执行SQL语句，我们可以使用执行sql脚本的方法。

* 创建`.sql`文件
* 将语句写入文件
* source 脚本路径

```mysql
mysql> source D:\mysql_learning\mysql_learning\document\vip.sql
Query OK, 0 rows affected, 1 warning (0.01 sec)

Query OK, 0 rows affected (0.02 sec)

Query OK, 1 row affected (0.00 sec)

Query OK, 1 row affected (0.00 sec)
mysql> select * from t_vip;
+------+----------+
| id   | name     |
+------+----------+
|    1 | zhangsan |
|    2 | lisi     |
+------+----------+
```

由于给字段`name`加了非空约束，因此每次添加数据的时候，如果没有添加`name`字段的数据，就会报错，这样就保证了数据的可行性和完整性。

```mysql
mysql> insert into t_vip(id) values(123);
ERROR 1364 (HY000): Field 'name' doesn't have a default value
```

## 唯一性约束

唯一性约束`unique`约束的字段不能重复，但是可以为`null`

```mysql
drop table if exists t_vip;
    create table t_vip(
        id int,
        name varchar(255) unique,
        email varchar(255)
    );
    insert into t_vip(id,name,email) values(1,'zhangsan','zhangsan@123.com');
    insert into t_vip(id,name,email) values(2,'lisi','lisi@123.com');
    insert into t_vip(id,name,email) values(3,'wangwu','wangwu@123.com');
    select * from t_vip;
```

这个时候加上name重复的信息，就会报错。

```mysql
mysql> insert into t_vip(id,name,email) values(4,'wangwu','wangwu@sina.com');
ERROR 1062 (23000): Duplicate entry 'wangwu' for key 't_vip.name'
```

新需求：name和email两个字段联合起来具有唯一性！！！！

也就是说，一条新的数据，与表中的数据进行比较，name或者email字段有一个可以重复，但是如果和某一个数据比较，发现name和email字段的信息都重复了，就会报错。

```mysql
drop table if exists t_vip;
        create table t_vip(
            id int,
            name varchar(255) unique,  // 约束直接添加到列后面的，叫做列级约束。
            email varchar(255) unique
        );
```

这种创建方式不能满足我们的新要求，因为这样是分别对两个字段进行唯一性约束，两个字段，各自唯一。

 如果

```mysql
insert into t_vip(id,name,email) values(1,'zhangsan','zhangsan@123.com');
insert into t_vip(id,name,email) values(2,'zhangsan','zhangsan@sina.com');
```

这样插入新的数据就会报错，因为name字段重复了，我们的需求就是有可能会有重名的人出现，但是email是不一定一样的。

```mysql
drop table if exists t_vip;
            create table t_vip(
                id int,
                name varchar(255),
                email varchar(255),
                unique(name,email) // 约束没有添加在列的后面，这种约束被称为表级约束。
            );
```

表级约束，多个字段联合起来进行唯一性约束，与一行数据进行比较，如果两个字段名都重复了，就会报错了。

```mysql
# 但是这样是不会报错的
insert into t_vip(id,name,email) values(1,'zhangsan','zhangsan@123.com');
insert into t_vip(id,name,email) values(2,'zhangsan','zhangsan@sina.com');
```

表级约束一般用在需要给多个字段联合起来添加某一个约束的时候，需要使用表级约束：例如允许重名的情况出现，但是不允许同时email也重复了。

`unique`和`not null`可以联合起来进行约束

```mysql
drop table if exists t_vip;
        create table t_vip(
            id int,
            name varchar(255) not null unique
        );
```

**在mysql当中，如果一个字段同时被not null和unique约束的话，该字段自动变成主键字段。（注意：oracle中不一样！）**

**`not null`没有表级约束，只能用列级约束**

## 主键约束

`primary key`简称pk

主键字段：在字段上加上主键约束，该字段就是主键字段。

主键值：主键上的每个值就是主键值。

主键是每一行记录的唯一标识，是一种类似身份证的存在！！

每张表都应该有主键约束，如果没有主键约束，表就无效了。

**主键的特征：not null + unique（主键值不能是NULL，同时也不能重复！）**

列级约束：

```mysql
create table t_vip(
            id int primary key,  //列级约束
            name varchar(255)
        );
        insert into t_vip(id,name) values(1,'zhangsan');
        insert into t_vip(id,name) values(2,'lisi');

        insert into t_vip(id,name) values(2,'wangwu');# 报错，id为2，重复了
        ERROR 1062 (23000): Duplicate entry '2' for key 'PRIMARY'

        insert into t_vip(name) values('zhaoliu');# 报错，id为null，不能为null
        ERROR 1364 (HY000): Field 'id' doesn't have a default value
```

表级约束：

```mysql
create table t_vip(
            id int,
            name varchar(255),
            primary key(id)  // 表级约束
        );
```

表级约束是用来对多个字段进行联合添加约束：

```mysql
create table t_vip(
            id int,
            name varchar(255),
            email varchar(255),
            primary key(id,name)  # id和name字段联合起来作为主键约束
        );
        insert into t_vip(id,name,email) values(1,'zhangsan','zhangsan@123.com');
        insert into t_vip(id,name,email) values(1,'lisi','lisi@123.com');# 这样是正确的，不会报错

        insert into t_vip(id,name,email) values(1,'lisi','lisi@123.com');# 错误，报错，1-lisi同时重复
        ERROR 1062 (23000): Duplicate entry '1-lisi' for key 'PRIMARY'
```

一个字段的主键约束被称作单一主键，多个字段联合作为主键被称作复合主键，不推崇复合主键。

同时，一张表只能有一个主键约束。

作为主键约束的字段一般是`int` `bigint` `char` 类型，一般都是定长的，不建议`varchar`类型

> 主键除了：单一主键和复合主键之外，还可以这样进行分类？
>         自然主键：主键值是一个自然数，和业务没关系。
>         业务主键：**主键值和业务紧密关联**，例如拿银行卡账号做主键值。这就是业务主键！    
> 
> 在实际开发中使用业务主键多，还是使用自然主键多一些？
>         **自然主键使用比较多**，因为主键只要做到不重复就行，不需要有意义。
>         业务主键不好，因为主键一旦和业务挂钩，那么当业务发生变动的时候，
>         可能会影响到主键值，所以业务主键不建议使用。**尽量使用自然主键。**

使用`auto_increment`自动维护主键值，`auto_increment`表示自增，从1开始，以1递增！

```mysql
mysql> create table t_vip(
    ->  id int primary key auto_increment,
    ->  name varchar(32)
    -> );
# 之后多次插入数据：
insert into t_vip(name) values('zhangsan');
+----+----------+
| id | name     |
+----+----------+
|  1 | zhangsan |
|  2 | zhangsan |
|  3 | zhangsan |
|  4 | zhangsan |
|  5 | zhangsan |
|  6 | zhangsan |
|  7 | zhangsan |
|  8 | zhangsan |
+----+----------+
```

## 外键约束

当我们要将两个表连接的时候，各自会将一个字段值作为两个表连接的“接口”，但是有时候这两个表中这个字段值会有点出入，导致两个表连接的时候会有记录无法匹配的情况出现，而外键约束则能保证这两个表中，作为两表接口的字段值能完全匹配上。

两个概念：

子表和父表；

子表引用父表中的一个字段值作为外键约束。

**顺序：**

删除表的顺序？
            先删子，再删父。        

创建表的顺序？
            先创建父，再创建子。

删除数据的顺序？
            先删子，再删父。    

插入数据的顺序？
            先插入父，再插入子。

**`foreign key(cno) references t_class(classno)`**

```mysql
drop table if exists t_student;
drop table if exists t_class;

create table t_class( # 父表
    classno int primary key,
    classname varchar(255)
);
create table t_student( # 子表
    no int primary key auto_increment,
    name varchar(255),
    cno int,
    foreign key(cno) references t_class(classno)# 参照t_class中的classno对cno进行外键约束
);

insert into t_class(classno, classname) values(100, '北京市大兴区亦庄镇第二中学高三1班');
insert into t_class(classno, classname) values(101, '北京市大兴区亦庄镇第二中学高三1班');

insert into t_student(name,cno) values('jack', 100);
insert into t_student(name,cno) values('lucy', 100);
insert into t_student(name,cno) values('lilei', 100);
insert into t_student(name,cno) values('hanmeimei', 100);
insert into t_student(name,cno) values('zhangsan', 101);
insert into t_student(name,cno) values('lisi', 101);
insert into t_student(name,cno) values('wangwu', 101);
insert into t_student(name,cno) values('zhaoliu', 101);

select * from t_student;
select * from t_class;
```

```mysql
mysql> select * from t_student;
+----+-----------+------+
| no | name      | cno  |
+----+-----------+------+
|  1 | jack      |  100 |
|  2 | lucy      |  100 |
|  3 | lilei     |  100 |
|  4 | hanmeimei |  100 |
|  5 | zhangsan  |  101 |
|  6 | lisi      |  101 |
|  7 | wangwu    |  101 |
|  8 | zhaoliu   |  101 |
+----+-----------+------+
8 rows in set (0.00 sec)

mysql> select * from t_class;
+---------+---------------------------------------------------+
| classno | classname                                         |
+---------+---------------------------------------------------+
|     100 | 北京市大兴区亦庄镇第二中学高三1班                 |
|     101 | 北京市大兴区亦庄镇第二中学高三1班                 |
+---------+---------------------------------------------------+
2 rows in set (0.00 sec)
```

这个时候如果在外键约束之外添加字段`cno`的字段值

```mysql
mysql> insert into t_student(name,cno) values('kuku',110);
ERROR 1452 (23000): Cannot add or update a child row: a foreign key constraint fails (`bjpowernnode`.`t_student`, CONSTRAINT `t_student_ibfk_1` FOREIGN KEY (`cno`) REFERENCES `t_class` (`classno`))
```

就会报错。

> 外键引用父表中的某个字段，该字段应该至少有unique唯一性约束，但不一定是主键
> 
> 外键值可以是null。

# 存储引擎

Mysql中特有的术语，Oracle中没有。

存储引擎就是一个表存储/组织数据的方式。不同的存储引擎，表存储数据的方式不同。

## 指定存储引擎

在建表的时候可以在最后小括号的")"的右边使用：
        ENGINE来指定存储引擎。
        CHARSET来指定这张表的字符编码方式。

mysql默认的存储引擎是：`InnoDB`
mysql默认的字符编码方式是：`utf8`

```mysql
建表时指定存储引擎，以及字符编码方式。
    create table t_product(
        id int primary key,
        name varchar(255)
    )engine=InnoDB default charset=gbk;
```

通过`show create table 表名;`就能看到表的存储引擎以及编码方式了

```mysql
show create table t_product;
+-----------+----------------------------------------------------------------------------------------------------------------------------------------------+
| Table     | Create Table
                                                    |
+-----------+----------------------------------------------------------------------------------------------------------------------------------------------+
| t_product | CREATE TABLE `t_product` (
  `id` int NOT NULL,
  `name` varchar(255) DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=gbk |
+-----------+----------------------------------------------------------------------------------------------------------------------------------------------+
1 row in set (0.00 sec)
```

## 查看mysql支持哪些存储引擎

输入命令

```mysql
show engines \G
*************************** 1. row ***************************
      Engine: MEMORY
     Support: YES
     Comment: Hash based, stored in memory, useful for temporary tables
Transactions: NO
          XA: NO
  Savepoints: NO
*************************** 2. row ***************************
      Engine: MRG_MYISAM
     Support: YES
     Comment: Collection of identical MyISAM tables
Transactions: NO
          XA: NO
  Savepoints: NO
*************************** 3. row ***************************
      Engine: CSV
     Support: YES
     Comment: CSV storage engine
Transactions: NO
          XA: NO
  Savepoints: NO
*************************** 4. row ***************************
      Engine: FEDERATED
     Support: NO
     Comment: Federated MySQL storage engine
Transactions: NULL
          XA: NULL
  Savepoints: NULL
*************************** 5. row ***************************
      Engine: PERFORMANCE_SCHEMA
     Support: YES
     Comment: Performance Schema
Transactions: NO
          XA: NO
  Savepoints: NO
*************************** 6. row ***************************
      Engine: MyISAM
     Support: YES
     Comment: MyISAM storage engine
Transactions: NO
          XA: NO
  Savepoints: NO
*************************** 7. row ***************************
      Engine: InnoDB
     Support: DEFAULT
     Comment: Supports transactions, row-level locking, and foreign keys
Transactions: YES
          XA: YES
  Savepoints: YES
*************************** 8. row ***************************
      Engine: BLACKHOLE
     Support: YES
     Comment: /dev/null storage engine (anything you write to it disappears)
Transactions: NO
          XA: NO
  Savepoints: NO
*************************** 9. row ***************************
      Engine: ARCHIVE
     Support: YES
     Comment: Archive storage engine
Transactions: NO
          XA: NO
  Savepoints: NO
9 rows in set (0.00 sec)
```

## MyISAM

它管理的表具有以下特征：

* 格式文件——存储表的结构（mytable.frm）
* 数据文件——存储表中的内容（mytable.MYD）

* 索引文件——存储表上索引（mytable.MYI）：索引是一本书的目录，缩小扫描范围，提高查询效率的一种机制。

对于一张表来说，只要是主键，或者加有`unique`约束字段的，都会自动创建索引。

MyISAM存储引擎特点：

* 可被转换为压缩、只读表来节省空间，这是这种存储引擎的优势！！！！

* 不支持事务机制，安全性较低。



## InnoDB

mysql的默认存储引擎。

InnoDB支持事务，支持数据库崩溃后的恢复机制。

```mysql
	– 每个 InnoDB 表在数据库目录中以.frm 格式文件表示
	– InnoDB 表空间 tablespace 被用于存储表的内容（表空间是一个逻辑名称。表空间存储数据+索引。）
	– 提供一组用来记录事务性活动的日志文件
	– 用 COMMIT(提交)、SAVEPOINT 及ROLLBACK(回滚)支持事务处理
	– 提供全 ACID 兼容
	– 在 MySQL 服务器崩溃后提供自动恢复
	– 多版本（MVCC）和行级锁定
	– 支持外键及引用的完整性，包括级联删除和更新
```



## MEMORY

使用 MEMORY 存储引擎的表，其数据存储在内存中，且行的长度固定，这两个特点使得 MEMORY 存储引擎非常快。

```mysql
    – 在数据库目录内，每个表均以.frm 格式的文件表示。
    – 表数据及索引被存储在内存中。（目的就是快，查询快！）
    – 表级锁机制。
    – 不能包含 TEXT 或 BLOB 字段。
```

这个引擎的优点就是在于查询效率极高，不需要和硬盘交互，但是也极不安全，电脑断电之后，数据就会消失，因为索引和数据都是存在内存中的。





# 事务

## 基本概念

事务是一个完整的业务逻辑，是一个最小的工作单元，不可再分。

一个完整的业务逻辑包括一系列的操作，这些操作是整个业务逻辑中的最小单元，这些操作要么同时成功，要么同时失败。

由于只有DML语句中才会有事务的概念，因此事务只和`insert` `update` `delete`语句有关。

说到底，说到本质上，一个事务其实就是多条DML语句同时成功，或者同时失败！

事务是怎么做到多条DML语句同时成功和同时失败的呢？

InnoDB存储引擎：提供一组用来记录事务性活动的日志文件

```mysql
	事务开启了：
	insert
	insert
	insert
	delete
	update
	update
	update
	事务结束了！
```

在事务的执行过程中，每一条DML的操作都会记录到“事务性活动的日志文件”中。在事务的执行过程中，我们可以提交事务，也可以回滚事务。





## 提交事务&回滚事务

* 提交事务

  ​		清空事务性活动的日志文件，将数据全部彻底持久化到数据库表中。
  ​		提交事务标志着，事务的结束。并且是一种全部成功的结束。

* 回滚事务

​					将之前所有的DML操作全部撤销，并且清空事务性活动的日志文件
​					回滚事务标志着，事务的结束。并且是一种全部失败的结束。

​	提交事务：commit; 语句
​	回滚事务：rollback; 语句（回滚永远都是只能回滚到上一次的提交点！）

在MySQL中，默认的事务行为是自动提交的，每次命令成功之后就会进行一次自动提交。

通过执行命令`start transaction`关闭系统的自动提交。



回滚事务演示：

```mysql
mysql> select * from t_student;
+----+-----------+------+
| no | name      | cno  |
+----+-----------+------+
|  1 | jack      |  100 |
|  2 | lucy      |  100 |
|  3 | lilei     |  100 |
|  4 | hanmeimei |  100 |
|  5 | zhangsan  |  101 |
|  6 | lisi      |  101 |
|  7 | wangwu    |  101 |
|  8 | zhaoliu   |  101 |
+----+-----------+------+
8 rows in set (0.00 sec)

mysql> start transaction;
Query OK, 0 rows affected (0.01 sec)

mysql> insert into t_student values(9,'ame',100);
Query OK, 1 row affected (0.01 sec)

mysql> insert into t_student values(10,'ame',100);
Query OK, 1 row affected (0.00 sec)

mysql> insert into t_student values(11,'ame',100);
Query OK, 1 row affected (0.00 sec)

mysql> select * from t_student;
+----+-----------+------+
| no | name      | cno  |
+----+-----------+------+
|  1 | jack      |  100 |
|  2 | lucy      |  100 |
|  3 | lilei     |  100 |
|  4 | hanmeimei |  100 |
|  5 | zhangsan  |  101 |
|  6 | lisi      |  101 |
|  7 | wangwu    |  101 |
|  8 | zhaoliu   |  101 |
|  9 | ame       |  100 |
| 10 | ame       |  100 |
| 11 | ame       |  100 |
+----+-----------+------+
11 rows in set (0.00 sec)

mysql> rollback;
Query OK, 0 rows affected (0.01 sec)

mysql> select * from t_student;
+----+-----------+------+
| no | name      | cno  |
+----+-----------+------+
|  1 | jack      |  100 |
|  2 | lucy      |  100 |
|  3 | lilei     |  100 |
|  4 | hanmeimei |  100 |
|  5 | zhangsan  |  101 |
|  6 | lisi      |  101 |
|  7 | wangwu    |  101 |
|  8 | zhaoliu   |  101 |
+----+-----------+------+
8 rows in set (0.00 sec)
```

提交事务演示：

```mysql
mysql> create table t_student(
    -> no int primary key auto_increment,
    -> name varchar(32)
    -> );
Query OK, 0 rows affected (0.03 sec)

mysql> select * from t_student;
Empty set (0.00 sec)

mysql> start transaction;
Query OK, 0 rows affected (0.00 sec)

mysql> insert into t_student values(1,'jack');
Query OK, 1 row affected (0.00 sec)

mysql> insert into t_student(name) values('nick');
Query OK, 1 row affected (0.00 sec)

mysql> insert into t_student(name) values('nick');
Query OK, 1 row affected (0.00 sec)

mysql> insert into t_student(name) values('nick');
Query OK, 1 row affected (0.00 sec)

mysql> insert into t_student(name) values('nick');
Query OK, 1 row affected (0.00 sec)

mysql> insert into t_student(name) values('nick');
Query OK, 1 row affected (0.00 sec)

mysql> commit;
Query OK, 0 rows affected (0.01 sec)

mysql> select * from t_student;
+----+------+
| no | name |
+----+------+
|  1 | jack |
|  2 | nick |
|  3 | nick |
|  4 | nick |
|  5 | nick |
|  6 | nick |
+----+------+
6 rows in set (0.00 sec)

mysql> rollback;
Query OK, 0 rows affected (0.00 sec)

mysql> select * from t_student;
+----+------+
| no | name |
+----+------+
|  1 | jack |
|  2 | nick |
|  3 | nick |
|  4 | nick |
|  5 | nick |
|  6 | nick |
+----+------+
6 rows in set (0.00 sec)
```

`commit`操作实际上是将数据持久化的操作，在进行这个操作之前，仍在事务进行当作，数据仍然可以进行回滚，但是数据持久化之后就不能进行回滚了。





## 事务的四个特性

* A ： 原子性

  事务是最小的工作单元，不可再分。

* C： 一致性

​			所有事务要求，在同一个事务当中，所有操作必须同时成功，或者同时失败，保证数据的一致性。

* I： 隔离性

  不同的事务之间具有隔离，当两个事务想要操作同一张表的时候，他们之间的墙就会产生一定的隔离作用

* D： 持久性

  事务开始的标志一般是`start transaction`, 事务最终结束的标志是进行`commit`操作，对数据进行了持久化，相当于将数据写进硬盘里。



## 事务的隔离性

事务和事务之间的隔离性具有四个不同的隔离级别：

* 读未提交 `read uncommitted`
  * 事务A可以读取到事务B未提交的数据。
  * 但是这种隔离级别会出现脏读现象，我们称读到脏数据
* 读已提交 `read committed`
  * 事务A只能读取到事务B已经提交的数据。
  * 不可重复读取数据：在事务开启之后，第一次读到的数据是3条，当前事务还没有结束，可能第二次再读取的时候，读到的数据是4条，3不等于4，称为不可重复读取。
* 可重复读 `repeatable read` （mysql默认的隔离级别）
  * 两个事务对同一张表进行操作，不管对方是怎样操作的，各自只能看到自己事务中所做出的操作，即使事务B提交了，事务A也无法读取事务B修改后的数据。
* 序列化 `serializable`（最高的隔离级别）
  * 效率最低，安全级别最高
  * 这种隔离级别表现为事务排队，不能并发，事务A还在操作表1，事务B如果想要对表1进行操作，需要等事务A结束。



## 验证各种事务隔离级别

查看隔离级别：

```mysql
查看系统隔离级别：select @@global.tx_isolation;
查看会话隔离级别(5.0以上版本)：select @@tx_isolation;
查看会话隔离级别(8.0以上版本)：select @@transaction_isolation;
```

```mysql
mysql> select @@transaction_isolation;
+-------------------------+
| @@transaction_isolation |
+-------------------------+
| REPEATABLE-READ         |  # mysql默认的隔离级别
+-------------------------+
```

设置隔离级别：

```mysql
mysql> set global transaction isolation level read uncommitted;
mysql> set global transaction isolation level read committed;
mysql> set global transaction isolation level repeatable read;
mysql> set global transaction isolation level serializable;
```

设置完后记得重新登陆一下mysql



* `read uncommitted`验证

![image-20220718140606285](https://raw.githubusercontent.com/danjuan-77/picgo/main/202207181406418.png)

右边事务进行`insert`后，左边事务是看的见的



* `read committed`验证

![image-20220718141117168](https://raw.githubusercontent.com/danjuan-77/picgo/main/202207181411356.png)

* `repeatable read`验证

![image-20220718142107958](https://raw.githubusercontent.com/danjuan-77/picgo/main/202207181421136.png)

右侧事务修改完之后，左侧事务也看不见修改。



* `serializable`验证

![image-20220718143721244](https://raw.githubusercontent.com/danjuan-77/picgo/main/202207181437364.png)

右边事务在等左边事务`commit`，才会执行。





# 索引

## 基本概念

通过给字段名上增加索引，可以提高查询的效率。

一张表的一个字段可以添加一个索引，当然，多个字段联合起来也可以添加索引。索引相当于一本书的目录，是为了缩小扫描范围而存在的一种机制。

```mysql
select * from t_user where name = 'jack';
```

如果name字段没有索引，系统会将所有name中的字段值一个个地进行匹配，

如果name字段有索引，会通过jack的索引首先找到一个大致地方位，避免全局进行扫描匹配，从而提高效率。

索引是一种将我们存入的数据进行有序存储的机制，通过对数据进行有序存储，就可以使用类似二分查找之类的算法进行快速查找。

## 实现原理

在任何数据库当中主键上都会自动添加索引对象，id字段上自动有索引，因为id是PK。另外在mysql当中，一个字段上如果有unique约束的话，也会自动创建索引对象。

在任何数据库当中，任何一张表的任何一条记录在硬盘存储上都有一个硬盘的物理存储编号。

在mysql当中，索引是一个单独的对象，不同的存储引擎以不同的形式存在，在MyISAM存储引擎中，索引存储在一个.MYI文件中。在InnoDB存储引擎中，索引存储在一个逻辑名称叫做tablespace的当中。在MEMORY存储引擎当中索引被存储在内存当中。不管索引存储在哪里，索引在mysql当中都是一个树的形式存在。（自平衡二叉树：B-Tree）

MySQL中的主键和`unique`约束字段会自动增加索引。



## 什么时候增加索引呢？

* 数据量庞大
* 该字段值经常出现在`where`语句中，作为条件的存在，这说明这个字段经常被扫描。
* 这个字段很少用到DML操作（因为每次的DML操作都会导致索引重新排序）。

建议不要随意添加索引，因为索引也是需要维护的，太多的话反而会降低系统的性能。
建议通过主键查询，建议通过unique约束的字段进行查询，效率是比较高的。



## 索引的查询，创建，删除

* 查询一个SQL语句是否用到了索引进行查询？

使用`explain`关键字

```mysql
explain select * from emp where ename='KING';
```

没有使用索引：![image-20220718170134099](https://raw.githubusercontent.com/danjuan-77/picgo/main/202207181701177.png)

这里的`rows=14`说明查了14行数据，逐行遍历了属于是。同时`type=all`，说明是全局扫描进行查询的。



使用索引：![image-20220718170018391](https://raw.githubusercontent.com/danjuan-77/picgo/main/202207181700492.png)

这里的`rows=1`，`type=ref`,`key=emp_ename_index`说明是使用了索引进行搜索的。



* 创建索引

给`表y`中的`x字段`创建`索引z`

```mysql
create index 索引名z on 表y（字段名x）;
```



* 删除索引

将`表x`中的`索引y`删除

```mysql
drop 索引名y on 表名x;
```



## 索引失效

* 1.使用模糊搜索的时候，模糊匹配使用%或者_开头就会失效

![image-20220718170531465](https://raw.githubusercontent.com/danjuan-77/picgo/main/202207181705546.png)

* 2.使用or的时候，要求or两边的字段都要有索引才会使用索引进行搜索，如果其中一边有一个字段没有索引，那么另一个字段上的索引也会失效。

![image-20220718170649248](https://raw.githubusercontent.com/danjuan-77/picgo/main/202207181706340.png)

* 3.使用复合索引，没有使用左侧的列查找，索引失效

复合索引：两个字段或者多个字段联合起来添加索引

```mysql
create index emp_job_sal_index on emp(job,sal);
```

正常使用索引，用job字段作为条件查询

![image-20220718171453215](https://raw.githubusercontent.com/danjuan-77/picgo/main/202207181714301.png)

索引失效，没有使用job字段作为条件查询

![image-20220718171527482](https://raw.githubusercontent.com/danjuan-77/picgo/main/202207181715585.png)

* 4.在where当中索引列参加了运算，索引失效

```mysql
create index emp_sal_index on emp(sal);
explain select * from emp where sal = 800;// 使用了索引
 explain select * from emp where sal+1 = 800;// 索引失效
```

正常使用索引：

![image-20220718171640722](https://raw.githubusercontent.com/danjuan-77/picgo/main/202207181716855.png)

索引失效：

![image-20220718171654289](https://raw.githubusercontent.com/danjuan-77/picgo/main/202207181716374.png)

* 5.在where当中索引列使用了函数

![image-20220718171804093](https://raw.githubusercontent.com/danjuan-77/picgo/main/202207181718178.png)



## 索引的分类

* 单一索引 一个字段上添加索引
* 复合索引 多个字段联合添加索引
* 主键索引 有主键的字段的索引
* 唯一性索引 `uniuqe`约束字段的索引



唯一性较弱的字段上添加索引的用处不大。





# 视图

## 概述

`view`

view可以看作是一张“虚拟表”，（但是他也是会作为文件存在的）

当我们通过复杂的查询语句获取一张表的时候，可以将这张表作为一个视图，和创建一个新表不同，在视图上进行的DML操作会对数据原本存在的表产生影响，也就是说，原表中的数据会被修改，但是创建新表，在新表中进行操作，不会对原表造成影响。

**视图就是个存放检索结果的临时表。**





## 创建视图，删除视图

创建视图：

```mysql
create view 视图名称 as DQM语句（例如select查询语句）;
```

删除视图：

```mysql
drop view 视图名称;
```

create view view_name as 这里的语句必须是DQL语句;





## 视图的作用

我们可以面向视图对象进行增删改查，对视图对象的增删改查，会导致原表被操作！（视图的特点：通过对视图的操作，会影响到原表数据。）

假设我们有一个复杂的SQL语句，这个语句需要在不同的位置上反复使用，但是每次写很长的程序就很慢。为了简化操作，可以使用视图，创建的视图对象，就是我们所需要反复操作的数据，之后我们想要修改这些数据，就省去了检索的步骤，可以直接对视图进行操作，达到对原表数据的增删查改。

C:Create（增）
R:Retrive（查：检索）
U:Update（改）
D:Delete（删）



创建视图对象：

```mysql
create view 
		emp_dept_view
	as
		select 
			e.ename,e.sal,d.dname
		from
			emp e
		join
			dept d
		on
			e.deptno = d.deptno;
			
mysql> select * from emp_dept_view;
+--------+---------+------------+
| ename  | sal     | dname      |
+--------+---------+------------+
| SMITH  |  800.00 | RESEARCH   |
| ALLEN  | 1600.00 | SALES      |
| WARD   | 1250.00 | SALES      |
| JONES  | 2975.00 | RESEARCH   |
| MARTIN | 1250.00 | SALES      |
| BLAKE  | 2850.00 | SALES      |
| CLARK  | 2450.00 | ACCOUNTING |
| SCOTT  | 3000.00 | RESEARCH   |
| KING   | 5000.00 | ACCOUNTING |
| TURNER | 1500.00 | SALES      |
| ADAMS  | 1100.00 | RESEARCH   |
| JAMES  |  950.00 | SALES      |
| FORD   | 3000.00 | RESEARCH   |
| MILLER | 1300.00 | ACCOUNTING |
+--------+---------+------------+
```

对视图对象进行修改：

```mysql
mysql> update emp_dept_view set sal=1000 where dname='ACCOUNTING';
Query OK, 3 rows affected (0.01 sec)
Rows matched: 3  Changed: 3  Warnings: 0
```

查看原表中的数据，发现被修改了：

```mysql
mysql> select * from emp;
+-------+--------+-----------+------+------------+---------+---------+--------+
| EMPNO | ENAME  | JOB       | MGR  | HIREDATE   | SAL     | COMM    | DEPTNO |
+-------+--------+-----------+------+------------+---------+---------+--------+
|  7369 | SMITH  | CLERK     | 7902 | 1980-12-17 |  800.00 |    NULL |     20 |
|  7499 | ALLEN  | SALESMAN  | 7698 | 1981-02-20 | 1600.00 |  300.00 |     30 |
|  7521 | WARD   | SALESMAN  | 7698 | 1981-02-22 | 1250.00 |  500.00 |     30 |
|  7566 | JONES  | MANAGER   | 7839 | 1981-04-02 | 2975.00 |    NULL |     20 |
|  7654 | MARTIN | SALESMAN  | 7698 | 1981-09-28 | 1250.00 | 1400.00 |     30 |
|  7698 | BLAKE  | MANAGER   | 7839 | 1981-05-01 | 2850.00 |    NULL |     30 |
|  7782 | CLARK  | MANAGER   | 7839 | 1981-06-09 | 1000.00 |    NULL |     10 |
|  7788 | SCOTT  | ANALYST   | 7566 | 1987-04-19 | 3000.00 |    NULL |     20 |
|  7839 | KING   | PRESIDENT | NULL | 1981-11-17 | 1000.00 |    NULL |     10 |
|  7844 | TURNER | SALESMAN  | 7698 | 1981-09-08 | 1500.00 |    0.00 |     30 |
|  7876 | ADAMS  | CLERK     | 7788 | 1987-05-23 | 1100.00 |    NULL |     20 |
|  7900 | JAMES  | CLERK     | 7698 | 1981-12-03 |  950.00 |    NULL |     30 |
|  7902 | FORD   | ANALYST   | 7566 | 1981-12-03 | 3000.00 |    NULL |     20 |
|  7934 | MILLER | CLERK     | 7782 | 1982-01-23 | 1000.00 |    NULL |     10 |
+-------+--------+-----------+------+------------+---------+---------+--------+
```



# DBA命令

## 数据导入

要进入Mysql

创建数据库

```mysql
create database database_name;
```

使用数据库

```mysql
use database_name;
```

初始化数据库

```mysql
source .sql文件地址，不能加双引号；
```



## 数据导出

要在windows的dos环境下进行

导出数据库

```shell
mysqldump database_name > 存放地址（.sql文件名） -u用户名 -p密码
```

导出数据库中的某个表

```shell
mysqldump database_name table_name > 存放地址（.sql文件名） -u用户名 -p密码
```

例如：

```shell
 C:\Users\LENOVO> mysqldump bjpowernnode emp > D:\test.sql -uroot -p123456
```

注意空格

![image-20220718190139768](https://raw.githubusercontent.com/danjuan-77/picgo/main/202207181901876.png)

# 数据库设计三范式

第一范式：要求任何一张表必须有主键，每一个字段原子性不可再分。

第二范式：建立在第一范式之上，要求所有非主键字段必须完全依赖主键，不能部分依赖

第三范式：建立在第二范式之上，要求所有非主键字段必须直接依赖主键，不要产生传递依赖

按照三范式设计数据库，可以避免表中数据的冗余，造成空间不必要的浪费。

三种基本关系：

<img src="https://raw.githubusercontent.com/danjuan-77/picgo/main/202207182004851.png" alt="image-20220718200454745" style="zoom:50%;" />

## 第一范式

**必须有主键，并且每一个字段都是原子性不可再分。**

```mysql
	学生编号 	学生姓名 		联系方式
	------------------------------------------
	1001		张三		zs@gmail.com,1359999999
	1002		李四		ls@gmail.com,13699999999
	1001		王五		ww@163.net,13488888888

```

不满足第一范式：没有主键，并且`联系方式`可再分

修改：

```mysql
	学生编号(pk) 		学生姓名	  邮箱地址		   联系电话
	---------------------------------------------------------
	1001				张三		zs@gmail.com	1359999999
	1002				李四		ls@gmail.com	13699999999
	1003				王五		ww@163.net		13488888888
```







## 第二范式

**要求所有非主键字段必须完全依赖主键，不要产生部分依赖。**

```mysql
	学生编号 		学生姓名  教师编号   教师姓名
-----------------------------------------------------
	1001			张三		001		王老师
	1002			李四		002		赵老师
	1003			王五		001		王老师
	1001			张三		002		赵老师
```

不满足第一范式：

```mysql
	学生编号+教师编号(pk)		     学生姓名  		 教师姓名
	----------------------------------------------------
	1001			001				张三			王老师
	1002			002				李四			赵老师
	1003			001				王五			王老师
	1001			002				张三			赵老师
```

但是由于复合主键，导致部分依赖主键：“张三”依赖1001，“王老师”依赖001，显然产生了部分依赖。数据冗余了。空间浪费了。“张三”重复了，“王老师”重复了。

对于这种多对多关系，我们采取`“建立三张表，关系表两外键”`的方式

```mysql
		学生表
		学生编号(pk)			学生名字
		------------------------------------
		1001					张三
		1002					李四
		1003					王五
		
		教师表
		教师编号(pk)		教师姓名
		--------------------------------------
		001					王老师
		002					赵老师

		学生教师关系表
		id(pk)				  学生编号(fk)			    教师编号(fk)
		------------------------------------------------------------
		1						1001						001
		2						1002						002
		3						1003						001
		4						1001						002
```



## 第三范式

**要求所有非主键字典必须直接依赖主键，不要产生传递依赖。**

```mysql
	  学生编号（PK）        学生姓名   班级编号       班级名称
	---------------------------------------------------------
		1001				张三		01			一年一班
		1002				李四		02			一年二班
		1003				王五		03			一年三班
		1004				赵六		03			一年三班
```

一年一班依赖01，01依赖1001，产生了传递依赖。

对于这种一对多的关系，我们采取`建立两张表，多的表加外键`

```mysql
		班级表：一
		班级编号(pk)				班级名称
		----------------------------------------
		01								一年一班
		02								一年二班
		03								一年三班

		学生表：多

		学生编号（PK）      学生姓名     班级编号(fk)
		-------------------------------------------
		1001				张三			01			
		1002				李四			02			
		1003				王五			03			
		1004				赵六			03	
```



## 总结

* 一对多

  两张表，多的表加外键

* 多对多

  三张表，关系表两个外键

* 一对一

  对于一些巨大的表，需要对表进行拆分，拆成两张表，外键唯一



> 数据库设计三范式是理论上的。
>
> 实践和理论有的时候有偏差。
>
> 最终的目的都是为了满足客户的需求，有的时候会拿冗余换执行速度。
>
> 因为在sql当中，表和表之间连接次数越多，效率越低。（笛卡尔积）
>
> 有的时候可能会存在冗余，但是为了减少表的连接次数，这样做也是合理的，并且对于开发人员来说，sql语句的编写难度也会降低。
>
> 面试的时候把这句话说上：他就不会认为你是初级程序员了！































































