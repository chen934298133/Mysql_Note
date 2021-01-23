## &#128044; Description of the problem
**汇总各个部门当前员工的title类型的分配数目，即结果给出部门编号dept_no、dept_name、其部门下所有的当前(dept_emp.to_date = '9999-01-01')员工的当前(titles.to_date = '9999-01-01')title以及该类型title对应的数目count，结果按照dept_no升序排序。**

**(注：因为员工可能有离职，所有dept_emp里面to_date不为'9999-01-01'就已经离职了，不计入统计，而且员工可能有晋升，所以如果titles.to_date 不为 '9999-01-01'，那么这个可能是员工之前的职位信息，也不计入统计)**


<details>
<summary>&#127808; View The SQL &#127808;</summary>

```sql
`dept_no` char(4) NOT NULL,
`dept_name` varchar(40) NOT NULL,
PRIMARY KEY (`dept_no`));
CREATE TABLE `dept_emp` (
`emp_no` int(11) NOT NULL,
`dept_no` char(4) NOT NULL,
`from_date` date NOT NULL,
`to_date` date NOT NULL,
PRIMARY KEY (`emp_no`,`dept_no`));
CREATE TABLE IF NOT EXISTS `titles` (
`emp_no` int(11) NOT NULL,
`title` varchar(50) NOT NULL,
`from_date` date NOT NULL,
`to_date` date DEFAULT NULL);
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
dept_name
</th>
<th>
title
</th>
<th>
count
</th>
</tr>
</tbody>
<tbody>
<tr>
<td>
d001
</td>
<td>
Marketing
</td>
<td>
Senior Engineer
</td>
<td>
1
</td>
</tr>
<tr>
<td>
d001
</td>
<td>
Marketing
</td>
<td>
Staff
</td>
<td>
1
</td>
</tr>
<tr>
<td>
d002
</td>
<td>
Finance
</td>
<td>
Senior Engineer
</td>
<td>
1
</td>
</tr>
<tr>
<td>
d003
</td>
<td>
Human Resources
</td>
<td>
Senior Staff
</td>
<td>
1
</td>
</tr>
<tr>
<td>
d004
</td>
<td>
Production
</td>
<td>
Senior Engineer
</td>
<td>
2
</td>
</tr>
<tr>
<td>
d005
</td>
<td>
Development
</td>
<td>
Senior Staff
</td>
<td>
1
</td>
</tr>
<tr>
<td>
d006
</td>
<td>
Quality Management
</td>
<td>
Engineer
</td>
<td>
2
</td>
</tr>
<tr>
<td>
d006
</td>
<td>
Quality Management
</td>
<td>
Senior Engineer
</td>
<td>
1
</td>
</tr>
</tbody>
</table>


## View The Answer

<details>
<summary>&#127808; View The Codes &#127808;</summary>

```sql
select d.dept_no,
       d.dept_name,
       t.title,
       count(t.title)as count
from departments d,dept_emp de,titles t
where de.emp_no=t.emp_no
and de.dept_no=d.dept_no
and de.to_date='9999-01-01'
and t.to_date='9999-01-01'
group by d.dept_no ,t.title
order by d.dept_no asc;
```
  
- 依旧考察多表连接
- 重点在于 `group by` 得是 `dept_no` 和 `title` ，因为 `title` 一样的就不能算是员工的一个类型了。
- 且在此题中也不能丢掉 `order by depy_no`
</details>
