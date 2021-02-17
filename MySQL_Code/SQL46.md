## &#128044; Description of the problem


### &#127800;  在audit表上创建外键约束，其emp_no对应employees_test表的主键id。(以下2个表已经创建了) 


<details>
<summary>&#127808; View The SQL &#127808;</summary>
  

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
create_date datetime NOT NULL
);
```
</details>


#### &#127800; 创建外键约束

<details>
<summary>&#127808; View The Codes &#127808;</summary>
  

```sql
  
ALTER TABLE audit
ADD CONSTRAINT FOREIGN KEY (emp_no)
REFERENCES employees_test(id);

# 创建外键语句结构：
# ALTER TABLE <表名>
# ADD CONSTRAINT FOREIGN KEY (<列名>)
# REFERENCES <关联表>（关联列） 

```
</details>
  
  
<details>
<summary>&#127808; 建表时如何添加外键约束 &#127808;</summary>

```sql
  
DROP TABLE audit;
CREATE TABLE audit(
    EMP_no INT NOT NULL,
    create_date datetime NOT NULL,
    FOREIGN KEY(EMP_no) REFERENCES employees_test(ID));
    # foreign key（emp_no） references employees_test(id));

```
</details>
