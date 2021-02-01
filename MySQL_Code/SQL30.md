## &#128044; Description of the problem

**使用子查询的方式找出属于 Action 分类的所有电影对应的 title 和 description**

#### film表

<table border="1" cellpadding="2" cellspacing="0">   <tbody>    <tr>     <td>      字段     </td>     <td>      说明     </td>    </tr>    <tr>     <td>      film_id     </td>     <td>      电影id     </td>    </tr>    <tr>     <td>      title     </td>     <td>      电影名称     </td>    </tr>    <tr>     <td>      description     </td>     <td>      电影描述信息     </td>    </tr>   </tbody>  </table>

<br>

<details>
<summary> &#127808; View The SQL &#127808; </summary>

```sql
CREATE TABLE IF NOT EXISTS film (
film_id smallint(5)  NOT NULL DEFAULT '0',
title varchar(255) NOT NULL,
description text,
PRIMARY KEY (film_id));
```
  
```sql
INSERT INTO film VALUES(1,'ACADEMY DINOSAUR','A Epic Drama of a Feminist And a Mad Scientist who must Battle a Teacher in The Canadian Rockies');
INSERT INTO film VALUES(2,'ACE GOLDFINGER','A Astounding Epistle of a Database Administrator And a Explorer who must Find a Car in Ancient China');
INSERT INTO film VALUES(3,'ADAPTATION HOLES','A Astounding Reflection of a Lumberjack And a Car who must Sink a Lumberjack in A Baloon Factory');
```
</details>

#### category表

<table border="1" cellpadding="2" cellspacing="0">   <tbody>    <tr>     <td>      字段     </td>     <td>      说明     </td>    </tr>    <tr>     <td>      category_id     </td>     <td>      电影分类id     </td>    </tr>    <tr>     <td>      name     </td>     <td>      电影分类名称     </td>    </tr>    <tr>     <td>      last_update     </td>     <td>      电影分类最后更新时间     </td>    </tr>   </tbody>  </table>

<br>

<details>
<summary> &#127808; View The SQL &#127808; </summary>

```sql
CREATE TABLE category  (
category_id  tinyint(3)  NOT NULL ,
name  varchar(25) NOT NULL, `last_update` timestamp,
PRIMARY KEY ( category_id ));
```
```sql

INSERT INTO category VALUES(1,'Action','2006-02-14 20:46:27');
INSERT INTO category VALUES(2,'Animation','2006-02-14 20:46:27');
INSERT INTO category VALUES(3,'Children','2006-02-14 20:46:27');
INSERT INTO category VALUES(4,'Classics','2006-02-14 20:46:27');
INSERT INTO category VALUES(5,'Comedy','2006-02-14 20:46:27');
INSERT INTO category VALUES(6,'Documentary','2006-02-14 20:46:27');
```
</details>

#### film_category表 

<table border="1" cellpadding="2" cellspacing="0">   <tbody>    <tr>     <td>      字段     </td>     <td>      说明     </td>    </tr>    <tr>     <td>      film_id     </td>     <td>      电影id     </td>    </tr>    <tr>     <td>      category_id     </td>     <td>      电影分类id     </td>    </tr>    <tr>     <td>      last_update     </td>     <td>      电影id和分类id对应关系的最后更新时间     </td>    </tr>   </tbody>  </table> 

<br>

<details>
<summary> &#127808; View The SQL &#127808; </summary>

```sql
CREATE TABLE film_category  (
film_id  smallint(5)  NOT NULL,
category_id  tinyint(3)  NOT NULL, `last_update` timestamp);
```
```sql

INSERT INTO film_category VALUES(1,1,'2006-02-14 21:07:09');
INSERT INTO film_category VALUES(2,1,'2006-02-14 21:07:09');
INSERT INTO film_category VALUES(3,6,'2006-02-14 21:07:09');
```
</details>

## Description of the output

<table border="1" cellpadding="2" cellspacing="0">   <tbody>    <tr>     <td>      <span>title</span><br>     </td>     <td>      <span>description</span><br>     </td>    </tr>    <tr>     <td>      <span>ACADEMY DINOSAUR</span><br>     </td>     <td>      <span>A Epic Drama of a Feminist And a Mad Scientist who must Battle a Teacher in The Canadian Rockies</span><br>     </td>    </tr>    <tr>     <td>      <span>ACE GOLDFINGER</span><br>     </td>     <td>      <span>A Astounding Epistle of a Database Administrator And a Explorer who must Find a Car in Ancient China</span><br>     </td>    </tr>   </tbody>  </table> 

## View The Answer

<details>
<summary>&#127808; View The Codes_1&#127808;</summary>
  


```sql
select f.title, f.description
from film f 
where f.film_id in (
    select fc.film_id
    from film_category fc right join category c
    on fc.category_id = c.category_id
    where c.name = "Action"
)
```
</details>

<details>
<summary>&#127808; View The Codes_2 &#127808;</summary>
  


```sql
select f.title, f.description
from (
select c.category_id , f.film_id
from film_category fc , category c , film f
WHERE f.film_id =fc.film_id
AND fc.category_id = c.category_id
AND c.name = 'Action'
) a , film f
WHERE f.film_id = a.film_id
;
```
</details>