# Category

## 添加主页面导航栏数量

管理后台 -> CATAOG -> Categories -> 点击要添加子 category 的目录 -> Add Subcategory


配置 category 页面的内容


## [remove left sidebar](https://magento.stackexchange.com/questions/106053/how-to-remove-block-from-left-or-right-panel-in-magento-2)

移除单个 catetory 页面左侧菜单栏。可以在后台配置实现。方法是添加 xml 布局。


管理后台 -> CATAOG -> Categories -> 选中子 Category -> Design

在 Layout Update XML 添加布局移除代码

```xml
<page xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:View/Layout/etc/page_configuration.xsd">

    <body>
        这里添加移除代码
    </body>
</page>
```

Its almost the very same way

```xml
<referenceBlock name="block.name.wantoberemoved" remove="true"/>
```

Remove compare products from sidebar

```xml
<referenceBlock name="catalog.compare.sidebar" remove="true" />
```

Remove Wishlist from sidebar

```xml
<referenceBlock name="wishlist_sidebar" remove="true" />
```



