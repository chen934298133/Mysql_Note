## &#128044; Description of the problem


### &#127800; 获取所有员工的emp_no、部门编号dept_no以及对应的bonus类型btype和received，没有分配奖金的员工不显示对应的bonus类型btype和received

<details>
<summary>&#127808; View The sql &#127808;</summary>
  
```sql
 CREATE TABLE `dept_emp` (
`emp_no` int(11) NOT NULL,
`dept_no` char(4) NOT NULL,
`from_date` date NOT NULL,
`to_date` date NOT NULL,
PRIMARY KEY (`emp_no`,`dept_no`));

CREATE TABLE `emp_bonus`(
emp_no int(11) NOT NULL,
received datetime NOT NULL,
btype smallint(5) NOT NULL);

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

### 返回的结果格式如下:

<table align="center" border="1" cellpadding="2" cellspacing="0">  <tbody>   <tr>    <th>     e.emp_no    </th>    <th>     dept_no    </th>    <th>     btype    </th>    <th>     received    </th>   </tr>  </tbody>  <tbody>   <tr>    <td>     10001    </td>    <td>     d001    </td>    <td>     1    </td>    <td>     2010-01-01    </td>   </tr>   <tr>    <td>     10002    </td>    <td>     d001    </td>    <td>     2    </td>    <td>     2010-10-01    </td>   </tr>   <tr>    <td>     10003    </td>    <td>     d004    </td>    <td>     3    </td>    <td>     2011-12-03    </td>   </tr>   <tr>    <td>     10004    </td>    <td>     d004    </td>    <td>     1    </td>    <td>     2010-01-01    </td>   </tr>   <tr>    <td>     10005    </td>    <td>     d003    </td>    <td>    </td>   </tr>   <tr>    <td>     10006    </td>    <td>     d002    </td>    <td>    </td>   </tr>   <tr>    <td>     10007    </td>    <td>     d005    </td>    <td>    </td>   </tr>   <tr>    <td>     10008    </td>    <td>     d005    </td>    <td>    </td>   </tr>   <tr>    <td>     10009    </td>    <td>     d006    </td>    <td>    </td>   </tr>   <tr>    <td>     10010    </td>    <td>     d005    </td>    <td>    </td>   </tr>   <tr>    <td>     10010    </td>    <td>     d006    </td>    <td>    </td>   </tr>  </tbody> </table>

<details>
<summary>&#127808; View the Codes &#127808;</summary>
  

```sql
SELECT e.emp_no, d.dept_no, b.btype, b.received
FROM employees e 

JOIN dept_emp d ON e.emp_no = d.emp_no

LEFT JOIN emp_bonus b ON e.emp_no = b.emp_no
```
</details>

