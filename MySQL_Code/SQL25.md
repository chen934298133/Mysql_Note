## Description of the title

**获取员工其当前的薪水比其manager当前薪水还高的相关信息，当前表示to_date='9999-01-01'。
结果第一列给出员工的emp_no，<br>
第二列给出其manager的manager_no，<br>
第三列给出该员工当前的薪水emp_salary,<br>
第四列给该员工对应的manager当前的薪水manager_salary**<br>

<details>
<summary>&#127808; View The SQL &#127808;</summary>

```sql
CREATE TABLE `dept_emp` (
`emp_no` int(11) NOT NULL,
`dept_no` char(4) NOT NULL,
`from_date` date NOT NULL,
`to_date` date NOT NULL,
PRIMARY KEY (`emp_no`,`dept_no`));
CREATE TABLE `dept_manager` (
`dept_no` char(4) NOT NULL,
`emp_no` int(11) NOT NULL,
`from_date` date NOT NULL,
`to_date` date NOT NULL,
PRIMARY KEY (`emp_no`,`dept_no`));
CREATE TABLE `salaries` (
`emp_no` int(11) NOT NULL,
`salary` int(11) NOT NULL,
`from_date` date NOT NULL,
`to_date` date NOT NULL,
PRIMARY KEY (`emp_no`,`from_date`));
```
</details>

## Description of the output

<table cellpadding="2" cellspacing="0" border="1" bordercolor="#cccccc">
<tbody>
<tr>
<th>
emp_no
</th>
<th>
manager_no
</th>
<th>
emp_salary
</th>
<th>
manager_salary
</th>
</tr>
</tbody>
<tbody>
<tr>
<td>
10001
</td>
<td>
10002
</td>
<td>
88958
</td>
<td>
72527
</td>
</tr>
<tr>
<td>
10009
</td>
<td>
10010
</td>
<td>
95409
</td>
<td>
94409
</td>
</tr>
</tbody>
</table>

## View The Answer


<details>
<summary>&#127808; 多表联查 &#127808;</summary>

```sql
SELECT a.emp_no, b.manager_no, a.emp_salary, b.manager_salary
FROM
    # a表为员工表与工资表连接
    (SELECT de.dept_no, de.emp_no, s.salary AS emp_salary
    FROM dept_emp de, salaries s
    WHERE de.emp_no = s.emp_no
    AND s.to_date = '9999-01-01') a,
    # b表为manager表与工资表连接
    (SELECT dm.dept_no, dm.emp_no AS manager_no, s.salary AS manager_salary
    FROM dept_manager  dm, salaries s
    WHERE dm.emp_no = s.emp_no
    AND s.to_date = '9999-01-01') b

WHERE a.dept_no = b.dept_no
AND a.emp_salary > b.manager_salary;
```
</details>

<details>
<summary>&#127808; View The Points &#127808;</summary>

1. 分别查询manager表与employee表
2. 联结两表，条件为部门编号相等，要求员工工资 > 经理工资
</details>

