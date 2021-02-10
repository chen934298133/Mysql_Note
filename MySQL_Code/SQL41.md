## &#128044; Description of the problem


### &#127800; 构造一个触发器audit_log，在向employees_test表中插入一条数据的时候，触发插入相关的数据到audit中。



<details>
<summary>&#127808; View The Codes &#127808;</summary>
  

```sql
CREATE TABLE employees_test(
ID INT PRIMARY KEY NOT NULL,
NAME TEXT NOT NULL,
AGE INT NOT NULL,
ADDRESS CHAR(50),
SALARY REAL
);
CREATE TABLE audit(
EMP_no INT NOT NULL,
NAME TEXT NOT NULL
);
```
</details>

#### &#127800; 创建触发器
```sql
CREATE TRIGGER trigger_name
trigger_time trigger_event ON tbl_name
FOR EACH ROW
trigger_stmt
```
- trigger_name：标识触发器名称，用户自行指定；
- trigger_time：标识触发时机，取值为 BEFORE 或 AFTER；
- trigger_event：标识触发事件，取值为 INSERT、UPDATE 或 DELETE；
- tbl_name：标识建立触发器的表名，即在哪张表上建立触发器；
- trigger_stmt：触发器程序体，可以是一句SQL语句，或者用 BEGIN 和 END 包含的多条语句，**每条语句结束要分号结尾。**

#### &#127800; NEW 与 OLD 详解
##### MySQL 中定义了 NEW 和 OLD，用来表示触发器的所在表中，触发了触发器的那一行数据。
**具体地：**

1. 在 INSERT 型触发器中，NEW 用来表示将要（BEFORE）或已经（AFTER）插入的新数据；
2. 在 UPDATE 型触发器中，OLD 用来表示将要或已经被修改的原数据，NEW 用来表示将要或已经修改为的新数据；
3. 在 DELETE 型触发器中，OLD 用来表示将要或已经被删除的原数据；
  - 使用方法： NEW.columnName （columnName 为相应数据表某一列名） 
  
  
<details>
<summary>&#127808; View The Codes &#127808;</summary>
  
```sql
CREATE TRIGGER audit_log AFTER INSERT ON employees_test FOR EACH ROW
BEGIN
     INSERT INTO audit
     VALUES (new.id, new.name);
END

# create trigger audit_log 
# after insert on employees_test for each row
# begin 
#     insert into audit
#     values(new.id, new.name);
# end
```
</details>