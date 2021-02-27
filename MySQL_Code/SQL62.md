## &#128044; Description of the problem

### &#127800;  在牛客刷题有一个通过题目个数的(passing_number)表，id是主键，简化如下: 

```sql
mysql> select * from grade;
+----+--------+
| id | number |
+----+--------+
|  1 | 111    |
|  2 | 333    |
|  3 | 111    |
|  4 | 111    |
|  5 | 333    |
+----+--------+
5 rows in set (0.03 sec)
```
### id为用户主键id，number代表积分情况，让你写一个sql查询，积分表里面出现三次以及三次以上的积分

#### 输出格式:
```sql
+--------+
| number |
+--------+
| 111    |
+--------+
1 row in set (0.00 sec)
```

<details>
<summary>&#127808; View The sql &#127808;</summary>
  
```sql
create table grade
( id smallint(5) not null primary key,
  number varchar(30) not null);
```
```sql
insert into grade
(id, number)
values
(1,'111'),
(2,'333'),
(3,'111'),
(4,'111'),
(5,'333');
Query OK, 5 rows affected (0.04 sec)
```
</details>

### Answer
<details>
<summary>&#127808; View the Codes &#127808;</summary>
  

```sql
select number
from grade
group by number
having count(*) >= 3
  
select a.number 
from (
select count(number)a, id, number
from grade
group by number
having  a >= 3
)a; 
```
</details>

