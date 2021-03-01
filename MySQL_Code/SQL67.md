## &#128044; Description of the problem

###  牛客每天有很多人登录，请你统计一下牛客每个用户最近登录是哪一天。有一个登录(login)记录表，简况如下: 

```sql
mysql> select * from login;
+----+---------+-----------+------------+
| id | user_id | client_id | data       |
+----+---------+-----------+------------+
|  1 |       2 |         1 | 2020-10-12 |
|  2 |       3 |         2 | 2020-10-12 |
|  3 |       2 |         2 | 2020-10-13 |
|  4 |       3 |         2 | 2020-10-13 |
+----+---------+-----------+------------+
4 rows in set (0.00 sec)
```
- 第1行表示user_id为2的用户在2020-10-12使用了客户端id为1的设备登录了牛客网
- ...
- 第4行表示user_id为3的用户在2020-10-13使用了客户端id为2的设备登录了牛客网

###  还有一个用户(user_67)表，简况如下:


```sql
mysql> select * from user_67;
+----+----------+
| id | name     |
+----+----------+
|  1 | tm       |
|  2 | fh       |
|  3 | wangchao |
+----+----------+
3 rows in set (0.00 sec)
```

###  还有一个客户端(client)表，简况如下:

```sql
mysql> select * from client;
+----+--------+
| id | name   |
+----+--------+
|  1 | pc     |
|  2 | ios    |
|  3 | anroid |
|  4 | h5     |
+----+--------+
4 rows in set (0.00 sec)
```
### &#127800; 请你写出一个sql语句查询每个用户最近一天登录的日子，用户的名字，以及用户用的设备的名字，并且查询结果按照user的name升序排序，上面的例子查询结果如下:

```sql
+----------+-----+------------+
| u_n      | c_n | d          |
+----------+-----+------------+
| fh       | ios | 2020-10-13 |
| wangchao | ios | 2020-10-13 |
+----------+-----+------------+
2 rows in set (0.00 sec)
```

<details>
<summary>&#127808; View The sql &#127808;</summary>
  
```sql
mysql> create table login
    -> (id smallint(5) not null primary key,
    -> user_id smallint(5) not null,
    -> client_id smallint(5) not null,
    -> data date not null);
Query OK, 0 rows affected (0.03 sec)
```
```sql
mysql> insert into login
    -> values
    -> (1,2,1,'2020-10-12')，
    -> (2,3,2,'2020-10-12'),
    -> (3,2,2,'2020-10-13'),
    -> (4,3,2,'2020-10-13');
```
```sql
mysql> create table user_67
    -> (id smallint(5) not null primary key,
    ->  name varchar(50) not null);
Query OK, 0 rows affected (0.01 sec)
```
```sql
mysql> insert into user_67
    -> values
    -> (1,'tm'),
    -> (2,'fh'),
    -> (3,'wangchao');
Query OK, 3 rows affected (0.03 sec)
```
```sql
mysql> create table client
    -> (id smallint(5) not null primary key,
    -> name varchar(50) not null);
Query OK, 0 rows affected (0.03 sec)
```
```sql
mysql> insert into client
    -> values
    -> (1,'pc'),
    -> (2,'ios'),
    -> (3,'anroid'),
    -> (4,'h5');
```
</details>

### Answer

<details>
<summary>&#127808; 错误答案 &#127808;</summary>
  
```sql
# 错误答案，使用pc登录，思考为何？
# +----------+------+------------+-----------+
# | u_n      | name | date       | client_id |
# +----------+------+------------+-----------+
# | fh       | pc   | 2020-10-13 |         1 |
# | wangchao | ios  | 2020-10-13 |         2 |
# +----------+------+------------+-----------+
# 2 rows in set (0.00 sec)

select u.name u_n, c.name, max(date) date, l.client_id
from login l 
join user_67 u on l.user_id = u.id
join client c on l.client_id = c.id
group by u_n
order by u_n asc;
```
</details>


<details>
<summary>&#127808; 正确答案 &#127808;</summary>
  
```sql
# 正确答案
select u.name u_n, c.name c_n, lo.date d
from login lo
join (
    select user_id, max(date) date
    from login group by user_id
    )t1 on lo.date = t1.date and lo.user_id = t1.user_id
join user u on u.id = lo.user_id
join client c on c.id = lo.client_id
order by u_n asc;
```
</details>

