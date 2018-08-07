[TOC]

# create

CREATE TABLE table_name [IF NOT EXISTS]
(
    column_name1 type [NOT NULL [DEFAULR default_value]] [AUTO_INCREMENT] desc,
    ...
    PRIMARY KEY(column_name[, more_colume, ...])
) ENGIN=INNODB, CHARSET=UTF-8;

- 主键必须是唯一的，可以使用多列，使用多列是，多格列组成的值是唯一的即可。

- 主键用来唯一标识该行数据，因此主键不能为 NULL，可以使用自动增长。

- 每个表值允许有一个 AUTO_INCREMENT, 而且他必须被序偶应。

使用 AUTO_INCREMENT 的一大缺点是，你不知道最后一个插入的 AUTO_INCREMENT 值，可以使用 SELECT last_insert_id() 获得。

- mysql 不允许使用函数作为默认值，只允许使用常量。

- 数据引擎，不指定将默认使用 MyISAM 引擎。

- 外键不能跨引擎。

- MyISAM 不支持事务，InnoDB 不支持全文本搜索。

# alert

添加

ALERT TABLE table_name
ADD column_name <type> [AFTER|BEFORE 原有列名], ...
FOREIGN KEY(column_name, ...) FORERENCES order (order_num);

ALTER TABLE `panda_site`.`panda_new_oauth_users`
MODIFY COLUMN `background` varchar(500) CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci NULL DEFAULT ‘https://www.pandarowcdn.com/user/background/user-default-bg.jpg’ AFTER `firebase_token`;

删除

ALERT TABLE table_name
DROP COLUMN column_name;

# DROP

DROP TABLE table_name;

# rename

RENAME TABLE table_name TO new_name [, table_name TO new_name] ...;
