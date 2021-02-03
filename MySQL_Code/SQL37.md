## &#128044; Description of the problem


### &#127800; 对first_name创建唯一索引uniq_idx_firstname，对last_name创建普通索引idx_lastname 

***提示：针对如下表actor结构创建索引：
(注:在 SQLite 中,除了重命名表和在已有的表中添加列,ALTER TABLE 命令不支持其他操作，
mysql支持ALTER TABLE创建索引)***

```sql
CREATE TABLE actor  (
   actor_id  smallint(5)  NOT NULL PRIMARY KEY,
   first_name  varchar(45) NOT NULL,
   last_name  varchar(45) NOT NULL,
   last_update  datetime NOT NULL);
```

<br>
MySQL中两种方式给字段添加索引

<details>
<summary>&#127808; ALTER TABLE tableName ADD INDEX (columnName1, columnName2); &#127808;</summary>
  

1. 添加主键

```sql
ALTER TABLE tbl_name ADD PRIMARY KEY (col_list);
// 该语句添加一个主键，这意味着索引值必须是唯一的，且不能为NULL。
```

2. 添加唯一索引

```sql
ALTER TABLE tbl_name ADD UNIQUE index_name (col_list);
// 这条语句创建索引的值必须是唯一的。
```

3. 添加普通索引

```sql
ALTER TABLE tbl_name ADD INDEX index_name (col_list);
// 添加普通索引，索引值可出现多次。
```

4. 添加全文索引

```sql
ALTER TABLE tbl_name ADD FULLTEXT index_name (col_list);
// 该语句指定了索引为 FULLTEXT ，用于全文索引。
```

5. 删除索引的语法

```sql
ALTER TABLE tbl_name DROP INDEX index_name；
ALTER TABLE tbl_name DROP PRIMARY KEY;
```
</details>

<details>
<summary>&#127808; CREATE INDEX index_name HeadOfState (columnName1, columnName2); &#127808;</summary>
  
1. 添加主键

```sql
# 不能用CREATE INDEX语句创建PRIMARY KEY索引。
```

2. 添加唯一索引

```sql
create unique index index_name on table_name (column_list) ;　　#表中有primary Key后不能用uniq index。
// 这条语句创建索引的值必须是唯一的。
```

3. 添加普通索引

```sql
create index index_name on table_name (column_list) ;
// 添加普通索引，索引值可出现多次。
```

4. 添加全文索引

```sql
ALTER TABLE tbl_name ADD FULLTEXT index_name (col_list);
// 该语句指定了索引为 FULLTEXT ，用于全文索引。
```
  
5. 删除索引的语法

```sql
DROP INDEX index_name ON tbl_name; 
// 或者
ALTER TABLE tbl_name DROP INDEX index_name；
ALTER TABLE tbl_name DROP PRIMARY KEY;
```
  
</details>

<details>
<summary>&#127808; 两者区别 &#127808;</summary>
  
1. CREATE INDEX必须提供索引名，对于ALTER TABLE，将会自动创建，如果你不提供；
2. CREATE INDEX一个语句一次只能建立一个索引，ALTER TABLE可以在一个语句建立多个，
    - 如：ALTER TABLE HeadOfState ADD PRIMARY KEY (ID), ADD INDEX (LastName,FirstName);
3. 只有ALTER TABLE 才能创建主键，
</details>
<br>

### 删除索引的注意点

<details>
<summary>&#127808; 删除索引的注意点&#127808;</summary>
  
```sql
DROP INDEX index_name ON tbl_name; 
// 或者
ALTER TABLE tbl_name DROP INDEX index_name；
ALTER TABLE tbl_name DROP PRIMARY KEY;

/* 其中，在前面的两条语句中，都删除了table_name中的索引index_name。而在最后一条语句中，只在删除PRIMARY KEY索引中使用，因为一个表只可能有一个PRIMARY KEY索引，因此不需要指定索引名。如果没有创建PRIMARY KEY索引，但表具有一个或多个UNIQUE索引，则MySQL将删除第一个UNIQUE索引。
如果从表中删除某列，则索引会受影响。对于多列组合的索引，如果删除其中的某列，则该列也会从索引中删除。如果删除组成索引的所有列，则整个索引将被删除。
删除索引的操作，如下面的代码：
mysql> drop index shili on tpsc ;
Query OK, 2 rows affected (0.08 sec)
Records: 2 Duplicates: 0 Warnings: 0
该语句删除了前面创建的名称为“shili”的索引。
*/
```
</details>


<br>

<details>
<summary>&#127808; View The Codes &#127808;</summary>
  
```sql
CREATE INDEX idx_lastname ON actor(last_name);
CREATE UNIQUE INDEX uniq_idx_firstname ON actor(first_name);

alter table actor add unique uniq_idx_firstname(first_name);
alter table actor add index idx_lastName(last_name);
```
</details>