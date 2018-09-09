利用group_concat函数和group by聚合函数返回串级的以逗号分割的非空字符串数据。如以下面book_mast表中以pub_id分组查询出多个逗号分隔的cate_id字符串

book_mast表

```
+---------+-------------------------------------+-------------+---------+--------+--------+------------+----------+---------+------------+
| book_id | book_name                           | isbn_no     | cate_id | aut_id | pub_id | dt_of_pub  | pub_lang | no_page | book_price |
+---------+-------------------------------------+-------------+---------+--------+--------+------------+----------+---------+------------+
| BK001   | Introduction to Electrodynamics     | 0000979001  | CA001   | AUT001 | P003   | 2001-05-08 | English  |     201 |      85.00 |
| BK002   | Understanding of Steel Construction | 0000979002  | CA002   | AUT002 | P001   | 2003-07-15 | English  |     300 |     105.50 |
| BK003   | Guide to Networking                 | 0000979003  | CA003   | AUT003 | P002   | 2002-09-10 | Hindi    |     510 |     200.00 |
| BK004   | Transfer  of Heat and Mass          | 0000979004  | CA002   | AUT004 | P004   | 2004-02-16 | English  |     600 |     250.00 |
| BK005   | Conceptual Physics                  | 0000979005  | CA001   | AUT005 | P006   | 2003-07-16 | NULL     |     345 |     145.00 |
| BK006   | Fundamentals of Heat                | 0000979006  | CA001   | AUT006 | P005   | 2003-08-10 | German   |     247 |     112.00 |
| BK007   | Advanced 3d Graphics                | 0000979007  | CA003   | AUT007 | P002   | 2004-02-16 | Hindi    |     165 |      56.00 |
| BK008   | Human Anatomy                       | 0000979008  | CA005   | AUT008 | P006   | 2001-05-17 | German   |      88 |      50.50 |
| BK009   | Mental Health Nursing               | 0000979009  | CA005   | AUT009 | P007   | 2004-02-10 | English  |     350 |     145.00 |
| BK010   | Fundamentals of Thermodynamics      | 0000979010  | CA002   | AUT010 | P007   | 2002-10-14 | English  |     400 |     225.00 |
| BK011   | The Experimental Analysis of Cat    | 0000979011  | CA004   | AUT011 | P005   | 2007-06-09 | French   |     225 |      95.00 |
| BK012   | The Nature  of World                | 0000979012  | CA004   | AUT005 | P008   | 2005-12-20 | English  |     350 |      88.00 |
| BK013   | Environment a Sustainable Future    | 0000979013  | CA004   | AUT012 | P001   | 2003-10-27 | German   |     165 |     100.00 |
| BK014   | Concepts in Health                  | 0000979014  | CA005   | AUT013 | P004   | 2001-08-25 | NULL     |     320 |     180.00 |
| BK015   | Anatomy & Physiology                | 0000979015  | CA005   | AUT014 | P008   | 2000-10-10 | Hindi    |     225 |     135.00 |
| BK016   | Networks and Telecommunications     | 00009790_16 | CA003   | AUT015 | P003   | 2002-01-01 | French   |      95 |      45.00 |
+---------+-------------------------------------+-------------+---------+--------+--------+------------+----------+---------+------------+
```
查询代码如下：

```
SELECT pub_id,GROUP_CONCAT(cate_id)
FROM book_mast
GROUP BY pub_id;
```
查询结果如下：
```
mysql> SELECT pub_id,GROUP_CONCAT(CATE_ID)
    -> FROM book_mast
    -> GROUP BY pub_id;
+--------+-----------------------+
| pub_id | GROUP_CONCAT(CATE_ID) |
+--------+-----------------------+
| P001   | CA002,CA004           | 
| P002   | CA003,CA003           | 
| P003   | CA001,CA003           | 
| P004   | CA005,CA002           | 
| P005   | CA001,CA004           | 
| P006   | CA005,CA001           | 
| P007   | CA005,CA002           | 
| P008   | CA005,CA004           | 
+--------+-----------------------+
8 rows in set (0.02 sec)
```

注意：完整的SQL，是需要注意group_concat的内排序，否则顺序不能保证，这时候需要加order by保证排序.如：

```
SELECT pub_id,GROUP_CONCAT(cate_id order by dt_of_pub desc)
FROM book_mast
GROUP BY pub_id;
```


[参考链接](https://www.w3resource.com/mysql/aggregate-functions-and-grouping/aggregate-functions-and-grouping-group_concat.php)
