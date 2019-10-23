### Artisan 简介

Artisan 是 Laravel 自带的命令行工具，有强大的 Symfony/Console 组件驱动。提供了一些对应用开发用帮助的命令。

### Artisan 的使用

由于 Artisan 还是php编写的，所以要运行 Artisan 需要使用php执行
php artisan ,然而并不是在任何地方都能执行成功，这是因为 Artisan 是Laravle框架中的内容，而 Laravel 是安装在项目中的，所以需要再项目下执行。

> 查看现有的命令

php artisan 
或者
php artisan list 

会看到:
```
Available commands:
  clear-compiled                 Remove the compiled class file
  down                           Put the application into maintenance mode
  env                            Display the current framework environment
  help                           Displays help for a command
...
```
这些就是该项目中所有的 artisan 命名列表，其中 左侧的是命名，右侧的是解释。

要执行这些命令，只需要

php artisan 命令名 参数列表

> 例如查看帮助信息：

php artisan help 某个命令

> 创建控制器

php artisan make:controller StudnetControler

> 创建模型
php artisan make:Module Student

> 创建中间件
php artisan make:middleware Activity



 

