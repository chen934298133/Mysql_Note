## SQL 23
**获取所有非manager员工当前的薪水情况，给出dept_no、emp_no以及salary ，当前表示to_date='9999-01-01'**

```sql
CREATE TABLE `salaries` (
`emp_no` int(11) NOT NULL,
`salary` int(11) NOT NULL,
`from_date` date NOT NULL,
`to_date` date NOT NULL,
PRIMARY KEY (`emp_no`,`from_date`));

```

## Description of the output
<table cellpadding="2" cellspacing="0" border="1" bordercolor="#cccccc">
<tbody>
<tr>
	<th>emp_no</th>
	<th>salary</th>
	<th>t_rank</th>
</tr>
</tbody>

<tbody>
<tr>
	<td>10005</td>
	<td>94692</td>
	<td>1</td>
</tr>

<tr>
	<td>10009</td>
	<td>94409</td>
	<td>2</td>
</tr>

<tr>
	<td>10010</td>
	<td>94409</td>
	<td>2</td>
</tr>

<tr>
	<td>10001</td>
	<td>88958</td>
	<td>3</td>
</tr>

<tr>
	<td>10007</td>
	<td>88070</td>
	<td>4
</td>
</tr>

<tr>
	<td>10004</td>
	<td>74057</td>
	<td>5</td>
</tr>

<tr>
	<td>10002</td>
	<td>72527</td>
	<td>6</td>
</tr>

<tr>
	<td>10003</td>
	<td>43311</td>
	<td>7</td>
</tr>

<tr>
	<td>10006</td>
	<td>43311</td>
	<td>7</td>
</tr>

<tr>
	<td>10011</td>
	<td>25828</td>
	<td>8</td>
	</tr>
</tbody>
</table>

<details>
<summary>&#127808; 使用窗口函数 &#127808;</summary>

```sql
# 牛客可以通过，但是MySQL通过不了，因为s.salary不是可聚合项

select s.emp_no,
       s.salary,
       dense_rank() over (order by s.salary desc) as t_rank
from salaries s
where s.to_date='9999-01-01'
```



<details>
<summary>&#127808; View The Points &#127808;</summary>

- 考察的是SQL窗口函数（OLAP函数）中用于排序的专用窗口函数用法 
- 三种用于进行排序的专用窗口函数： 
	- RANK() 
		- 在计算排序时，若存在相同位次，会跳过之后的位次。
		- 例如，有3条排在第1位时，排序为：1，1，1，4······
	- DENSE_RANK() 
		- 这就是题目中所用到的函数，在计算排序时，若存在相同位次，不会跳过之后的位次。
		- 例如，有3条排在第1位时，排序为：1，1，1，2······
	- ROW_NUMBER() 
		- 这个函数赋予唯一的连续位次。
		- 例如，有3条排在第1位时，排序为：1，2，3，4······

### 窗口函数用法： 

```sql
	<窗口函数> OVER ( ORDER BY <排序用列清单> ）

	 dense_rank() over (order by salary desc) as t_rank
```
</details>
    
</details>

<details>
<summary>&#127808; 不使用窗口函数 &#127808;</summary>

```sql
# 先构建不含salary的rank表，再将rank表和salaries表内接，然后排序得到结果
  
SELECT a.emp_no, a.salary, b.t_rank
FROM salaries AS a
INNER JOIN
    (SELECT s1.emp_no, COUNT(DISTINCT s2.salary) AS t_rank
    FROM salaries AS s1, salaries AS s2
    WHERE s1.to_date='9999-01-01'  AND s2.to_date='9999-01-01'  AND s1.salary <= s2.salary
    GROUP BY s1.emp_no)
    AS b
ON a.emp_no=b.emp_no  AND a.to_date='9999-01-01'

ORDER BY a.salary DESC, a.emp_no ASC;
```
</details>
