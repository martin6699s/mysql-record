```
CREATE TABLE `test` (
  `id` int(11) unsigned NOT NULL,
  `num` int(11) DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

```
```

set @x:=0;
insert into test(`id`,`num`) VALUES(1,10),(2,10),(6,60),(7,60),(10,60),(11,60)
on duplicate key update 
`id` = VALUES(`id`) + (0 * (@x := @x + 1));

select @x;
```
@x即为获取更新的条数；
此在高性能mysql中看到。乘零是为了不影响id的更新。