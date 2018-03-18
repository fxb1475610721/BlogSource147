---
title: Hexo+GitHub搭建静态博客平台(一)-环境配置及建站
date: 2018-01-27 06:41:23
categories:
  - 静态博客搭建
tags:
  - GitHub
  - Hexo
  - 静态博客
---

> CSDN博客专栏：[GitHub + Hexo 搭建博客平台](http://blog.csdn.net/column/details/19262.html)

## 配置网站

我们可以在 `_config.yml` 文件中修改大部份的配置。

注意：此篇博文中讲解的是配置的含义，而详细的配置将在接下来的博文中进行介绍。

### 网站

| 参数 | 描述 |
| :--- | :--- |
| title | 网站标题 |
| subtitle | 网站副标题 |
| description | 网站描述 |
| author | 您的名字 |
| language | 网站使用的语言 |
| timezone | 网站时区。**Hexo 默认使用您电脑的时区**。[时区列表](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones)。比如说：America/New\_York, Japan, 和 UTC 。 |

其中， `description` 主要用于SEO，告诉搜索引擎一个关于您站点的简单描述，通常建议在其中包含您网站的关键词。 `author` 参数用于主题显示文章的作者。 `timezone` 建议保持默认即可。

### 网址

| 参数 | 描述 | 默认值 |
| :--- | :--- | :--- |
| url | 网址 | |
| root | 网站根目录 | |
| permalink | 文章的 [永久链接](https://hexo.io/zh-cn/docs/permalinks.html "永久链接") 格式 | :year/:month/:day/:title/ |
| permalink\_defaults | 永久链接中各部分的默认值 | |

> **网站存放在子目录**
>
> 如果您的网站存放在子目录中，例如 `http://yoursite.com/blog`，则请将您的 url 设为 `http://yoursite.com/blog` 并把 root 设为 `/blog/`。

### 目录

| 参数 | 描述 | 默认值 |
| :--- | :--- | :--- |
| source\_dir | 资源文件夹，这个文件夹用来存放内容。 | source |
| public\_dir | 公共文件夹，这个文件夹用于存放生成的站点文件。 | public |
| tag\_dir | 标签文件夹 | tags |
| archive\_dir | 归档文件夹 | archives |
| category\_dir | 分类文件夹 | categories |
| code\_dir | Include code 文件夹 | downloads/code |
| i18n\_dir | 国际化（i18n）文件夹 | :lang |
| skip\_render | 跳过指定文件的渲染，您可使用 [glob](https://github.com/isaacs/node-glob) 表达式来匹配路径。 | |

> 提示:如果您刚刚开始接触Hexo，通常没有必要修改这一部分的值。

### 文章

| 参数 | 描述 | 默认值 |
| :--- | :--- | :--- |
| new\_post\_name | 新文章的文件名称 | :title.md |
| default\_layout | 预设布局 | post |
| auto\_spacing | 在中文和英文之间加入空格 | false |
| titlecase | 把标题转换为 title case | false |
| external\_link | 在新标签中打开链接 | true |
| filename\_case | 把文件名称转换为 \(1\) 小写或 \(2\) 大写 | 0 |
| render\_drafts | 显示草稿 | false |
| post\_asset\_folder | 启动 Asset 文件夹 | false |
| relative\_link | 把链接改为与根目录的相对位址 | false |
| future | 显示未来的文章 | true |
| highlight | 代码块的设置 | |

> 相对地址
>
> 默认情况下，Hexo生成的超链接都是绝对地址。例如，如果您的网站域名为 `example.com` ,您有一篇文章名为 `hello` ，那么绝对链接可能像这样： `http://example.com/hello.html` ，它是绝对于域名的。相对链接像这样： `/hello.html` ，也就是说，无论用什么域名访问该站点，都没有关系，这在进行反向代理时可能用到。通常情况下，建议使用绝对地址。

### 分类 & 标签

| 参数 | 描述 | 默认值 |
| :--- | :--- | :--- |
| default\_category | 默认分类 | uncategorized |
| category\_map | 分类别名 | |
| tag\_map | 标签别名 | |

### 日期 / 时间格式

Hexo 使用 [Moment.js](http://momentjs.com/) 来解析和显示时间。

| 参数 | 描述 | 默认值 |
| :--- | :--- | :--- |
| date\_format | 日期格式 | YYYY-MM-DD |
| time\_format | 时间格式 | H:mm:ss |

### 分页

| 参数 | 描述 | 默认值 |
| :--- | :--- | :--- |
| per\_page | 每页显示的文章量 \(0 = 关闭分页功能\) | 10 |
| pagination\_dir | 分页目录 | page |

### 扩展

| 参数 | 描述 |
| :--- | :--- |
| theme | 当前主题名称。值为false时禁用主题 |
| deploy | 部署部分的设置 |

## 指令

### init

```bash
$ hexo init [folder]
```

新建一个网站。如果没有设置 `folder` ，Hexo 默认在目前的文件夹建立网站。

### new

```bash
$ hexo new [layout] <title>
```

新建一篇文章。如果没有设置 `layout` 的话，默认使用 [\_config.yml](https://hexo.io/zh-cn/docs/configuration.html) 中的 `default_layout` 参数代替。**如果标题包含空格的话，请使用引号括起来。**

### generate

```bash
$ hexo generate
```

生成静态文件。

| 选项 | 描述 |
| :--- | :--- |
| -d, --deploy | 文件生成后立即部署网站 |
| -w, --watch | 监视文件变动 |

该命令可以简写为

```bash
$ hexo g
```

### publish

```bash
$ hexo publish [layout] <filename>
```

发表草稿。

### server

```bash
$ hexo server
```

启动服务器。默认情况下，访问网址为： `http://localhost:4000/`。

| 选项 | 描述 |
| :--- | :--- |
| -p, --port | 重设端口 |
| -s, --static | 只使用静态文件 |
| -l, --log | 启动日记记录，使用覆盖记录格式 |

### deploy

```bash
$ hexo deploy
```

部署网站。

| 参数 | 描述 |
| :--- | :--- |
| -g, --generate | 部署之前预先生成静态文件 |

该命令可以简写为：

```bash
$ hexo d
```

### render

```bash
$ hexo render <file1> [file2] ...
```

渲染文件。

| 参数 | 描述 |
| :--- | :--- |
| -o, --output | 设置输出路径 |

### migrate

```bash
$ hexo migrate <type>
```

从其他博客系统 [迁移内容](https://hexo.io/zh-cn/docs/migration.html)。

### clean

```bash
$ hexo clean
```

清除缓存文件 \(`db.json`\) 和已生成的静态文件 \(`public`\)。

在某些情况（尤其是更换主题后），如果发现您对站点的更改无论如何也不生效，您可能需要运行该命令。

### list

```bash
$ hexo list <type>
```

列出网站资料。

### version

```bash
$ hexo version
```

显示 Hexo 版本。

## 选项

### 安全模式

```bash
$ hexo --safe
```

在安全模式下，不会载入插件和脚本。当您在安装新插件遭遇问题时，可以尝试以安全模式重新执行。

### 调试模式

```bash
$ hexo --debug
```

在终端中显示调试信息并记录到 debug.log。当您碰到问题时，可以尝试用调试模式重新执行一次，并 提交调试信息到 GitHub。

### 简洁模式

```bash
$ hexo --silent
```

隐藏终端信息。

### 自定义配置文件的路径

```bash
$ hexo --config custom.yml
```

自定义配置文件的路径，执行后将不再使用 `_config.yml`。

### 显示草稿

```bash
$ hexo --draft
```

显示 `source/_drafts` 文件夹中的草稿文章。

### 自定义 CWD

```bash
$ hexo --cwd /path/to/cwd
```

自定义当前工作目录（Current working directory）的路径。

## 博客迁移

注意：我只接触过Jekyll，其它的没有接触，因此在此只写明迁移Jekyll的方法，更多详见《[迁移](https://hexo.io/zh-cn/docs/migration.html)》。

把 `_posts` 文件夹内的所有文件复制到 `source/_posts` 文件夹，并在 `_config.yml` 中修改 `new_post_name` 参数。

```bash
new_post_name: :year-:month-:day-:title.md
```

>博客编号：20180120074123