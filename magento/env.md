# 环境配置

[配置 env.php 的文档](https://devdocs.magento.com/guides/v2.3/config-guide/cli/config-cli-subcommands-config-mgmt-set.html)


对于开发或测试，有时候我们会在一台电脑上配置多个网站或者开发环境使用的端口号跟别人不一样却要使用一个数据库。由于 Magento 的资源加载地址是在数据库中配置的 `core_config_data` 表的 `web/secure/base_url` 和 `web/unsecure/base_url` 字段。

这时，我们希望使用 env 的配置覆盖数据库则地址。  `bin/magento config:set` 是magento 的设置指令。 带有 `-le | --lock-env` 餐数会将配置写入 `env.php`， 否则会写入数据库。

配置资源文件（css,js,image...）加载地址。

```
bin/magento config:set --lock-env --scope=websites --scope-code=base web/unsecure/base_url http://127.0.0.1:8081/


# 然后刷新缓存
php bin/magento cache:flush
```

***需要注意的是，数据库中配置的 url 配置的是 `localhost` 时， 会出现表单提交失败的诡异情况。而改成 `127.0.0.1` 后， env.php 如果配置的 url 如果是 `localhost` 跟数据库不一致，会出现管理后台的进入 `302` 重定向的死循环。 所以对于本地环境，建议两处都配置 `127.0.0.1`***







