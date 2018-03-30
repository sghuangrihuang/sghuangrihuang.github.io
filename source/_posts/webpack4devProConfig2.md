---
title: webpack4.X 开发环境配置注意事项（二）
date: 2018-03-30 09:20:23
tags: webpack
categories: skill
---

webpack4.X 开发环境配置（二）

<!-- more -->
<The rest of contents | 余下全文>

### mode: 模式配置

`mode` 是 webpack 4 中新增加的参数选项，其有两个可选值：**production** 和 **development**

#### **production**
  1.  默认提供所有可能的优化，如代码压缩/作用域提升等不支持 watching
  2.  process.env.NODE_ENV 的值不需要再定义，默认是 production

  ``` javascript
   /** webpack.prod.conf.js **/
   // webpack 2/3 
  module.exports = {
    plugins: [
      new UglifyJsPlugin(),
      new webpack.DefinePlugin({ "process.env.NODE_ENV": JSON.stringify("production") }),
      new webpack.optimize.ModuleConcatenationPlugin(),
      new webpack.NoEmitOnErrorsPlugin()
    ]
  }
  // webpack 4  
  module.exports = {
    mode: 'production'
  }
  ```

#### **development**
  1.  主要优化了增量构建速度和开发体验
  2.  process.env.NODE_ENV 的值不需要再定义，默认是 development
  3.  开发模式下支持注释和提示，并且支持 eval 下的 source maps

  ``` javascript
   /** webpack.dev.conf.js **/
   // webpack 2/3 
  module.exports = {
    plugins: [
      new webpack.NamedModulesPlugin(),
      new webpack.DefinePlugin({ "process.env.NODE_ENV": JSON.stringify("development") })
    ]
  }
     
   // webpack 4  
  module.exports = {
    mode: 'development'
  }
  ```

### extract-text-webpack-plugin

针对安装 **extract-text-webpack-plugin** 插件， 必须要根据相对应的版本信息进行安装，否则报错

```
Error: Chunk.entrypoints: Use Chunks.groupsIterable and filter by instanceof Entrypoint instead
```

对此要根据对应版本安装
``` npm
# 针对于  webpack 4
$ npm install extract-text-webpack-plugin@next --save-dev

# 针对于  webpack 3
$ npm install extract-text-webpack-plugin@3.0.2 --save-dev
```
