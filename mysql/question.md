# Question & Answer

# Mysql 意外锁表

25号早上的时候后台无法访问,最后是查出mysql数据库数据库备份的操作被一个事务操作锁住所导致。

1.现在已经查出当时该事务操作的原因.
我的google_suggest_spider在凌晨4点30分的时候会查询204服务器上的app_coupon_brand表(该表被锁)
相关语句是:
website_sql = "select website from {table} where status = %s".format(table = brand_table)
website_list = remote_db.get_values(website_sql,'unreviewed');
问题在于为什么一个查询操作也会对表执行一个事务操作?
google上查找相关的资料,最终确定python MySqlDb模块默认autocommit 关闭,所以即使是select操作,
也会在一个事务中执行.
解决方法: 1.在执行语句后立刻执行conn.commit() 或者 conn.close()
                 2.conn.autocommit(True)  设置autocommit为True


Mysql官方提供的pythonApi:  MySqlDb模块
相关文档:
https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlconnection-autocommit.html

https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html
Pymysql模块 也是默认关闭autocommit
https://gist.github.com/mindriot101/664924f7a0e4e961aea9

2.本地相关测试截图:
执行上述语句后睡眠

SELECT * FROM information_schema.innodb_trx \G 将会显示当前数据库事务操作

在对代码进行修改,及时commit或者关闭conn,或者设置conn.autocommit(True).后该问题得到解决
