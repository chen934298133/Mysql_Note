## Description of the title

**获取所有非manager员工当前的薪水情况，给出dept_no、emp_no以及salary ，当前表示to_date='9999-01-01'**

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
CREATE TABLE `employees` (
`emp_no` int(11) NOT NULL,
`birth_date` date NOT NULL,
`first_name` varchar(14) NOT NULL,
`last_name` varchar(16) NOT NULL,
`gender` char(1) NOT NULL,
`hire_date` date NOT NULL,
PRIMARY KEY (`emp_no`));
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
dept_no
</th>
<th>
emp_no
</th>
<th>
salary
</th>
</tr>
</tbody>
<tbody>
<tr>
<td>
d001
</td>
<td>
10001
</td>
<td>
88958
</td>
</tr>
<tr>
<td>
d004
</td>
<td>
10003
</td>
<td>
43311
</td>
</tr>
<tr>
<td>
d005
</td>
<td>
10007
</td>
<td>
88070
</td>
</tr>
<tr>
<td>
d006
</td>
<td>
10009
</td>
<td>
95409
</td>
</tr>
</tbody>
</table>

## View The Answer


<details>
<summary>&#127808; 多表联查+NOT IN &#127808;</summary>

```sql
select de.dept_no, nm.emp_no, s.salary
from
    (select emp_no 
    from employees
    where emp_no not in (select emp_no 
                         from dept_manager)) nm
inner join dept_emp de on nm.emp_no = de.emp_no
inner join salaries s on nm.emp_no = s.emp_no
where s.to_date = '9999-01-01'
order by de.dept_no;
```
</details>


