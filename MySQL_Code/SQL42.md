## &#128044; Description of the problem


### &#127800; 删除emp_no重复的记录，只保留最小的id对应的记录。



<details>
<summary>&#127808; View The Codes &#127808;</summary>
  

```sql
CREATE TABLE IF NOT EXISTS titles_test (
id int(11) not null primary key,
emp_no int(11) NOT NULL,
title varchar(50) NOT NULL,
from_date date NOT NULL,
to_date date DEFAULT NULL);

insert into titles_test values ('1', '10001', 'Senior Engineer', '1986-06-26', '9999-01-01'),
('2', '10002', 'Staff', '1996-08-03', '9999-01-01'),
('3', '10003', 'Senior Engineer', '1995-12-03', '9999-01-01'),
('4', '10004', 'Senior Engineer', '1995-12-03', '9999-01-01'),
('5', '10001', 'Senior Engineer', '1986-06-26', '9999-01-01'),
('6', '10002', 'Staff', '1996-08-03', '9999-01-01'),
('7', '10003', 'Senior Engineer', '1995-12-03', '9999-01-01'); 
```
</details>

#### &#127800; 删除指定数据
- MySQL中不允许在子查询的同时删除表数据（不能一边查一边把查的表删了）
- 必须给原始数据表取一个别名再删除，查询出结果，给结果取别名之后再删除

<details>
<summary>&#127808; View The Codes &#127808;</summary>
  
#### &#10060; 错误方法 &#10060;
```sql
DELETE FROM titles_test
WHERE id NOT IN(
    SELECT MIN(id)
    FROM titles_test
    GROUP BY emp_no);
```
  
#### 正确方法
```sql
DELETE FROM titles_test 
WHERE id NOT IN
    (SELECT * FROM(
        SELECT MIN(id) 
        FROM titles_test 
        GROUP BY emp_no) AS a
    )
```
</details>