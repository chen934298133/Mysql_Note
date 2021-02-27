## &#128044; Description of the problem

#### 请你对于表actor批量插入如下数据(不能有2条insert语句哦!) 

<table align="center" border="1" cellpadding="2" cellspacing="0">  <tbody>   <tr>    <th>     actor_id    </th>    <th>     first_name    </th>    <th>     last_name    </th>    <th>     last_update    </th>   </tr>  </tbody>  <tbody>   <tr>    <td>     1    </td>    <td>     PENELOPE    </td>    <td>     GUINESS    </td>    <td>     2006-02-15 12:34:33    </td>   </tr>   <tr>    <td>     2    </td>    <td>     NICK    </td>    <td>     WAHLBERG    </td>    <td>     2006-02-15 12:34:33    </td>   </tr>  </tbody> </table>

**题目已经先执行了如下语句:** 

```sql
drop table if exists actor;
CREATE TABLE actor (
   actor_id  smallint(5)  NOT NULL PRIMARY KEY,
   first_name  varchar(45) NOT NULL,
   last_name  varchar(45) NOT NULL,
   last_update  DATETIME NOT NULL)
```

<br>

<details>
<summary>&#127808; View The Codes &#127808;</summary>
  
看见题解处一个小哥的推荐，如何导入百万条数据？
[其中使用Load data infile导入的方法最优](https://blog.nowcoder.net/n/1cadd83c427c4d12b548ac21f038fdc0)
```sql
insert into actor
(actor_id,first_name,last_name,last_update)
VALUES(1,'PENELOPE','GUINESS','2006-02-15 12:34:33'),
      (2,'NICK','WAHLBERG','2006-02-15 12:34:33');
```
</details>