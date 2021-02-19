## &#128044; Description of the problem


### &#127800; 获取Employees中的first_name，查询按照first_name最后两个字母，按照升序进行排列

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
```
</details>

### &#127800; 输出格式：
<table align="center" border="1" cellpadding="2" cellspacing="0">  <tbody>   <tr>    <th>     first_name    </th>   </tr>  </tbody>  <tbody>   <tr>    <td>     Chirstian    </td>   </tr>   <tr>    <td>     Tzvetan    </td>   </tr>   <tr>    <td>     Bezalel    </td>   </tr>   <tr>    <td>     Duangkaew    </td>   </tr>   <tr>    <td>     Georgi    </td>   </tr>   <tr>    <td>     Kyoichi    </td>   </tr>   <tr>    <td>     Anneke    </td>   </tr>   <tr>    <td>     Sumant    </td>   </tr>   <tr>    <td>     Mary    </td>   </tr>   <tr>    <td>     Parto    </td>   </tr>   <tr>    <td>     Saniya    </td>   </tr>  </tbody> </table>
<details>
<summary>&#127808; View the Codes &#127808;</summary>
  

```sql
# substr可分割字符串，将倒数后两个字符串分割出来，然后进行排序即可
# substr（字段,指定分割位置，长度）
#（字段,指定分割位置） 分割位置到最后
SELECT first_name FROM employees
ORDER BY SUBSTR(first_name,-2,2);

# 同样还有一个 left 函数。
# SELECT first_name FROM employees 
# ORDER BY RIGHT(first_name,2);
```
</details>

