## &#128044; Description of the problem

**给出每个员工每年薪水涨幅超过 5000 的员工编号 emp_no 、薪水变更开始日期 from_date 以及薪水涨幅值 salary_growth ，并按照 salary_growth 逆序排列。**

**提示：**

**在 sqlite 中获取 datetime 时间对应的年份函数为 strftime('%Y', to_date)
(数据保证每个员工的每条薪水记录 to_date-from_date = 1 年，而且同一员工的下一条薪水记录 from_data = 上一条薪水记录的 to_data)**

<details>
<summary> &#127808; View The SQL &#127808; </summary>

```sql
CREATE TABLE `salaries` (
`emp_no` int(11) NOT NULL,
`salary` int(11) NOT NULL,
`from_date` date NOT NULL,
`to_date` date NOT NULL,
PRIMARY KEY (`emp_no`,`from_date`));
如：插入
INSERT INTO salaries VALUES(10001,52117,'1986-06-26','1987-06-26');
INSERT INTO salaries VALUES(10001,62102,'1987-06-26','1988-06-25');
INSERT INTO salaries VALUES(10002,72527,'1996-08-03','1997-08-03');
INSERT INTO salaries VALUES(10002,72527,'1997-08-03','1998-08-03');
INSERT INTO salaries VALUES(10002,72527,'1998-08-03','1999-08-03');
INSERT INTO salaries VALUES(10003,43616,'1996-12-02','1997-12-02');
INSERT INTO salaries VALUES(10003,43466,'1997-12-02','1998-12-02');
```
</details>

## Description of the output

<table border="1" cellpadding="2" cellspacing="0">   <tbody>    <tr>     <td>      <span>e</span><span>mp_no</span><br>     </td>     <td>      <span>from_date</span><br>     </td>     <td>      <span>salar</span><span>y_</span><span>growth</span><br>     </td>    </tr>    <tr>     <td>      <span>10</span><span>001</span><br>     </td>     <td>      <span>198</span><span>7-06-26</span><br>     </td>     <td>      <span>9985</span><br>     </td>    </tr>   </tbody>  </table> 

## View The Answer

<details>
<summary>&#127808; View The Codes &#127808;</summary>
  
- 给出每个员工每年薪水涨幅超过 5000 的员工编号，薪水变更开始日期以及薪水涨幅值，并按照薪水涨幅值逆序排列。
- 由薪水涨幅值可知要求后一年的工资减去前一年的工资并且大于 5000，于是想到可使用两张表使用 join 连接起来，然后取每条记录的两个工资相减，连接条件是员工号相同， s2 表是 s1 表的后一年，且 s2 表工资减 s1 表的工资大于 5000 ，最后加上薪水涨幅值的逆序排序条件即可


```sql
select s1.emp_no, s2.from_date, (s2.salary-s1.salary) salary_growth
  
from salaries s1
join salaries s2
on s1.emp_no = s2.emp_no 
and s1.to_date = s2.from_date
  
where s2.salary - s1.salary > 5000
order by salary_growth desc
```
</details>
