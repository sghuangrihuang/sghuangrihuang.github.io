---
title: Vue-cli基于proxyTable配置解决跨域方案
date: 2018-03-16 09:15:05
tags: vue
categories: skill
---

通过简单的 **proxyTable** 配置进而解决开发环境跨域的问题

<!-- more -->
<The rest of contents | 余下全文>

### 序言

开发阶段，通常都是在本地调试，本地起的服务域名通常是 localhost:端口号。这样会产生一些接口的跨域问题，除了常规的一些跨域方案，我们实际上可以借助 **node.js** 服务帮我们代理这些接口。


### 解决方案

我们借助 vue-cli 脚手架帮我们生成一些初始化代码。在 **config/index.js** 文件中，我们修改 **dev** 下 **proxyTable** 的配置

有关于API proxy的说明[详细看](https://vuejs-templates.github.io/webpack/proxy.html)

这个参数主要是一个地址映射表，你可以通过设置将复杂的url简化，例如我们要请求的地址是`http://xxx.com.cn/api/1`，可以按照如下设置：
```javascript
  ...
  proxyTable: {
    '/api': {
      target: 'http://xxx.com.cn', //你的目标域名
      changeOrigin: true, // 为true, 那么本地会虚拟一个服务端接收你的请求并代你发送该请求，这样就不会有跨域问题了，当然这只适用于开发环境
      pathRewrite: {
        '^/api': ''
      }
    }
  }
  ...
```
这样我们在写url的时候，只用写成/api/1就可以代表`http://xxx.com.cn/api/1`

vue-cli的这个设置来自于其使用的插件http-proxy-middleware
github：[https://github.com/chimurai/http-proxy-middleware](https://github.com/chimurai/http-proxy-middleware)

### 总结

实际上解决方案有很多种，主要会大家是否去看得懂 **vue-cli** 的 **webpack** 环境配置，通过对 **webpack** 的[api](https://doc.webpack-china.org/api/)配置 进而达到我们想要的效果
 