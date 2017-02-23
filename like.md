1、like里‘-’下划线表示匹配单个字符；
2、where pro_name like '%' 无法匹配 NULL；
3、和like更像的是正则表达式REGEXP通配符：
     例如 select product_name from product where product_name REGEXP '.000' order by product_name;
     '.000'中'.'表示匹配除了'\n'外的单个任意字符，即可匹配到2000，3000，a000等；和正则表达式匹配规则一样。     

