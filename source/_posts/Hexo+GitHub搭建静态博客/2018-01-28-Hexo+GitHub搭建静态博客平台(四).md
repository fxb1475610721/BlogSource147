---
title: Hexo+GitHub搭建静态博客平台(四)-Hexo基本操作
date: 2018-1-28 09:07:13
categories:
  - 静态博客搭建
tags:
  - GitHub
  - Hexo
  - 静态博客
---

> CSDN博客专栏：[GitHub + Hexo 搭建博客平台](http://blog.csdn.net/column/details/19262.html)

# 写作

你可以执行下列命令来创建一篇新文章：

```bash
$ hexo new [layout] <title>
```

您可以在命令中指定文章的布局（`layout`），默认为 `post`，可以通过修改 `_config.yml` 中的 `default_layout` 参数来指定默认布局。

## 布局（Layout）

`Hexo` 有三种默认布局：`post`、`page` 和 `draft`，它们分别对应不同的路径，而您自定义的其他布局和 `post` 相同，都将储存到 `source/_posts` 文件夹。

| 布局 | 路径 |
| :--- | :--- |
| post | source/\_posts |
| page | source |
| draft | source/\_drafts |

> **不要处理我的文章**
> 如果你不想你的文章被处理，你可以将 `Front-Matter` 中的`layout:` 设为 `false` 。

## 文件名称

`Hexo` 默认以标题做为文件名称，但您可编辑 `new_post_name` 参数来改变默认的文件名称，举例来说，设为 `:year-:month-:day-:title.md` 可让您更方便的通过日期来管理文章。

| 变量 | 描述 |
| :--- | :--- |
| :title | 标题（小写，空格将会被替换为短杠） |
| :year | 建立的年份，比如， 2015 |
| :month | 建立的月份（有前导零），比如， 04 |
| :i\_month | 建立的月份（无前导零），比如， 4 |
| :day | 建立的日期（有前导零），比如， 07 |
| :i\_day | 建立的日期（无前导零），比如， 7 |

## 草稿

刚刚提到了 `Hexo` 的一种特殊布局：`draft`，这种布局在建立时会被保存到 `source/_drafts` 文件夹，您可通过 `publish` 命令将草稿移动到 `source/_posts` 文件夹，该命令的使用方式与 `new` 十分类似，您也可在命令中指定 `layout` 来指定布局。

```bash
$ hexo publish [layout] <title>
```

草稿默认不会显示在页面中，您可在执行时加上 `--draft` 参数，或是把 `render_drafts` 参数设为 `true` 来预览草稿。

## 模版（Scaffold）

在新建文章时，`Hexo` 会根据 `scaffolds` 文件夹内相对应的文件来建立文件，例如：

```bash
$ hexo new photo "My Gallery"
```

在执行这行指令时，`Hexo` 会尝试在 `scaffolds` 文件夹中寻找 `photo.md`，并根据其内容建立文章，以下是您可以在模版中使用的变量：

| 变量 | 描述 |
| :--- | :--- |
| layout | 布局 |
| title | 标题 |
| date | 文件建立日期 |

# Front-matter

Front-matter 是文件最上方以 `---` 分隔的区域，用于指定个别文件的变量，举例来说：

```YAML
---
title: Hello World
date: 2013/7/13 20:46:25
---
```

以下是预先定义的参数，您可在模板中使用这些参数值并加以利用。

| 参数 | 描述 | 默认值 |
| :--- | :--- | :--- |
| layout | 布局 | |
| title | 标题 | |
| date | 建立日期 | 文件建立日期 |
| updated | 更新日期 | 文件更新日期 |
| comments | 开启文章的评论功能 | true |
| tags | 标签（不适用于分页） | |
| categories | 分类（不适用于分页） | |
| permalink | 覆盖文章网址 | |

## 分类和标签

**只有文章支持分类和标签**，您可以在 `Front-matter` 中设置。在其他系统中，分类和标签听起来很接近，但是在 `Hexo` 中**两者有着明显的差别**：分类具有顺序性和层次性，也就是说 `Foo, Bar` 不等于 `Bar, Foo`；而标签没有顺序和层次。

> 分类方法的分歧:通常分类可以是同级的，也可以是父子分类。**但是Hexo不支持指定多个同级分类。** 下面的指定方法：
> categories:
>
> * Diary
> * Life
> 会使分类Life成为Diary的子分类，而不是并列分类。因此，有必要为您的文章选择尽可能准确的分类。

## JSON Front-matter

除了 `YAML` 外，你也可以使用 `JSON` 来编写 `Front-matter`，只要将 `---` 代换成 `;;;` 即可。

# 标签插件（Tag Plugins）\[非重点\]

声明：功能非常强大，但是简书以及CSDN不支持，为了保证通用性，此功能不详细深入。如果想详细了解可参考《[标签插件](https://hexo.io/zh-cn/docs/tag-plugins.html)》。

**标签插件** 和 **Front-matter** 中的标签不同，它们是用于在文章中快速插入特定内容的插件。

## 引用块

在文章中插入引言，可包含作者、来源和标题。

**别号**： `quote`

```
{% blockquote [author[, source]] [link] [source_link_title] %}
content
{% endblockquote %}
```

## 代码块

在文章中插入代码。

**别名**： code

```
{% codeblock [title] [lang:language] [url] [link text] %}
code snippet
{% endcodeblock %}
```

## Pull Quote

在文章中插入 Pull quote。

```
{% pullquote [class] %}
content
{% endpullquote %}
```

## jsFiddle

在文章中嵌入 jsFiddle。

```
{% jsfiddle shorttag [tabs] [skin] [width] [height] %}
```

## Gist

在文章中嵌入 Gist。

```
{% gist gist_id [filename] %}
```

## iframe

在文章中插入 iframe。

```
{% iframe url [width] [height] %}
```

## Image

在文章中插入指定大小的图片。

```
{% img [class names] /path/to/image [width] [height] [title text [alt text]] %}
```

## Link

在文章中插入链接，并自动给外部链接添加 target=”\_blank” 属性。

```
{% link text url [external] [title] %}
```

## Include Code

插入 source 文件夹内的代码文件。

```
{% include_code [title] [lang:language] path/to/file %}
```

## Youtube

在文章中插入 Youtube 视频。

```
{% youtube video_id %}
```

## Vimeo

在文章中插入 Vimeo 视频。

```
{% vimeo video_id %}
```

## 引用文章

引用其他文章的链接。

```
{% post_path slug %}
{% post_link slug [title] %}
```

## 引用资源

引用文章的资源。

```
{% asset_path slug %}
{% asset_img slug [title] %}
{% asset_link slug [title] %}
```

## Raw

如果您想在文章中插入 Swig 标签，可以尝试使用 Raw 标签，以免发生解析异常。

```
{% raw %}
content
{% endraw %}
```

# 资源文件夹

资源（Asset）代表 `source` 文件夹中除了文章以外的所有文件，例如图片、CSS、JS 文件等。比方说，如果你的Hexo项目中只有少量图片，那最简单的方法就是将它们放在 `source/images` 文件夹中。然后通过类似于`！[](/images/image.jpg)`的方法访问它们。

## 相对路径引用的标签插件

通过常规的 `markdown` 语法和相对路径来引用图片和其它资源可能会导致它们在存档页或者主页上显示不正确。在Hexo 2时代，社区创建了很多插件来解决这个问题。但是，随着Hexo 3 的发布，许多新的标签插件被加入到了核心代码中。这使得你可以更简单地在文章中引用你的资源。

```
{% asset_path slug %}
{% asset_img slug [title] %}
{% asset_link slug [title] %}
```

比如说：当你打开文章资源文件夹功能后，你把一个 `example.jpg` 图片放在了你的资源文件夹中，如果通过使用相对路径的常规 `markdown` 语法 `![](/example.jpg)` ，它将 **不会** 出现在首页上。（但是它会在文章中按你期待的方式工作）

正确的引用图片方式是使用下列的标签插件而不是 `markdown` ：

```
{% asset_img example.jpg This is an example image %}
```

通过这种方式，图片将会同时出现在文章和主页以及归档页中。

# 数据文件

有时您可能需要在主题中使用某些资料，而这些资料并不在文章内，并且是需要重复使用的，那么您可以考虑使用 Hexo 3.0 新增的「数据文件」功能。此功能会载入 `source/_data` 内的 `YAML` 或 `JSON` 文件，如此一来您便能在网站中复用这些文件了。

举例来说，在 `source/_data` 文件夹中新建 `menu.yml` 文件：

```
Home: /
Gallery: /gallery/
Archives: /archives/
```

您就能在模板中使用这些资料：

```
<% for (var link in site.data.menu) { %>
<a href="<%= site.data.menu[link] %>"> <%= link %> </a>
<% } %>
```

渲染结果如下 :

```
<a href="/"> Home </a>
<a href="/gallery/"> Gallery </a>
<a href="/archives/"> Archives </a>
```

# 服务器

## hexo-server

`Hexo 3.0` 把服务器独立成了个别模块，您必须先安装 `hexo-server` 才能使用。

```bash
$ npm install hexo-server --save
```

安装完成后，输入以下命令以启动服务器，您的网站会在 `http://localhost:4000` 下启动。在服务器启动期间，`Hexo`** 会监视文件变动并自动更新，您无须重启服务器。**

```bash
$ hexo server
```

如果您想要更改端口，或是在执行时遇到了 `EADDRINUSE` 错误，可以在执行时使用 `-p` 选项指定其他端口，如下：

```bash
$ hexo server -p 5000
```

### 静态模式

在静态模式下，服务器只处理 `public` 文件夹内的文件，而不会处理文件变动，在执行时，您应该先自行执行 `hexo generate`，此模式通常用于生产环境（production mode）下。

```bash
$ hexo server -s
```

### 自定义 IP

服务器默认运行在 `0.0.0.0`，您可以覆盖默认的 `IP` 设置，如下：

```bash
$ hexo server -i 192.168.1.1
```

指定这个参数后，您就只能通过该IP才能访问站点。例如，对于一台使用无线网络的笔记本电脑，除了指向本机的 `127.0.0.1` 外，通常还有一个 `192.168.*.*` 的局域网IP，如果像上面那样使用 `-i` 参数，就不能用 `127.0.0.1` 来访问站点了。对于有公网IP的主机，如果您指定一个局域网IP作为 `-i` 参数的值，那么就无法通过公网来访问站点。

## Pow

`Pow` 是一个 `Mac` 系统上的零配置 `Rack` 服务器，它也可以作为一个简单易用的静态文件服务器来使用。

### 安装

```bash
$ curl get.pow.cx | sh
```

### 设置

在 `~/.pow` 文件夹建立链接（symlink）。

```bash
$ cd ~/.pow
$ ln -s /path/to/myapp
```

您的网站将会在 `http://myapp.dev` 下运行，网址根据链接名称而定。

# 生成器

使用 `Hexo` 生成静态文件快速而且简单。

```bash
$ hexo generate
```

## 监视文件变动

`Hexo` 能够监视文件变动并立即重新生成静态文件，在生成时会比对文件的 `SHA1 checksum`，只有变动的文件才会写入。

```bash
$ hexo generate --watch
```

## 完成后部署

您可执行下列的其中一个命令，让 `Hexo` 在生成完毕后自动部署网站，两个命令的作用是相同的。

```bash
$ hexo generate --deploy
$ hexo deploy --generate
```

上面两个命令可以简写为:

```bash
$ hexo g -d
$ hexo d -g
```

# 部署

`Hexo` 提供了快速方便的一键部署功能，让您只需一条命令就能将网站部署到服务器上。

```bash
$ hexo deploy
```

在开始之前，您必须先在`_config.yml` 中修改参数，一个正确的部署配置中至少要有 `type` 参数，例如：

```YAML
deploy:
type: git
```

您可同时使用多个 `deployer`，`Hexo` 会依照顺序执行每个 `deployer`。

```YAML
deploy:
- type: git
repo:
- type: heroku
repo:
```

> 缩进
>
> YAML依靠缩进来确定元素间的从属关系。因此，请确保每个deployer的缩进长度相同，并且使用空格缩进。

## Git

安装 [hexo-deployer-git](https://github.com/hexojs/hexo-deployer-git)。

```bash
$ npm install hexo-deployer-git --save
```

修改 `站点配置文件` :

```YAML
deploy:
type: git
repo: <repository url>
branch: [branch]
message: [message]
```

![](http://ozduqh728.bkt.clouddn.com/20180212/git_Peizhi.png)

**Hexo 生成的所有文件都放在 public 文件夹中，您可以将它们复制到您喜欢的地方。**

而Heroku、Rsync、OpenShift、FTPSync的部署可以参考《[部署](https://hexo.io/zh-cn/docs/deployment.html)》。

> 博客编号：20180120090713