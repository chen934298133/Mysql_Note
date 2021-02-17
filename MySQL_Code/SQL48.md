## &#128044; Description of the problem


### &#127800; 请你写出更新语句，将所有获取奖金的员工当前的(salaries.to_date='9999-01-01')薪水增加10%。
#### 注: (emp_bonus里面的emp_no都是当前获奖的所有员工)


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


#### &#127800; 更新指定数据

<table align="center" border="1" cellpadding="2" cellspacing="0">  <tbody>   <tr>    <th>     name    </th>   </tr>  </tbody>  <tbody>   <tr>    <td>     Facello'Georgi    </td>   </tr>   <tr>    <td>     Simmel'Bezalel    </td>   </tr>   <tr>    <td>     Bamford'Parto    </td>   </tr>   <tr>    <td>     Koblick'Chirstian    </td>   </tr>   <tr>    <td>     Maliniak'Kyoichi    </td>   </tr>   <tr>    <td>     Preusig'Anneke    </td>   </tr>   <tr>    <td>     Zielinski'Tzvetan    </td>   </tr>   <tr>    <td>     Kalloufi'Saniya    </td>   </tr>   <tr>    <td>     Peac'Sumant    </td>   </tr>   <tr>    <td>     Piveteau'Duangkaew    </td>   </tr>   <tr>    <td>     Sluis'Mary    </td>   </tr>  </tbody> </table>


<details>
<summary>&#127808; 这版本不够用吗？ &#127808;</summary>
  
```sql
update salaries 
set salary = 1.1 * salary
where emp_no in (select emp_no from emp_bonus)
and to_date='9999-01-01'
```
</details>

<details>
<summary>&#127808; 为啥要这么复杂？是因为效率高吗 &#127808;</summary>
  
```sql
update salaries set salary = 1.1 * salary
where emp_no in (select emp_no from 
                     ( select s.emp_no
                       from salaries s inner join emp_bonus e
                       on s.emp_no = e.emp_no
                     )a
                   where to_date='9999-01-01'
                );

update emp_bonus as eb 
inner join salaries as s 
on eb.emp_no = s.emp_no
set s.salary = s.salary * 1.1
where s.to_date = '9999-01-01';
```
</details>

  
