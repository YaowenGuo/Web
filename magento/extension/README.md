# 插件开发

Magento 的插件开发放到 `app/code` 目录下

任务 Magento 都需要一下三个文件

- <模块目录>/composer.json: Magento 使用 composer 管理依赖，此文件定义了组件在运行时所需的依赖项。
- <模块目录>/registration.php: 此文件在安装时向 Magento 注册组件，它使用组件的根目录名称作为组件名称。
- <模块目录>/etc/module.xml：此文件定义有关组件的基本信息，Magento 使用这里的版本号来确定是否要执行更行。



## 创建一个 HelloWord 程序

### 创建基本文件

在 `app/code` 创建一个目录，作为模块跟目录。 例如 `chichihaha/google-analytics`。注意这里必须是两层目录，这是 Magento 强制要求的，第一层是供应商，也就是开发商，第二层是软件包。


创建 `app/code/chichihaha/google-analytics/etc/module.xml`，其基本结构是。按照约定，扩展包名最好是以开发商打头，这样方便辨认，而且在列出软件包时，也会将相同开头的排序到邻近位置。


```xml
<?xml version="1.0"?>
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:Module/etc/module.xsd">
    <module name="chichihaha_Google_Analytics" setup_version="0.0.1"/>
</config>
```

创建 `chichihaha/google-analytics/registration.php`，其进本结构为

```php
<?php
\Magento\Framework\Component\ComponentRegistrar::register(
    \Magento\Framework\Component\ComponentRegistrar::MODULE,
    'chichihaha_Google_Analytics',
    __DIR__
);
```

到这里，尽管我们没有任何代码，但是已经是一个模块了，我们可以将其注册给 Magento

### 注册模块

查看现有的模块

```
php bin/magento module:status
```

注册新模块

```
php bin/magento module:enable chichihaha_Google_Analytics --clear-static-content
```

禁用模块， 有一些模块需要在禁用时将安装时的静态文件也清除，添加 `--clear-static-content` 参数


```
php bin/magento module:disable Mageplaza_GoogleAnalytics --clear-static-content
```


### 卸载模块

虽然 Magento 的包很多都是直接拷贝到 `app/code` 目录下安装的，但是安装命令却有一些配置，卸载是也要先取消这些配置。

1. 卸载包

```bash
php bin/magento module:uninstall --clear-static-content <Vender>_<Package> # 根据 registration.php 注册名字定
```

2. 移除 complser

```
composer remove <Vender>/<Package> # 根据 composer.php 注册名字定
```

3. 内存超过限制的设置，在php 命令后添加参数 `-dmemory_limit=3G`， 如：

```
php -dmemory_limit=3G  bin/magento setup:di:compile
```

4. 删除包文件

### 注册/卸载后更新数据

```
bin/magento setup:upgrade
```





