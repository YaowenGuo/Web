# js 包管理工具

## 初始化

npm init

npm 会在执行命令的目录生成 `package.json` 文件，里面以 json 的格式配置的包依赖。用于安装是配置响应版本。


## 安装包
一般情况下，我们都是在项目下执行安装，这是因为不同项目的依赖可能不同，一般会将依赖安装在项目中，防止全局安装的冲突。npm 安装默认也是项目作用域的。如下命名会从 package.json 中读取依赖配置，然后安装。
```
npm install
```
想要指定安装的包，可以执行
```
npm install <包名>
如
npm install node

还可以指定版本
npm install <包名@版本号>

如
npm install node@2.1.0

```

### 全局安装

安装增加 -g 参数。一些目录没有访问权限的话，还需要 sudo 权限。

```
sudo npm install node@2.1.0 -g
```

## 查看安装的包版本

```
npm list <包名>  [-g]
```

## 卸载

```
npm uninstall <包名> [-g]
```

## 查看该目录环境的包环境是否有错误

```
npm ls

npm ls -g --depth=0
```

## 解决依赖安装的问题

在指定安装某个包时， npm 并不会自动安装它的依赖，因此会出现一些依赖不存在而安装失败的问题，这时可以用如下指定查看都有哪些依赖，以及安装依赖
```
npm info "eslint-config-airbnb@latest" peerDependencies -g

npx install-peerdeps --dev eslint-config-airbnb
```

https://www.npmjs.com/package/eslint-config-airbnb
