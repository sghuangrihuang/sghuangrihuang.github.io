---
title: git连接Github请求错误
date: 2018-11-12 11:32:00
tags: git
categories: skill
---

HttpRequestException encountered 解决方案

<!-- more -->
<The rest of contents | 余下全文>

### 问题所在

``` git
$ git push origin master

fatal: HttpRequestException encountered
```

由于 Github 禁用了TLS v1.0 and v1.1，必须更新Windows的git凭证管理器


### git凭证管理器

通过[下载地址](https://github.com/Microsoft/Git-Credential-Manager-for-Windows/releases/)下载最新的GCMV-1.x.x.exe，并安装就可以了

