---
title: MySQL
date: 2019-02-26 10:52:43
tags:
	- 笔记
categories: 课程
---

<h5>新增数据库</h5>

''' create database 数据库名字 [库选项]；

库选项：用来约束数据库，分为字符集设定charset、校对集设定collation
注：常用字符集为GBK、utf8


'''create database mydatabase charset utf8;

创建中文名的database：

'''
set names gbk
create database 我的数据库 charset utf8;
'''

查看所有数据库：
'''show databases;

查看指定部分的数据库，即模糊查询
'''show databases like 'pattern';

更新、修改数据库：
--数据库名字不可以修改
--数据库仅允许修改：字符集charset和校对集collation
'''alter database 数据库的名字 charset GBK;


删除数据库：
'''drop database 数据库名字
注意：删除不可逆

新增数据表：
'''create table if not exists 表名(字段名字 数据类型，字段名字 数据类型)[表选项]；'''
'''
create table if not exists mydatabase.student(
name varchar(10),
gender varchar(10),
number varchar(10), 
age int
)
charset utf8;
'''

查看所有表：

'''show tables '''

查看表结构：查看表中的字段信息
'''desc columns from 表名
或者：
describe columns from 表名
或者：
show columns from 表名'''


- 修改数据表
	- 修改表本身：表名、表选项(charset collation)
	- '''修改表名：
rename table 老表名 to 新表名
修改表选项：
alter table my_student charset utf8'''

- 删除数据表
	- '''drop table 表名;'''

- 4.3数据操作
	- A.新增数据：insert
		- 场景1：给table中的所有字段都插入数据：无需指定字段所属的列，但要求数据的顺序必须与表中字段列的顺序一致
		- '''insert into 表名 values (1列的值，2列的值，3列的值，……)；'''
		- 场景2：只在部分字段中插入数据，则需要选定字段列表：
		- '''insert into 表名 字段列表 values （值列表1),(值列表2)，……；
		- insert into my_student(number, sex, name, id) values(“itcast001”，“male”，“Tom”，“3”，),(“itcast002”，“female”，“Mary”，“15”，)'''
	- 查看数据
		- '''查看表中全部数据：
		- select * from 表名
		- 按条件查看数据：
		- select 筛选列名 from 表名 where 筛选条件；
		- select id,number,sex from my_student where id=1；
	- 更新数据
		- update 表名 set 字段 = 值 [where 筛选条件]
		- #这里不加table
	- 删除数据 
		- delete from 表名 where 筛选条件
		- #这里不加table
	- 