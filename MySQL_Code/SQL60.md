## &#128044; Description of the problem

### &#127800; 按照salary的累计和running_total，其中running_total为前N个当前( to_date = '9999-01-01')员工的salary累计和，其他以此类推。 具体结果如下Demo展示。。

<details>
<summary>&#127808; View The sql &#127808;</summary>
  
```sql
CREATE TABLE `salaries` ( `emp_no` int(11) NOT NULL,
`salary` int(11) NOT NULL,
`from_date` date NOT NULL,
`to_date` date NOT NULL,
PRIMARY KEY (`emp_no`,`from_date`));
```
</details>

### 输出格式:

<table align="center" border="1" cellpadding="2" cellspacing="0">  <tbody>   <tr>    <th>     emp_no    </th>    <th>     salary    </th>    <th>     running_total    </th>   </tr>  </tbody>  <tbody>   <tr>    <td>     10001    </td>    <td>     88958    </td>    <td>     88958    </td>   </tr>   <tr>    <td>     10002    </td>    <td>     72527    </td>    <td>     161485    </td>   </tr>   <tr>    <td>     10003    </td>    <td>     43311    </td>    <td>     204796    </td>   </tr>   <tr>    <td>     10004    </td>    <td>     74057    </td>    <td>     278853    </td>   </tr>   <tr>    <td>     10005    </td>    <td>     94692    </td>    <td>     373545    </td>   </tr>   <tr>    <td>     10006    </td>    <td>     43311    </td>    <td>     416856    </td>   </tr>   <tr>    <td>     10007    </td>    <td>     88070    </td>    <td>     504926    </td>   </tr>   <tr>    <td>     10009    </td>    <td>     95409    </td>    <td>     600335    </td>   </tr>   <tr>    <td>     10010    </td>    <td>     94409    </td>    <td>     694744    </td>   </tr>   <tr>    <td>     10011    </td>    <td>     25828    </td>    <td>     720572    </td>   </tr>  </tbody> </table>

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

