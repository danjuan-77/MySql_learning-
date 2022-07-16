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
source D:/mysql_learning/mysql_learning/document/bjpowernode.sql
```

注意文件名不能有双引号，不能用反斜杠，命令结尾没有分号

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



## 分组函数/多行处理函数

**输入多行，输出一行。**

* count 计数
* sum 求和
* avg 平均值
* max 最大值
* min 最小值

> 注意：
> 		分组函数在使用的时候必须先进行分组，然后才能用。
> 		如果你没有对数据进行分组，整张表默认为一组。

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
    ->  	deptno,job,max(sal)
    -> from
    ->  	emp
    -> group by
    ->  	deptno,job# 根据多个选项进行分组
    -> order by
    ->  	deptno;
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
> 		内连接：
> 			等值连接
> 			非等值连接
> 			自连接
>
> ​		外连接：
> ​			左外连接（左连接）
> ​			右外连接（右连接）
>
> ​		全连接

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

















