## &#128044; Description of the problem

**牛客刷题有一个通过题目个数的(passing_number)表，id是主键，简化如下:**
```sql
mysql> select * from passing_number;
+----+--------+
| id | number |
+----+--------+
|  1 | 4      |
|  2 | 3      |
|  3 | 3      |
|  4 | 2      |
|  5 | 5      |
|  6 | 5      |
+----+--------+
```
**第1行表示id为1的用户通过了4个题目;**<br>
**.....**<br>
**第6行表示id为6的用户通过了4个题目;**<br>

### &#127800; 请你根据上表，输出通过的题目的排名，通过题目个数相同的，排名相同，此时按照id升序排列，数据如下:

```
+----+--------+--------+
| id | number | t_rank |
+----+--------+--------+
|  6 | 5      |      1 |
|  5 | 5      |      1 |
|  1 | 4      |      2 |
|  3 | 3      |      3 |
|  2 | 3      |      3 |
|  4 | 2      |      4 |
+----+--------+--------+
6 rows in set (0.02 sec)
```

## 解释
**id为5的用户通过了5个排名第1，**<br>
**id为1和id为6的都通过了2个，并列第2**


<details>
<summary>&#127808; View The sql &#127808;</summary>
  
```sql
create table passing_number
( id smallint(5) not null primary key,
  number varchar(30) not null);
```
```sql
mysql> insert into passing_number
(id, number)
values
(1,'4'),
(2,'3'),
(3,'3'),
(4,'2'),
(5,'5'),
(6,'5');
Query OK, 6 rows affected (0.01 sec)
```
</details>

### Answer
<details>
<summary>&#127808; 法一：笛卡尔积去重 &#127808;</summary>
  
1. 设置双表，表1为原表， 表2与表一做笛卡尔积后去重
2. 去重后，用count计数，记录 表2.number 去重后  >= 表1.number(若排名最高则只有自己等于自己，rank为1。若排名第二，则有两个 number >= 自己)
  
```sql
select a.id, a.number, count(distinct b.number) t_rank
from passing_number a, passing_number b
where a.number <= b.number
group by a.id, a.number
order by t_rank asc;
```
</details>

<details>
<summary>&#127808; 法二：窗口函数 &#127808;</summary>
  
```sql
SELECT *, dense_rank() over(order by number desc) t_rank 
FROM passing_number ORDER BY number DESC, id;
```
```sql
# 仅8.0以上使用，8.0以下使用会报错哦
ERROR 1064 (42000): 
  You have an error in your SQL syntax;
  check the manual that corresponds to your MySQL server version for the right syntax to use near '(order by number desc) t_rank
FROM passing_number ORDER BY number DESC, id' at line 1
```
</details>

