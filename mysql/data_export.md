# 备份

## 导出外部文件

> 受限刷新未写入数据

FLUSH TABLES;

> 检测表件是否正确

ANALYZE TABLE table_name;

> CHECK TABLE 更详细的检查

CHECK TABLE table_name , ...;


1、mysqldump 备份并压缩sql文件
$ mysqldump -h主机ip -u用户名 -p密码（也可不输入） 数据库名   | gzip > 压缩后文件位置

2、mysql直接用压缩文件恢复

$ gunzip < backupfile.sql.gz | mysql -u用户名 -p密码（也可不输入） 数据库名

## 拷贝所有数据

mysqlhotcopy 从一个数据库复制所有数据。


## 转储所有数据到某个外部文件

BACKUP TABLE
SELECT INTO OUTFILE

RESTORE FILE 恢复文件。


# 诊断启动问题

使用手动启动，启动的 mysqld 接受命令行选项

- --help 显示帮助
- --safe-mode 装载减去某些最佳配置的服务器
- --verbose 显示全文本消息。
- --version 显示版本信息

# 日志

- 错误日志： 位于data 目录中的 hostname.err 文件
- 查询日志： data目录下的 hostname.log
- 二进制日志：跟新过的数据的所有语句。
- 缓慢查询日志：记录执行缓慢的任何查询。hostname-slow.log
