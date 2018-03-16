---
title: webpack-dev-server参数说明
date: 2017-08-20 14:00:00
tags: webpack
categories: skill
---

本人总结 **webpack-dev-server** 配置参数中文说明 

<!-- more -->
<The rest of contents | 余下全文>

``` javascript

  devServer : {
    --quiet: //控制台中不输出打包的信息，开发中一般设置为false，进行 打印，这样查看错误比较方面
    --no-info: // 不显示任何信息
    --colors: //对信息进行颜色输出
    --no-colors: //对信息不进行颜色输出
    --compress:  //开启gzip压缩
    --host: //设置ip
    --port: //设置端口号，默认是:8080
    --inline: //webpack-dev-server会在你的webpack.config.js的入口配置文件中再添加一个入口,
    --hot: //开发热替换
    --open: //启动命令，自动打开浏览器
    --history-api-fallback: //查看历史url
  }
  
```