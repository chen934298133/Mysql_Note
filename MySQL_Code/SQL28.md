## &#128044; Description of the problem

**查找描述信息 (film.description) 中包含 robot 的电影对应的分类名称 (category.name) 以及电影数目 (count(film.film_id))，而且还需要该分类包含电影总数量 (count(film_category.category_id)) >=5 部**

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
INSERT INTO film VALUES(4,'AFFAIR PREJUDICE','A Fanciful Documentary of a Frisbee And a Lumberjack who must Chase a Monkey in A Shark Tank');
INSERT INTO film VALUES(5,'AFRICAN EGG','A Fast-Paced Documentary of a Pastry Chef And a Dentist who must Pursue a Forensic Psychologist in The Gulf of Mexico');
INSERT INTO film VALUES(6,'AGENT TRUMAN','A Intrepid Panorama of a robot And a Boy who must Escape a Sumo Wrestler in Ancient China');
INSERT INTO film VALUES(7,'AIRPLANE SIERRA','A Touching Saga of a Hunter And a Butler who must Discover a Butler in A Jet Boat');
INSERT INTO film VALUES(8,'AIRPORT POLLOCK','A Epic Tale of a Moose And a Girl who must Confront a Monkey in Ancient India');
INSERT INTO film VALUES(9,'ALABAMA DEVIL','A Thoughtful Panorama of a Database Administrator And a Mad Scientist who must Outgun a Mad Scientist in A Jet Boat');
INSERT INTO film VALUES(10,'ALADDIN CALENDAR','A Action-Packed Tale of a Man And a Lumberjack who must Reach a Feminist in Ancient China');
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
INSERT INTO category VALUES(7,'Drama','2006-02-14 20:46:27');
INSERT INTO category VALUES(8,'Family','2006-02-14 20:46:27');
INSERT INTO category VALUES(9,'Foreign','2006-02-14 20:46:27');
INSERT INTO category VALUES(10,'Games','2006-02-14 20:46:27');
INSERT INTO category VALUES(11,'Horror','2006-02-14 20:46:27');
INSERT INTO category VALUES(12,'Music','2006-02-14 20:46:27');
INSERT INTO category VALUES(13,'New','2006-02-14 20:46:27');
INSERT INTO category VALUES(14,'Sci-Fi','2006-02-14 20:46:27');
INSERT INTO category VALUES(15,'Sports','2006-02-14 20:46:27');
INSERT INTO category VALUES(16,'Travel','2006-02-14 20:46:27');
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
INSERT INTO film_category VALUES(1,6,'2006-02-14 21:07:09');
INSERT INTO film_category VALUES(2,11,'2006-02-14 21:07:09');
INSERT INTO film_category VALUES(3,6,'2006-02-14 21:07:09');
INSERT INTO film_category VALUES(4,11,'2006-02-14 21:07:09');
INSERT INTO film_category VALUES(5,6,'2006-02-14 21:07:09');
INSERT INTO film_category VALUES(6,6,'2006-02-14 21:07:09');
INSERT INTO film_category VALUES(7,5,'2006-02-14 21:07:09');
INSERT INTO film_category VALUES(8,6,'2006-02-14 21:07:09');
INSERT INTO film_category VALUES(9,11,'2006-02-14 21:07:09');
INSERT INTO film_category VALUES(10,15,'2006-02-14 21:07:09');
```
</details>

## Description of the output

<table border="1" cellpadding="2" cellspacing="0">   <tbody>    <tr>     <td>      <span><span>分类名称</span>category.name</span><br>     </td>     <td>      <span><span>电影数目</span>count(film.</span><span>film_id)</span><br>     </td>    </tr>    <tr>     <td>      <span>Documentary</span><br>     </td>     <td>      1     </td>    </tr>   </tbody>  </table>

## View The Answer

<details>
<summary>&#127808; View The Codes &#127808;</summary>
  
- 先找到每个电影分类下电影总数量大于5的category_id
- 注意：并不是包含robot条件下的
- like匹配: %robot% 


```sql
select c.name as '分类名称category.name',
       count(fc.film_id) as '电影数目count(film.film_id)'
from film f,category c,film_category fc
where f.description like '%robot%'
and f.film_id = fc.film_id
and c.category_id = fc.category_id
and c.category_id in (select category_id
                      from film_category
                      group by category_id
                       having count(film_id)>=5);
```
</details>
