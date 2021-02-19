## &#128044; Description of the problem


### &#127800; 分页查询employees表，每5行一页，返回第2页的数据

<details>
<summary>&#127808; View The sql &#127808;</summary>
  
```sql
CREATE TABLE `employees` (
`emp_no` int(11) NOT NULL,
`birth_date` date NOT NULL,
`first_name` varchar(14) NOT NULL,
`last_name` varchar(16) NOT NULL,
`gender` char(1) NOT NULL,
`hire_date` date NOT NULL,
PRIMARY KEY (`emp_no`));
```
</details>

<details>
<summary>&#127808; View the Codes &#127808;</summary>
  

```sql
# LIMIT 语句结构： LIMIT X,Y 
#    Y ：返回几条记录
#    X：从第几条记录开始返回（第一条记录序号为0，默认为0） 

SELECT * FROM employees
LIMIT 5,5
```
</details>

