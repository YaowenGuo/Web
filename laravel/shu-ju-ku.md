laravel 中提供了DB facade(原始查找)，查询构造器 和 Eloquent ORM三种数据库操作方式。

#### 链接数据库

数据表创建好之后，首先要链接数据库。在database.php中发现，有如下的操作：
```php
'mysql' => [
            'driver' => 'mysql',
            'host' => env('DB_HOST', '127.0.0.1'),
            'port' => env('DB_PORT', '3306'),
            'database' => env('DB_DATABASE', 'forge'),
            'username' => env('DB_USERNAME', 'forge'),
            'password' => env('DB_PASSWORD', ''),
            'unix_socket' => env('DB_SOCKET', ''),
            'charset' => 'utf8mb4',
            'collation' => 'utf8mb4_unicode_ci',
            'prefix' => '',
            'strict' => true,
            'engine' => null,
        ],

```
这就是获取数据库相关配置的地方，而数据库的配置就在.env文件中，修改相应的变量即可。
```php
DB_CONNECTION=mysql
DB_HOST=192.168.8.152
DB_PORT=3307
DB_DATABASE=panda_site
DB_USERNAME=root
DB_PASSWORD=root

```
可以看到，两边是一一对应的。

#### 使用DB facade 执行sql指令。

可以在Controlor的方法中直接执行SQL语句
```php
public function test() {
    $testSql = DB::select('select * from student');
    return var_dump($testSql);
}
```
插入
$boolValue = DB::insert('insert into student(name, age) values (?, ?)', ['sao', 14]);

修改
DB::update('update student set age = ? where name = ?', [20, 'sao']); 返回修改的行数。



#### 查询构造器

- Laravel 中的查询构造器（Query Builder）提供方便流畅的接口，从来创建及执行数据库语法。

- 使用PDO 参数绑定，以保护应用程序免于SQL注入，因此传入的参数不需要额外转移特殊字符。
- 基本上可以满足所有的数据库操作，而且支持的数据库比较广泛。


##### 新增数据
DB::table(表名)->insert([列名 => 值， 列名=> 值, ...]); 返回bool类型，是否插入成功。
DB::table(表名)->innsertGetId([列名 => 值， 列名=> 值, ...]); 返回插入时的自增id值。

想要插入多条数据的话，只要传入多维数组即可。

##### 更新数据库
> 更新为指定数据

$num = DB::table(表名)
    ->where('id', 12)
    ->update([列名 => 值， 列名=> 值, ...]);
返回影响的行数。


> 自增/自减更新

$num = DB::table(表名)
    ->where('id', 4)
    ->increment('age', 3); 给age的age自增3。返回受影响的行数
自增的同时，还能够改变其它字段
$num = DB::table(表名)
    ->where('id', 4)
    ->increment('age', 3, ['name' => 'lili']);
    

##### 删除数据
> delete

自增的同时，还能够改变其它字段
$num = DB::table(表名)
    ->where('id', '>=', 4)
    ->delete();
    
    
> 清空数据表 ！危险

$num = DB::table(表名)->truncate(); // 不返回内容

##### 查询
所有的数据库，查询都是重点。
> 整行数据
DB::table(表名)->get(); 获取所有数据。


DB::table(表名)
    ->where('id', ">=", 1000)
    ->orderBy('id', 'desc') 
    ->first(); 获取首条数据。
    
想要增加多个查询限制条件，则将where改成whereRaw函数即可，
如：whereRaw("id >= ? and age = ?", [10000, 14]);

> 获取指定字段

DB::table(表名)
->pluck('name')。

或者使用lists
DB::table(表名)
->lists('name')。
特殊的是lists可以指定某个字段作为返回数据的键

DB::table(表名)
->lists('name', 'id')。 // 指定id作为返回值的键。

> 获取多个字段 select

DB::table(表名)
    ->select('name', 'id')
    ->get();
    
> 分批加载数据，防止数据量太大内存沾满

DB::table("表名")
    ->trunk(每次返回的数量, function($student) {
       dd($student);
       // 如果想要满足某种条件终止查询，可以return false。
    });

##### 聚合函数

count、max、min、avg、sum

DB::table("表名")->max(age);


