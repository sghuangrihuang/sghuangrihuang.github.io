---
title: github + hexo 博客的搭建
date: 2017-07-20 20:00:00
tags: config
---
基于 github 和 hexo 的博客搭建方法
<!-- more -->
<The rest of contents | 余下全文>

### 序言

由于之前写hexo博客的时候忘记把hexo的源码给保存好，导致后面的博客只能重写，为此创建一文章说明如何快速的把基于hexo的github项目的环境搭建

### 搭建流程

1.  创建仓库：http://sghuangrihuang.github.io
2.  创建两个分支：**master** 与 **hexo**
3.  设置**hexo**为默认分支（因为我们只需要手动管理这个分支上的Hexo网站文件）
4.  通过使用`git clone https://github.com/sghuangrihuang/sghuangrihuang.github.io.git` 拷贝仓库
5.  在本地sghuangrihuang.github.io文件夹下通过Git bash依次执行(此时当前分支应显示为hexo)
    *  `npm install hexo --save`
    *  `hexo init`
    *  `npm install `
    *  `npm install hexo-deployer-git --save`
6.  修改**_config.yml**中的**deploy**参数
    *   **type**: `git`
    *   **repository**: `https://github.com/sghuangrihuang/sghuangrihuang.github.io.git`
    *   **branch**: `master`
7.   依次执行git命令提交网站相关的文件
      *   `git add .`
      *   `git commit -m "..."`
      *   `git push origin hexo`

8.  执行**hexo g -d**生成网站并部署到GitHub上

这样一来，在GitHub上的[http://sghuangrihuang.github.io](http://sghuangrihuang.github.io)仓库就有两个分支，一个hexo分支用来存放网站的原始文件，一个master分支用来存放生成的静态网页

### 日常改动

重复步骤7和步骤8，顺序一定要是先提交hexo 后发布在master分支上

### 本地资料丢失

1.  git克隆仓库：`git clone https://github.com/sghuangrihuang/sghuangrihuang.github.io.git` 
2.  在本地新拷贝的ghuangrihuang.github.io文件夹下执行`npm install`指令
3.  重复步骤7和步骤8

### 总结

无论怎样，主要是思路就是一个hexo分支用来存放网站的原始文件，一个master分支用来存放生成的静态网页。相信可以帮助到大家

---
> 作者：**CrazyMilk**
> 链接：https://www.zhihu.com/question/21193762/answer/79109280 
> 来源：知乎 著作权归作者所有。
> 商业转载请联系作者获得授权，非商业转载请注明出处。