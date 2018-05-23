# select data

[TOC]

使用 select 查询数据必须至少给出两条信息——想要什么，以及从什么地方选择。

关键字不区分大小写，但是表名列名区分大小写。


## distinct 去重

只适合查询单列的时候去重，因为 distince 必须放在查询列的最前面，表示对所有列去重，而不能部分使用 distinct。

select distinct <name, gender> from <table_name>;

选择多列时，除非指定的两列都相同，否则所有行都会被检索出来。


## 限制结果

select <column_name_list> from <table> limit num;

想要指定开始的行

select <column_name_list> from <table> limit 5, 20;

第一个数字是开始的行数，需要说明的是，mysql的行是从0开始的。因此 `limit 1, 1` 将检索出第二行而不是第一行。

mysql5 给出了一中新的表示方法。

select <column_name_list> from <table> limit 5 offset 20;

意为从20行开始查出5行。

## 完全限定表名

<database_name>.<table_name>

## order by 排序

默认数据一般以它在底层表中出现的顺序显示。如果不明确排序，则不能假定检索出的数据顺序有意义。

order by 子句可以跟一列或多列的名字，对这些列进行排序。多个列时，优先按照前面的列排序，前面列的值形同，按照后面的列排序。

支持 ASC和DESC排序。


## where 子句

位于 order by 子句之前。

支持 = , !=, >, >=, <, <=, between A and B

多个条件用and 、 or 连接。 当多个并列时， AND优先级更高。

is null  和 not is null。


in (2, 25, 3);

## like 模糊查询

% 任意多个字符
_ 任意一个字符

比较慢，建议先通过其他条件过滤，然后剩余数据进行模糊查询。


## 正则表达式进行过滤

查询、替换、截取
mysql仅仅实现了正则表达式的一个子集。

子句
<column_name> regexp "<regular expresion>"

在 where 子句之后，order by 子句之前。其实就是like子句的位置。

mysql 的正则表达式自2.23.4之后，不区分大小写。为区分大小写，可以使用BINARY关键字。如 `where prod_name regexp binary "JdtPack .000"`


Mysql的转义字符有些特殊，要转义`.`，需要使用`\\.`，第一个表示转义字符。为了匹配`\`，需要使用`\\\`。多数正则表达式实现使用单个反斜杠转义字符就成使用这些字符本身。但MySQL要求使用两个。这是因为MySQL字节解释一个，正则表达式库解释一个。
