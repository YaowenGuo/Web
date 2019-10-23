通过商议小小节的内容，发现 Laravel 的数据迁移功能非常好用。那如何自定义迁移自己的数据表呢？


> 新建迁移文件

新建迁移文件主要有两种：

- 新建一个 students 表的迁移文件
  php artisan make:migration create_students_table
  
 --table 和 --create 参数可以用来指定数据库表名称，以及迁移迁移文件是否要创建新的数据库表。
 
- 生成模型的同时生成迁移文件
  php artisan make:model Stiudent -m
  
