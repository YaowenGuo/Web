# show

> 查看数据库

show databases;

> 切换使用的数据库

use <database_name>

> 查看数据库中的表

show tables;

> 查看表的列

show columns form <table name>

mysql 还有一个简写形式

desc[ribe] <table_name>

> 显示广泛的服务器信息

show status;

> 显示创建数据库和创建表的语句

show create database <database_name>;
show create table <table_name>;

> 查看服务误和警告

show errors;
show warnings;

> 查看更多show信息

show help;
