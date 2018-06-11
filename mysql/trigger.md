# trigger

触发器是 MySQL5 新增的

当一个事件发生时，自动的执行一个操作。触发器是 MySQL 响应一下任意语句而自动执行的一条 MySQL 语句（或位于 BEGIN 和 END 之间的一组有）：

- DELETE
- INSERT
- UPDATE

其他 MySQL 语句不支持触发器。

## 创建

在创建触发器时，需要该出4方面的信息：

- 唯一的触发器名，必须在每个表中唯一，但不是在整个数据库中唯一。这在其他数据库是不允许的，MySQL 是否会在将来改为全库唯一不确定，所有最好是全库唯一的。
- 触发器关联的表
- 触发器应该响应的活动（DELETE、INSERT、UPDATE）
- 触发器何时执行（处理之前或处理之后）


CREATE TRIGGER newproduct AFTER INSERT ON products
FOR EACH ROW
SELECT 'Product added';

对 products 表每插入一行（FOR EACH ROW），之后都输出一条 'Product added' 的消息。

只有表才支持触发器，视图和临时表都不支持。

触发器按每个表每个事假每次地定义，每个表每个事件每次只允许一个触发器。因此每个表最多支持6个触发器（事件前和事件之后）。

如果 BEFORE 触发器失败，则 MySQL 将不执行请求操作，此外，如果 DEFORE 触发器或者语句本身出错， AFTER 触发器将不执行。

## 删除触发器

DROP TRIGGER trigger_name;

触发器不能更新或覆盖，为了修改一个触发器，必须先删除它，然后在重新创建。
