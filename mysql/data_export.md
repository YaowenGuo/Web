1、mysqldump 备份并压缩sql文件
mysql>mysqldump -h主机ip -u用户名 -p密码（也可不输入） 数据库名   | gzip > 压缩后文件位置

2、mysql直接用压缩文件恢复

mysql>gunzip < backupfile.sql.gz | mysql -u用户名 -p密码（也可不输入） 数据库名
