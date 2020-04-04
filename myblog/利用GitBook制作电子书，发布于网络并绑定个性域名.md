---
title: 利用GitBook制作电子书，发布于网络并绑定个性域名
date: 2019-02-21 20:01:08
categories: 版本控制
tags: [Blog,GitBook,GitHub] 
---

如何使用 GitBook 制作电子书，发布于网络并绑定个性域名？<!-- more -->

# 一、制作电子书

## 0. GitBook介绍

[GitBook](https://github.com/GitbookIO/gitbook) 是一个使用 GitHub/Git 和 Markdown 来制作电子书的命令行工具（Node.js 库）。另外，有一个网站 [http://gitbook.com](http://link.zhihu.com/?target=http%3A//gitbook.com) 可以帮助用户更好的使用 Gitbook，它是使用 GitBook 格式创建和托管图书的在线平台。它提供托管，协作功能和易于使用的编辑器。Gitbook 与 [http://gitbook.com](http://link.zhihu.com/?target=http%3A//gitbook.com) 的关系类似 Git 和 GitHub，一个是工具，另一个是基于工具创建的网站。

> 注：GitBook 平台在今年的 4 月 9 日发布了新的版本 v2。新的版本官网已经变成 [`www.gitbook.com`](https://www.gitbook.com/?t=11) （旧的地址为 [`legacy.gitbook.com`](https://legacy.gitbook.com/) ）。新旧版本有很多的不一样，网上很多资料都是针对旧版。 比如新版不再支持把每本书作为一个 `Git Repository`  来进行版本管理。更多 v2 的重大改变可以看 [这里](https://docs.gitbook.com/v2-changes/important-differences)。

你可以利用 Git 命令管理电子书版本，如果你是 GitHub 的重度使用者，还可以把你的 GitBook 帐户和 GitHub 帐户关联起来，这样不论在任何一方修改了内容，都可以互相同步。下面是制作电子书和使用步骤。

## 1. 安装Node.js

由于 GitBook 是基于 Node.js 开发的，所以依赖 Node.js 环境。如果你的系统中还未安装 Node.js，请点击 [Node.js下载页面](https://nodejs.org/en/download/)，根据你所使用的系统下载对应的版本。如果已安装则略过本步骤。

Windows 版和 Mac 版的 Node.js 都是常规的安装包，连续下一步安装即可。Linux 版可以通过 yum、apt-get 之类的工具安装，也可以通过源码包安装。

## 2. 安装GitBook命令行工具

打开“命令提示符”（Mac 系统打开“终端”）输入以下命令全局安装 gitbook-cli：

``` markdown
npm install gitbook-cli -g
```

`gitbook-cli` 是 GitBook 的一个命令行工具。它将自动安装所需版本的 GitBook 来构建一本书。

执行下面的命令，查看 GitBook 版本，以验证安装成功。

``` markdown
gitbook --version
```

GitBook  命令：

``` 
gitbook init //初始化目录文件
gitbook build [书籍路径] [输出路径] //构建书籍，生成静态网页，默认输出到 _book 目录
gitbook serve [--port 端口号]  //包含build命令，生成静态网页并运行服务器
gitbook pdf ././mybook.pdf  //生成 pdf/epub/mobi 格式的电子书

gitbook help //列出gitbook所有的命令
gitbook --help //输出gitbook-cli的帮助信息
gitbook ls //列出本地所有的gitbook版本
gitbook ls-remote //列出远程可用的gitbook版本
gitbook fetch 标签/版本号 //安装对应的gitbook版本
gitbook update //更新到gitbook的最新版本
gitbook uninstall 2.0.1 //卸载对应的gitbook版本
```



## 3. 新建GitBook项目

新建一个目录，并进入该目录使用 gitbook 命令初始化电子书项目。

``` markdown
gitbook init
```

初始化后的目录中会出现 `README.md` 和 `SUMMARY.md` 两个基本文件，如果你希望将书籍创建到一个新目录中，可以通过运行 `gitbook init ./directory` 这样做。当然你也可以自己手动创建这两个文件。`README.md` 是电子书的介绍，`SUMMARY.md` 是电子书的目录结构。

注意：一个 GitBook 项目至少要包含 README.md 和 SUMMARY.md，书本的第一页内容是从文件 README.md 文件中提取的。如果这个文件名没有出现在 SUMMARY.md 文件中，则它会被添加为章节的第一个条目。而由于一些托管在 GitHub 上的书会将 README.md 作为项目的介绍而不是书的介绍，从 gitbook v2 起，可以在 book.json 中指定某个文件作为 README。如：

``` json
{
    "structure": {
        "readme": "introduction.md"
    }
}
```

> 个人的一个实践情况：如果不想要书籍的目录默认把 README.md 文作为书籍第一章，可以新建 introduction.md 文件（名称随意），并在 readme 指定该文件，则书籍第一章为 introduction.md 内容。但是有个注意的是，如果在 summary.md 文件某个目录中有指定了 README.md 文件作为章节内容，则书籍第一章不会是 introduction.md 内容，而是 README.md 内容。

## 4. 编辑书籍内容

GitBook 使用 `SUMMARY.md` 来定义书本的章节和子章节的结构。它用来生成书本内容的预览表。它的格式是一个简单的链接列表。另外可以在里面添加一些 Markdown 格式的标题和分割线。例如：

``` 
# 概要
- [章节 1](chapter1.md)
- [章节 2](chapter2.md)
- [章节 3](chapter3.md)

# 基础
- [章节 1](chapter1/README.md)
  - [1.1 a](chapter1/a.md)
  - [1.2 b](chapter1/b.md)
---
- [章节 2](chapter2/README.md)
  - [2.1 c](chapter2/c.md)
  - [2.2 d](chapter2/d.md)

# 进阶
- [章节 3](chapter3/README.md)
```

接下来就可以在相应的 MD 文件里书写内容了。文件内容编写使用 Markdown 语法格式。另外，GitBook 的目录，限定为三级。

注：`README.md` 和 `SUMMARY.md` 这两个文件你也可以自己手动新建和编写，名称大小写无关。

## 5. 预览电子书

写完内容，可以通过以下方式来预览电子书：

``` 
gitbook serve
```

该命令实际上是先调用 `gitbook build`  编译书籍，然后会启动一个 web 服务器，监听在本地的 4000 端口。在浏览器中输入 `http://localhost:4000`，即可预览查看。

> 注：`gitbook build` 命令会在当前文件夹中生成 `_book `文件夹（生成 HTML 版本的电子书），用户可以将这个文件夹内容托管到网上，从而实现内容的发布。

这里有个问题记录下，我在使用 `gitbook serve` 后报错，如下：

``` xml
Template render error: (F:\JavaEE-tutorial\ch1\02-Java基本语法.md) [Line 434, Column 22]
  expected variable end
```

根据错误，我有找到对应位置的内容：

``` java
scores = new int[][]{{1, 2, 3},{3, 4, 5},{6} };
```

即这行这里的数字 1 前面连续的花括号问题，后面尝试解决了：只要这两个花括号不要连续就行，比如空一格 `{ {` 就不会有错了。另外，我还发现 MD 源文章的标题不能使用半角下的圆括号 `（`、`)`，否则预览电子书的时候点击对应文章的目录没有反应。另外我也发现在基于 Hexo 博客搭建编写的文章里出现了连续花括号同样会报错，解决方法只要不连续就行。

## 6. 生成电子书

生成 PDF 格式电子书：`gitbook pdf .`，默认为 `book.pdf`，如果自定义名称，可：`gitbook pdf 目录 目录/书名.pdf`，如在当前文件夹下输出：

``` markdown
gitbook pdf ./ ./书名.pdf
```

注意：如上操作出现报错话，试一试先使用 npm 安装上 gitbook-pdf：`npm install gitbook-pdf -g`。参考：[使用Gitbook写开源书籍，过一把作家瘾](https://www.jianshu.com/p/7476afdd9248)。

另外，由于生成 PDF 文件依赖于 `ebook-convert`，故首先在该处 [ebook-convert下载链接](http://calibre-ebook.com/download) 点击下载所需要的版本。安装完毕，程序会自动将包含 `ebook-convert.exe` 的文件夹添加到 PATH 变量中。

需要在当前目录生成 epub 或者 mobi 格式的，分别执行下面的命令即可：`gitbook epub .`、`gitbook mobi .`。

如果需要定制 PDF 输出，可以在 `book.json` 中的配置 PDF 输出样式。可以在网上该样式配置，就不在这里详细讲解了。

提下，若想要输出的 PDF 目录对应的是数字页码，可以试试下面解决方式：

- [Change PDF generation engine to either wkhtmltopdf or phantom.js](https://github.com/GitbookIO/gitbook/issues/1470) 
- [Conversion to PDF with calibre should show table of content with page numbers](https://github.com/GitbookIO/gitbook/issues/1223) 

## 7. 使用插件

Gitbook 本身功能丰富，但同时可以使用插件来进行个性化定制。Gitbook 插件里已经有 100 多个插件，可以在 `book.json` 文件的 `plugins` 和 `pluginsConfig` 字段添加插件及相关配置，添加后别忘了进行安装。

安装插件的方式非常简单，只需要将所需要的插件添加到 `book.json` 中，如：

``` json
{
    "plugins": ["mathjax"]
}
```

然后执行：`gitbook install`，即可安装，安装的插件在 node_modules 文件夹。

Gitbook 默认带有 5 个插件：

- highlight
- search
- sharing
- font-settings
- livereload

如果要去除自带的插件， 可以在插件名称前面加 `-`。

本人有使用的 GitBook 插件：

- "anchor-navigation-ex"：

  一个可以目录收缩的插件，比较实用。<https://helight.info/2018-11-23/1146/>

- ~~"back-to-top-button"：击右下角按钮，回到顶部。~~ 
- "code"：代码块添加行号和复制按钮，复制按钮可关闭。
- "copy-code-button"：为代码块添加复制的按钮。
- "-lunr", "-search", "search-pro"：支持中文搜索, 在使用此插件之前，需要将默认的`search`和`lunr` 插件去掉。默认的 search 不支持中文查询。
- "github"：在右上角显示 github 仓库的图标链接。
- "github-buttons"：提供了一个非官方的 GitHub 的 star 和 fork 等的显示。
- "splitter"：提供了一个可以拖动的分割正文和目录的垂直条。使侧边栏的宽度可以自由调节。
- "-sharing", "sharing-plus"：分享当前页面，比默认的 sharing 插件多了一些分享方式。
- ~~"page-toc-button"： 悬浮目录。使用 anchor-navigation-ex 已经可以了。~~
- "klipse"：嵌入一块功能，可在代码段中实时交互，即（输入代码 > 执行结果。
- "pageview-count"：阅读量统计。
- "auto-scroll-table"：为避免表格过宽，增加滚动条。
- "lightbox"：点击查看大图。

——参考：<https://www.cnblogs.com/mingyue5826/p/10307051.html>  【荐】

- "disqus"：添加 disqus 评论。
- "prism"：

  系统自带插件的高亮功能并不完善，可使用 prism 插件增强，该插件需要先禁用 `highlight` 插件。使用 `prism` 高亮插件的优点在于，可以使用不同的配色方案，且语法关键词识别度比 `highlight` 插件高。`prism` 支持的语言可在其[官方网站](https://prismjs.com/#languages-list)查询。

  ``` json
  {
      "plugins": ["-highlight", "prism", "prism-themes"]
  }
  "pluginsConfig": {
      "prism": {
          "css": [
              "prismjs/themes/prism-solarizedlight.css"
          ]
      }
  }
  ```

- "ace"：使 GitBook 支持 ace，作用：插入代码高亮编辑器。

- “KaTex”：为了支持数学公式，可以使用 `KaTex` 和 `MathJax` 插件，官网上说 `Katex` 速度要快于 `MathJax`。

  注意：MathJax 允许你在你的网页中包含公式，无论是使用 LaTeX、MathML 或者 AsciiMath 符号，这些公式都会被 javascript 处理为 HTML、SVG 或者 MathML 符号。但是 GitHub，GitLab 都不支持引入 js，这个方法在 GitHub，GitLab 上都无效，即在 GitHub 是看不到数学公式的效果。

- "anchors"：添加 GitHub 风格的锚点样式。

- "edit-link"：使用该插件可以链接到当前页的源文件上。

——参考：<http://gitbook.zhangjikai.com/plugins.html>  【荐】

- "atoc"：插入 TOC 目录。
- "latex-codecogs"：使用数学方程式。参考 <https://lowzj.com/notes/math-formula.html>



# 二、发布于网络

## 1. 在gitbook.com上发布和管理书籍

以上所有的步骤都是在本地进行的，如果需要实现电子书的版本管理，或者把电子书发布到网络上，还可以通过 Git 命令将本地的项目托管到 GitBook.com 上。

首先进入 [GitBook.com](https://www.gitbook.com/) 注册一个账号(本人使用的 Google 账号登录)，选择“Create an organization”创建一个 Organization。另外，从官网可以看到：

![](https://img-1256179949.cos.ap-shanghai.myqcloud.com/20190219145307.png)

一个组织下免费用户只能有 2 个协作者，一个公开空间，一个私有空间。如果想要创建多本公开图书，创建多个组织就行，再在每个组织下创建公开图书。

再创建完 Organization 后，在选择 “Creat a new Space” 创建一个 Space（旧版叫 Book），然后就可以在线写书了。

访问之前先进行几个设置，先到 Organization –> “Settings” –> “Your Organization URL” 设置你的 url，比如 `strivebo`，再打开电子书，进入 “Domains” –> “GitBook URL” –> 设置域名 `https://strivebo.gitbook.io/` 的后部分，比如设置为 `javaee`，这样就可以使用 `https://strivebo.gitbook.io/javaee` 在线访问了。

## 2. 在github.com上发布和管理书籍

如果你喜欢使用 GitHub 管理电子书。还可以把您的 GitBook 帐户和 GitHub 帐户关联起来，这样两者的修改内容就可以互相同步了。你可以在 Account Settings 中的 Github 设置选项中去进行绑定。

完成关联后即可设置同步电子书项目了。以电子书项目“JavaEE-tutorial”为例，进入某个电子书的设置页面，切换到“Integrations”选项卡。在“GitHub”中设置和添加需要同步的仓库。如图（下图为已经添加了 GitHub 仓库）：

![](https://img-1256179949.cos.ap-shanghai.myqcloud.com/20190221143040.png)

> 注：其中设置过程中，有个选择 ”Which content should be used for the first synchronization ?“，我们这里选择“I write my content on GitHub“选项，即选择 GitHub 内容自动同步到 GitBook。

添加完成会自动导入你添加的 GitHub 仓库内容。以后你上传到 GitHub 的内容就会自动同步到 GitBook 了。

另外，你也可以托管到 Github Pages，这个就不细讲了。我的 GitHub Page 用来搭建个人博客了，如果想要了解如何使用 GitHub Page 可以找我写的搭建博客的文章看看。

忘了说，你还可以发布到虚拟空间，也就是自己买的云服务器，使用步骤：

1. 在本地写作完，`gitbook build` 生成静态网页，即会在书籍目录下生成 `_book` 的目录，
2. 在使用只需要将这个目录的文件上传到我们的虚拟空间中就可以了。



# 三、绑定域名

虽然 GitBook 上的所有的图书都可以通过地址 `http://{Organization}.gitbooks.io/{Gitbookn}/` 访问， 但我们有时候还是希望将图书绑定我们自己的域名上。

如何做呢？以腾讯云操作如下：

第一步，GitBook 的网站上进入你的电子书的，打开 “Domains” –> “Custom Domain” 设置你的个性域名，比如我设置了一个二级域名为：`javaee.strivebo.com`；

第二步，进入腾讯云 [云解析](https://console.qcloud.com/cns/domains)，如下操作，选择一级域名，点击「分配其子域名至项目」：

![](https://img-1256179949.cos.ap-shanghai.myqcloud.com/20190221170338.png)

然后在弹出的对话框填入二级域名前缀，项目名称，选择「默认项目」如图：

![](https://img-1256179949.cos.ap-shanghai.myqcloud.com/20190221170539.png)

第三步，打开「协作子域名」选择刚刚添加的二级域名，点击解析，添加一条 CNAME 记录，将 `javaee.strivebo.com` 解析为 `strivebo.gitbooks.io.`，如下图：

![](https://img-1256179949.cos.ap-shanghai.myqcloud.com/20190221170902.png)

第四步，就是等待域名解析记录在全球范围内生效，然后就可以地址栏输入 `javaee.strivebo.com` 阅读图书了。等待的时候不是固定的，如果你等待了很久还是不能访问，不妨翻墙试一下。

> 注意：在添加 CNAME 解析的时候记录值，记得后面 `.io` 还有一个 `.`，如果你不加，这里在添加完解析会默认给加上。

===========================

Update 2019-7-26 这里更新下内容：

在第三步，设置解析的域名，官方目前给出的是，解析到：

```
Add this CNAME record to your domain by visiting your DNS provider or registrar.
CNAME  hosting.gitbook.com
```

即解析到 `hosting.gitbook.com`。

如果你新建了多个组织用来制作多本免费的在线电子书，并且都各自绑定域名，注意，域名解析那都是设置为解析到这个。

另外有一点注意，域名解析那里设置的二级域名，**在 GitBook 网站的 Custom Domain 那也是要设置同样的二级域名，**否则在检查 DNS 解析会提示该错误：

``` 
The domain is missing a CNAME record pointing to hosting.gitbook.com or the changes haven't propagated yet.
```

关于域名解析，可以使用 nslookup 命令看看（windows 下可用）。简单使用，输入：nslookup，然后输入网址。

参考：[云解析 子域名分项目管理 - 操作指南 - 文档平台 - 腾讯云](https://cloud.tencent.com/document/product/302/7800)