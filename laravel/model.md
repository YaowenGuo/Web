
#### 新建模型
1. 在app目录下新建php文件，首先要做的就是添加命名空间 namespace App;其实User.php就是一个默认创建的Model。
2. 在php文件新建一个类，统一继承自Model。也可以定义基础Model，然后继承。

#### 使用模型
1. 在控制器中调用Model中的方法。
这时候 Model<-->Controler<-->View 就构成了MVC的结构。
