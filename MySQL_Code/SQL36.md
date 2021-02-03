## &#128044; Description of the problem

**对于如下表actor，其对应的数据为:**

<br>

<table border="1" cellpadding="2" cellspacing="0">  <tbody>   <tr>    <th>     actor_id    </th>    <th>     first_name    </th>    <th>     last_name    </th>    <th>     last_update    </th>   </tr>  </tbody>  <tbody>   <tr>    <td>     1    </td>    <td>     PENELOPE    </td>    <td>     GUINESS    </td>    <td>     2006-02-15 12:34:33    </td>   </tr>   <tr>    <td>     2    </td>    <td>     NICK    </td>    <td>     WAHLBERG    </td>    <td>     2006-02-15 12:34:33    </td>   </tr>  </tbody> </table>

<br>

**请你创建一个actor_name表，并且将actor表中的所有first_name以及last_name导入该表**

actor_name表结构如下：
<table border="1" cellpadding="2" cellspacing="0">  <tbody>   <tr>    <th>     列表    </th>    <th>     类型    </th>    <th>     是否为NULL    </th>    <th>     含义    </th>   </tr>  </tbody>  <tbody>   <tr>    <td>     first_name    </td>    <td>     varchar(45)    </td>    <td>     not null    </td>    <td>     名字    </td>   </tr>   <tr>    <td>     last_name    </td>    <td>     varchar(45)    </td>    <td>     not null    </td>    <td>     姓氏    </td>   </tr>  </tbody> </table>

<br>

<details>
<summary>&#127808; View The Codes &#127808;</summary>
  
```sql
CREATE TABLE actor_name    -- 创建表
(first_name varchar(45) NOT NULL,
 last_name varchar(45) NOT NULL);
 
INSERT INTO actor_name  -- 插入数据
SELECT first_name,last_name
FROM actor;
```
</details>