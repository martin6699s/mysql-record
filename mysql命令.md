1、mysql> SHOW PROCESSLIST;查看有哪些线程在mysql上运行，可帮助识别有问题的查询语句；查询结果中command列 显示当前连接执行的命令，一般就是休眠(sleep),查询(query),连接(connect)。还有比较重要的state列，显示使用当前连接的sql语句状态，通过该列可查看有问题的sql;

2、mysql> EXPLAIN EXTENDED+sql语句，优化查询；

3、msyql> SHOW STATUS LIKE 'Handler_read_%' 查看处理程序变量，有利于查看索引是否合理;
Handler_read_rnd_next：在数据文件中读下一行的请求数。如果你正进行大量的表扫描，该值较高。通常说明你的表索引不正确或写入的查询没有利用索引。
Handler_read_key：如果索引正在工作，这个值代表一个行被索引值读的次数，如果值越低，表示索引得到的性能改善不高，因为索引不经常使用（这个值越高越好）。而且Handler_read_key相对于Handler_read_rnd_next不能太低，比例Handler_read_rnd_next:Handler_read_key 个人感觉不要超过100:1；

4、mysql> SHOW GLOBAL STATUS LIKE 'com_select'; 调出服务器完成的查询请求次数；
   计算表扫描率：
　　表扫描率 = Handler_read_rnd_next / Com_select
　　如果表扫描率超过4000，说明进行了太多表扫描，很有可能索引没有建好，增加read_buffer_size值会有一些好处，但最好不要超过8MB。




