当你需要对数据进行统计，需要使用到聚合函数时，可以通过group by 分组得到对应的数据。例如
假如每篇文章都会记录文章点击量，article表存储文章，还有张article_click_log表(里面有article_id字段,userId字段,时间戳字段等),
每次有人点击进来就记录进article_click_log表，现在想统计最高点击量的四篇文章ID，可以这样写mysql语句：
SELECT `article_click_log`.`article_id`, count(`article_click_log`.`id`) AS `counts` FROM `article_click_log` INNER JOIN `article` ON `article`.`id` = `article_click_log`.`article_id` 
GROUP BY `article_click_log`.`article_id` ORDER BY `counts` DESC LIMIT 4

