1、like里‘-’下划线表示匹配单个字符；
2、where pro_name like '%' 无法匹配 NULL；
3、和like更像的是正则表达式REGEXP通配符：
     例如 select product_name from product where product_name REGEXP '.000' order by product_name;
     '.000'中'.'表示匹配除了'\n'外的单个任意字符，即可匹配到2000，3000，a000等；和正则表达式匹配规则一样。
4、今天遇到like '%你好%' 匹配不到中文的问题，
解决思路：
   - 比较二进制 
      -- select product_name from product where product_name like binary '%你好%'; 
   - 网上说的使用locate(substr,str)函数也是可以的, 只要找到返回的结果都是大于0 ，但要注意参数位置，
   第一次使用参数位置不对，错误认为它在第一个位置出现会返回0
      -- select product_name where locate('你好',product_name) > 0;

