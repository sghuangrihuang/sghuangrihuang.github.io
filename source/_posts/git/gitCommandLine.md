---
title: git命令总结
date: 2018-04-02 15:40:27
tags: git
categories: skill
---

git命令总结查询

<!-- more -->
<The rest of contents | 余下全文>

### 序言

由于git操作过于多，现发布文章来方便以后 git 命令查询

### 初次运行 Git 前的配置

#### 用户信息

> 配置全局配置

``` npm 
$ git config --global user.name "sghuangrihuang"
$ git config --global user.email 287545836@qq.com
```

**备注**：针对配置全局用户名和邮箱之后，还重复性输入验证码，可选择安装[Git Credential Manager](https://github.com/Microsoft/Git-Credential-Manager-for-Windows/releases/tag/v1.14.0)的其中的 GCMW-1.14.0.exe。 具体详情可看我另外一篇[文章](https://sghuangrihuang.github.io/2018/03/15/gitPushHttpRequestError/)

#### 检查配置信息

> 如果想要检查你的配置，可以使用 git config --list 命令来列出所有 Git 当时能找到的配置

``` npm
$ git config --list
```

> 通过git config `<key>`： 来检查 Git 的某一项配置

``` npm
$ git config user.name
sghuangrihuang
```

#### 获得帮助

通过如下途径可获得 Git 命令的使用手册

``` npm
$ git help <verb> 
$ git <verb> --help
$ man git-<verb>
```

要想获得 config 命令的手册

``` npm
$ git help config
```

### Git 操作

#### 获取 Git 仓库

##### 现有目录初始化

Git 来对现有的项目进行管理，可使用如下命令行
``` npm
$ git init
```
此命令将创建一个名为 .git 的子目录，这个子目录含有你初始化的 Git 仓库中所有的必须文件，这些文件是 Git 仓库的骨干

##### 克隆现有的仓库

克隆仓库的命令格式是 `git clone [url] `

``` npm
$ git clone https://github.com/sghuangrihuang/sghuangrihuang.github.io.git
```

#### 记录每次更新到仓库

##### 检查当前文件状态
要查看哪些文件处于什么状态，可以用`git status` 命令。
```npm
$ git status
```

##### 跟踪新文件
使用`git add [fileName]`,进行对文件跟踪

``` npm
$ git add README.md
```

##### 暂存已修改文件

若在执行`git status`，只要在 **Changes to be committed** 这行下面的，就说明是已暂存状态

##### 状态简览

可使用`git status -s`，进行项目状态简单预览

``` npm
$ git status -s
 M README
MM Rakefile
A  lib/git.rb
M  lib/simplegit.rb
?? LICENSE.txt
```

说明
* ??：新添加的未跟踪文件
* A：新添加到暂存区中的文件
* M：修改过的文件
* 右M：该文件被修改了但是还没放入暂存区
* 左M：该文件被修改了并放入了暂存区
* MM：暂存区和工作区都有该文件被修改了

##### 忽略文件
我们可以创建一个名为 **.gitignore** 的文件，列出要忽略的文件模式

```
$ > .gitignore
```

##### 提交更新

存放在暂存区的可使用`git commit`进行提交
```
$ git commit
```

可使用如下命令将提交信息与命令放在同一行
```
$ git commit -m "message"
```

也可使用  -a 选项 进行所有已经跟踪过的文件暂存起来一并提交
```
$ git commit -a -m 'message'
```

#### 查看提交历史

查看日志信息
``` 
$ git log
```

#### 撤消操作

可以运行带有 **--amend** 选项的提交命令尝试重新提交

```
$ git commit --amend
```

#### 远程仓库的使用

##### 查看远程仓库

查看远程仓库的名字。默认仓库名为origin
```
$ git remote
```

查看远程名字以及URL地址
```
$ git remote -v
```

##### 添加远程仓库

可通过命令`git remote add [shortname] [url]`，添加仓库

``` npm
$ git remote add gitee https://gitee.com/sghuangrihuang 
```

##### 远程仓库抓取数据

可通过命令`git fetch [remote-name]`，从远程仓库中获得数据
```
$ git fetch gitee
```

##### 推送到远程仓库
可通过命令 `git push [remoteName] [branchName]`,推送到远程仓库，前提是已经提交信息

``` npm
$ git push origin master
```

##### 远程仓库的移除与重命名

想要将 gitee 重命名为 mayun，可以用 `git remote rename`
```
$ git remote rename gitee mayun
```

若想删除特定的仓库，可用 `git remote rm`

```
$ git remote rm mayun
```

#### 打标签

##### 列出标签
在 Git 中列出已有的标签是非常简单直观的。 只需要输入 `git tag`
```
$ git tag
```

##### 创建标签
默认标签是打在最新提交的commit上的：`git tab [tagName]`
```
$ git tag v1.0
```

##### 附注标签
附注标签 运行 tag 命令时指定 **-a** 选项

```
$ git tag -a v1.2 -m 'message'
```

##### 查看标签信息

可以通过 `git show [tagName]` 查看标签信息

```
$ git show v1.2
```

##### 后期打标签

查看提交信息 包含提交信息以及commit id

```
$ git log --pretty=oneline --abbrev-commit
```

后期打标签 命令：`git tag [tagName] [commitId]`

```
$ git tag v1.2 1234567
```

##### 共享标签

通过 `git push origin [tagName]` 指定标签推送到共享服务器

```
$ git push origin v1.2 
```

通过 `git push origin  --tags` 全部标签推送到共享服务器

```
$ git push origin  --tags
```

### Git 分支
#### 分支简介
##### 分支创建
通过`git branch [branchName]` 进行本地分支创建

```
$ git branch dev
```

##### 分支切换

通过 `git checkout [branchName]`，进行本地分支切换

```
$ git checkout dev
```

也通过 添加 **-b** 选项，进行创建及切换分支

```
git checkout -b dev
```
##### 删除分支

通过 `git branch -d [branchName]`，进行删除指定分支

```
git branch -d dev
```

#### 分支管理

##### 分支合并

##### 分支信息
通过`git branch`进行分支信息查看
```
$ git branch
```

可添加 **-v**选项 进行分支信息提交状态
```
$ git branch -v
```

#### 远程分支

##### 推送分支到服务器

通过 `git push origin  [branchName]`，进行分支到服务器推送

```
git push origin dev
```

##### 远程分支拉取

通过 `git checkout -b [branchName] [BranchName]`，从远程的BranchName分支来取到本地创建且进行branchName分支切换

```
git checkout -b dev origin/dev
```

##### 删除远程分支

通过 **--delete** 进行远程分支删除

```
$ git push origin --delete dev
```

##### 下载指定仓库分支

`git clone -b [branchName] --single-branch [url] [projectNewName]`进行下载指定仓库分支

```
git clone -b webapp  --single-branch https://github.com/sghuangrihuang/practiceProject.git webapp
```

### 版本回退

通过`git reset --hard [commitId]`，进行版本回退，
再通过`git push origin HEAD --force` 提交到远程仓库

```
$ git reset --hard 123456789abcd
$ git push origin HEAD --force
```

