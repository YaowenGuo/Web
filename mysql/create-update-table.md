[TOC]

# create

CREATE TABLE table_name [IF NOT EXISTS]
(
    column_name1 type NOT NULL AUTO_INCREMENT desc,
    ...
    PRIMARY KEY(column_name[, more_colume, ...])
) ENGIN=INNODB, CHARSET=UTF-8;

主键必须是唯一的，可以使用多列，使用多列是，多格列组成的值是唯一的即可。

主键用来唯一标识该行数据，因此主键不能为 NULL，可以使用自动增长。
