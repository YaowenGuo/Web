# sql mode

Mysql 有许多用于设置 mysql 执行方式的变量，被称为 VARIABLES.

## 查看 show

SHOW VARIABLES;

可以使用 like 过滤结果

SHOW VARIABLES LIKE "sql_mod%";


## sql_mode
### ONLY_FULL_GROUP_BY

5.7 之后 group by 默认是严格模式，是指 select 的内容，只能是 group by 的列或聚集函数对于 group by 的操作。 不允许出现 group by 子句之外的列。

例如

SELECT name, age FROM user
GROUP BY name;

则 age 是不确定的，因为按照 name 分组后，一组中的 age 值并不相同，mysql 5.7 之前， mysql 会选择一个输出，由于没有规则，这个值变得不确定。

而对于语义限制都比较严谨的多家数据库，如SQLServer、Oracle、PostgreSql都不支持select target list中出现语义不明确的列，这样的语句在这些数据库中是会被报错的，这也是SQL92的标准。所以从MySQL 5.7版本开始修正了这个语义，就是我们所说的ONLY_FULL_GROUP_BY语义。

最好是修改 sql 语句，这样能保证数据的正确和向后兼容，但是如果确定要使用老的查询模式，可以使用。

去掉ONLY_FULL_GROUP_BY，重新设置值。

set @@sql_mode ='STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER
,NO_ENGINE_SUBSTITUTION';

3、上面是改变了全局sql_mode，对于新建的数据库有效。对于已存在的数据库，则需要在对应的数据下执行：

SET GLOBAL sql_mode=(SELECT REPLACE(@@sql_mode,'ONLY_FULL_GROUP_BY',''));

但是这种设置方式会在 mysql 重启后失效，想要永久有效就需要配置 mysqld.cnf 文件，添加

sudo nano /etc/mysql/my.cnf
Add this to the end of the file

[mysqld]  
sql_mode = "STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION"
sudo service mysql restart to restart MySQL

This will disable ONLY_FULL_GROUP_BY for ALL users



解决方案二：

MySQL有any_value(field)函数，他主要的作用就是抑制ONLY_FULL_GROUP_BY值被拒绝

官方有介绍，地址：https://dev.mysql.com/doc/refman/5.7/en/miscellaneous-functions.html#function_any-value

我们可以把select语句中查询的属性（除聚合函数所需的参数外），全部放入any_value(field)函数中；

例如：select name,any_value(sex) from test_table group by name

这样sql语句不管是在ONLY_FULL_GROUP_BY模式关闭状态还是在开启模式都可以正常执行，不被mysql拒绝。
