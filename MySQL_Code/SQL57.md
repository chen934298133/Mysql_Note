## &#128044; Description of the problem


### &#127800; 使用关键字 exists 查找未分配具体部门的员工的所有信息。

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

<table align="center" border="1" cellpadding="2" cellspacing="0">  <tbody>   <tr>    <th>     emp_no    </th>    <th>     birth_date    </th>    <th>     first_name    </th>    <th>     last_name    </th>    <th>     gender    </th>    <th>     hire_date    </th>   </tr>  </tbody>  <tbody>   <tr>    <td>     10011    </td>    <td>     1953-11-07    </td>    <td>     Mary    </td>    <td>     Sluis    </td>    <td>     F    </td>    <td>     1990-01-22    </td>   </tr>  </tbody> </table>

<details>
<summary>&#127808; View the Codes &#127808;</summary>
  

```sql
select a.*
from employees a
where not exists (
    select emp_no 
    from dept_emp b 
    where a.emp_no = b.emp_no
)
```
</details>

