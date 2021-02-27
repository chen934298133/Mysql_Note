## &#128044; Description of the problem

### &#127800; 现在有一个需求，让你统计正常用户发送给正常用户邮件失败的概率:有一个邮件(email)表，id为主键， type是枚举类型，枚举成员为(completed，no_completed)，completed代表邮件发送是成功的，no_completed代表邮件是发送失败的。简况如下:

```sql
mysql> select * from email;
+----+---------+------------+--------------+------------+
| id | send_id | receive_id | type         | date       |
+----+---------+------------+--------------+------------+
|  1 |       2 |          3 | completed    | 2020-01-11 |
|  2 |       1 |          3 | completed    | 2020-01-11 |
|  3 |       1 |          4 | no_completed | 2020-01-11 |
|  4 |       3 |          1 | completed    | 2020-01-12 |
|  5 |       3 |          4 | completed    | 2020-01-12 |
|  6 |       4 |          1 | completed    | 2020-01-12 |
+----+---------+------------+--------------+------------+
6 rows in set (0.00 sec)
```
- 第1行表示为id为2的用户在2020-01-11成功发送了一封邮件给了id为3的用户;
- ...
- 第3行表示为id为1的用户在2020-01-11没有成功发送一封邮件给了id为4的用户;
- ...
- 第6行表示为id为4的用户在2020-01-12成功发送了一封邮件给了id为1的用户;

### &#127800; 有一个任务(task)表如下，主键也是id，如下:

```
mysql> select * from user;
+----+--------------+
| id | is_blacklist |
+----+--------------+
|  1 |            0 |
|  2 |            1 |
|  3 |            0 |
|  4 |            0 |
+----+--------------+
4 rows in set (0.00 sec)
```
- 第1行表示id为1的是正常用户;
- 第2行表示id为2的不是正常用户，是黑名单用户，如果发送大量邮件或者出现各种情况就会容易发送邮件失败的用户
- ...
- 第4行表示id为4的是正常用户
### &#127800; 现在让你写一个sql查询，每一个日期里面，正常用户发送给正常用户邮件失败的概率是多少，结果保留到小数点后面3位(3位之后的四舍五入)，并且按照日期升序排序，上面例子查询结果如下: 

```sql
+------------+-------+
| date       | p     |
+------------+-------+
| 2020-01-11 | 0.500 |
| 2020-01-12 | 0.000 |
+------------+-------+
2 rows in set (0.00 sec)

```


<details>
<summary>&#127808; View The sql &#127808;</summary>
  
```sql
create table email
(id smallint(5) not null primary key,
send_id smallint(5) not null,
receive_id smallint(5) not null,
type varchar(255) not null,
date date() not null);
```
```sql
create table user
(id smallint(5) not null primary key,
is_blacklist smallint(5) not null
);
```
```sql
insert ignore into email
(id, send_id, receive_id, type, date)
values
#(1,2,3,'completed','2020-01-11'),
(2,1,3,'completed','2020-01-11'),
(3,1,4,'no_completed','2020-01-11'),
(4,3,1,'completed','2020-01-12'),
(5,3,4,'completed','2020-01-12'),
(6,4,1,'completed','2020-01-12');
```
```sql
insert into user
values
(1, 0),
(2, 1),
(3, 0),
(4, 0);
```
</details>

### Answer
<details>
<summary>&#127808; left join &#127808;</summary>
  

```sql
select e.date, round(
    sum(case e.type 
        when 'no_completed' then 1 
        else 0 
        end) * 1.0 / count(e.type),3) p
from email e 
join user u1 on e.send_id = u1.id  
join user u2 on u2.id = e.receive_id
where u1.is_blacklist = 0 and u2.is_blacklist=0
group by e.date
order by e.date;
```
</details>

