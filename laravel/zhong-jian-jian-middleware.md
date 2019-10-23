#### 4. 中间件(Middleware)

什么事中间件？ Laravel 中间件提供一个方便的机制来过滤进入应用程序的 HTTP 请求。

> 场景: 有一个活动，在指定日期后开始，如果活动没有开始，只能访问宣传页面。

```
public function acitivtyBefore()
{
    return "活动快要开始了，敬请期待"；
}

public function activirtyIn()
{
    return "活动进行中，谢谢参与"；
}
```

#### 添加路由后，新建中间件。


中间件位于 Http/Middleware 目录下。新建 php 文件，添加命名空间。
新建类和方法。例如

```
<?php

namespace App\Http\Middleware;

class Activity
{
    // 参数固定
    public function handle($request, \Csolure $next)
    {
        if (time() < strtotime('2016-06-06'))
        {
            return redirect()->route('acitivtyBefore');
        }
        return $next($request); // 继续请求
    }
}
```

> 继续访问的重定向的不同方法

1，通过控制器中的方法定向，如

return redirect("acitivtyBefore")

2. 通过url 重定向

使用route()，action(),url()方法。

#### 在 Http/Kernel.php 中注册中间件。

```
protected $middleware = []; // 全局的
protected $middlewareGroups = []; // toure gourp 的
protected $routeMiddleware = []; // route 的
```
所以一般只要在最后一个的数组中添加即可，例如
```
protected $routeMiddleware = [
    'activity' => \App\Http\Middleware\Activity::class, // 中间件定义个名称和类名
]; // route 的

```

> 使用中间件

在路由中添加
```
Route::group(['middleware' => ['中间件名，如以上的是activity']], function() {之前要做访问控制的路由添加到此处})；

```