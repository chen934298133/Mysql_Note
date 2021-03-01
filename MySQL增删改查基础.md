# &#127800; 数据库 &#127800;
## &#127800; 1. 新增数据库

```sql
create database 数据库名字 [库选项]；

# [库选项]：用来约束数据库，分为字符集设定charset、校对集设定collation
# 注：常用字符集为GBK、utf8

create database mydatabase charset utf8;
```

```sql
# 创建中文名的database
set names gbk
create database 我的数据库 charset utf8;
```

## &#127800; 2. 删除数据库：

```sql
# 注意：删除不可逆
drop database 数据库名字
```

## &#127800; 3. 更新、修改数据库：

```sql
# 数据库名字不可以修改
# 数据库仅允许修改：字符集charset和校对集collation
alter database 数据库的名字 charset GBK;
```


## &#127800; 4. 查看数据库：

```sql
# 查看所有数据库：
show databases;
```

```sql
# 查看指定部分的数据库，即模糊查询
show databases like 'pattern';
```


# &#127800; 数据表 &#127800; 
## &#127800; 1. 新增数据表
```sql
# 新增可能存在的数据表：
create table if not exists 表名(字段名字 数据类型，字段名字 数据类型)[表选项]；

create table if not exists mydatabase.student(
name varchar(10),
gender varchar(10),
number varchar(10), 
age int
)
charset utf8;
```
## &#127800; 2. 删除数据表

```sql
delete from 表名 where 筛选条件
# 这里不加table
```

## &#127800; 3. 更新、修改数据表

```sql
# 修改表名：
rename table 老表名 to 新表名
# 修改表选项：
alter table my_student charset utf8
# 修改表字段名
alter table login change data date date;
```


## &#127800; 4. 查看数据表

```sql
# 查看所有表：
show tables 
```
```sql
# 查看表结构：查看表中的字段信息
desc columns from 表名
# 或者：
describe columns from 表名
# 或者：
show columns from 表名
```

# &#127800; 数据操作 &#127800;
## &#127800; 1 新增数据
```sql
# 场景1: 给table中的所有字段都插入数据：无需指定字段所属的列，但要求数据的顺序必须与表中字段列的顺序一致
insert into 表名 
values 
(1列的值，2列的值，3列的值，……)；

# 场景2：只在部分字段中插入数据，则需要选定字段列表：
insert into 表名 
(字段列表) 
values 
(值列表1),(值列表2)，……；

eg:
# 场景一：
INSERT IGNORE INTO actor 
 VALUES(
     3, 'ED', 'CHASE', '2006-02-15 12:34:33'
 );
# ignore 若存在则忽略

# 场景二：
insert into my_student
(number, sex, name, id) 
values
("itcast001"，"male"，"Tom"，"3"),
("itcast002"，"female"，"Mary"，"15")；


```
## &#127800; 2 删除数据
## &#127800; 3 修改数据
```sql
# 更新数据表
update 表名 set 字段 = 值 [where 筛选条件]
# 这里不加table
```
## &#127800; 4 查询数据

```sql
# 查看表中全部数据：
select * from 表名
# 按条件查看数据：
select 筛选列名 from 表名 where 筛选条件；

eg:
select id,number,sex 
from my_student 
where id=1；
```

