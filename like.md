1、like里‘-’下划线表示匹配单个字符；
2、where pro_name like '%' 无法匹配 NULL；
3、和like更像的是正则表达式REGEXP通配符：
     例如 select product_name from product where product_name REGEXP '.000' order by product_name;
     '.000'中'.'表示匹配除了'\n'外的单个任意字符，即可匹配到2000，3000，a000等；和正则表达式匹配规则一样。
4、今天遇到like '%你好%' 匹配不到中文的问题，解决思路：比较二进制 -- select product_name from product where product_name like binary '%你好%'; 
网上说的使用locate(`product_name`,'你好')函数[locate(substr,str)]返回substr第一次出现的位置，有可能第0位，所以判断不准；     

