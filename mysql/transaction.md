# Transaction processing

并非所有的数据库都支持事务处理，MyISAM 和 InnoDB 是最常用的两种引擎。MyISAM 不支持事务处理

事务处理可以用于维护数据库的完整性，它保证成批的MySQL操作要么完全执行，要么完全不执行。

- 事务（transaction）：指一组 SQL 语句
- 回退（rollback）指撤销指定 SQL 语句的过程
- 提交（commit）指将未存储的SQL语句结果写入数据库表。
- 保留点（savepoint）指事务处理中设置的临时占位符（place-holder），你可以对它发布回退（与回退整个事务处理不同）。

## 标识需要回退的内容

START TRANSACTION;
-- SQL 操作

ROLLABCK;

`START TRANSACTION` 标识了事务的开始位置，`ROLLABCK` 标识了事务的结束位置，两者之间的位置的 SQL 语句是一个事务。如果在执行该事务过程中出现了某种错误，则数据会会退到事务执行前的状态。即使有一部分执行成功了。

- 需要注意的是，虽然能够在事务中写 CREATE 和 DROP 操作，但是执行回退后，它们无法被撤销。


## 提交

一般的 MySQL 都是针对数据库表执行和编写的，这就是所谓的隐含提交（implicit commit）即，提交（写或保存）操作时自动完成的(想要不使用默认提交，可以执行 SET autocommit=0)。但是在事务处理中，提交不会隐含地进行，为进行提交，需要使用COMMIT 明确地指出。

START TRANSACTION;
-- SQL 操作

COMMIT;

- 当 COMMIT 和 ROLLBACK 语句执行后，事务会自动关闭。


## 使用保留点

START TRANSACTION;
-- SQL 操作
SAVEPOINT delete1;
-- SQL 操作
ROLLABCK TO delete1;
