## &#128044; Description of the problem

### &#127800; 有一个person表，主键是id，如下:

```sql
mysql> select * from person;
+----+------+
| id | name |
+----+------+
|  1 | fh   |
|  2 | tm   |
+----+------+
2 rows in set (0.00 sec)
```

### &#127800; 有一个任务(task)表如下，主键也是id，如下:

```
mysql> select * from task;
+----+-----------+----------------+
| id | person_id | content        |
+----+-----------+----------------+
|  1 |         2 | tm1 works well |
|  2 |         2 | tm2 works well |
+----+-----------+----------------+
2 rows in set (0.00 sec)
```
### &#127800; 请你找到每个人的任务情况，并且输出出来，没有任务的也要输出，而且输出结果按照person的id升序排序，输出情况如下:




<details>
<summary>&#127808; View The sql &#127808;</summary>
  
```sql
create table person
(id smallint(5) not null primary key,
name varchar(30) not null)
```
```sql
create table task
(id smallint(5) not null primary key,
person_id smallint(5) not null,
content varchar(255) not null
);
```
```sql
insert into person
(id, name)
values
(1,'fh'),
(2,'tm');
```
```sql
insert into task
(id, person_id, content)
values
(1, 2, 'tm1 works well'),
(2, 2, 'tm2 works well');
```
</details>

### Answer
<details>
<summary>&#127808; left join &#127808;</summary>
  

```sql
select p.id, p.name, t.content
from person p left join task t
on p.id = t.person_id
order by p.id
```
</details>