## Eloquent ORM 简介、模型的建立以及查询数据库


#### 简介
- Laravel 自带的 Eloquent ORM是一个简洁、优美的ActiveRecord 实现，用来实现数据库操作。

- 每个数据表都有一个与之对应的模型(Model)，用来和数据表交互。

#### 模型的建立

在 app 目录下新建与数据库表对应的模型(Model)php文件
1. 命名空间为 app。
2. 新建模型类，继承自 Model。
3. 与数据库表关联，默认是和类名的复数表名进行关联的。例如类名叫Student,则表名默认会关联到students。 但是大多数情况下，表名和类名可能并不一样，需要单独指定： protected $table = 'student';

4. 默认以 id 作为主键，但是主键如果不叫 id ，也需要单独指定。例如 
    protected $primaryKey = 'id';
    
#### 访问数据库

只需要在控制器中调用 新定义 Model 对象从 Model 中继承来的静态方法即可。

##### all() 返回一个数据表的集合，元素为模型对象。
$students = Student::all();

##### find(id) 通过 主键查询， 返回的是一条数据模型对象。
$student = Studnet::find(1001);

##### findOrFail(key) 通过主键查找，如果没有找到，就会抛出异常，

##### get(); 返回对象集合。

##### first() 查询第一个条。

##### 查询条件

$students = Student::where('id', '>', '1001')
    ->orderBy('age')
    ->first();

之前所提到的函数，这里应该都能使用。

##### trunk(数量， function(数据对象){ 操作方法 }) ；
跟之前的操作方式一致。

##### 聚合函数

count、max、min、avg、sum
Studnet::count(); 可以直接使用，因为已经关联好了表。


#### ORM中的新增，自定义时间戳，以及批量赋值

##### 通过模型新增数据，需要自定义时间戳
新生成一个模型对象，然后给各个属性赋值，最后调用模型的save() 方法即可，但是，此时插入的数据会发现，插入时间和更新时间都是当年，而不够精确。这是因为ORM 会自动维护插入时间和更新时间这两个字段。如果不想要自动更新，可以在模型（model） 中设置关闭。
在对应的模型中添加：
public $timestamps = false;

更多时候，我们希望它能够自动维护时间戳，但是想要按照一定的格式，这时候可以指定时间戳格式。同样在模型中添加
protected function getDateFormat() {
    reutrn date();// 当前时间戳
}

获取时间戳，只需要访问对象的create_at属性即可
$studnet = Studnet::find(2017);
echo $studnet->created_at;
但是，此时获取的是一个已经格式化了的日期字符串。要想获取原始的时间戳，只需要在模型中添加一个方法。
protected function asDateTime($value) {
    return $value;
}

此时就可以自己对时间戳格式化
echo date('Y-m-d H:i:s', $student->created_at);

##### 使用模型的create方法新增数据（设计到批量赋值)

只需要调用继承来的静态create()方法，参数是一个字段名为key的map。返回的是一个对象。在创建对象的时候，会插入数据。但是现在执行会出错，因为laravel默认不允许批量插入数据，想要此方法执行成功，可以在模型中添加允许批量插入的字段。

protected $fillable = $['name', 'age', ...字段名称];

还可以指定不允许批量插入的字段

protected $guarded = [不允许批量插入的字段名];


查找，不存在则插入

$student = Student::firstOrCreate(['name'=>'小李']); // 返回查询或者插入的对象。

查找/创建，并不自动插入，需要的话，就自己调用save方法保存。

$student = Student::firstOrNew(['name'=>'小李']);


#### 修改数据

##### 通过模型更新数据

先查找，后保存
$student = Student::find(1024);
$student->name = 'KT';
$studnet->save(); // 保存到数据库


##### 结合查询语句批量更新

$num = Student::where('id', '>', '1000')
    ->update(['age'=>40]); //返回更新的行数
    
    
#### 删除数据

##### 通过模型删除

$student = Studnet::find(1000);
$bool = $student.delete();

##### 通过主键删除

$num = Studnet::destroy(1000); // 返回删除数量，还可以传入多个id。

##### 删除指定条件的数据

$num = Student::where('id', '>', 1000)->delete();

















