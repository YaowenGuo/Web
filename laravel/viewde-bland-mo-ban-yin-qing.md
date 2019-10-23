## Blade 模板引擎简介及模板继承的使用
- Blade 是 Laravel 提供的一个简单但是功能强大的引擎。
- 和其他流行的php模板引擎不一样，blade并不限制你在模板中使用原生php代码。
- 所有Blade视图页面都将被编译成原生的php代码并缓存起来，除非模板文件改变了，否则不会重新编译。

在view下新建根 view 布局文件后缀是.blade.php。

在该模板中编写html代码，使用
```
@section(“片段名称”)
临时内容
@show
```
在模板中预留一个位置，为讲台被其他页面修改的位置。

要实现模板时，只需要在子页面中写继承自哪个模板
```
@entends（‘layout.main') # 继承自 view/layout/main.blade.php

# 饭后重写
@section('模板中的section名')
# 要代替的内容
# 如果要连模板中的内容一起输出，添加
    @parent
    
@endsection

```

预留位置除了@section之外，还可以使用@yield('名字') 。@yield只能定义一个位置，不能自己附带内容。

```
@yield('名字')
```
重写@yield('名字')跟重写@section一样，都使用@section ... @endsection

标签。

## 基础语法和include的使用

### 模板中输出变量

只需要{{php变量名}}即可
<p>{{$name}}</p>

### 模板中调用php代码
也是在双花括号中写即可

{{time()}}
{{in_array($name, $array)}}
{{var_dump($array)}}
{{isset($name) ? $name : '默认值'}}
{{$name or "默认值"}}

### 原样输出

想要输数花括号，在花括号前加@
@{{$name or "默认值"}}


### 模板中的注释

{{-- 注释 --}} 模板注释在网页中是看不到的。
### 引入自视图include的使用
有些模块并不是在每个页面都需要，但是一部分页面却需要。可以使用include将其引入进来。
@include("路径.文件名") 文件名不用带后缀

在include的时候，还可以传递参数
@include("路径.文件名", ['message'=>'value', ...])

## 流程控制
有些页面需要根据页面的不同，生成不同的内容，就需要if判断
### if
@if ($name == 'sean') 
    <p> 等等</p>
@elseif($name == 'a')
    <h1>a</h1>
@else
    ss
@endif

### unless
和if一样用户条件判断，但是if的取反
@unlsess ($name != 'a')
    a
@endless

### for

@for ($i = 0; i < 10; i++)
   {{$i}}
@endfor

### foreach

@foreach ($array as $value)
    <p>{{$value}}</p>
@endforeach

@forelse ($array as $value)
    <p>{{$value}}</p>
@empty
    数据不存在时的显示
@endforelse

## 模板中的URL
例如，控制器中的方法
public function urlTest（） {
return “testUrl”;
}

添加路由
Route::get('testUrl', ['as' => 'url', 'uesrs' => 'RouteTestUrl@testUrl'])

### @url()
通过路由的名称生成url
<a href=“{{ url('testUrl') }}”>url()</a>
### @action()
通过控制器及指定方法名生成url
<a href=“{{ action('StudnetControler@urlTest') }}”>action()</a>
### @route()
通过路由的别名生成url
<a href=“{{ route('url') }}”>route()</a>
