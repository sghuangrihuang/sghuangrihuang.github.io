---
title: webpackConfig参数说明
date: 2017-08-15 12:00:00
tags: webpack
categories: skill
---

本人总结 **webpackConfig** 配置参数中文说明 

<!-- more -->
<The rest of contents | 余下全文>

``` javascript

// webpack.config.js
const path = require('path')
const webpack = require('webpack')
const HtmlWebpackPlugin = require('html-webpack-plugin')
const CleanWebpackPlugin = require('clean-webpack-plugin')

const nodeEnv = process.env.NODE_ENV || 'developer';
const isPro = nodeEnv === 'production';

module.exports = {
  // 入口文件
  entry: './src/index.js',
  //  webpack 开始打包

  // 出口文件
  output: {
    //  webpack 如何输出结果的相关选项

    filename: '[name].[hash].bundle.js',
    //  针对单入口 name 对应main  而多入口则对应entry对象键名
    // 「入口分块(entry chunk)」的文件名模板（出口分块？）
    path: path.resolve(__dirname, 'dist')
    // 所有输出文件的目标路径
    // 必须是绝对路径（使用 Node.js 的 path 模块）
  },
  devServer: {
    // compress是否启用gzip 压缩
    compress: true,
    // port指定要监听请求的端口号
    port: 8080,
    // 告诉服务器从哪里提供内容 不添加话 devServer默认根目录是在webpack.config同一级的目录下
    // index.html（必须保存index.html文件存在 不然报错）
    // contentBase: './dist',
    // hot是否开启热更新
    hot: true,
    // inline开启应用程序启用内联模式(inline mode)。
    // 这意味着一段处理实时重载的脚本被插入到你的包(bundle)中，并且构建消息将会出现在浏览器控制台。
    inline: true,
    //当出现编译错误或警告时，在浏览器中显示一个全屏覆盖。默认情况下禁用。一旦设置就是启用
    overlay: {
      //同时显示警告和错误
      errors: true,
      warnings: true
    }
  },
  module: {
    // 关于模块配置
    rules: [
      // 模块规则（配置 loader、解析器等选项）
      {
        // 解析后缀为.css的文件
        test: /\.css$/,
        use: [
          'style-loader',
          'css-loader'
        ]
      },
      {
        test: /\.js$/,
        // 可以不用定义这个字段的属性值，eslint会自动忽略node_modules和bower_components
        exclude: /(node_modules|bower_components)/, //排除去这些文件夹进行eslint检查
        include: /src/,// 针对性对./src/文件夹下所有的js文件进行eslint检查
        enforce: 'pre', // 在babel-loader对源码进行编译前进行lint的检查
        use: [{
          loader: 'eslint-loader',
          options: {rules: {semi: 0}}
        }]
      }
    ]
  },
  plugins: [
      
    // CleanWebpackPlugin(paths [, {options}])
    // paths 一个数组，数组的每一个元素为要删除的路径
    // options {
    //一个根的绝对路径 对应webpackconfig绝对路径 __dirname
    //  "root": __dirname,
    // 是否开启在控制台输出信息
    //  "verbose": true,
    // 默认为false，删除所有的文件， 为true时，模拟删除，并不删除文件
    //  "dry": false,
    // 默认false， 为true时删除所有的编译文件
    //  "watch": false
    // }
    new CleanWebpackPlugin(['dist']),
    new webpack.DefinePlugin({
        // set NODE_ENV=production && webpack
      __DEV__: JSON.stringify(isPro)
    }),
    // 热更新webpack扩展插件 devServer.hot设置为true 就添加
    new webpack.HotModuleReplacementPlugin(),
    // HtmlWebpackPlugin 创建html文件
    new HtmlWebpackPlugin({
      title: 'webpack demo',
      hash: true
    })
  ]
}
```