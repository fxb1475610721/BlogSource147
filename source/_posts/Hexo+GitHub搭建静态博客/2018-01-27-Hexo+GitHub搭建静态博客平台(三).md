---
title: Hexo+GitHub搭建静态博客平台(三)-Next主题基本使用
date: 2018-01-27 08:41:23
categories:
  - 静态博客搭建
tags:
  - GitHub
  - Hexo
  - 静态博客
  - Next
---

> CSDN博客专栏：[GitHub + Hexo 搭建博客平台](http://blog.csdn.net/column/details/19262.html)

博客网站搭建好后就是为自己的网站设置一个美观的主题了， `hexo` 官方提供了许多[官方主题](https://hexo.io/themes/),还有许多别人编写的主题，例如：[hexo-theme-jekyll](https://github.com/pinggod/hexo-theme-jekyll) 和 [hexo-theme-yilia](https://github.com/litten/hexo-theme-yilia)。还有很多就不一一列举了，我将介绍也是我将使用的是 [Next主题](https://github.com/iissnan/hexo-theme-next) 。

# 导入并使用主题

导入主题的方式很简单，有两种：

1. 进入博客根目录 `/themes/` , 执行 `$git clone ...` 命令，将主题克隆下来
2. 直接将主题下载并解压到博客根目录 `/themes/`

为了简洁些我们将其目录重命名为next。配置主题时，我们需要修改博客根目录的 `_config.yml` 中的默认 `theme: landscape`改为 `theme: 使用主题`就可以了。然后我们就可以正常启动博客，来验证主题是否应用成功了。

注意：修改 `theme:` 的时候后面必须有一个空格。

# Next主题的使用

Next的官方网址为：[http://theme-next.iissnan.com/](http://theme-next.iissnan.com/)

> 在 Hexo 中有两份主要的配置文件，其名称都是 `_config.yml`。 其中，一份位于站点根目录下，主要包含 `Hexo` 本身的配置；另一份位于主题目录下，这份配置由主题作者提供，主要用于配置主题相关的选项。
> **为了描述方便，在以下说明中，将前者称为 **`站点配置文件`**， 后者称为 **`主题配置文件`**。**

### 主题设定

> **主题的配置文件修改时会自动更新，因此无需重启服务器。**

### 选择 Scheme

`Scheme` 是 `NexT` 提供的一种特性，借助于 `Scheme`，`NexT` 为你提供多种不同的外观。同时，几乎所有的配置都可以在 `Scheme` 之间共用。目前 NexT 支持三种 Scheme，他们是：

1. `Muse` - 默认 Scheme，这是 NexT 最初的版本，黑白主调，大量留白
2. `Mist` - Muse 的紧凑版本，整洁有序的单栏外观
3. `Pisces` - 双栏 Scheme，小家碧玉似的清新

`Scheme` 的切换通过更改 `主题配置文件`，搜索 `scheme` 关键字。 你会看到有三行 `scheme` 的配置，将你需用启用的 `scheme` 前面注释 `#` 去除即可。

### 设置语言

编辑 `站点配置文件`， 将 `language` 设置成你所需要的语言。建议明确设置你所需要的语言，例如选用简体中文，配置如下：

```
language: zh-Hans
```

目前 NexT 支持的语言如以下表格所示：

| 语言 | 代码 | 设定示例 |
| :--- | :--- | :--- |
| **English** | en | language: en |
| **简体中文** | zh-Hans | language: zh-Hans |
| Français | fr-FR | language: fr-FR |
| Português | pt | language: pt or language: pt-BR |
| **繁體中文** | zh-hk 或者 zh-tw | language: zh-hk |
| Русский язык | ru | language: ru |
| Deutsch | de | language: de |
| 日本語 | ja | language: ja |
| Indonesian | id | language: id |
| Korean | ko | language: ko |

### 设置菜单

菜单配置包括三个部分，第一是菜单项（名称和链接），第二是菜单项的显示文本，第三是菜单项对应的图标。 `NexT` 使用的是 [Font Awesome](http://fontawesome.io/) 提供的图标， `Font Awesome` 提供了 600+ 的图标，可以满足绝大的多数的场景，同时无须担心在 `Retina` 屏幕下 图标模糊的问题。

编辑 `主题配置文件`，修改以下内容：

**&lt;1&gt; 设置菜单项**

设定菜单内容, 对应的字段是 `menu`。 菜单内容的设置格式是：`item name: link`。其中 `item name` 是一个名称，这个名称并不直接显示在页面上，她将用于匹配图标以及翻译。

```
menu:
home: /
archives: /archives
#about: /about
#categories: /categories
tags: /tags
#commonweal: /404.html
```

> **若你的站点运行在子目录中，请将链接前缀的 / 去掉**

`NexT` 默认的菜单项有（标注 ♠ 的项表示需要手动创建这个页面）：

| 键值 | 设定值 | 显示文本（简体中文） |
| --- | --- | --- |
| home | home: / | 主页 |
| archives | archives: /archives | 归档页 |
| categories | categories: /categories | 分类页 ♠ |
| tags | tags: /tags | 标签页 ♠ |
| about | about: /about | 关于页面 ♠ |
| commonweal | commonweal: /404.html | 公益 404 ♠ |

**&lt;2&gt; 设置菜单项的显示文本。**

在第一步中设置的菜单的名称并不直接用于界面上的展示。`Hexo` 在生成的时候将使用这个名称查找对应的语言翻译，并提取显示文本。因为我们设置为简体中文，因此会自动进行翻译。这些翻译文本放置在 NexT 主题目录下的 `languages/{language}.yml` （`{language}` 为你所使用的语言）。

以简体中文为例，若你需要添加一个菜单项，比如 `something`。那么就需要**修改简体中文对应的翻译文件**`languages/zh-Hans.yml`，在 menu 字段下添加一项：

```
menu:
home: 首页
archives: 归档
categories: 分类
tags: 标签
about: 关于
search: 搜索
commonweal: 公益404
something: 有料
```

**&lt;3&gt; 设定菜单项的图标**

设定菜单项的图标，对应的字段是 `menu_icons`。 此设定格式是 `item name: icon name`，其中 `item name` 与上一步所配置的菜单名字对应，`icon name` 是 `Font Awesome` 图标的名字。而 `enable` 可用于控制是否显示图标，你可以设置成 `false` 来去掉图标。

```
menu_icons:
enable: true
# Icon Mapping.
home: home
about: user
categories: th
tags: tags
archives: archive
commonweal: heartbeat
```

在菜单图标开启的情况下，如果菜单项与菜单未匹配（没有设置或者无效的 `Font Awesome` 图标名字） 的情况下，NexT 将会使用 **?** 作为图标。

> **请注意键值（如 **`home`**）的大小写要严格匹配**

### 设置侧栏

默认情况下，侧栏仅在文章页面（拥有目录列表）时才显示，并放置于右侧位置。 可以通过修改 `主题配置文件` 中的 `sidebar` 字段来控制侧栏的行为。侧栏的设置包括两个部分，其一是侧栏的位置， 其二是侧栏显示的时机。

**&lt;1&gt; 设置侧栏的位置**

修改 `sidebar.position` 的值，支持的选项有：

* `left` - 靠左放置
* `right` - 靠右放置

```
sidebar:
position: left
```

**&lt;2&gt; 设置侧栏显示的时机**

修改 `sidebar.display` 的值，支持的选项有：

* `post` - 默认行为，在文章页面（拥有目录列表）时显示
* `always` - 在所有页面中都显示
* `hide` - 在所有页面中都隐藏（可以手动展开）
* `remove` - 完全移除

### 设置头像

编辑 `主题配置文件`，修改字段`avatar`， 值设置成头像的链接地址。其中，头像的链接地址可以是：

![](http://ozduqh728.bkt.clouddn.com/20180212/setHeadPhoto.png)

## 集成常用的第三方服务

**详见：**[第三方服务集成](http://theme-next.iissnan.com/third-party-services.html)

## 百度统计

> 注意： `baidu_analytics` 不是你的百度 id 或者 百度统计 id

**&lt;1&gt;** 登录 [百度统计](https://tongji.baidu.com/web/welcome/login)， 定位到站点的代码获取页面

**&lt;2&gt;** 复制 `hm.js?` 后面那串统计脚本 id，如：

[![](http://ozduqh728.bkt.clouddn.com/20180126/baidu_analytics.png "20180126/baidu\_analytics")](http://ozduqh728.bkt.clouddn.com/20180126/baidu_analytics.png)

**&lt;3&gt;** 编辑 `主题配置文件`， 修改字段 `baidu_analytics` 字段，值设置成你的百度统计脚本 `id`。

### 阅读次数统计（LeanCloud）

在注册完成 [LeanCloud](https://leancloud.cn/) 帐号并验证邮箱之后，我们就可以登录我们的 `LeanCloud` 帐号，进行一番配置之后拿到 `AppID` 以及 `AppKey` 这两个参数即可正常使用文章阅读量统计的功能了。

登录 `LeanCloud` ，然后新建一个 `应用` 来专门进行博客的访问统计的数据操作。新建的 `应用` 名称我们可以随意输入，即便是输入的不满意我们后续也是可以更改的:

我创建的应用的名称为 `fxb_LeanCloud` 创建完成之后我们点击新创建的应用的名字来进行该应用的参数配置:

[![](http://ozduqh728.bkt.clouddn.com/20180126/data.png "20180126/data")](http://ozduqh728.bkt.clouddn.com/20180126/data.png)

在应用的数据配置界面，左侧下划线开头的都是系统预定义好的表，为了便于区分我们新建一张表来保存我们的数据。点击左侧右上角的图标，新建Class：

[![](http://ozduqh728.bkt.clouddn.com/20180126/creat_class.png "20180126/creat\_class")](http://ozduqh728.bkt.clouddn.com/20180126/creat_class.png)

> 注意：此处的新建 **Class名字必须** 为 `Counter` 。

[![](http://ozduqh728.bkt.clouddn.com/20180126/no_limited.png "20180126/no\_limited")](http://ozduqh728.bkt.clouddn.com/20180126/no_limited.png)

> 由于LeanCloud升级了默认的ACL权限，如果你想避免后续因为权限的问题导致次数统计显示不正常，建议在此处选择 `无限制` 。

创建完成之后，左侧数据栏应该会多出一栏名为 `Counter` 的栏目。接下来我们获取应用的 `AppID` 以及 `AppKey` ，有了它们，我们就有权限能够通过主题中配置好的Javascript代码与这个应用的Counter表进行数据存取操作了:

[![](http://ozduqh728.bkt.clouddn.com/20180126/app_ID&Key.png "20180126/app\_ID&amp;Key")](http://ozduqh728.bkt.clouddn.com/20180126/app_ID&Key.png)

复制 `AppID` 以及 `AppKey` 并在 `NexT主题` 的 `_config.yml` 文件中我们相应的位置填入即可，正确配置之后文件内容像这个样子:

```YAML
leancloud_visitors:
enable: true
app_id: ***joaeuuc4h***
app_key: ***E9UJsJpw1o***
```

这个时候重新生成部署Hexo博客，应该就可以正常使用文章阅读量统计的功能了。

**需要特别说明的是：** 记录文章访问量的唯一标识符是文章的发布日期以及文章的标题，因此请确保这两个数值组合的唯一性，如果你更改了这两个数值，会造成文章阅读数值的清零重计。

#### Web安全

因为 `AppID` 以及 `AppKey` 是暴露在外的，因此如果一些别有用心之人知道了之后用于其它目的是得不偿失的，为了确保只用于我们自己的博客，建议开启Web安全选项，这样就只能通过我们自己的域名才有权访问后台的数据了，可以进一步提升安全性。

选择应用的设置的安全中心选项卡：

[![](http://ozduqh728.bkt.clouddn.com/20180126/web_safe.png "20180126/web\_safe")](http://ozduqh728.bkt.clouddn.com/20180126/web_safe.png)

如果你不知道怎么填写安全域名而或者填写完成之后发现博客文章访问量显示不正常，打开浏览器调试模式，发现如下图的输出:

[![](http://ozduqh728.bkt.clouddn.com/20180126/error_LeanCloud.png "20180126/error\_LeanCloud")](http://ozduqh728.bkt.clouddn.com/20180126/error_LeanCloud.png)

这说明你的安全域名填写错误，导致服务器拒绝了数据交互的请求，你可以更改为正确的安全域名。

#### 后台管理

当你配置部分完成之后，初始的文章统计量显示为0，但是这个时候我们 `应用`的 `Counter` 表中并没有相应的记录，只是单纯的显示为0而已，当博客文章在配置好阅读量统计服务之后第一次打开时，便会自动向服务器发送数据来创建一条数据，该数据会被记录在对应的应用的 `Counter` 表中。

### Local Search【本地搜索】

安装 `hexo-generator-searchdb`，在站点的根目录下执行以下命令：

```bash
$ npm install hexo-generator-searchdb --save
```

编辑 `站点配置文件`，新增以下内容到任意位置：

```YAML
search:
path: search.xml
field: post
format: html
limit: 10000
```

编辑 `主题配置文件`，启用本地搜索功能：

```YAML
# Local search
local_search:
enable: true
```

### 评论系统 - 来必力

登陆 [来必力](https://livere.com/) 获取你的 `LiveRe UID`。编辑 `主题配置文件`， 编辑 `livere_uid` 字段，设置如下：

```YAML
livere_uid: #your livere_uid
```

LiveRe 有两个版本：

* `City`
版：是一款适合所有人使用的免费版本；
* `Premium`
版：是一款能够帮助企业实现自动化管理的多功能收费版本。

第一步安装：

[![](http://ozduqh728.bkt.clouddn.com/20180126/city_anzhuang.png "20180126/city\_anzhuang")](http://ozduqh728.bkt.clouddn.com/20180126/city_anzhuang.png)

第二步填写信息：

[![](http://ozduqh728.bkt.clouddn.com/20180126/livere-get-code.png "20180126/livere-get-code")](http://ozduqh728.bkt.clouddn.com/20180126/livere-get-code.png)

第三步获取UID：

[![](http://ozduqh728.bkt.clouddn.com/20180126/uid_get.png "20180126/uid\_get")](http://ozduqh728.bkt.clouddn.com/20180126/uid_get.png)

### 内容分享服务

#### JiaThis

编辑 `主题配置文件`， 添加/修改字段 `jiathis`，值为 `true`。

```YAML
# JiaThis 分享服务
jiathis: true
```

#### 百度分享

编辑 `主题配置文件`，添加/修改字段baidushare，值为 `true`。

```YAML
baidushare:
type: button #百度分享展示的方式button|slide
```

---

**问题待解决**：分享服务本地浏览正常，部署到GitHub上后失效！

当前解决状态：

查看网页生成网址源码，与分享服务提供的源码基本一致。但仍无法执行，我将JiaThis或百度分享的代码直接贴到hexo生成文件中也是这种情况。

暂时理解：

可能是JavaScript加载问题导致的，因为其文字加载正常，但是后续出现问题！

解决帮助：

next的分享代码生成在文件夹：themes → next → layout → \_partials → share

> 博客编号：20180120084123
