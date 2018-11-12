---
title: git push 出现的重复输入用户名和密码 
date: 2018-03-15 22:57:36
tags: git
categories: skill
---
Git push failing with Fatal: HttpRequestException encountered
<!-- more -->
<The rest of contents | 余下全文>

### 序言

由于我采用的是 **vs code** 编辑器 使用其进行`git push`操作，但是每次操作都必须要重新输入 **username** 和 **password** 并且还报错 **HttpRequestException encountered** 错误，可明明我已经设置 **git** 的全局属性，还是出现这个**error**。
之前在公司push提交的时候，完全不会，后来同事也是跟我一样，出现这个问题，以为是某某配置没搞好问题

### 问题所在

既然知道是报错：**HttpRequestException encountered**
那就正对这情况，加上对 **git** 的操作只是局限在使用上，能力有限，只进行搜索
刚好发现同样问题的同人[Git push error](https://superuser.com/questions/1297583/git-push-failing-with-fatal-httprequestexception-encountered)

### 解决方案

由于 **Github** disabled TLS v1.0，并且采用新的[V1.1](https://githubengineering.com/crypto-removal-notice/)版本

针对 使用 **windows** 和 **github** , 建议下载并且安装 **Git Credential Manager** [下载地址](https://github.com/Microsoft/Git-Credential-Manager-for-Windows/releases/tag/v1.14.0) 其中的 **GCMW-1.14.0.exe**