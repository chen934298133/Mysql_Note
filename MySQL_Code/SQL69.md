## &#128044; 68. Description of the problem

###  牛客每天有很多人登录，请你统计一下牛客每个用户最近登录是哪一天。有一个登录(login)记录表，简况如下: 

```sql
mysql> select * from login;
+----+---------+-----------+------------+
| id | user_id | client_id | date       |
+----+---------+-----------+------------+
|  1 |       2 |         1 | 2020-10-12 |
|  2 |       3 |         2 | 2020-10-12 |
|  3 |       1 |         2 | 2020-10-12 |
|  4 |       2 |         2 | 2020-10-13 |
|  5 |       1 |         2 | 2020-10-13 |
|  6 |       3 |         1 | 2020-10-14 |
|  7 |       4 |         1 | 2020-10-14 |
|  8 |       4 |         1 | 2020-10-15 |
+----+---------+-----------+------------+
8 rows in set (0.00 sec)
```
- 第1行表示user_id为2的用户在2020-10-12使用了客户端id为1的设备登录了牛客网，因为是第1次登录，所以是新用户
- ...
- 第4行表示user_id为2的用户在2020-10-13使用了客户端id为2的设备登录了牛客网，因为是第2次登录，所以是老用户
- ...
- 最后1行表示user_id为4的用户在2020-10-15使用了客户端id为1的设备登录了牛客网，因为是第2次登录，所以是老用户



### &#127800; 请你写出一个sql语句查询每个日期登录新用户个数，并且查询结果按照日期升序排序，上面的例子查询结果如下:

```sql
+------------+----------------------+
| date       | IFNULL(n1.new_num,0) |
+------------+----------------------+
| 2020-10-12 |                    3 |
| 2020-10-13 |                    0 |
| 2020-10-14 |                    1 |
| 2020-10-15 |                    0 |
+------------+----------------------+
```

**查询结果表明:**<br>
2020-10-12，有3个新用户(user_id为2，3，1)登录<br>
2020-10-13，没有新用户登录<br>
2020-10-14，有1个新用户(user_id为4)登录<br>
2020-10-15，没有新用户登录<br>


<details>
<summary>&#127808; View The sql &#127808;</summary>
  
```sql
mysql> create table login
    -> (id smallint(5) not null primary key,
    -> user_id smallint(5) not null,
    -> client_id smallint(5) not null,
    -> date date not null);
Query OK, 0 rows affected (0.03 sec)
```
```sql
insert into login
(id, user_id, client_id, date)
values
(1,2,1,'2020-10-12'),
(2,3,2,'2020-10-12'),
(3,1,2,'2020-10-12'),
(4,2,2,'2020-10-13'),
(5,1,2,'2020-10-13'),
(6,3,1,'2020-10-14'),
(7,4,1,'2020-10-14'),
(8,4,1,'2020-10-15')
on duplicate key 
update id = values(id), user_id = values(user_id), client_id = values(client_id), date = values(date);
```
</details>

### &#127800;  Answer

<details>
<summary>&#127808; IFNULL() + left join &#127808;</summary>
  
```sql
SELECT l.date,IFNULL(n1.new_num,0)
FROM login l
# 左连接表l1，有数据则显示数据，null则显示0
LEFT JOIN(
    # 表l1显示当日新登录用户个数，
    SELECT l1.date,COUNT(DISTINCT l1.user_id) AS new_num
    from login l1
    # 若 (表l1用户的登录日期 = 该用户最早的登录日期) 则累加 1
    where l1.date =(
        SELECT min(date) 
        FROM login l2
        where l2.user_id = l1.user_id
    )
    GROUP BY l1.date
) n1
ON l.date = n1.date
GROUP BY l.date
ORDER BY l.date
```
</details>


<details>
<summary>&#127808; 窗口函数row_number()over(partition by user_id order by date) &#127808;</summary>
  
```sql
select a.date,sum(case when t_rank=1 then 1 else 0 end)
# row_number()over(partition by user_id order by date) 按照user_id排序，累计date
# 即第二次登陆则会获取到一个新的date，t_rank为2
from (select date, row_number()over(partition by user_id order by date)as t_rank
     from login
     ) as a
group by a.date
```
</details>