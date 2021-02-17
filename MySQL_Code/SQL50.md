## &#128044; Description of the problem


### &#127800; 将employees表中的所有员工的last_name和first_name通过(')连接起来。(sqlite不支持concat，请用||实现，mysql支持concat)


<details>
<summary>&#127808; View The SQL &#127808;</summary>

```sql
create table emp_bonus(
emp_no int not null,
btype smallint not null);
CREATE TABLE `salaries` (
`emp_no` int(11) NOT NULL,
`salary` int(11) NOT NULL,
`from_date` date NOT NULL,
`to_date` date NOT NULL, PRIMARY KEY (`emp_no`,`from_date`)); 
  
INSERT INTO emp_bonus VALUES (10001,1);
INSERT INTO salaries VALUES(10001,85097,'2001-06-22','2002-06-22');
INSERT INTO salaries VALUES(10001,88958,'2002-06-22','9999-01-01');
```
</details>


#### &#127800; concat连接

<table align="center" border="1" cellpadding="2" cellspacing="0">  <tbody>   <tr>    <th>     name    </th>   </tr>  </tbody>  <tbody>   <tr>    <td>     Facello'Georgi    </td>   </tr>   <tr>    <td>     Simmel'Bezalel    </td>   </tr>   <tr>    <td>     Bamford'Parto    </td>   </tr>   <tr>    <td>     Koblick'Chirstian    </td>   </tr>   <tr>    <td>     Maliniak'Kyoichi    </td>   </tr>   <tr>    <td>     Preusig'Anneke    </td>   </tr>   <tr>    <td>     Zielinski'Tzvetan    </td>   </tr>   <tr>    <td>     Kalloufi'Saniya    </td>   </tr>   <tr>    <td>     Peac'Sumant    </td>   </tr>   <tr>    <td>     Piveteau'Duangkaew    </td>   </tr>   <tr>    <td>     Sluis'Mary    </td>   </tr>  </tbody> </table>

<details>
<summary>&#127808; View the Codes &#127808;</summary>
  
```sql
select concat_ws("'", last_name, first_name) as Name
from employees

# select concat(last_name, "'", first_name) as name
#  from employees;
```
</details>

