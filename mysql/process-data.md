# process data

查询时对数据进行处理，使其满足需要的数据格式或数量需求。

字段（field），术语通常用于计算字段的连接上
列（column），通常用于列数据处理上。
有时可以互用，都表示数据表的一列。

## concate 拼接字段
concatenate field
concate 接受任意多个字符串或者字段参数，将它们按照先后顺序连接成一个字符串返回。

MySQL 将查询出来的一列数据拼装成一个字符串
使用GROUP_CONCAT函数。  
SELECT GROUP_CONCAT(查询的字段 separator ',') FROM table  

## 删除两端内容

trim(),ltrim(),rtrim()

## 算数运算

mysql支持在列查询中进行 `+，-，*，/`运算。

upper() 字符串大写
lower() 字符串大写
left() 左侧字母
right() 右侧字母
length() 字符串长度
str_length() 字符个数
locate() 字符子串的起始位置
substring() 切割字符串
soundex() 返回 soundex 值。将文本转为为其字母数字表示的发音的字符串。


> 时间

NOW() 	返回当前的日期和时间
CURDATE() 	返回当前的日期
CURTIME() 	返回当前的时间
DATE() 	提取日期或日期/时间表达式的日期部分
EXTRACT() 	返回日期/时间按的单独部分
DATE_ADD() 	给日期添加指定的时间间隔
DATE_SUB() 	从日期减去指定的时间间隔
DATEDIFF() 	返回两个日期之间的天数
DATE_FORMAT() 	用不同的格式显示日期/时间
adddate()  增加一天
addtime() 增加一个时间
dayOfWeek() 返回星期几
minus()
second()
hour()
day()
month()
year()
now()

***= 符号可以比较日期，这是因为查出的结果也是按照字符串获取的。
也能使用 between - and - 进行区间比较***

> 数值

abs() 绝对值
cos() 返回一个角度的余弦值
sin() 正弦值
tan() 正切值
exp() 一个数的指数
sqrt() 平方根
mod() 余数
pi() π
rand() 随机数

> 汇总数据

avg() 平均数 忽略为null的值
count() 数量， * 不忽略 null 和 空字符串。 指定字段将忽略 null 值的行。
max() 最大数 包括文本
min() 最小数 包括文本
sum() 和

5.0 之后版本，可以对数据汇总函数的列参数指定修饰，all 或 distinct. 如 avg(distinct price)。

## 分组数据
group by 子句指示 mysql 分组数据，然后对每个组，而不是整体进行聚集。

- group by 可以包含任意数目的列，这使得能对分组进行嵌套，为数据分组提供更细致的控制。
- 如果 group by 嵌套了分组，数据将在最会嵌套的分组上进行汇总。换句话说，在建立分组时，所有的列都一起参与计算（而不能从个别的列取回数据）。
- 如果分组中的列具有 null 值，则 null 将作为一个分组返回，
- group by 子句必须出现在 where 子句之后，order by 子句之前。

**rollup**

 使用 with rollup 将不止对最终的列进行分组，还会增加中间和总的分组。例如：
group by a, b with rollup; 结果中将增加 a(a中的每一个值都会有一行), null 的分组，表示对 a 进行 group by 的结果；null， b(b 中的每一个值都会有一行) 表示对 b group by 的结果； null， null 表示整个查询的总量。


## having 过滤分组

不能使用 where 子句，因为 where 过滤的是行而不是分组。而所有类型的 where 子句都可以用 having 代替。另一种理解是，where 在数据分组前进行过滤，having 在分组后进行过滤，where 过滤的值不包含在分组中，这会改变统计的结果。因此一个sql查询中既可以包含 where 对某些行过滤， 还可以包含 having 子句对过滤后的结果进行分组统计。

> 子句顺序

select
from
where
group by
having
order by
limit
