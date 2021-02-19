## &#128044; Description of the problem


### &#127800; 按照dept_no进行汇总，属于同一个部门的emp_no按照逗号进行连接，结果给出dept_no以及连接出的结果employees

<details>
<summary>&#127808; View The sql &#127808;</summary>
  
```sql
CREATE TABLE `dept_emp` (
`emp_no` int(11) NOT NULL,
`dept_no` char(4) NOT NULL,
`from_date` date NOT NULL,
`to_date` date NOT NULL,
PRIMARY KEY (`emp_no`,`dept_no`));
```
</details>

### &#127800; 输出格式：
<table align="center" border="1" cellpadding="2" cellspacing="0">  <tbody>   <tr>    <th>     dept_no    </th>    <th>     employees    </th>   </tr>  </tbody>  <tbody>   <tr>    <td>     d001    </td>    <td>     10001,10002    </td>   </tr>   <tr>    <td>     d002    </td>    <td>     10006    </td>   </tr>   <tr>    <td>     d003    </td>    <td>     10005    </td>   </tr>   <tr>    <td>     d004    </td>    <td>     10003,10004    </td>   </tr>   <tr>    <td>     d005    </td>    <td>     10007,10008,10010    </td>   </tr>   <tr>    <td>     d006    </td>    <td>     10009,10010    </td>   </tr>  </tbody> </table>
<details>
<summary>&#127808; View the Codes &#127808;</summary>
  

```sql
# 聚合函数group_concat（X，Y），其中X是要连接的字段，Y是连接时用的符号，可省略，默认为逗号
# 此函数必须与GROUP BY配合使用
select dept_no, group_concat(emp_no)as employees from dept_emp
group by dept_no
```
</details>

