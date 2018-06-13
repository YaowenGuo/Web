# safe

用户应该对他们需要的数据具有适当的访问权限，不能多也不能少。

- 访问控制权限的目的不仅仅是方式用户的而已企图，数据梦魇更为常见的是无意识错误的结果。如打错 MySQL 语句，在不合适的数据库库中操作或其他一些用户错误。

- 绝不要使用 root 登录，除非绝对需要它时。


## 管理用户

MySQL 的用户账号和信息存储在名为 mysql 的MySQL 数据库中。一般不需要直接访问 mysql 数据库和表。

USE mysql;

SELECT user FROM user;

### 创建账户

CREATE USER user_name [IDENTIFIED BY 'password'];

创建用户时不一定需要口令。

- 指定散列口令 IDENTIFIED BY 指定的口令为纯文本，MySQL 将保存到 user 表之前对齐进行加密，为了作为散列值指定口令，使用`IDENTIFIED BY PASSWORD`。

- 使用 GRANT 或 INSERT GRANT 语句也可以常见用户账号，但一般来说 GRANTE USER 是最清楚和最简单的句子，此外，也可以通过直接插入行到 user 表增加用户，不过为安全起见，一般不建议这样做。MySQL 用来存储用户账号信息的表极其重要，对他们的任何损坏都可能严重地伤害到 MySQL 服务器。因此，相对于直接处理来说，最好是用标记和函数来出来这些表。

### 重命名

RENAME USER user_name TO new_name;

### 删除用户

DROP USER user_name;

### 设置访问权限

新建的用户没有任何访问权限

SHOW GRANTS FOR user_name;

`USAGE ON *.*`， USAGE 表示根本没有权限。
`user_name%host`, 如果不指定主机名，则默认的主机名为`%`，授予用户访问权限而不管主机名。



GRANT SELECT ON databae_name.[table_name] TO user_name;

必须给出以下信息

- 要授予的权限
- 被授予权限的数据库或表
- 用户名

### 撤销权限

REVOKE SELECT ON databae_name.[table_name] TO user_name;

GRANT 和 REVOKE 可以在基本层次上控制访问权限。

- 整个服务器，使用 GRANT ALL 和 REVOKE ALL;
- 整个数据库，使用 ON DATABASE.* ;
- 整个表， 使用 ON DATABASE.table;
- 特定的列
- 特定的存储过程


### 更改密码

SET PASSWORD [FOR user_name] = password('new password');

为自己指定密码时，可以不指定用户名。
