# Full text search

并非所有的数据库引擎都支持全文本搜索。InnoDB 就不支持，Mysql的 MyISAM 引擎支持。

和之前的通配符和正则表达式的匹配相比

- 性能： 通配符和正则表达式匹配通常要求 MySQL 尝试匹配表中所有行（而且这些搜索极少使用表索引）。因此，由于被搜索行数不断增加，这些搜索可能非常耗时。
- 明确控制： 使用通配符和正则表达式匹配，很难（而且并不总是能）明确地控制匹配什么和不匹配什么。例如，指定一个词必须匹配，一个词必须不匹配，而一个词仅在第一个词确实匹的情况下才可以匹配或者才可以不匹配。
- 智能化的结果： 虽然基于通配符和正则表达式的搜索听提供了非常灵活的搜索，但他们都不能提供一种智能化的选择结果的方法。例如，一个特殊词的搜索将会返回包含该词的所有行，而不区分包含单个匹配的行和包含多个匹配的行（按照可能是更好的匹配来排列它们）。类似，一个特殊词的搜索将不会找到包含该词但包含其他相关词的行。

使用全文本搜索，MySQL 不需要分别查看每个行，不需要分别分析和处理每个词。MySQL 常见指定列中各个词的一个索引，搜索可以针对这些词进行。这样，MySQL 可以快速有效地决定哪些词匹配，哪些词不匹配，它们的匹配频率等。

> 先决条件

为了进行全文本搜索，必须索引被搜索的列，而且要随着数据的改变不断地重新索引。在对表进行适当的设计后，MySQL 会自动进行所有的索引和重新索引。

> 启用

一般在创建表时启用全文本索引，CREATE TABLE 接受 FULLTEXT 子句，它给出被索引列的一个逗号分隔的表。

create table table_name
(
    行。。。
    FULLTEXT(列名, ...)
) engine=MyISAM;

FULLTEXT 指示对列进行索引，之后 MySQL 自动维护改索引，在增加、更新或删除行时，自动更新改索引。

 不要再导入数据时使用 FULLTEXT, 跟新索引要花时间，虽然不是很多。如果正在导入一个表，不应该启用 FULLTEXT， 应该先导入数据，然后修改表，建立 FULLTEXT 索引。

 > match() 和 aginst() 进行全文本搜索

 match 指定搜索的列， aginst 指定搜索用的表达式。

select note_text
from table_name
where match(note_text) aginst('rabbit');

搜索 note_text 包含 rabbit 的行。

- 传递给 match 的值必须与 FULLTEXT 中定义的相同，如果指定了多个列，则必须列出它们，并且次序相同。
- 对匹配程度高的排序在前。相同匹配程度的，按照字母序。

select note_text, match(note_text) aginst('rabbit') as rank
from table_name;

查询全文本搜索计算出的等级值。
