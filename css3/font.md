# font

一直以来 Web 设计师都想要为网站添加一些优雅的字体，但是浏览器仅限于使用用户系统上的字体，这样一来，一大批网站受限于字体数量的不足。 令人欣慰的是 CSS3 带来了解决方案，让用户再也不用使用图片、FLASH、JS 这种繁琐的技术。

[TOC]

## @font-face 嵌入字体

@font-face 将自定义字体嵌入到网页中，浏览器在遇到 @font-face 指定的字体位置后加载字体到本地缓存，并对页面中指定了改字体的内容应用字体。
```
@font-face {
    font-family: <YourWebFontName>;
    src: <source> [<format>][, <source> [<format>]]*;
    [font-weight: <weight>;]
    [font-style: <style>;]
}
```

- YourWebFontName: 指定自定义字体的名称，最好是使用下载的默认字体文件名，它将作为 Web 元素中的 font-family 属性值使用。
- src: 指定自定义字体在网站的路径。可以写多个 src 指定多个来源，浏览器会按序查找，直到找到一个可用的字体。
- format: 自定义字体的格式，主要用来帮助浏览器识别，其值主要有: truetype、opentype、truetype-aat、embedded-opentype、avg 等。
- font-weight: 指出字体的粗细类型
- font-style: 字体是否为斜体等类型，类似的还有 font-variant、font-size、font-stretch。


每个 @font-face 定义一种字体，想要定义多种字体可以声明多个 @font-face。


## 字体转换工具

如果只有字体只有一种格式的文件，可能想要转换成其它样式的文件。在线工具

Fontssquirrel

Codeandmore


获得字体的网站
Google Web Fonts
Dafont.com
