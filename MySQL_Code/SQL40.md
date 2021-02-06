## &#128044; Description of the problem


### &#127800; 现在在last_update后面新增加一列名字为create_date, 类型为datetime, NOT NULL，默认值为'2020-10-01 00:00:00'


```sql
CREATE TABLE  actor  (
   actor_id  smallint(5)  NOT NULL PRIMARY KEY,
   first_name  varchar(45) NOT NULL,
   last_name  varchar(45) NOT NULL,
   last_update  datetime NOT NULL);
```

<details>
<summary>&#127808; View The Codes &#127808;</summary>
  
```sql
alter table actor 
add column create_date datetime not null 
default '2020-10-01 00:00:00'    
after last_update;
```
</details>