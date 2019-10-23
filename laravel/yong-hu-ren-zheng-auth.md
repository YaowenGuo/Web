Laravel 自带了一些组件，用于帮助用户快速构建常用功能，例如用户认证

> 生成 Auth 所需的文件，只需要执行
php artisan make:auth

你会发现，该命名不仅在 Web.php 中生成里一个路由，还在wiew下生成里一个auth目录，存放生成的登录、注册，密码找回的视图。
layouts 目录下放了一个 app.blade.php 的基本视图，其中一些路径不对，需要修改
其中的css和js路径不对，改成动态生成的
```
...
<link href="{{ asset('css/app.css') }}" rel='stylesheet'>
<script src="{{ asset('js/app.js') }}"></script>


> 路由
Web.app 中多了一个Auth::routes()路由。它存在于 vender/laravel/src/Routing/Router.php 中 auth() 方法实现。

> 数据库和表

生成 auth 功能之后，立即使用并不会成功，这是因为还没有链接数据库和构建数据库使用的表。

修改数据库配置，连接数据库，然后将 Laravel 自带的用户表迁移到我们的数据库中，
> 迁移数据

数据表位于 database/migrations 目录下。两张表为
2014_10_12_000000_create_users_table.php // 创建user表
2014_10_12_100000_create_password_resets_table.php // 创建用户密码重置表。

> 执行数据迁移，只需要在项目目录下执行

php artisan migrate

这时，数据表已经创建成功了。

 
