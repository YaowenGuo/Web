# 存储过程

MySQL5 才开始支持存储过程。

[TOC]

存储过程是为有复杂业务逻辑处理而提供的功能，有一些比较复杂的逻辑，需要进行多个表的复杂操作，甚至还需要根据查询结果来判断是否需要操作另一表。例如，商品销售、付款。这些信息都牵涉到不同用户的信息操作的同步完成。

- 通过把复杂的逻辑封装在容易使用的单元中，复用这些单元，简化操作。
- 由于不要求反复建立一系列处理过程，这保证了数据的完整性，所有的操作都是用同一存储过程，使测试更加充分，防止了额外的错误。
- 简化由于表名，字段名的更改导致的修改。业务逻辑人员甚至不需要知道操作的过程，只需要知道存储过程的名称。
- 提高性能，因为存储过程要比单条的 SQL 语句组合要快。
- 存在一些只能在单个请求中的元素或特性，存储过程可以用他们编写更加灵活和强大的功能代码。
- 更复杂，需要更多的知识与经验
- 存储过程的访问和创建权限可以分别分配。可以有灵活的安全控制权限。


## 创建存储过程

MySQL 的存储过程实际上是一种函数函数，实际使用也一样。

CREATE PROCEDURE procedure_name(args...)
BEGIN
    处理内容，可以使用SQL语句和逻辑操作...
END;

> 例如求平均价

CREATE PROCEDURE averagePrice()
BEGIN
    SELECT avg(prace) AS price_average
    FROM products;
END;

- CREATE PROCEDURE 用来创建存储过程
- procedure_name 必须制定一个全库唯一的标识符来表示存储过程，用于调用时标识。后面的`()`是必须的，即使没有参数。
- BEGIN 和 END 限制存储体的开始和结束，标识该存储过程的范围。

这段代码虽然没有返回任何数据，但是不代表不能查看查询的结果，执行改存储过程

## 调用存储过程

CALL procedure_name(args);

call averagePrice();
将返回和单独调用内部的 SQL 语句相同格式的查询输出，但是averagePrice() 外却没有获得查询结果的返回值。

> MySQL 命令行客户机的分割符. 如果使用 MySQL 命令行使用程序，应当注意
默认的 MySQL 语句的分割符是`;`，MySQL 命令行实用程序也使用`;`作为语句的分隔符，如果命令行使用程序处理了存储过程中的`;`分割符，则存储过程在交给 MySQL 时是没有分割符的，这会是存储过程中的 SQL 出现句法错误。解决办法是临时更改命令行实用程序的语句分割符。

DELIMITER //

CREATE PROCEDURE averagePrice()
BEGIN
    SELECT avg(prace) AS price_average
    FROM products;
END //

DELIMITER ;

其中`DELIMITER //` 告诉命令行实用程序使用`//`作为语句分割符，`DELIMITER ;`从新设置回 `;`。 此时看到存储过程的结束分割符不再使用`;`，而是使用更改后的`//`。但是存储过程内部还是保持了`;`。

除 `;` 外，任何字符都可以作为语句分割符。

## 删除存储过程

如果你想要修改存储过程，就会发现已经有同名的存过过程，新的存储过程是创建不成功的，此时就需要先删除存储过程，然后再创建

DROP PROCEDURE procedure_name [IF EXISTS]:
注意此时标识符后并没有括号。

## 使用参数

CREAT PROCEDURE productPracing (
    OUT low DECIMAL(8, 2),
    OUT high DECIMAL(8, 2)
    OUT average DECIMAL(8, 2)
)
BEGIN
    SELECT min(price) INTO low FROM products；
    SELECT max(price) INTO high FROM products；
    SELECT avg(price) INTO average FROM products；
END;

关键字 OUT 表示传出数据，类似的 IN 表示传入数据，INOUT 表示传入传出数据。

> 调用

CALL productPracing(@priceLow, @priceHigh, @priceAverage);

所有 MySQL 变量都要以 @ 符号开头。

调用该函数并不现实任何结果，只是将结果存储在了变量中。想要现实变量的值。

SELECT @priceLow, @priceHigh, @priceAverage;


> 查看存储过程
SHOW CREATE PROCEDURE procedure_name;

SHOW PROCEDURE STATUS;

可以指定过滤模式

SHOW PROCEDURE STATUS LIKE ‘price’;

> 更复杂的存储过程

存储过程是可以对条件进行判断和声明局部变变量的。

```
CREATE PROCEDURE ordertotal(
    IN onumber INT,
    INT taxable BOOLEAN,
    OUT ototal DECIMAL(2, 8)
) COMMENT 'Obtion order total, Optionally add tax'
BEGIN
    -- Declare variable for ototal
    DECLARE total DECIMAL(8, 2);
    -- Declare tax percentage
    DECLARE taxrate INT DEFAULT 6;

    -- Get the order ototal
    SELECT sum(item_price * quantity)
    FROM order_items
    WHERE order_num = onumber
    INTO total;

    -- Is this taxable?
    IF taxable THEN
        SELECT total + (total / 100 * texrate) INTO total;
    ENDIF

    -- And finally, save to out variable.
    SELECT total INTO ototal;

END;
```

IF () THEN
...
ELSEIF () THEN
...
ELSE
...
ENDIF
