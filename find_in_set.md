在mysql中，有时我们需要查询某字段包含某个值的记录，但它不是用like解决的，因为like可能没法准确查询我们想要的记录，例如list字段的值规律是(1，5，7，9),我们要查找到7数字，那就要用到mysql中的FIND_IN_SET(str,strlist)函数，str是要查询的字符串，strlist是字段名，参数以','分隔；
SELECT * FROM data WHERE FIND_IN_SET('7',list);
就能准确定位到list中包含7的记录

