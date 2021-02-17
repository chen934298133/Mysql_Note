## &#128044; Description of the problem


### &#127800; 将所有to_date为9999-01-01的全部更新为NULL,且 from_date更新为2001-01-01。



<details>
<summary>&#127808; View The SQL &#127808;</summary>
  

```sql
CREATE TABLE IF NOT EXISTS titles_test (
id int(11) not null primary key,
emp_no int(11) NOT NULL,
title varchar(50) NOT NULL,
from_date date NOT NULL,
to_date date DEFAULT NULL);

insert into titles_test values ('1', '10001', 'Senior Engineer', '1986-06-26', '9999-01-01'),
('2', '10002', 'Staff', '1996-08-03', '9999-01-01'),
('3', '10003', 'Senior Engineer', '1995-12-03', '9999-01-01'),
('4', '10004', 'Senior Engineer', '1995-12-03', '9999-01-01'),
('5', '10001', 'Senior Engineer', '1986-06-26', '9999-01-01'),
('6', '10002', 'Staff', '1996-08-03', '9999-01-01'),
('7', '10003', 'Senior Engineer', '1995-12-03', '9999-01-01'); 
```
</details>

#### &#127800; 更新后的值: 

<table align="center" border="1" cellpadding="2" cellspacing="0">   <tbody>    <tr>     <td>      <span>i</span><span>d </span><br>     </td>     <td>      <span>e</span><span>mp_no </span><br>     </td>     <td>      <span>ti</span><span>tle </span><br>     </td>     <td>      <span>fro</span><span>m_date </span><br>     </td>     <td>      <span>to_da</span><span>te </span><br>     </td>    </tr>    <tr>     <td>      <span>1</span><br>     </td>     <td>      <span>10</span><span>001</span><br>     </td>     <td>      <span>Senior Engineer</span><br>     </td>     <td>      <span>2001-01-01</span><br>     </td>     <td>      <span>NULL</span><br>     </td>    </tr>    <tr>     <td>      <span>2</span><br>     </td>     <td>      <span>10</span><span>002</span><br>     </td>     <td>      <span>St</span><span>aff</span><br>     </td>     <td>      <span>2001-01-01</span><br>     </td>     <td>      <span>NULL</span><br>     </td>    </tr>    <tr>     <td>      3     </td>     <td>      <span>10</span><span>003</span><br>     </td>     <td>      <span>Senior Engineer</span><br>     </td>     <td>      <span>2001-01-01</span><br>     </td>     <td>      <span>NUL</span><span>L</span><br>     </td>    </tr>    <tr>     <td>      4     </td>     <td>      <span>10</span><span>004</span><br>     </td>     <td>      <span>Senior Engineer</span><br>     </td>     <td>      <span>2001-01-01</span><br>     </td>     <td>      <span>NU</span><span>LL</span><br>     </td>    </tr>    <tr>     <td>      5     </td>     <td>      <span>100</span><span>01</span><br>     </td>     <td>      <span>Senior Engineer</span><br>     </td>     <td>      <span>2001-01-01</span><br>     </td>     <td>      <span>N</span><span>ULL</span><br>     </td>    </tr>    <tr>     <td>      6     </td>     <td>      <span>10</span><span>002</span><br>     </td>     <td>      <span>St</span><span>aff</span><br>     </td>     <td>      <span>2001-01-01</span><br>     </td>     <td>      <span>NU</span><span>LL</span><br>     </td>    </tr>    <tr>     <td>      7     </td>     <td>      <span>100</span><span>03</span><br>     </td>     <td>      <span>Senior Engineer</span><br>     </td>     <td>      <span>2001-01-01</span><br>     </td>     <td>      <span>NUL</span><span>L</span><br>     </td>    </tr>   </tbody>  </table>

#### &#127800; 更新指定数据

<details>
<summary>&#127808; View The Codes &#127808;</summary>
  

```sql
update titles_test
set from_date ='2001-01-01', to_date = null
where to_date ='9999-01-01';
```
</details>