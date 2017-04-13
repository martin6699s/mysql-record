1. repeat函数--repeat(`字段名`,'A','B'),表示在字段上的数据 凡是有A存在的都替换成B;
最近就遇到一问题，假如在article表(mysql5.6 innodb)中，已知有5000篇文章，需要把文章中"公司A"替换成"公司B","大人"替换成"小孩","员工"替换成"职工","专家"替换成"砖家"，已知第一篇文章id是1，第5000篇文章id是16000
这时候就可以用到repeat函数：
例如把"大人"替换成"小孩""
```
update article set content = replace(content,'大人','小孩') where id <=16000;
```
测试影响条数373条,处理时间:142ms;
算挺耗时间的，另一种思路是利用程序语言如php的str_replace处理后再更新到数据库，这种没适合，之后试试看。
还有就是mysql5.6.4终于有全文检索新特性了，在varchar,text上都可以用，加上会不会对性能提升呢，对中文支持不好。


mysql5.6.35
ALTER TABLE `article` ADD FULLTEXT INDEX `article_full_text_index_content` (`content` ASC);
加了这条用时237s,共426006条数据；