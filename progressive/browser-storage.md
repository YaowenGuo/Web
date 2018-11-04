# Browser Storage

[TOC]


## Storage Type

> Local Storage

- Easy to use key/value
- Available almost everywhere

bad
- Can only store strings
- Synchronous cause significant performance problems
- It's not transactional. So if you try and do two write at the same time you'll end up overwriting something important.


结论： 只适合存储简单数据类型。

> Cache

- Easy to use
- Fast
- Asynchronous

There are two type caches.
1. Application Cache

Application Cache 被标准弃用，浏览器不兼容， 不成熟, 被serviceWorkers 替代

2. Cache Storage 用来替代Application cache的解决方案；
- Cache Storage: Like local storage, it's not transactional.
  isn't available everywhere yet.

> indexDB

- FAST
- Complex data
- Asynchronous
- Transactional
- Available everywhere

bad

- ugly API: with lots of setup required and call backs to handle.

So there are few good libraries.

Mozilla: localForage.
Lovefield


**One thing to keep in mind, browser make no promises that they'll keep data around forever. Data can be removed without warning. It's important to sync critical data to the cloud as soon as possible.**

> Web SQL

仅 webkit 系浏览器支持，Chrome，Safari。Edge 和 Firefox 不支持。

### 可用的类型

综上可见，现在可用的存储方式是
简单数据类型：Local Storage
复杂数据类型：indexDB



### 以下两种不适合用于渐进式网页应用

> sessionStorage

SessionStorage

data that gets cleared after the browser window is closed.

和localStorage 一样，唯一的区别就是只存在于页面关闭之前，应用的不是很多

> cookie

大小不同。Cookie的大小是受限的，并且每次你请求一个新的页面的时候Cookie都会被发送过去，这样无形中浪费了带宽，另外cookie还需要指定作用域，不可以跨域调用。

cookie分两种，会话cookie 和 持久性cookie; 若不设置过期时间，则表示这个cookie的生命期为浏览器会话期间，关闭浏览器窗口，cookie就消失








## Local Storage

localStorage是什么：在HTML5中，新加入了一个localStorage特性，这个特性主要是用来作为本地存储来使用的，解决了cookie存储空间不足的问题(cookie中每条cookie的存储空间为4k)，localStorage中一般浏览器支持的是5M大小，这个在不同的浏览器中localStorage会有所不同。
2）localStorage会可以将第一次请求的数据直接存储到本地，这个相当于一个5M大小的针对于前端页面的数据库，相比于cookie可以节约带宽，但是这个却是只有在高版本的浏览器中才支持的；
3）localStorage 方法存储的数据没有时间限制。第二天、第二周或下一年之后，数据依然可用。

local Storage 只能存储 key->value 的字符创形式，所以接口非常简单。想要存储复杂的数据，可以将 json 对象转化为字符串进行存储。
### 测试

You can test out what’s in local storage by going to the JavaScript console and typing it in. Actually do this, don’t just read it.
```
> localStorage
Storage {length: 0}
```

### 存储

```
localStorage.setItem('key', 'value');
localStorage.key = "value";
```

### 获取

```
localStorage.getItem('key');
localStorage.key;
```

### 删除

```
localStorage.removeItem('key');
```

### 清空

```
localStorage.clear();
```

## indexDB


<!-- ## sessionStorage
## cookie
## Service Worker -->
