## &#128044; Description of the problem

**创建一个actor表，包含如下列信息**

<table border="1" cellpadding="2" cellspacing="0">  <tbody>   <tr>    <th>     列表    </th>    <th>     类型    </th>    <th>     是否为NULL    </th>    <th>     含义    </th>   </tr>  </tbody>  <tbody>   <tr>    <td>     actor_id    </td>    <td>     smallint(5)    </td>    <td>     not null    </td>    <td>     主键id    </td>   </tr>   <tr>    <td>     first_name    </td>    <td>     varchar(45)    </td>    <td>     not null    </td>    <td>     名字    </td>   </tr>   <tr>    <td>     last_name    </td>    <td>     varchar(45)    </td>    <td>     not null    </td>    <td>     姓氏    </td>   </tr>   <tr>    <td>     last_update    </td>    <td>     date    </td>    <td>     not null    </td>    <td>     日期    </td>   </tr>  </tbody> </table>

<br>

<details>
<summary>&#127808; View The Codes &#127808;</summary>
  
看见题解处一个小哥的推荐，如何导入百万条数据？
[其中使用Load data infile导入的方法最优](https://blog.nowcoder.net/n/1cadd83c427c4d12b548ac21f038fdc0)
```sql
CREATE table actor(
actor_id smallint(5) NOT NULL PRIMARY KEY,
first_name varchar(45) NOT NULL,
last_name varchar(45) NOT NULL,
last_update date NOT NULL
) 
```
</details>