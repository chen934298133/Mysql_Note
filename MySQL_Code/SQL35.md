## &#128044; Description of the problem

**对于表actor插入如下数据,如果数据已经存在，请忽略(不支持使用replace操作)**

<br>

<table border="1" cellpadding="2" cellspacing="0">  <tbody>   <tr>    <th>     actor_id    </th>    <th>     first_name    </th>    <th>     last_name    </th>    <th>     last_update    </th>   </tr>  </tbody>  <tbody>   <tr>    <td>     '3'    </td>    <td>     'ED'    </td>    <td>     'CHASE'    </td>    <td>     '2006-02-15 12:34:33'    </td>   </tr>  </tbody> </table>

<br>

<details>
<summary>&#127808; View The Codes &#127808;</summary>
  
```sql
 INSERT IGNORE INTO actor 
 VALUES(
     3, 'ED', 'CHASE', '2006-02-15 12:34:33'
 );
```
</details>