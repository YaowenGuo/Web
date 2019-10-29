# 生产环境和测试环境切换

生产环境

```bash
# 查看当前模式
bin/magento deploy:mode:show

# 切生产模式
bin/magento deploy:mode:set production

# 切开发模式
bin/magento deploy:mode:set developer
```