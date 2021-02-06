## &#128044; Description of the problem


### &#127800; 针对salaries表emp_no字段创建索引idx_emp_no，查询emp_no为10005, 使用强制索引。


```sql
CREATE TABLE `salaries` (
`emp_no` int(11) NOT NULL,
`salary` int(11) NOT NULL,
`from_date` date NOT NULL,
`to_date` date NOT NULL,
PRIMARY KEY (`emp_no`,`from_date`));
create index idx_emp_no on salaries(emp_no);
```

<details>
<summary>&#127808; View The Codes &#127808;</summary>
  
- sqlLite 使用 indexed by 进行强制索引
- mysql 使用 force index 进行强制索引

```sql
select * from salaries
FORCE INDEX ( idx_emp_no)
where emp_no =10005
```
</details>