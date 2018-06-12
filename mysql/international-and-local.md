# 全球化和本地化

## 字符集和校对顺序

不同的字符集需要以不同的方式存储和检索，MySQL 支持不同的字符集。

- 字符集为字母和符号的集合
- 编码为某个字符集成员的内部表示
- 校对为对顶字符如何比较的指令。校对设计到排序、检索、匹配。例如 搜索 `apple`是，`Apple` ..是否被搜索出来。大小写排序等等。

## 使用字符集和校对

> MySQL 支持众多的字符集，查看支持的字符集

SHOW CHARACTER SET;

显示所有支持的字符集，以及每个字符集的描述和默认校对。

> 查看所支持校对的完整列表

SHOW COLLATION;

可以看到有的字符集不止一种校对，例如，latin1对不同的欧洲语言有几种校对，而且许多校对出现两次，一次徐芬大小写（`_cs` 结尾），一次不区分大小写（`_ci` 结尾）。

指定字符校对的位置

- 安装 DBMS 时，指定该 DBMS 创建的 数据库的默认字符集合校对方式
- 创建数据库时，可以指定该数据库的字符集和校对方式
- 创建表时，可以指定表的或者分别是定列的

> 为了确定所用的字符集和校对

SHOW VARIABLES LIKE `character%`;
SHOW VARIBALES LIKE `collaction%`;

CREATE TABLE table_name
(
    ...
    name VARCHAR(30) DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci
) DEFAULT CHARACTER SET hebrew
  COLLATE hebrew_general_ci;

> 搜索时指定校对规则

SELECT * FROM table_name
ORDER BY lastname, firstname COLLATE utf8_general_ci;

- COLLATE 还可以用于 ORDER BY、HAVING、聚类函数、别名等。

> 字符即产幻

cast() 和 convert()
