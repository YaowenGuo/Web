# Online

 > 上线的 css 不生效

 ```bash
 php bin/magento setup:upgrade && php bin/magento setup:static-content:deploy en_US -f && php bin/magento indexer:reindex && php bin/magento cache:clean && php bin/magento cache:flush && php bin/magento cache:enable
 ```

对于本地的部署，有时候内存显示超出限制

 ```
php bin/magento setup:upgrade
php -dmemory_limit=3G bin/magento setup:di:compile
php -dmemory_limit=3G bin/magento setup:static-content:deploy en_US -f
php -dmemory_limit=3G bin/magento indexer:reindex
php bin/magento cache:clean && php bin/magento cache:flush
```