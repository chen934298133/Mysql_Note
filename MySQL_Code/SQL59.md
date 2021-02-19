## &#128044; Description of the problem


### &#127800; 获取有奖金的员工相关信息。给出emp_no、first_name、last_name、奖金类型btype、对应的当前薪水情况salary以及奖金金额bonus。 bonus类型btype为1其奖金为薪水salary的10%，btype为2其奖金为薪水的20%，其他类型均为薪水的30%。 当前薪水表示to_date='9999-01-01'

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
  
CREATE TABLE `dept_emp` (
`emp_no` int(11) NOT NULL,
`dept_no` char(4) NOT NULL,
`from_date` date NOT NULL,
`to_date` date NOT NULL,
PRIMARY KEY (`emp_no`,`dept_no`));
  
create table emp_bonus(
emp_no int not null,
received datetime not null,
btype smallint not null);
  
CREATE TABLE `salaries` (
`emp_no` int(11) NOT NULL,
`salary` int(11) NOT NULL,
`from_date` date NOT NULL,
`to_date` date NOT NULL, PRIMARY KEY (`emp_no`,`from_date`));
```
</details>

### 返回的结果格式如下:

<table align="center" border="1" cellpadding="2" cellspacing="0">  <tbody>   <tr>    <th>     emp_no    </th>    <th>     first_name    </th>    <th>     last_name    </th>    <th>     btype    </th>    <th>     salary    </th>    <th>     bonus    </th>   </tr>  </tbody>  <tbody>   <tr>    <td>     10001    </td>    <td>     Georgi    </td>    <td>     Facello    </td>    <td>     1    </td>    <td>     88958    </td>    <td>     8895.8    </td>   </tr>   <tr>    <td>     10002    </td>    <td>     Bezalel    </td>    <td>     Simmel    </td>    <td>     2    </td>    <td>     72527    </td>    <td>     14505.4    </td>   </tr>   <tr>    <td>     10003    </td>    <td>     Parto    </td>    <td>     Bamford    </td>    <td>     3    </td>    <td>     43311    </td>    <td>     12993.3    </td>   </tr>   <tr>    <td>     10004    </td>    <td>     Chirstian    </td>    <td>     Koblick    </td>    <td>     1    </td>    <td>     74057    </td>    <td>     7405.7    </td>   </tr>  </tbody> </table>

<details>
<summary>&#127808; View the Codes &#127808;</summary>
  

```sql
select e.emp_no,e.first_name,e.last_name,b.btype,s.salary,
(CASE b.btype
WHEN 1 THEN 0.1*salary
WHEN 2 THEN 0.2*salary
ELSE 0.3*salary
END) bouns
from employees e,emp_bonus b,salaries s
where  s.emp_no=e.emp_no and e.emp_no =b.emp_no
and s.to_date='9999-01-01'
```
</details>

