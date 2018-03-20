---
title: node,http请求headers注意事项
date: 2018-03-20 23:23:31
tags: node
categories: skill
---

node, http 请求 headers 注意事项

<!-- more -->
<The rest of contents | 余下全文>

### 序言

今日，使用 **node.js** 作为项目后台的时候编写一个 **修改用户头像** 接口，想实现一个简单的node接口，以vue框架为项目的前后台分离设想。但是出现请求 **http** 报错，如下。

``` javascript
// Error: Can't set headers after they are sent.
router.post('/editUsersAvatar', function(req, res, next) {
  let form = new formidable.IncomingForm()
  form.parse(req, function(err, fields, files) {
    if (err) {
      res.send(JSON.stringify({
        "state": 500,
        "message": "服务器错误"
      }))
    }
    let response = {
      "state": 200,
      "message": "服务器请求成功",
      "data": files
    }
    res.send(JSON.stringify(response));
  });
});
```


### 问题所在

针对报错显示：不能发送headers因为已经发送过一次了

实际上：在处理HTTP请求时，服务器会先输出响应头，然后再输出主体内容，而一旦输出过一次响应头（比如执行过 `res.writeHead()` 或 `res.write()` 或 `res.end()`），你再尝试通过 `res.setHeader()` 或 `res.writeHead()` 来设置响应头时（有些方法比如 `res.redirect()` 会调用 `res.writeHead()`），就会报这个错误

同理 我所写的接口之中 采用了 **formidable** 模块的的form.parse函数 进行二次请求，对此发送headers头

### 解决方案

针对这种情况 最简单的方式就是直接 **return** 这个结果

``` javascript
router.post('/editUsersAvatar', function(req, res, next) {
  ...
  return res.send(JSON.stringify(response));
  ...
});
```

项目源码[传送门](https://github.com/sghuangrihuang/practiceProject/blob/ee8dedaebe311e3e335ee8d906eb732254e4f3a0/node/20171121/ApiServer/routes/users.js)

### 总结

针对前端而言，http协议，最好去懂下，不然遇到很多问题，只能靠瞎蒙。《HTTP权威指南》一本啃天下
