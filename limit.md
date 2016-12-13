SELECT * FROM users LIMIT [offset,] rows | rows OFFSET offset;
LIMIT 用于强制select语句返回指定的记录数。
LIMIT接受一或者二个整型常量。
第一个参数指定返回记录行的偏移量.初始记录行的偏移量是0 而不是1。
第二个参数指定返回记录行的最大数目。

// 为了检索从某一个偏移量到记录集的结束所有的记录行，可以指定第二个参数是使用比较大的数。
SELECT * FROM table LIMIT 95,95,18446744073709551615; //检索记录行96-last.

