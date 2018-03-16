---
title: axios Post发送数据方案
date: 2018-03-07 21:04:45
tags: vue
categories: skill
---

**axios** 作为 **Vue** 官方提供的 **HTTP** 库，其中 **POST** 请求居然是采用这种方式发送数据

<!-- more -->
<The rest of contents | 余下全文>

### 序言

最近在做**vue**项目的时候，采用**axios**，进行**ajax**网络请求，但是使用过程中出现**post**无法传递数据

``` javascript
getList () {
  let params = {
    name: 'admin',
    code: '123456'
  }
  axios.post(url, params).then((res) => {
    if (res.state == 200) {
      console.log(res)
    }
  })
}
```

### 问题所在

通过查看发送信息以及传统jQuery的post请求来看，发现一细节

``` javascript
// axios 
// Content-Type：application/json;charset=UTF-8
// Request Payload: { name: 'admin', code: '123456'}

// jQ
// Content-Type：application/x-www-form-urlencoded;charset=UTF-8
// Request name=admin&code=123456
```

### 解决方案

#### 1、设置请求头

首先通过axios全局 把post请求头设置为`application/x-www-form-urlencoded`

``` javascript
axios.defaults.headers.post['Content-Type'] = 'application/x-www-form-urlencoded'
```

#### 2、处理数据

通过[axios](https://github.com/axios/axios#using-applicationx-www-form-urlencoded-format)官方提供信息推荐我们使用其下两个方式进行处理post请求数据

##### 1.URLSearchParams
  ``` javascript
  var params = new URLSearchParams();
  params.append('name', 'admin');
  params.append('code', '123456');
  axios.post(url, params);
  ```

##### 2.qs库
  ``` javascript
  var qs = require('qs');
  axios.post(url, qs.stringify({ 'name': 'admin' }));
  ```

### 后台获取数据方式

在axios使用Post发送数据时，默认是直接把**json**放到请求体中提交到后端的。针对后端而言，获取数据的方式有两种
  1. `@RequestParam` (通过字符串中解析出参数，很明显后端默认使用这种请求获取数据)
  2. `@ResponseBody` (从请求体中取参数)


### 总结

针对axios Post无法传递数据，解决方案就是：先设置post请求头为标准的`application/x-www-form-urlencoded`, 其次针对请求数据采用qs库进行格式化




