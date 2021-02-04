## &#128044; Description of the problem


### &#127800; 针对actor表创建视图actor_name_view，只包含first_name以及last_name两列，并对这两列重新命名，first_name为first_name_v，last_name修改为last_name_v：


```sql
CREATE TABLE  actor  (
   actor_id  smallint(5)  NOT NULL PRIMARY KEY,
   first_name  varchar(45) NOT NULL,
   last_name  varchar(45) NOT NULL,
   last_update datetime NOT NULL);
```

<details>
<summary>&#127808; View The Codes &#127808;</summary>
  
```sql
CREATE VIEW actor_name_view 
AS
SELECT first_name first_name_v ,last_name last_name_v
FROM  actor;
```
</details>