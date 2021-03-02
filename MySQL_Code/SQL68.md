## &#128044; 68. Description of the problem

###  牛客每天有很多人登录，请你统计一下牛客每个用户最近登录是哪一天。有一个登录(login)记录表，简况如下: 

```sql
mysql> select * from login;
+----+---------+-----------+------------+
| id | user_id | client_id | date       |
+----+---------+-----------+------------+
|  1 |       2 |         1 | 2020-10-12 |
|  2 |       3 |         2 | 2020-10-12 |
|  3 |       2 |         2 | 2020-10-13 |
|  4 |       2 |         2 | 2020-10-13 |
|  5 |       4 |         1 | 2020-10-13 |
|  6 |       1 |         2 | 2020-10-13 |
|  7 |       1 |         2 | 2020-10-14 |
+----+---------+-----------+------------+
7 rows in set (0.00 sec)
```
- 第1行表示user_id为2的用户在2020-10-12使用了客户端id为1的设备第一次新登录了牛客网
- ...
- 第4行表示user_id为3的用户在2020-10-12使用了客户端id为2的设备登录了牛客网
- ...
- 最后1行表示user_id为1的用户在2020-10-14使用了客户端id为2的设备登录了牛客网 


### &#127800; 请你写出一个sql语句查询新登录用户次日成功的留存率，即第1天登陆之后，第2天再次登陆的概率,保存小数点后面3位(3位之后的四舍五入)，上面的例子查询结果如下:

```sql
+-------+
| p     |
+-------+
| 0.500 |
+-------+
```

**查询结果表明:**<br>
user_id为1的用户在2020-10-12第一次新登录了，在2020-10-13又登录了，算是成功的留存<br>
user_id为2的用户在2020-10-12第一次新登录了，在2020-10-13又登录了，算是成功的留存<br>
user_id为3的用户在2020-10-12第一次新登录了，在2020-10-13没登录了，算是失败的留存<br>
user_id为4的用户在2020-10-13第一次新登录了，在2020-10-14没登录了，算是失败的留存<br>
固次日成功的留存率为 2/4=0.5<br>
(sqlite里查找某一天的后一天的用法是:date(yyyy-mm-dd, '+1 day')，四舍五入的函数为round，sqlite 1/2得到的不是0.5，得到的是0，只有1*1.0/2才会得到0.5<br>
mysql里查找某一天的后一天的用法是:DATE_ADD(yyyy-mm-dd,INTERVAL 1 DAY)，四舍五入的函数为round)<br>


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
# (1,2,1,'2020-10-12')，
(2,3,2,'2020-10-12'),
(3,2,2,'2020-10-13'),
(4,2,2,'2020-10-13'),
(5,4,1,'2020-10-13'),
(6,1,2,'2020-10-13'),
(7,1,2,'2020-10-14')
on duplicate key 
update id = values(id), user_id = values(user_id), client_id = values(client_id), date = values(date);
```
</details>

### &#127800;  Answer

<details>
<summary>&#127808; DATE_ADD() &#127808;</summary>
  
```sql
select 
# 经过查询条件过滤的用户数量
round(count(distinct l.user_id)*1.0
      /
      # 全部用户的数量
      (select count(distinct user_id) from login) 
      ,3) p
from login l
# 条件为在注册日期第二天登录
where (l.user_id,l.date)
in (select user_id,DATE_ADD(min(date),INTERVAL 1 DAY) 
    from login 
    group by user_id
   );
```
</details>

