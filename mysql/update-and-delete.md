[TOC]

# update

**更新数据是一个危险行为，一定要添加筛选条件，除非确定更新所有的行。**

UPDATE table_name
SET column_name1 = new_value, ...
SHERE filter_limit;

WHERE 中可以使用子查询。

IGNORE 如果在更新过程中出现一个错误，将导致更新结束，剩下的无法执行。为了能够在发生错误后，继续执行之后的更新，可以使用 IGNORE 关键字。

UPDATE IGNORE table_name
SET ...


# delete

**千万不要忘记筛选条件**

DELETE FROM table_name
WHERE ...;

# 清空表

RRUNCATE TABEL table_name;

清空整张表，比 delete 更快，不会逐行扫描。
