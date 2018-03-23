---
title: webpack4.X 开发环境配置注意事项 
date: 2018-03-23 16:04:53
tags: webpack
categories: skill
---

webpack4.X 开发环境配置

<!-- more -->
<The rest of contents | 余下全文>

### 序言

由于webpack一转眼就更新到4.x版本，很快市面上的所有的框架都可能要替换4.X的版本了 既然如此，我们就应该快速的先体验下4.X版本的神奇之处

### 安装webpack
还是熟悉的操作，先使用npm进行全局安装webpack
``` cmd
$ npm install webpack -g
```

### 项目的搭建
使用命令行创建文件夹 **webpack-demo** ，其次添加 `package.json`的文件，保存项目的基本信息

``` cmd
$ mkdir webpack-demo && cd webpack-demo
$ npm init -y
```

### 直接编写webpack

``` javascript
// webpack.config.js
const path = require('path');

module.exports = {
  entry: './src/index.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: '[name].bundle.js'
  }
}
```

``` javascript
// ./src/index.js
function sayHello() {
  return 'Hello, Webpack4.X'
}

document.write(sayHello());
```


### 项目打包报错
一般而言，直接执行相对应的webpack命令，进行打包的话 那就完全没问题的
``` javascript
$ webpack
```

可是居然报错了，错误代码如下
``` javascript
The CLI moved into a separate package: webpack-cli.
Please install 'webpack-cli' in addition to webpack itself to use the CLI.
-> When using npm: npm install webpack-cli -D
-> When using yarn: yarn add webpack-cli -D
```

意思就是说，cli已经转移到另外一个单独的包：`webpack-cli`。
除了安装wepback之外，请再安装 `webpack-cli`。

对此我们就直接在本地进行安装  webpack-cli
```
$ npm install webpack-cli -D
```

### 全局安装 webpack-cli 

再次执行打包 `webpack`，又同样报错

``` javascript
The CLI moved into a separate package: webpack-cli.
Please install 'webpack-cli' in addition to webpack itself to use the CLI.
-> When using npm: npm install webpack-cli -D
-> When using yarn: yarn add webpack-cli -D
```

很明显，那就是我们webpack-cli的安装不起任何作用。
回归到一开始，我们使用全局安装webpack主要是为了直接在任何地方都可以直接`webpack`这个命令行，既然官网把这个操作进行的移除到cli中，既然如此同样进行全局安装 `webpack-cli`

```
$ npm install webpack-cli -g
```

### 设置mode参数

在刚才的操作，已经可以打包完毕了，但是呢这里还报了个警告
``` javascript
WARNING in configuration
The 'mode' option has not been set. Set 'mode' option to 'development' or 'production' to enable defaults for this environment.
```

意思就是说，`mode`选项没有被设置，请为这个环境设置`mode`选项为 **development** 或者 **production** 
既然如此 那就我们就直接设置

```
$ webpack --mode development
```

### 总结


1.  全局安装webpack
2.  全局安装webpack-cli
3.  webpack命令必须要设置mode选项为 development 或者 production
4.  webpack建议采用src目录存储入口文件