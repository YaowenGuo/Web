# 常用指令

## 生产环境和测试环境切换

```
# 切生产模式
bin/magento deploy:mode:set production

# 切开发模式
bin/magento deploy:mode:set developer
```


## 部署

> 本地

```
php bin/magento setup:upgrade
php -dmemory_limit=3G bin/magento setup:di:compile
php -dmemory_limit=3G bin/magento setup:static-content:deploy en_US -f
php -dmemory_limit=3G bin/magento indexer:reindex
php bin/magento cache:clean && php bin/magento cache:flush
```

> 对于线上，希望一下执行

```
php bin/magento setup:upgrade && php bin/magento setup:static-content:deploy en_US -f && php bin/magento indexer:reindex && php bin/magento cache:clean && php bin/magento cache:flush && php bin/magento cache:enable
```

> 特殊情况需要编译，注意编译时，网站会有暂时维护模式，不能正常访问

```
php bin/magento setup:upgrade && php bin/magento setup:di:compile && php bin/magento setup:static-content:deploy en_US -f && php bin/magento indexer:reindex && php bin/magento cache:clean && php bin/magento cache:flush && php bin/magento cache:enable
```



## 模块


查看现有的模块

```
php bin/magento module:status
```

注册新模块

```
php bin/magento module:enable chichihaha_Google_Analytics --clear-static-content
```

禁用模块， 有一些模块需要在禁用时将安装时的静态文件也清除，添加 `--clear-static-content` 参数


```注意， 启用一个模块候，要重新 compile。 否则会有的模块问题导致线上无法访问的情况```


```
php -dmemory_limit=3G bin/magento setup:di:compile
```


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


