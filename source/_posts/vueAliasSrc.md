---
title: Vue自定义路径别名
date: 2017-09-11 18:00:00
tags: vue
categories: skill
---

通过配置 **vue-cli** 可以在生成的模板中在导入组件时使用了这样的语法： 路径别名

<!-- more -->
<The rest of contents | 余下全文>

### 序言

初始化项目的时候 大家可能会看到这样的导入路径

``` javascript
  import index from '@/components/Index'
```

实际上这些就是 **路径别名**

### 自定义路径别名

我们也可以在基础配置文件中添加自己的路径别名，比如下面这个就把 **~** 设置为路径 **src/components** 的别名：

``` javascript
  // build/webpack.base.config.js
  resolve: {
      extensions: ['.js', '.vue', '.json'],
      alias: {
      'vue$': 'vue/dist/vue.esm.js',
      '@': resolve('src'),
      '~': resolve('src/components')
    }
  }

  // 引用
  import Vfooter from '~/v-footer'
```