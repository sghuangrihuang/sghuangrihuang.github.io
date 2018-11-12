---
title: webpack-dev-server参数说明
date: 2017-08-20 14:00:00
tags: webpack
categories: skill
---

本人总结 **webpack-dev-server** 配置参数中文说明 

<!-- more -->
<The rest of contents | 余下全文>

### 参数
``` javascript
  devServer: Object
```

*	**Object**
	*	`headers {Object}`：在所有响应中添加首部内容
	*	`quiet {Boolean}`: 控制台中不输出打包的信息，开发中一般设置为false，进行打印，这样查看错误比较方面
	*	`no-info {Boolean}`: 启用 noInfo 后，诸如「启动时和每次保存之后，那些显示的 webpack 包(bundle)信息」的消息将被隐藏。错误和警告仍然会显示
	*	`compress {Boolean}`:  是否开启gzip压缩。默认为false，不开启
	*	`host {ip}` : 指定使用一个 host ip。默认是 localhost
	*	`port {Number}` : 设置端口号，默认是:8080
	*	`inline  {Boolean}`: 在 dev-server 的两种不同模式之间切换。默认情况(true)下，应用程序启用内联模式(inline mode)。这意味着一段处理实时重载的脚本被插入到包(bundle)中，并且构建消息将会出现在浏览器控制台。也可以使用iframe (false) 模式，它在通知栏下面使用`<iframe>` 标签，包含了关于构建的消息
	*	`before {Function}`：提供在服务器内部所有其他中间件之前执行自定义中间件的能力。可用作接口调试
	*	`proxy {Object}`：假若单独的后端开发服务器 API，并且希望在同域名下发送 API 请求。[http](https://github.com/chimurai/http-proxy-middleware)可做HTTP代理
	*	`hot {Boolean}`: 是否开启热替换。默认为false，不开启
		*	插件必须要开启new webpack.HotModuleReplacementPlugin()
	*	`open {Boolean}`: 是否自动打开浏览器。默认为false，不开启
	*	`contentBase {Boolean|String|Array}`：告诉服务器从哪里提供内容。只有在你想要提供静态文件时才需要
	*	`overlay {Boolean | Object}`：当有编译器错误或警告时，在浏览器中显示全屏覆盖。值为true时，只显示报错
	*	`clientLogLevel {String}`：当使用内联模式(inline mode)时，在开发工具的控制台将显示消息的等级。默认值为 info，可选值none, error, warning 或者 info


### 参数使用

#### devServer.proxy
``` javascript
'/api': {
  target: 'http://xxx.com.cn', //你的目标域名
  changeOrigin: true, // 本地会虚拟一个服务端接收你的请求并代你发送该请求
  pathRewrite: {
  // 以路径为api作为标志转代理
    '^/api': ''
}
```

#### devServer.before
``` javascript
before(app) {
  app.get('/some/path', function(req, res) {
    res.json({ custom: 'response' });
  });
}
```

#### devServer.overlay
``` javascript
overlay: {
  warnings: true,
  errors: true
}
```
