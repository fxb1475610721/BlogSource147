---
title: Hexo+GitHub搭建静态博客平台(六)-使用Travis CI实现自动化部署
date: 2018-03-05 17:54:56
categories:
	- 静态博客搭建
tags:
	- Github
	- Hexo
	- 静态博客 
	- Travis CI
---

# 前言

使用`hexo + gitPages`搭建好个人博客后，每当要发表一篇博文，第一步得手动使用`hexo g`命令生成静态网页，然后还得通过`hexo d`命令将静态文件推送到GitHub远程仓库，虽然不算繁琐且可以编写批处理命令进行简化，但是有更简单的，为何不用呢？。

我们可以通过 `Travis CI` 就能实现自动化构建自己的博客，我们只需将写好的`Markdown`格式的博文，我们将博文推送\(push\)到GitHub的时候，就可以触发自己编写好的脚本，实现自动化部署。

首先我们需要了解`Travis CI`分为两种：

* [Travis CI .org](https://travis-ci.org/auth) for public repositories【公共仓库】
* [Travis CI .com](https://travis-ci.com/auth) for private repositories【私有仓库】

针对私有仓库的当然是收费的，接下来我们使用的是 [`Travis CI .org`](https://travis-ci.org/auth) 。

# Travis CI 自动化构建实现

## 登录Travis CI.org

首先我们使用`GitHub`账号登录 [Travis CI .org](https://travis-ci.org/auth) ，然后我们我们就进入如下界面：

![](http://ozduqh728.bkt.clouddn.com/20180305/使用Travis CI实现自动化部署_00.png)

第一次进入可能下面没有你的仓库列表，我们可以点击右上角的`Sync Account`即可。

## 添加自动化构建仓库

其实上图中已经看到了，我们将需要自动化构建仓库前面的开关打开即可！当然我们可以回到主页\[点击网站图标\]，然后进行如下操作：![](http://ozduqh728.bkt.clouddn.com/20180305/使用Travis CI实现自动化部署_01.png)

然后也就跳转回你的`Profile`界面了，我们打开自己要实现自动化构建的仓库：

![](http://ozduqh728.bkt.clouddn.com/20180305/使用Travis CI实现自动化部署_02.png)

注意：需要是你的博客源码的仓库，我的博客源码与网站的静态文件是两个仓库，其实使用一个仓库，选用两个分支即可！

![](http://ozduqh728.bkt.clouddn.com/20180305/使用Travis CI实现自动化部署_03.png)

## 设置仓库

![](http://ozduqh728.bkt.clouddn.com/20180305/使用Travis CI实现自动化部署_04.png)

我们需要打开下面的几个开关：

![](http://ozduqh728.bkt.clouddn.com/20180305/使用Travis CI实现自动化部署_05.png)

说明：

* Build only if .travis.yml is present：只有在`.travis.yml`文件中配置的分支改变了才构建
* Build pushed branches：当推送完这个分支后开始构建

至此， 我们已经开启了要构建的仓库，但是构建完后，我们怎么将生成的文件推送到github上呢？

我们使用Travis CI服务的目标是，我们只要将博文源文件推送到GitHub，Travis CI就自动构建并`push`静态文件到`GitHub Pages！`接下来，我们就是为Travis CI赋予操作GitHub的权利了！

## GitHub生成Personal access tokens

我们登录GitHub后进入设置界面，选择最下面的Developer settings：

![](http://ozduqh728.bkt.clouddn.com/20180305/使用Travis CI实现自动化部署_06.png)

接下来就是生成`Personal access tokens`：

![](http://ozduqh728.bkt.clouddn.com/20180305/使用Travis CI实现自动化部署_07.png)我们需要为此赋予权限，此处我除了删除权限，其它一股脑都赋予了：

![](http://ozduqh728.bkt.clouddn.com/20180305/使用Travis CI实现自动化部署_08.png)

注意：`Personal access tokens`生成后会在上方显示出来，我们应当立即复制此秘钥，否则你将再也看不到了！

![](http://ozduqh728.bkt.clouddn.com/20180305/使用Travis CI实现自动化部署_09.png)

## 在Travis CI配置Personal access tokens

![](http://ozduqh728.bkt.clouddn.com/20180305/使用Travis CI实现自动化部署_10.png)

当然，我们也可以在配置文件中书协自己的Personal access tokens，但是配置文件与源码是放在一起的，别人获得了此钥匙就相当于可以控制你的GitHub了，当然非常不安全，因此还是建议在网站上进行配置！

## 编写配置文件

配置文件的配置时非常灵活的，但是的主要目标 已经确定，所以配置基本上都一致。我们首先在博客的根目录下创建`.travis.yml`文件，下面是我的配置信息：

```yaml
language: node_js
node_js:
- "9" # nodejs的版本，查看命令 node -v

branches:
only:
- master # 设置自动化部署的源码分支

# 安装依赖组件
install:
- npm install

# 执行的命令
script:
- hexo clean
- hexo generate

# 执行的成功后执行
after_success:
- hexo deploy
```

至此，一切就绪！你可以编写一篇博文，然后推送到GitHub进行测试，如果你查看的比较快的话，你还可以看到Travis CI网页上执行的全过程，当然最终也可以看到其全貌！

![](http://ozduqh728.bkt.clouddn.com/20180305/%E4%BD%BF%E7%94%A8Travis%20CI%E5%AE%9E%E7%8E%B0%E8%87%AA%E5%8A%A8%E5%8C%96%E9%83%A8%E7%BD%B2_11.png)

>博文编号：20180305175456