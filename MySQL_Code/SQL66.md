## &#128044; Description of the problem

### &#127800; 牛客每天有很多人登录，请你统计一下牛客每个用户最近登录是哪一天。有一个登录(login)记录表，简况如下: 

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

### &#127800; 请你写出一个sql语句查询每个用户最近一天登录的日子，并且按照user_id升序排序，上面的例子查询结果如下:


```sql
+---------+------------+
| user_id | d          |
+---------+------------+
|       2 | 2020-10-13 |
|       3 | 2020-10-13 |
+---------+------------+
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

</details>

### Answer
<details>
<summary>&#127808; MAX MIN &#127808;</summary>
  

```sql
select user_id, max(date) d
from login 
group by user_id
order by user_id;
```
</details>

