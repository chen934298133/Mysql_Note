## &#128044; Description of the problem

**将employees表的所有员工的last_name和first_name拼接起来作为Name，中间以一个空格区分**


<details>
<summary>&#127808; View The Codes &#127808;</summary>

### 函数CONCAT()
- `concat(last_name, ' ', first_name)`
  
  
### 函数CONCAT_WS（）。使用语法为：CONCAT_WS(separator,str1,str2,…)
- 如： `concat_ws(' ', last_name, first_name)`


```sql
select concat_ws(' ', last_name, first_name) as Name
from employees；
```

```sql
select concat(last_name, ' ', first_name) as Name
from employees
```

</details>