利用dateformat函数格式化日期：

查出自2017年7月1日开始，每日注册量：
select count(id) , date_format(`created_at`,'%Y-%m-%d') from users where created_at >= '2017-07-01' group by date_format(`created_at`,'%Y-%m-%d') ;

