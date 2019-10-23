#### 怎么新建一个控制器

在Http/Controllers目录下新建php文件。

控制器在项目的app/Http/Controllers目录下

* 控制器的命名空间要和遵循php5规范，和目录一致，所以命名空间是namespace App\Http\Controllers;
* 命名一个新的类，命名和文件名一直，并继承自控制器基类Controllers
* 在类中新建方法。

#### 控制器和路由怎么进行关联

* 在路由中新建相应的路由，Route::get\("http子路径", “控制器类名@类中方法名”\);  就关联了路由和控制器。或者使用Route::get\("http子路径", \['use“ =&gt; '控制器类名@类中方法名” , 'as' =&gt; '路由别名'\);  进行关联。



#### 关联控制器后，路由的特性怎么用

传参数

过滤


#### 1. Request
每次在浏览器输入网址刷新页面，都是一个请求，php服务器返回浏览器的都是一个响应。

- laravel中的请求使用的是symfony/http-foundation组件。要想在Controlerh中获取请求信息，只需要在Controller的方法中传入一个Request对象即可。Request一定要是Illuminate\Http\Request，因为laravel中的请求使用的是symfony/http-foundation组件
例如
```
class NameController extends Controller
{
    public function dispatchRequest(Request $request/*传入的请求对象。*/)
    {
    }
    ...
}
```
- 所有的请求数据均存放在Request对象中，请求中存放了$_GET, $_POST, $_COOKIE, $_FILES, $_SERVER等数据。

##### 获取请求中的值
1. 获取rul中的值，例如https://baidu.com?name=a。想要获取a
只需要调用Request的input方法，传入‘name’的键即可。

```
$value = $request->input('name');
// 还可以传入默认值，在不存在改键使，返回默认值。
$value = $request->input('name', '小李');

// 是否存在该值
$has = $request->has('name');

// 取所有参数
$all = $request->all();
```
##### 判断请求类型
获取请求类型

```
$type = $request->method();

// 判断是否是某种类型
$isType = $request->isMethod('GET');

// 判断是不是Ajax请求
$isAjax = $request->ajax();

// 判断请求路径是不是 域名/name/
$isPath = $request->is('name/*')

// 当前的url
$url = $request->url()
```

#### 2. Session

由于HTTP协议是无状态的，所以session提供一中保存用户数据的方法。Laravel 支持多种 session 后端驱动，并且提供清楚、统一的API。也内置支持如 Memcached、Redis、和数据库的后端驱动，默认使用 file 的 Session 驱动。Session的配置文件在 config/session.php 文件中。

Latavel使用 Session 有三种方式， 
- HTTP Request 类的 session() 方法。
- session() 辅助函数。
- Session Facade

如何使用 session
首先在Route中添加 web 键
```
Route::group(['middleware' => ['web']], function() {
    // 需要添加 Session 的路由
    Route::post('/ask/ask/report', 'QuestionController@questionReport');
    Route::post('/ask/ask/close', 'QuestionController@closeQuestion');
});
```

然后就能在 Controller 中使用了。
```
// 1. HTTP Request.sesson() 方法。
$request->session()->put('key1', 'value1');
// 获取，在另一个路由的控制方法中获取，**注意，这些控制方法的路由需要都是加了sesson的。（在Route中添加web键） **

$value = $request->session()->get('key1');

// 2. session 的辅助函数
session()->put('key2', 'value2');
// 获取
echo session()->get('key2');

// 3. 通过 Session 类
Session::put('key3', 'value3');
// 获取
echo Session::get('key3');

```
以上获取都可以添加默认值。
```
echo Session::get('key3', 'default');
```

以数据的形式存储
```
Session::put('key3', 'v1');
Session::put('key3', 'v2');

// 此时返回的将是一个数组
echo Session::get('key3');
```

删除数据

```
// 取得时候同时删除
echo Session::pull('key3');

// 直接删除
Session::forget('key3');

// 删除所有
Session::flush()
```

取出所有的值
```
dd(Session::all());
```

是否存在
```
dd(Session::has('key1'));
```

暂存，第一访问存在，再次访问不存在
```
Session::flash('key4', 'value4');

```

#### 3. 响应（Response）

常见的响应类型:字符串、视图、Json、重定向

返回Json
```
$data = [
    'errorCode' => 0,
    'errorMsg' => 'success'
]
return response->json($data);
```

重定向
```
return redirect('url');
//还可以携带参数
return redirect('url')->with('key','value',);
// 其实是存在了session中，并且使用的一一次性的flash。因此可以在session中获取到。

// 在控制器中还可以使用action()跳转
return redirect()->action('控制器名@方法名')->with('key','value',);
;

// route 路由别名进行跳转
return redirect()->route('别名')->with('key','value',);
;


```
