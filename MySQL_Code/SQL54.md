## &#128044; Description of the problem


### &#127800; 查找排除最大、最小salary之后的当前(to_date = '9999-01-01' )员工的平均工资avg_salary。

<details>
<summary>&#127808; View The sql &#127808;</summary>
  
```sql
CREATE TABLE `salaries` ( `emp_no` int(11) NOT NULL,
`salary` int(11) NOT NULL,
`from_date` date NOT NULL,
`to_date` date NOT NULL,
PRIMARY KEY (`emp_no`,`from_date`)); 
```
```sql
INSERT INTO salaries VALUES(10001,85097,'2001-06-22','2002-06-22');
INSERT INTO salaries VALUES(10001,88958,'2002-06-22','9999-01-01');
INSERT INTO salaries VALUES(10002,72527,'2001-08-02','9999-01-01');
INSERT INTO salaries VALUES(10003,43699,'2000-12-01','2001-12-01');
INSERT INTO salaries VALUES(10003,43311,'2001-12-01','9999-01-01');
INSERT INTO salaries VALUES(10004,70698,'2000-11-27','2001-11-27');```
INSERT INTO salaries VALUES(10004,74057,'2001-11-27','9999-01-01');
```
</details>

### &#127800; 输出格式：
<table align="center" border="1" cellpadding="2" cellspacing="0">  <tbody>   <tr>    <th>     avg_salary    </th>   </tr>  </tbody>  <tbody>   <tr>    <td>     73292    </td>   </tr>  </tbody> </table>
<details>
<summary>&#127808; View the Codes &#127808;</summary>
  

```sql
select avg(salary) as avg_salary from salaries
    where  to_date = '9999-01-01'
    and salary != (select max(salary) from salaries where to_date ='9999-01-01')
    and salary != (select min(salary) from salaries where to_date ='9999-01-01')
```
</details>

