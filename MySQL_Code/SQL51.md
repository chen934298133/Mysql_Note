## &#128044; Description of the problem


### &#127800; 查找字符串'10,A,B' 中逗号','出现的次数cnt。



<details>
<summary>&#127808; View the Codes &#127808;</summary>
  
思路：
把串 "10,A,B" 中的 逗号用空串替代， 变成了 "10AB"
然后原来串的长度 - 替换之后的串的长度 就是 被替换的 逗号的个数
  
```sql
SELECT
	LENGTH('10,A,B') - LENGTH(REPLACE('10,A,B',",","")) cnt;
```
</details>

