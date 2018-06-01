# insert;

## 插入完整的行

inseat into table_name
values (col, .....);

按表中的顺序给出值，没有值的要使用 NULL 占位，它将被 MySQL 忽略。

这对于会经常改变表结构的表非常不安全。

## 插入不完整的行

insert into table_name
(column_name, ...)
value
(value, ...);

这里指定了列名，值要按照列名的顺序依次填写。

可以省略列，只有具有默认值或允许为NULL的列可以省略。


数据库经常被多个客户访问，对处理什么请求以及以什么顺序处理请求管理是 MySQL 的任务。insert 操作可能很耗时（特别是当有很多索引需要更新时），并且它可能降低等待处理的 select 语句的性能。

如果数据检索是重要的，则已可以通过在 insert 和 into 之间 添加关键字 low_priority，指示 MySQL 降低 insert 语句优先级。这也使用与 update 和 delete 语句。

## 插入多行数据

insert into table_name
(column_name, ...)
value
(value, ...),
(value, ...);

比使用多条插入要快。

## 插入检索出的数据

insert into table_name
(column_name, ...)
select
(column_name, ...),
from origin_table_name;

只关系列的位置，因此列名不同不受影响。
