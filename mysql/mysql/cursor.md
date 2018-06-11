# coursor

MySQL 查询的结构集为普通的多行时，是无法进行下一行、第一行或前10行之类的操作的。也不存在每次一行地逐步处理数据的方法。（或者在上层语言中处理返回的结果集，然后才能处理。）

有时候需要在 MySQL 中对结果集前进一行或后退一行货多行，这就需要使用游标。游标是一个存储在 MySQL 服务器上的数据库查询，它不是一条 SELECT 语句，而是被该语句检索出来的结果集。

游标主要用于交互式应用，其中用户需要滚动屏幕上的数据，并对数据进行浏览或做出更改。

不像多数的 DBMS，MySQL游标只能用于存储过程（和函数）。


步骤：
1. 在能够使用游标前，必须声明（定义）它。这个过程实际上没有检索数据，它只是定义了要使用的 SELECT 语句。
2. 一旦声明后，必须打开游标以供使用。这个过程用前面定义的 SELECT 语句把数据实际检索出来。
3. 对于填有数据的游标，根据需要取出各行。
4. 在游标结束使用时，不需关闭游标。

## DECLARE 创建

DECLARE 创建游标定指定响应的 SQL 语句。

CREATE PROCEDURE processOrders()
BEGIN
    -- 声明游标
    DECLARE ordernumbers CURSOR
    FOR
    SELECT order_num FROM orders;

    DECLARE o INT;
    DECLARE done BOOLEAN DEFAULT 0;
    DECLARE CONTINUE HANDLER FOR SQLSTATE '02000' SET done=1; -- 02000 是一个未找到的条件，当 REPEAT 由于没有更多的行供循环而不能继续时，出现这个条件。

    -- 打开游标，声明之后可以多次关闭打开，但是要对应。
    OPEN ordernumbers;

    -- Loop through all rows；
    REPEAT
        FETCH ordernumbers INTO o; -- 获取一个
    UNTIL done END REPEAT;

    -- 关闭游标

    CLOSE ordernumbers;

END;

存储过程执行完成后，游标就消失了，因为它局限于存储过程。

DECLARE 定义的局部变量必须在定义任意游标或句柄之前定义，而句柄必须在游标之后定义。不遵守词循序将产生错误消息。

## 打开存储过程

OPEN ordernumbers;

## 关闭

CLOSE ordernumbers;
