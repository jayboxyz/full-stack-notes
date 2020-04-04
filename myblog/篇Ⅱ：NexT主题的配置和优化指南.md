---
title: 篇Ⅱ：NexT主题的配置和优化指南
date: 2019-02-17 20:01:08
categories: Blog
tags: [NexT,Blog] 
---

NexT 主题的配置和优化指南。<!-- more -->

## 写在前面

(1) 什么是 Hexo：[官网传送门](https://hexo.io/zh-cn/docs/)

(2) Hexo 官网：[Hexo.io](https://hexo.io/ )

(3) Hexo 主题的选择：

- 官网：[Themes | Hexo](https://hexo.io/themes/)
- GitHub：[Themes · hexojs](https://github.com/hexojs/hexo/wiki/Themes )
- 知乎：[有哪些好看的 Hexo 主题？](https://www.zhihu.com/question/24422335) 

本人使用主题为 NexT v5.1.4。搭建过程各个软件和工具的版本信息如下：

``` xml
nodejs：v8.10.0
npm：5.6.0  #命令 npm -v 可以查看到
NexT主题版本：5.1.4  #打开站点配置文件_config.yml搜索version可以找到
```

> 注：新版的 NexT 主题源码早已转移在了这个仓库 <https://github.com/theme-next/hexo-theme-next

`hexo version` 的信息如下：

```
hexo-cli:1.1.0
os:Windows_NT 6.1.7601 win32 x64
http_parser:2.7.0
node:8.10.0
v8:6.2.414.50
uv:1.19.1
z1ib:1.2.11
ares:1.10.1-DEU modules:57
nghttp2:1.25.0openss1:1.0.2n icu:60.1
unicode:10.0
cldr:32.0
tz:2017c
```



## 一、主题基本配置

关于博客主题的选择问题，考虑了很久一直决定不下来选哪个主题合适，在尝试了多个觉得不错的主题之后，最终还是决定选择 GitHub 最多 star 的 NexT 主题了。有那么多人在用，普遍大众应该还是很认可的。NexT 主题版本更新日志和下载：[NexT – Theme for Hexo](https://theme-next.org/) | [NexT主题 - GitHub](https://github.com/iissnan/hexo-theme-next)

关于这个主题的相关配置、优化定制网上容易找到非常多的资料，但基本的配置，还是建议直接看官方文章：

- [主题配置 - NexT 使用文档](http://theme-next.iissnan.com/theme-settings.html)
- [主题配置参考 · iissnan/hexo-theme-next Wiki](https://github.com/iissnan/hexo-theme-next/wiki/%E4%B8%BB%E9%A2%98%E9%85%8D%E7%BD%AE%E5%8F%82%E8%80%83)（ NexT 主题 GitHub 上其 wiki 页面关于主题设置教程）

本文会介绍 NexT 主题大部分的基本配置修改以及优化定制博客。

网上比较全面的修改指南，供参考：

- 2016-04-07 [Hexo站点、NexT主题修改全记录](http://www.lzblog.cn/2016/04/07/Hexo%E7%AB%99%E7%82%B9%E3%80%81NexT%E4%B8%BB%E9%A2%98%E4%BF%AE%E6%94%B9%E5%85%A8%E8%AE%B0%E5%BD%95/)
- 2018-05-01 [关于Hexo6.0搭建个人博客(进阶篇)](https://segmentfault.com/a/1190000014676320)
- 2017-05-24 [hexo的next主题个性化配置教程](https://segmentfault.com/a/1190000009544924)
- ……

### (0) 主题设置/动态背景/显示当前浏览进度

(1) 主题设置

主题设定：打开主题配置文件，搜索 scheme 关键字。 你会看到有四行 scheme 的配置。我选择了 scheme: Pisces，下面是我的设置：

``` 
# Schemes
#scheme: Muse
#scheme: Mist
scheme: Pisces
#scheme: Gemini
```

- Muse：默认 Scheme，这是 NexT 最初的版本，黑白主调，大量留白
- Mist：Muse 的紧凑版本，整洁有序的单栏外观

- Pisces：双栏 Scheme，小家碧玉似的清新
- Gemini：左侧网站信息及目录，块+片段结构布局 

(2) 动态背景

目前 NexT 主题有 4 种动态背景：

``` 
Canvas-nest
three_waves
canvas_lines
canvas_sphere
```

设置方法很简单，直接设置里需要的动态背景为`true`。

(3) 显示当前浏览进度

修改`themes/next/_config.yml`， scrollpercent 值由 `false` 改为 `true`：

``` 
# Scroll percent label in b2t button
scrollpercent: true
```

### (1) 关于文章所属「分类」和「标签」的设置

之前我使用的别的主题，只要在 source 文件夹下新建的文章前面按如下格式表明所属分类和标签：

```
title: 自学编程成功概率有多少可能
date: 2017-05-26 19:57:47
tags: [编程,感悟]
categories: 技术 
```

但是在 NexT 主题下的设置的步骤如下：

1) 先`hexo new page categories`新建 categorier 文件夹，其中会自动生成一个`index.md`文件，修改（即添加一行）为：

```
---
title: categories
date: 2018-01-23 17:14:51
type: "categories"
---
```
同理，「标签」也一样，`hexo new page tags`，生成 tags 文件夹，其中会自动生成一个`index.md`文件，修改为：
```
---
title: tags
date: 2018-01-23 17:14:51
type: "tags"
---
```

2) 然后写的博客文章，表明所属「分类」和拥有哪些「标签」，官方文档所说的格式如下：

```
categories:
- Diary
tags:
- PS3
- Games
```

但是我亲测，如下也是可以的：
```
categories: 技术
tags: [编程,感悟]
```

另外，对于 NexT 这个主题，对于「关于」这个菜单和上面新建分类和标签一样，也是需要手动创建文件夹的，`hexo new page about`，这样会生成 about 文件夹，同时自动生成`index.md`文件，然后可以在这个`.md`文件中写上自我个人介绍。（亲测过，`index.md`这个文件的名字不能修改，否则「关于」菜单出错）

关于这部分的设置，官方文档称其为「Front-matter」，「Front-matter」 是文件最上方以 `---` 分隔的区域，用于指定个别文件的变量，举例来说：

```
---
title: Hello World
date: 2013/7/13 20:46:25
---
```

以下是预先定义的参数，您可在模板中使用这些参数值并加以利用。

| 参数       | 描述                 | 默认值       |
| :--------- | -------------------- | ------------ |
| layout     | 布局                 |              |
| title      | 标题                 |              |
| date       | 建立日期             | 文件建立日期 |
| updated    | 更新日期             | 文件更新日期 |
| comments   | 开启文章的评论功能   | true         |
| tags       | 标签（不适用于分页） |              |
| categories | 分类（不适用于分页） |              |
| permalink  | 覆盖文章网址         |              |

### (2) 添加本地添加搜索菜单

1) 安装 `hexo-generator-searchdb` 插件：`npm install hexo-generator-searchdb --save` 

2) 打开站点配置文件找到 Extensions 在下面添加（其实，新增以下内容到任意位置即可）

```
search:
      path: search.xml
      field: post
      format: html
      limit: 10000
```

3) 打开主题配置文件找到 Local search，将 enable 设置为 true，启动本地搜索功能，这样就能在页面可以看到搜索菜单了：

```
# Local search
local_search:
  enable: true
```

### (3) 添加文章字数统计、阅读时长（next主题已经集成）

Hexo 提供了 `hexo-wordcount` 插件，新版本的 next 中集成了这一点，只需要安装插件然后开启功能就 ok。

第一步：安装 word_count 插件，在博客根目录下打开终端：`npm install hexo-wordcount --save`

 第二步：在主题配置文件 `Blog\themes\next\config.yml` 中打开 post_wordcount 统计功能：

```
# Post wordcount display settings
# Dependencies: https://github.com/willin/hexo-wordcount
post_wordcount:
  item_text: true
  wordcount: true # 单篇 字数统计
  min2read: true # 单篇 阅读时长
  totalcount: false # 网站 字数统计
  separated_meta: true
```

如果仅仅只是打开 wordcount、min2read，部署之后会发现文章的【字数统计】和【阅读时长】后面没有对应的 xxx 字，xx 分钟等字样，只有光秃秃的数字在那里。

解决方案：找到 \themes\next\layout\_macro\post.swig 文件，将“字”、“分钟” 字样添加到如下位置即可。

```
<span title="{{ __('post.wordcount') }}">
     {{ wordcount(post.content) }} 字
</span>

    ...
<span title="{{ __('post.min2read') }}">
     {{ min2read(post.content) }} 分钟
</span>
```

然后才可以看到显示：`阅读时长 ≈ 2 分钟`，但若是不需要显示 `≈` ，就修改这个地方：

```
{% if theme.post_wordcount.item_text %}
        <span class="post-meta-item-text">{{ __('post.min2read') }} &asymp;</span>
 {% endif %}
```

把这里的` &asymp;`删除即可。

注：如果想要在文章中使用，可以这样插入 `<i class="fa fa-smile-o" style="font-size:28px;color:#FF8247;"></i>` 即可使用。

参考：[Hexo添加字数统计、阅读时长、友情链接](http://www.crocutax.com/2017/05/11/Hexo%E6%B7%BB%E5%8A%A0%E5%AD%97%E6%95%B0%E7%BB%9F%E8%AE%A1%E3%80%81%E9%98%85%E8%AF%BB%E6%97%B6%E9%95%BF%E3%80%81%E5%8F%8B%E6%83%85%E9%93%BE%E6%8E%A5/)

### (4) 设置友情链接

在主题配置文件添加，示例：

``` 
# title
links_title: Links
links:
  MacTalk: http://macshuo.com/
  Title: http://example.com/
```

另外，侧边栏友情链接及菜单等旁边的图标，可以到 [图标库](https://fontawesome.com/icons?from=io) 找到自己喜欢的图标然后复制到相应代码中，也可以到这里找：[Font Awesome，一套绝佳的图标字体库和CSS框架](http://fontawesome.dashgame.com/)。

### (5) 设置侧边栏头像

编辑主题的 `_config.yml`，新增字段 `avatar`， 值设置成头像的链接地址。

其中，头像的链接地址可以是：

1. 完整的互联网 URL，例如：`https://avatars1.githubusercontent.com/u/32269?v=3&s=460`
2. 站点内的地址，例如：
   - `/uploads/avatar.jpg` 需要将你的头像图片放置在 `站点的 source/uploads/`（可能需要新建`uploads`目录）
   - `/images/avatar.jpg` 需要将你的头像图片放置在 `主题的 source/images/` 目录下。

### (6) 设置订阅微信公众号

> 注：此特性在版本 5.0.1 中引入，要使用此功能请确保所使用的 NexT 版本在此之后。

在每篇文章的末尾显示微信公众号二维码，扫一扫，轻松订阅博客。将公众号二维码存放于博客`source/uploads/`目录下。然后编辑 主题配置文件，示例如下：

``` 
# Wechat Subscriber
wechat_subscriber:
  enabled: false
  qcode: /uploads/wechat.jpg
  description: 欢迎扫描二维码关注公众号一起成长~
```

### (7) 开启打赏、禁用打赏文字抖动

**1、开启打赏**

越来越多的平台（微信公众平台，新浪微博，简书，百度打赏等）支持打赏功能，付费阅读时代越来越近，特此增加了打赏功能，支持微信打赏和支付宝打赏。 只需要主题配置文件中填入微信和支付宝收款二维码图片地址即可开启该功能。打赏功能配置示例：

``` 
reward_comment: 坚持原创技术分享，您的支持将鼓励我继续创作！
wechatpay: /path/to/wechat-reward-image
alipay: /path/to/alipay-reward-image
```

本人操作：把收款二维码存放在了 NexT 主题的`source/uploads/`目录下，然后配置如下：

``` 
# Reward  赞赏  
reward_comment: 觉得文章对您有帮助请我喝杯咖啡吧^_^ 
wechatpay: /uploads/wechatpay.jpg
alipay: /uploads/alipay.jpg
```

**2、禁用打赏文字抖动**

1）方法一：

具体的做法就是注释掉文字抖动函数，文件路径：`/themes/next/source/css/_common/components/post/post-reward.styl`

``` xml
## 注释打赏文字抖动函数，将下面代码注释掉
#wechat:hover p{
    animation: roll 0.1s infinite linear;
    -webkit-animation: roll 0.1s infinite linear;
    -moz-animation: roll 0.1s infinite linear;
}
#alipay:hover p{
    animation: roll 0.1s infinite linear;
    -webkit-animation: roll 0.1s infinite linear;
    -moz-animation: roll 0.1s infinite linear;
}
```

方法二：

可以在 `themes\next\source\css\_custom\custom.styl` 中添加重叠样式（推荐）：

``` html
//二维码不抖动
#wechat:hover p, #alipay:hover p {
    animation: none;
}
```



### (8) 添加RSS订阅功能

`RSS(Really Simple Syndication)` 简易信息聚合，在互联网上被广泛采用的内容包装和投递协。是一种描述同步网站内容的格式，使用 `xml` 格式。当网站内容更新时，可以通过订阅 `RSS` 源在 `RSS` 阅读器上获取更新的信息。大多数内容提供的网站都会提供 `RSS` 订阅的功能，方便用户去获取最新的内容。

这里主介绍怎么给自己的 `hexo` 博客添加 `RSS` 源。

①在 hexo 的根目录下执行命令：

``` 
npm install hexo-generator-feed --save
```

②在主题配置文件 `/theme/next/_config.yml` 文件中配置该插件：

```xml
feed:
    type: atom
    path: atom.xml
    limit: 20
    hub:
    content:
    content_limit:
    content_limit_delim: ' '
```

参数的含义：

``` 
type: RSS的类型(atom/rss2)
path: 文件路径,默认是atom.xml/rss2.xml
limit: 展示文章的数量,使用0或则false代表展示全部
hub:
content: 在RSS文件中是否包含内容 ,有3个值 true/false默认不填为false
content_limit: 指定内容的长度作为摘要,仅仅在上面content设置为false和没有自定义的描述出现
content_limit_delim: 上面截取描述的分隔符,截取内容是以指定的这个分隔符作为截取结束的标志.在达到规定的内容长度之前最后出现的这个分隔符之前的内容,，防止从中间截断.
```

此外还有一种方法，就是在 `next` 主题的 `_config.yml` 文件中有个 `rss` 的配置，直接设置为 `true` 就可以了。

配置好之后运行 `hexo g`就可以找到你博客的 `pubilc` 文件夹下发现 `atom.xml` 文件了，然后运行 `hexo` 服务就可以在个人站点处看到 `RSS` 的订阅图标了,点击这个图标就可以出现 `RSS` 订阅的地址,就可以添加到你的 `RSS` 阅读器方便查看博客的最新文章。

参考：[为hexo博客添加RSS订阅功能](https://segmentfault.com/a/1190000012647294)

### (9) 文章字数统计、阅读时长开启和关闭，以及使用图标还是文本

打开 NexT 主题配置文件 `_config.yml`，修改：

``` xml
post_wordcount:
  item_text: true # 文章 字数统计 阅读时长 使用图标 还是 文本表示
  wordcount: true
  min2read: true
  totalcount: false
  separated_meta: false # 是否换行显示 字数统计 及 阅读时长
```

参考：[Hexo Next主题开启字数统计及阅读时长](https://shjhe.github.io/hexo/2018/07/04/Hexo%20Next%E4%B8%BB%E9%A2%98%E5%BC%80%E5%90%AF%E5%AD%97%E6%95%B0%E7%BB%9F%E8%AE%A1%E5%8F%8A%E9%98%85%E8%AF%BB%E6%97%B6%E9%95%BF/)

另外，如果想要把「发表于」、「分类于」、「阅读时长」修改为英文，可以打开 `\themes\next\languages\zh-Hans.yml` 文件，修改 posted、visitors 等值为英文，如下：

``` 
post:
  created: 创建于
  modified: 更新于
  sticky: 置顶
  posted: Posted on #发表于
  visitors: Visitors #阅读次数 
  in: In #分类于
  read_more: 阅读全文
  untitled: 未命名
  toc_empty: 此文章未包含目录
  wordcount: 字数统计
  min2read: 阅读时长
  totalcount: Site words total count
```

 ### 遇到的问题

我在配置过程中有被官方文档坑了，目前猜测是官方文档没及时更新原因。在此，我记录下遇到的坑：

#### 1）菜单图标显示异常

问题：「首页」、「分类」、「标签」等这些菜单旁边的图标都显示是问号，未显示正常图标，我按照官方示例配置是这样的：

``` 
menu:
  home: / 
  categories: /categories/  
  tags: /tags/  
  archives: /archives/  
  about: /about/    
  #schedule: /schedule/ || calendar
  #sitemap: /sitemap.xml || sitemap
  #公益: /404/ || heartbeat

# Enable/Disable menu icons.    
menu_icons:
  enable: true
  home: home
  about: user
  categories: th
  tags: tags
```

网上很多文章写的都是上面那样的配置，但后来找到原因了，真正的配置是下面这样的：

```
menu:
  home: / || home
  archives: /archives || archive
  categories: /categories || th
  tags: /tags || tags
  about: /about || user
  
menu_icons:
  enable: true
```

原来 NexT 这个主题中的「菜单设置」被注释掉的那些配置样例，才是正确的配置。OS：官方文档真是坑人啊。

#### 2）友情链接图标显示异常

问题：「友情链接」图标未正常显示。

官方文档包括网上很多文章写的都是如下：

```
social:
  GitHub: https://github.com/yourname
  邮箱: mailto:test@gamil.com
social_icons:
  enable: true
  icons_only: false
  transition: false
  GitHub: github
  邮箱: envelope
```

但正确配置其实是如下，和菜单配置类似：

```
social:
  GitHub: https://github.com/yourname || github
  邮箱: mailto:test@gamil.com || envelope
social_icons:
  enable: true
  icons_only: false
  transition: false
```



## 二、进阶优化配置

添加第三方服务，官网文档：[第三方服务集成 - NexT 使用文档](https://theme-next.iissnan.com/third-party-services.html)。

- 评论系统
- 数据统计与分析
- 内容分享服务
- 搜索服务
- 其他服务

### (1) 在线联系（DaoVoice）

参考：  [hexo的next主题个性化教程:打造炫酷网站](http://shenzekun.cn/hexo%E7%9A%84next%E4%B8%BB%E9%A2%98%E4%B8%AA%E6%80%A7%E5%8C%96%E9%85%8D%E7%BD%AE%E6%95%99%E7%A8%8B.html)（含全站总字数、DaoVoice 在线联系等等）。

首先在 [DaoVoice](https://account.daocloud.io/signin) 注册账号，注册完成后会得到一个 app_id，记下这个 app_id 的值，然后打开 `/themes/next/layout/_partials/head.swig`，写下如下代码：

``` 
{% if theme.daovoice %}
  <script>
  (function(i,s,o,g,r,a,m){i["DaoVoiceObject"]=r;i[r]=i[r]||function(){(i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;a.charset="utf-8";m.parentNode.insertBefore(a,m)})(window,document,"script",('https:' == document.location.protocol ? 'https:' : 'http:') + "//widget.daovoice.io/widget/0f81ff2f.js","daovoice")
  daovoice('init', {
      app_id: "{{theme.daovoice_app_id}}"
    });
  daovoice('update');
  </script>
{% endif %}
```

接着打开主题配置文件，在最后写下如下代码：

``` 
# Online contact 
daovoice: true
daovoice_app_id: 这里填你的获得的 app_id
```

> *注1：安装成功后可以在 DaoVoice 控制台上的聊天设置里设置聊天窗口样式。*
>
> *注2：我的 DaoVoice 账户注册使用的 GitHub 账户。*

### (2) 评论Disqus和文章显示评论数——已更换为LeanCloud的Valine评论功能

Disqus 官网：https://disqus.com/ （本人使用的是谷歌账号注册和登录）

NexT 主题集成 Disqus 评论，可以打开 NexT 配置文件 `_config.yml` 搜索「disqus」可以找到。

一开始我采用了 Disqus 评论，操作参考：[Hexo 集成 Disqus 评论](http://www.cylong.com/blog/2017/03/26/hexo-next-disqus/)。在完成 Disqus 网站注册和配置后（如何配置就不说了，看链接），打开 NexT 主题配置文件 `config.yml` 文件。

①大于等于 5.1.1 版本，将 disqus 下的 enable 设定为 true，同时提供你的 shortname，count 用于指定是否显示评论数量：

``` 
disqus:
  enable: true
  shortname:
  count: true
```

> enable 和 count 都设置为 true 后，这样你的所有文章会显示评论数，及页面下面会自动加载 Disqus 的评论插件。 

②小于 5.1.1 版本，设定 disqus_shortname 的值即可：

``` 
disqus_shortname: shortname
```

接下来就可以进入后台管理设置你的评论了。

***——update：2019-02-14 已弃用 Disqus 评论。参考了知乎文章：[Hexo（NexT 主题）评论系统哪个好？ - 知乎](https://www.zhihu.com/question/267598518)，采用了  Valine，不用登陆就可以用。*** 

> *顺便提一下关于几个评论系统的介绍：多说和网易云已经倒下了，其次畅言需要备案，Disqus， Hypercomments 和 LiveRe 都是国外的，加载速度贼慢。*

***Valine 设置步骤：***

1. 先需要去注册一个账号：[Leancloud官网，点我注册](https://leancloud.cn/)

   注册完以后需要创建一个应用，名字可以随便起，然后 **进入应用 -> 设置 -> 应用key**，获取你的 appid 和 appkey。

2. 拿到你的 appid 和 appkey 之后，打开主题配置文件 `_config.yml` 搜索 valine，填入 appid 和 appkey。

我的配置：

   ``` 
valine:
    enable: true
    appid: 你的appid    
    appkey: 你的appkey 
    notify: false # mail notifier , https://github.com/xCss/Valine/wiki
    verify: false # Verification code
    placeholder: Just go go # comment box placeholder
    avatar: mm # gravatar style   
    guest_info: nick,mail,link # custom comment header
    pageSize: 10 # pagination size
   ```

另外：如果提示安全问题，请参考网上 [该文](https://11.tt/posts/2018/add-valine-to-your-blog/#%E9%85%8D%E7%BD%AE%E5%AE%89%E5%85%A8%E5%9F%9F%E5%90%8D) 添加安全域名。即在 Leancloud -> 设置 -> 安全中心 -> Web 安全域名，把你的域名加进去。

***(1) Valine邮件提醒***

Valine 官方提供的邮件提醒功能是基于`Leancloud的密码重置邮件提醒`，操作步骤如下：

进入 [Leancloud]() -> 选择你的评论所存放的`应用` -> `设置` -> `邮件模板`，按下图设置好用于`重置密码`的邮件主题>然后保存：

1. 修改邮件主题：`你在 的评论收到了新的评论`

2. 修改内容：将下面的代码复制到“内容”中，并将其中的`你的网址首页链接`改为你的网址首页链接。

   ``` html
   <p>Hi, {{username}}</p>
   <p>
       你在 {{appname}} 的评论收到了新的回复，请点击查看：
   </p>
   <p><a href="你的网址首页链接" style="display: inline-block; padding: 10px 20px; border-radius: 4px; background-color: #3090e4; color: #fff; text-decoration: none;">马上查看</a></p>
   ```

3. 点击“保存”按钮

4. 修改 NexT 主题配置文件，搜索 `valine`（快速定位），将其中的`notify`改为`true`。

设置完成后：

1. 发表评论需要像下面这样的验证

   ![](https://img-1256179949.cos.ap-shanghai.myqcloud.com/20190216212041.png)

2. 如果评论者 A 评论文章时候留下了邮箱，那么其他人比如 B，点击回复 A 的时候，那么 A 的邮箱就会收到相应的邮件通知，提示：

   ![](https://img-1256179949.cos.ap-shanghai.myqcloud.com/20190216212307.png)

   注意：点击查看，会跳转到评论的博客主页，而不是对应的评论文章。

注意事项：

``` xml
- 发送次数过多，可能会暂时被Leancloud 屏蔽邮件发送功能
- 由于`邮件提醒`功能使用的“Leancloud的密码重置邮件提醒”，只能传递`昵称`、`邮箱`两个属性，所以邮件提醒链接`无法直达指定文章页`。请悉知。
- 开启`邮件提醒`会默认开启`验证码`选项。
- 该功能目前还在测试阶段，谨慎使用。
- 目前`邮件提醒`正处于测试阶段，仅在`子级`对存在邮件地址的`父级`发表评论时发送邮件
```

参考：[NexT主题设置Valine评论系统邮件提醒](https://www.nhtzj.com/3315416634/)

***(2)文章显示评论数问题：*** 

**注意，换为  Valine 后，发现文章的评论数不显示，**尝试了改动某处看是否能解决问题，发现解决了。操作这样的：把 disqus 的评论关闭，即设置主题配置文件下的 disqus 下的 enable 为 false，即可正常显示评论数。

### (3)文章阅读次数（注： 使用的LeanCloud）

①打开 LeanCloud 官网，进入 [注册页面](https://leancloud.cn/login.html#/signup) 注册。完成邮箱激活后，点击头像，进入`控制台`页面，创建一个新应用(类型为`JavaScript SDK`)，点击应用进入；

②创建名称为 `Counter` 的 Class；

③修改配置文件，编辑网站根目录下的 `_config.yml` 文件，添加如下：

```
leancloud_visitors:
  enable: true
  app_id: 你的app_id
  app_key: 你的app_key
```

其中，app_id 和 app_key 在你所创建的应用的`设置->应用Key`中。

注：为了保证应用的统计计数功能仅应用于自己的博客系统，你可以在`应用->设置->安全中心`的`Web安全域名`中加入自己的博客域名，以保证数据的调用安全。

参考：

- [为NexT主题添加文章阅读量统计功能](https://notes.wanghao.work/2015-10-21-%E4%B8%BANexT%E4%B8%BB%E9%A2%98%E6%B7%BB%E5%8A%A0%E6%96%87%E7%AB%A0%E9%98%85%E8%AF%BB%E9%87%8F%E7%BB%9F%E8%AE%A1%E5%8A%9F%E8%83%BD.html#%E9%85%8D%E7%BD%AELeanCloud)
- [Hexo之NexT主题优化（4）-添加文章访问数和站点访问数](http://happywayq.com/Hexo%E7%9A%84NexT%E4%B8%BB%E9%A2%98%E4%BC%98%E5%8C%96-%E6%B7%BB%E5%8A%A0%E6%96%87%E7%AB%A0%E8%AE%BF%E9%97%AE%E6%95%B0%E5%92%8C%E7%AB%99%E7%82%B9%E8%AE%BF%E9%97%AE%E6%95%B0/)
- [Hexo的NexT主题个性化：添加文章阅读量](http://www.jeyzhang.com/hexo-next-add-post-views.html)

### (4 动态背景、点击出现桃心效果、去除文章底部带#号的标签、文章下面标签样式更改

修改模板 `/themes/next/layout/_macro/post.swig`，搜索 `rel="tag">#`，将`#`换成：

``` 
<i class="fa fa-tag"></i>
```

参考：[2018最新版Hexo博客Next主题6.0配置优化](https://blog.csdn.net/qq_32454537/article/details/79482896)

标签样式更改，打开 `\themes\next\source\css\_custom\custom.styl`，添加：

``` css
//文章下面的标签样式
.posts-expand .post-tags a{
	box-shadow:0 1px 3px rgba(0,0,0,.12), 0 1px 2px rgba(0,0,0,.24);
	transition:.2s ease-out;
	padding: 3px 5px;
	margin: 5px;
	background: #eee;
	border-bottom: none;
	border-radius: 10px;
	&:hover {
    color: $blue;
    //text-decoration: underline;
  }
}
```

### (5) 更改正文和代码的字体/更改内容区域的宽度

**(1) 更改正文和代码字体的样式和大小** 

NexT 从 5.0.1 版本开始提供一个字体定制特性。以下的修改将覆盖`source/css/_variables/base.styl`「字体定制」的特性。 编辑主题下的 `source/css/_variables/custom.styl` 文件，新增两个变量：

``` 
// 正文字体的大小
$font-size-base = 16px

// 代码字体的大小
$code-font-size = 14px
```

注1：代码字体我设置的为 14px，正文字体设置的为 16px，字体族设置的为 `$font-family-base = Lato,"PingFang SC","Microsoft YaHei",sans-serif`。

注2：关于代码大小设置，除了可以修改主题下的 `source/css/_variables/custom.styl` 文件，还可以通过修改同目录下的 `source/css/_variables/base.styl` 文件达到同一目的，base.styl 会覆盖 custom.style 的修改。

``` 
// Code & Code Blocks
// --------------------------------------------------
$code-font-family               = $font-family-monospace
$code-font-size                 = 15px
```

另外，代码大小设置还可以直接改样式文件``source/css/_common/_vendor/highlight/hilight.styl`：

``` 
$code-block
  background: highlight-background
  margin: 20px 0
  padding: 15px
  overflow: auto
  font-size 15px //$code-font-size;    // 改这里
  color: highlight-foreground
  line-height:  $line-height-code-block
```

参考：[代码字体大小怎么改？ · Issue #306 · iissnan/hexo-theme-next](https://github.com/iissnan/hexo-theme-next/issues/306)

**(2) 修改代码区主题** 

新版的 Next 主题卡得很严，需要这样修改。需要动的地方有：主题的 `_config.yml` 文件，站点的 `_config.yml` 文件。

先在站点的配置文件中，搜索`hightlight`：

``` xml
highlight:
  enable: true
  line_number: true
  auto_detect: false
  tab_replace:
```

文字自动检测默认不启动，所以改成 `true` 使其起作用。看英文应该能明白什么意思。解释下，line_number 表示是否显示代码行号，auto_detect 表示是否对未标识哪种语言的代码进行自动检测，tab_replace 表示是否替换 tab 为空格。附上一个关于 Hexo 的站点及主题配置文件常见配置项的中文解释 [Hexo 搭建个人博客 · 进阶篇](http://ruikye.com/2014/08/30/Hexo-%E6%90%AD%E5%BB%BA%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2-%C2%B7-%E8%BF%9B%E9%98%B6%E7%AF%87/)，我有摘录并放在本文附录部分。

注意：我有把 auto_detect 设置为了 true，但 `hexo s` 生成博客时报错：`TypeError: Cannot set property 'lastIndex' of undefined`，后来网上找到了同样遇到该问题的人，链接：[Hexo博客(12)使用google-code-prettify代码高亮 | masikkk](http://masikkk.com/article/hexo-12-google-code-prettify/)，根据文章说，将站点配置文件 `_config.yml` 中的 highlight 选项的 auto_detect 设为 false，完美解决。确实如此。

再到主题的配置文件找到 `highlight_theme: normal`，注释显示有五种显示主题可用，分别是：

```
normal
night
night eighties
night blue
night bright
```

选择什么要看个人审美了。

**(3) 更改内容区域的宽度** 

NexT 对于内容的宽度的设定如下：

- 700px，当屏幕宽度 < 1600px
- 900px，当屏幕宽度 >= 1600px
- 移动设备下，宽度自适应

如果你需要修改内容的宽度，同样需要编辑样式文件。 编辑主题的 `source/css/_variables/custom.styl` 文件，新增变量：

``` 
// 修改成你期望的宽度
$content-desktop = 700px

// 当视窗超过 1600px 后的宽度
$content-desktop-large = 900px
```

注，当你使用 Pisces 风格时可以用下面的方法，我即采用的如下设置：

``` 
//当你使用 Pisces 风格时可以用下面的方法，在 source/css/_variables/custom.styl 中添加
$main-desktop = 1200px
$content-desktop = 950px
```



参考官网文档：

- [常见问题 - NexT 使用文档](https://theme-next.iissnan.com/faqs.html)

### (6) 添加自定义菜单  

以新建「相册」菜单为例：在博客目录下的 source 文件夹下新建名为 photo 文件夹，然后在 photo 文件夹下新建一个 index.md 文件，然后在该文件填写：

``` 
---
title: 相册
date: 2018-04-16 22:14:07
type: "photo"
---
```

然后打开主题配置文件 `_config.yml`，在 menu 中添加：

```
menu:
  home: / || home
  archives: /archives || archive
  categories: /categories || th
  tags: /tags || tags
  #添加了「相册」菜单
  相册: /photo || camera
```

> *解释下：这里的「相册」是博客中显示的菜单名称，紧跟的 photo 要和前面 index.md 文件的 type 值一致，|| 后面的菜单的图标，图标名称来自于 [FontAwesome icon](http://fontawesome.io/icons/)，若没有配置图标，默认会使用问号图标。*

参考：[hexo高阶教程：next主题优化之加入网易云音乐、网易云跟帖、炫酷动态背景、自定义样式，打造属于你自己的定制化博客](https://juejin.im/post/58eb2fd2a0bb9f006928f8c7)

### (7) 添加音乐、视频

**1、添加单曲音乐**

进入 [网易云音乐](https://music.163.com/) 的官网，搜索歌曲，点开歌曲，点击「生成外链播放器」生成外链，直接拿来用就行。iframe 插件可以在代码中设置宽高等参数，auto 为设置是否自动播放，auto 设为 0 表示手动播放，为 1 表示自动播放。flash 不可以自己设置参数。

自动播放示例：

``` html
<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=350 height=86 src="//music.163.com/outchain/player?type=2&id=185678&auto=0&height=66"></iframe>
```

<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=350 height=86 src="//music.163.com/outchain/player?type=2&id=185678&auto=1&height=66"></iframe>



**2、添加歌单**

如果想要加入歌单，就需要找到歌单或者自己创建歌单，热后点击歌单，找到并点击进去「生成外链播放器」，其余操作就和上面一样了。不过，若歌单有变化的话，这个外链的歌曲同样跟着变。示例：

``` html
<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=530 height=450 src="//music.163.com/outchain/player?type=0&id=2637966813&auto=0&height=430"></iframe>
```

<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=530 height=450 src="//music.163.com/outchain/player?type=0&id=2637966813&auto=1&height=430"></iframe>

**3）添加视频**

打开视频网站，比如优酷、YouTube 等。以优酷为例，打开某个视频后，点击「分享」，再复制 iframe 代码粘贴到 Markdown 文章即可。示例：

``` html
<iframe height=498 width=510 src='http://player.youku.com/embed/XMTU0ODEwMzM3Ng==' frameborder=0 'allowfullscreen'></iframe>
```

### (8) 设置标题样式（为浅蓝色）

进入主题目录 `hexo\themes\next\source\css\_common\components\post\` 修改 `post.sty` 文件，在配置的后面添加下面的代码。该文件是博文的样式表。

``` 
/*添加下面的CSS代码来修改博客标题样式*/
.page-post-detail .post-title {
  font-size: 26px;
  text-align: center;
  word-break: break-word;
  font-weight: $posts-expand-title-font-weight
  background-color: #b9d3ee;
  border-radius:.3em;
  line-height:1em;
  padding-bottom:.12em;
  padding-top:.12em;
  box-shadow:2px 2px 7px #9fb6cd;
  +mobile() {
    font-size: 22px;
  }
}
/*添加上面的CSS代码来修改博客标题样式*/
@import "post-expand";
@import "post-collapse";
@import "post-type";
@import "post-title";
```

*注意：如果想把主页标题样式一同修改，可以用把 `.page-post-detail` 去掉。*

参考：[hexo框架基于next主题定制](http://www.aisun.org/2017/10/hexo-next+dingzhi/)（各种优化，很全面）

### (9) 设置文章封面图片

如果只是插入本地图片作为文章封面，即在博客首页的时候会显示文章的封面图片，进入这篇文章的详细页面后，将不显示这张图片。

按如下方式操作：

1）修改 `\themes\next\layout\_macro\post.swing` 文件。将如下代码复制：

```js
{% if post.summary_img  %}
  <div class="out-img-topic">
    <img src={{ post.summary_img }} class="img-topic">
  </div>
{% endif %}
```

添加到下图所示的位置:

![](https://neveryu.github.io/images/hexo-next-five-1.png)

2）在新建的文章添加一个字段属性：`summary_img`。`summary_img` 的值是图片的路径，如： 

```html
---
title: CSS 各种Hack手段
date: 2017-06-25 03:25:24
categories: 前端
tags: [CSS]
comments: false
summary_img: /images/css-hack-1.png
---
```

当然也可以不设置`summary_img`的图片路径，即也就不会显示封面图。

**PS：这里有个注意点，亲测，图片存放的文件夹只能新建在 `source` 目录下。**

参考文章：

- [Hexo 图片插入](http://www.xinxiaoyang.com/programming/2016-11-25-hexo-image-bug/)
- [Hexo-NexT搭建个人博客（五）——插入封面](https://neveryu.github.io/2017/07/15/hexo-next-five/) 

### (10) 网页加载进度条

打开 `/themes/next/layout/_partials/head.swig` 文件，在文件末尾添加如下代码：

``` 
<!-- 网页加载条 -->
<script src="https://neveryu.github.io/js/src/pace.min.js"></script>
```

然后，打开 `/themes/source/css/_custom/custom.styl` 文件，在文件末尾添加如下代码：

```
/*网页加载条*/
/* This is a compiled file, you should be editing the file in the templates directory */
.pace {
  -webkit-pointer-events: none;
  pointer-events: none;
  -webkit-user-select: none;
  -moz-user-select: none;
  user-select: none;
}

.pace-inactive {
  display: none;
}

.pace .pace-progress {
  background: #1e92fb;
  position: fixed;
  z-index: 2000;
  top: 0;
  right: 100%;
  width: 100%;
  height: 3px;
}

.pace .pace-progress-inner {
  display: block;
  position: absolute;
  right: 0px;
  width: 100px;
  height: 100%;
  box-shadow: 0 0 10px #e90f92, 0 0 5px #e90f92;
  opacity: 1.0;
  -webkit-transform: rotate(3deg) translate(0px, -4px);
  -moz-transform: rotate(3deg) translate(0px, -4px);
  -ms-transform: rotate(3deg) translate(0px, -4px);
  -o-transform: rotate(3deg) translate(0px, -4px);
  transform: rotate(3deg) translate(0px, -4px);
}

.pace .pace-activity {
  display: block;
  position: fixed;
  z-index: 2000;
  top: 15px;
  right: 15px;
  width: 14px;
  height: 14px;
  border: solid 2px transparent;
  border-top-color: #e90f92;
  border-left-color: #e90f92;
  border-radius: 10px;
  -webkit-animation: pace-spinner 400ms linear infinite;
  -moz-animation: pace-spinner 400ms linear infinite;
  -ms-animation: pace-spinner 400ms linear infinite;
  -o-animation: pace-spinner 400ms linear infinite;
  animation: pace-spinner 400ms linear infinite;
}

@-webkit-keyframes pace-spinner {
  0% { -webkit-transform: rotate(0deg); transform: rotate(0deg); }
  100% { -webkit-transform: rotate(360deg); transform: rotate(360deg); }
}
@-moz-keyframes pace-spinner {
  0% { -moz-transform: rotate(0deg); transform: rotate(0deg); }
  100% { -moz-transform: rotate(360deg); transform: rotate(360deg); }
}
@-o-keyframes pace-spinner {
  0% { -o-transform: rotate(0deg); transform: rotate(0deg); }
  100% { -o-transform: rotate(360deg); transform: rotate(360deg); }
}
@-ms-keyframes pace-spinner {
  0% { -ms-transform: rotate(0deg); transform: rotate(0deg); }
  100% { -ms-transform: rotate(360deg); transform: rotate(360deg); }
}
@keyframes pace-spinner {
  0% { transform: rotate(0deg); transform: rotate(0deg); }
  100% { transform: rotate(360deg); transform: rotate(360deg); }
}
/*网页加载条 END*/
```

参考：[Hexo-NexT搭建个人博客（五） | Never_yu's Blog](https://neveryu.github.io/2017/07/15/hexo-next-five/)

另外，还看到一个方法，参考：[Hexo-NexT配置超炫网页效果 - 简书](https://www.jianshu.com/p/9f0e90cc32c2)

> 编辑主题配置文件搜索`pace`，将其值改为`ture`就可以了，选择一款你喜欢的样式。
>
> ```
> # Progress bar in the top during page loading.
> pace: ture
> # Themes list:
> #pace-theme-big-counter
> #pace-theme-bounce
> #pace-theme-barber-shop
> #pace-theme-center-atom
> #pace-theme-center-circle
> #pace-theme-center-radar
> #pace-theme-center-simple
> #pace-theme-corner-indicator
> #pace-theme-fill-left
> #pace-theme-flash
> #pace-theme-loading-bar
> #pace-theme-mac-osx
> #pace-theme-minimal
> # For example
> # pace_theme: pace-theme-center-simple
> pace_theme: pace-theme-minimal
> ```

### (11) 底部：显示(或隐藏)底部"强力驱动"和版本

打开 `themes/next/_config.yml` 文件，将 `powered` 设置为 `true`， 显示“强力驱动”；将 `enable` 设置为 `true`，显示版本信息。

``` diff
# 页脚
footer:
  # Specify the date when the site was setup.
  # If not defined, current year will be used.
  since: 2018

  # Icon between year and copyright info.
  # icon: user
  icon: sun-o

  # If not defined, will be used `author` from Hexo main config.
  copyright:
  # -------------------------------------------------------------
  # Hexo link (Powered by Hexo).
-  powered: true
+  powered: false
  theme:
    # Theme & scheme info link (Theme - NexT.scheme).
-    enable: true
+    enable: false
    # Version info of NexT after scheme info (vX.X.X).
    version: true
```

参考：[Hexo+NexT 打造一个炫酷博客 - 掘金](https://juejin.im/post/5bcd2d395188255c3b7dc1db#heading-52)（各种定制优化，非常全面）

如果需要修改，可以参考下节 (12) 的内容。

### (12) 底部：设定站点建立时间和作者名称

(1) 设定站点建立时间

这个时间将在站点的底部显示，例如 `© 2013 - 2015`。编辑主题配置文件 `_config.yml`，新增字段 `since`：

``` 
since: 2013
```

其中，网站页面会在 `-` 后面的年份会自动根据当前年份显示。参考：[设定站点建立时间 · iissnan/hexo-theme-next Wiki](https://github.com/iissnan/hexo-theme-next/wiki/%E8%AE%BE%E5%AE%9A%E7%AB%99%E7%82%B9%E5%BB%BA%E7%AB%8B%E6%97%B6%E9%97%B4)

(2) 修改站点时间后面的作者名称

找到 `\themes\next\layout\_partials\`下面的`footer.swig`文件，打开可以发现如下语句：

![](https://img-1256179949.cos.ap-shanghai.myqcloud.com/20190216135929.png)

第一个框，是底部的站点时间后面的作者名称，如果想加东西，一定要在双大括号外面写。如：`xxx{{config.author}}`，当然你要是想改彻底可以变量都删掉，看个人意愿。

***(3) 顺带补充其他——修改底部"强力驱动"和版本信息***

第二个框，是底部的 “由Hexo驱动” 的 Hexo 链接，先给删掉防止跳转，如果想跳转当然也可以自己写地址，至于中文一会处理。注意删除的时候格式不能错，只把`<a>`标签这部分删除即可，留着两个单引号''，否则会出错。在我所使用的 next 版本删除 `<a>` 标签后结果如下：

``` xml
{% if theme.footer.powered %}
  <div class="powered-by">{#
  #}{{ __('footer.powered', '') }}{#
#}</div>
{% endif %}
```

第三个框，是更改底部的“主题-Next.XX”，这个比较爽直接将`-` 后面`</div>` 之前的都删掉，，删掉之后在上一行 `-` 后面可以随意加上你想显示的东西，不要显示敏感信息哟，请自重。在我所使用的 next 版本删除 `-` 后面的对应代码的结果如下：

``` 
{% if theme.footer.theme.enable %}
  <div class="theme-info">{#
  #}{{ __('footer.theme') }} &mdash; </div>
{% endif %}
```

注意，我这里的`&mdash;` 对应 `-`， 这里后面可以加上自己想要添加的内容，比如：

``` html
<a herf="https://pages.github.com/">Hosted By GitHub Page</a>
```

接下来，处理剩余的中文信息。找到这个地方` \themes\next\languages\ ` 下面的语言文件zh-Hans.yml（这里以中文为例，有的习惯用英文的配置文件，道理一样，找对应位置即可） 打开之后，如图：

![](https://img-1256179949.cos.ap-shanghai.myqcloud.com/20190216143647.png)

看到了吧，这个就是传值传过去的，你想显示什么就在这里面大肆的去改动吧。其实在第二个框中，就可以把值都改掉，不用接受传值的方式，完全自己可以重写。不过我不建议那样做，因为传值这样只要是后续页面需要这几个值那么就都会通过取值去传过去，要是在刚才 footer 文件中直接写死，后续不一定哪个页面需要传值，但是值为空了或者还是原来的，可就尴尬了。所以还是这样改动吧。

参考：[Hexo Next底部powered by的logo栏更改以及注意事项（附官方文档,文末有福利链） - 掘金](https://juejin.im/post/5b440ba251882519f6475079)

### (13) 底部：添加网站已运行时间

在`themes/layout/_parrials/footer.swing` 中添加：

``` js
<!--添加网站的运行时间-->
<span id="sitetime"> <br></span>
<script language="javascript">
	function siteTime(){
		window.setTimeout("siteTime()", 1000);
		var seconds = 1000
		var minutes = seconds * 60
		var hours = minutes * 60
		var days = hours * 24
		var years = days * 365

		var today = new Date()
		var todayYear = today.getFullYear()
		var todayMonth = today.getMonth()
		var todayDate = today.getDate()
		var todayHour = today.getHours()
		var todayMinute = today.getMinutes()
		var todaySecond = today.getSeconds()
		var t1 = Date.UTC(2017,4,18,11,00,00)
		var t2 = Date.UTC(todayYear,todayMonth,todayDate,todayHour,todayMinute,todaySecond)
		var diff = t2-t1

		var diffYears = Math.floor(diff/years)
		var diffDays = Math.floor((diff/days)-diffYears*365)
		var diffHours = Math.floor((diff-(diffYears*365+diffDays)*days)/hours)
		var diffMinutes = Math.floor((diff-(diffYears*365+diffDays)*days-diffHours*hours)/minutes)
		var diffSeconds = Math.floor((diff-(diffYears*365+diffDays)*days-diffHours*hours-diffMinutes*minutes)/seconds)
		document.getElementById("sitetime").innerHTML=" 本站已运行"+diffYears+" 年 "+diffDays+" 天 "+diffHours+" 小时 "+diffMinutes+" 分钟 "+diffSeconds+" 秒<br>"
	}
	siteTime()
</script>
```

参考：[Hexo和Next主题的相关设置（持续更新） - 简书](https://www.jianshu.com/p/3a01cc514ce7)

### (14) 底部：添加访问人数和访问量(使用的不蒜字统计)、全站总字数

**(1) 添加人数和访问量**

不蒜子是号称极简网页计数器，事实上也是如此，仅仅需要两步即可完成统计，分别为引入不蒜子 JS 和显示统计数，为访问量统计与访问人数统计。

①引入不蒜子 JS

打开 `\themes\next\layout_partials\footer.swig` 文件，在顶部添加如下代码：

``` js
<script async src="https://dn-lbstatics.qbox.me/busuanzi/2.3/busuanzi.pure.mini.js"></script>
```

②显示统计数

*访问量统计：*

算法a：pv 的方式，单个用户连续点击 n 篇文章，记录 n 次访问量。

``` html
<span id="busuanzi_container_site_pv">
    本站总访问量<span id="busuanzi_value_site_pv"></span>次
</span>
```

*访问人数统计：*

算法b：uv的方式，单个用户连续点击 n 篇文章，只记录 1 次访客数。

``` html
<span id="busuanzi_container_site_uv">
  本站访客数<span id="busuanzi_value_site_uv"></span>人次
</span>
```

接着在合适的地方添加需要显示的统计数字代码（同上文件），我是在如下位置添加的：

``` xml
<!-- 不蒜字统计 -->
<div>
	<i class="fa fa-user-md"></i>
	<span id="busuanzi_container_site_uv">
	  访问人数：<span id="busuanzi_value_site_uv"></span>
	</span>&nbsp;|&nbsp;
	
	<i class="fa fa-eye"></i>
	<span id="busuanzi_container_site_pv">
	  总访问量：<span id="busuanzi_value_site_pv"></span>
	</span>&nbsp;|&nbsp;
	
	<!-- 添加博客全站总字数统计-->
	<i class="fa fa-pencil"></i>
	<span class="post-count">博客全站共 {{ totalcount(site) }} 字</span>
</div>
	
{% if theme.footer.custom_text %}
  <div class="footer-custom">{#
  #}{{ theme.footer.custom_text }}{#
#}</div>
{% endif %}
```

*注：之前就是使用的该方式添加的访问人数、访问量，但后来发现博客并不显示了，猜测可能是服务商关闭或是别的什么问题。* 

参考：

- [Hexo+Github博客小功能之添加不蒜子访问统计](https://blog.csdn.net/FanLinXi_WuXi/article/details/81988904)
- [Hexo搭建属于自己的博客](https://www.zxpblog.cn/2018/08/11/Hexo%E6%90%AD%E5%BB%BA%E5%8D%9A%E5%AE%A2/) 

**(2) 添加博客全站字数统计**

添加单篇文章的字数统计，参考「(3) 添加文章字数统计、阅读时长（next主题已经集成）」小节内容。

底部添加全站总字数，方法类似。先安装：`npm install hexo-wordcount --save`，打开 `/themes/next/layout/_partials/footer.swig` 在合适位置添加相应代码，我的和不蒜字统计在一起。

添加在别的地方，参考：[Hexo-NexT配置超炫网页效果 - 简书](https://www.jianshu.com/p/9f0e90cc32c2)

**!!!最后，根据 (11)、(12)、(13) 、(14) 节的的修改后的结果：**

![](https://img-1256179949.cos.ap-shanghai.myqcloud.com/20190216134149.png)

### (15) 设置文章加密访问

打开 `themes/next/layout/_partials/head.swig`文件，在 ``之前插入代码：

``` js
<script>
    (function(){
        if('{{ page.password }}'){
            if (prompt('请输入密码') !== '{{ page.password }}'){
                alert('密码错误');
                history.back();
            }
        }
    })();
</script>
```

然后写文章时加上`password: xxx`，如：

``` 
---
title: 2018
date: 2018-10-25 16:10:03
password: 123456
---
```

参考：[最全Hexo博客搭建+主题优化+插件配置+常用操作+错误分析 | 遇见西门](https://www.simon96.online/2018/10/12/hexo-tutorial/)（非常全面~）

### (16) 文章末尾添加"本文结束"标记/文章末尾追加版权信息

参考：[Hexo+NexT 打造一个炫酷博客 - 掘金](https://juejin.im/post/5bcd2d395188255c3b7dc1db#heading-52)

### (17) 取消文章目录对标题的自动编号和取消目录

(1) 取消文章目录对标题的自动编号

修改 NexT 主题配置文件 `_config.yml`，搜索  `number` ，值改为 `false`。

(2) 取消目录

如果想干脆取消目录，修改 NexT 主题配置文件 `_config.yml`，搜索  `toc:` ，修改 toc 下的 enable 值改为 `false`。

``` 
toc:
  enable: false

  number: false
```

参考：[hexo的NexT主题，怎么取消“文章目录”对标题的自动编号？](https://segmentfault.com/q/1010000008494901)

### (18) 在右上角或者左上角实现fork me on github

点击 [这里](https://github.com/blog/273-github-ribbons) 或者 [这里](http://tholman.com/github-corners/) 挑选自己喜欢的样式，并复制代码。 例如，我是使用的一款右上角的，复制如下代码：

![](https://img-1256179949.cos.ap-shanghai.myqcloud.com/20190216021508.png)

然后粘贴刚才复制的代码到 `themes/next/layout/_layout.swig` 文件中（放在 `<div class="headband"></div>` 的下面），并把 `href` 改为你的 GitHub 地址。

参考：[hexo的next主题个性化配置教程 - SegmentFault 思否](https://segmentfault.com/a/1190000009544924)

### (19) 底部大改版：添加自定义版权等信息、访问人数/次、网站运行时间、修改底部的桃心

注：已对「(12) 设定站点建立时间」、「(13) 添加网站已运行时间」做的修改做了更换；以及隐藏了底部"强力驱动"和版本内容（如何隐藏见该文 (11) 节操作）。

**(1) 底部添加自定义版权信息** 

![](https://img-1256179949.cos.ap-shanghai.myqcloud.com/20190216155259.png)

> *注：如上，左侧是之前的，右侧是修改后的。* 

打开 `\themes\next\layout\_partials\` 文件夹下的 `footer.swig` 文件。现把修改后的代码摘入如下，方便复制：

``` xml
<div class="copyright">{#
#}{% set current = date(Date.now(), "YYYY") %}{#
#}<font color=black face=STLiti>Copyright &nbsp;</font><font color=black>&copy;</font> {% if theme.footer.since and theme.footer.since != current %}<font color=black face=STLiti>{{ theme.footer.since }} - </font>{% endif %}{#
#}<font color=black face=STLiti><span itemprop="copyrightYear">{{ current }}</span></font>
  <span class="with-love">
    <i class="fa fa-{{ theme.footer.icon }}"></i>
  </span>
  <span class="author" itemprop="copyrightHolder" style="font-family:STLiti;color:black;">{{ theme.footer.copyright || config.author }} . All Rights Reserved.</span>

  {% if theme.post_wordcount.totalcount %}
    <span class="post-meta-divider">|</span>
    <span class="post-meta-item-icon">
      <i class="fa fa-area-chart"></i>
    </span>
    {% if theme.post_wordcount.item_text %}
      <span class="post-meta-item-text">{{ __('post.totalcount') }}&#58;</span>
    {% endif %}
    <span title="{{ __('post.totalcount') }}">{#
    #}{{ totalcount(site, '0,0.0a') }}{#
  #}</span>
  {% endif %}
</div>
```

这是效果：![](https://img-1256179949.cos.ap-shanghai.myqcloud.com/20190216155600.png)

这里使用的是「华文隶书」字体，你也可以通过修改`face=STLiti` 换为别的字体。要注意的是，当你这里使用了「华文隶书」字体，别人访问该网页的电脑或手机若没有安装该字体，则不会显示此字体样式。我自己在手机端访问，就发现不会显示此字体样式。

**但倘若是想要别人在没有安装「华文隶书」字体的电脑或手机上显示该字体样式，有办法吗？**答案是有的。只需要把该字体 ttf 文件放在 NexT 主题源码中，比如 `\themes\next\source\images\` 文件夹下，然后打开 `\themes\next\source\css\_custom\custom.styl` 文件，添加：

``` xml
//压缩的字体
@font-face {
	font-family: STLiti;
	src: url("/images/STLITI.TTF");
}
```

即可。

> 这里提下，电脑安装了 Office， 会自动安装一些字体，包括「华文隶书」。如何安装字体：[下载和安装自定义字体以便在 Office 中使用 - Office 支持](https://support.office.com/zh-cn/article/%E4%B8%8B%E8%BD%BD%E5%92%8C%E5%AE%89%E8%A3%85%E8%87%AA%E5%AE%9A%E4%B9%89%E5%AD%97%E4%BD%93%E4%BB%A5%E4%BE%BF%E5%9C%A8-office-%E4%B8%AD%E4%BD%BF%E7%94%A8-0ee09e74-edc1-480c-81c2-5cf9537c70ce)
>
> - 方法1：双击下载好的 ttf 文件，点击「安装」即可。
> - 方法2：复制下载好的 ttf 文件，粘贴到 `C:\Windows\Fonts` 会自动安装字体。
>
> 卸载字体：进入 `C:\Windows\Fonts` 选择需要卸载的字体删除即可。

**(2) 底部添加访问人数、人次，全站总字数，以及网站运行时间**

打开 `\themes\next\layout\_partials\` 文件夹下的 `footer.swig` 文件，添加如下内容：

``` js
<!--此处为建站时间 -->
    <script>
    var now = new Date(); 
function createtime() { 
    var grt= new Date("04/17/2017 20:01:01");
    now.setTime(now.getTime()+250); 
    days = (now - grt ) / 1000 / 60 / 60 / 24; dnum = Math.floor(days); 
    hours = (now - grt ) / 1000 / 60 / 60 - (24 * dnum); hnum = Math.floor(hours); 
    if(String(hnum).length ==1 ){hnum = "0" + hnum;} minutes = (now - grt ) / 1000 /60 - (24 * 60 * dnum) - (60 * hnum); 
    mnum = Math.floor(minutes); if(String(mnum).length ==1 ){mnum = "0" + mnum;} 
    seconds = (now - grt ) / 1000 - (24 * 60 * 60 * dnum) - (60 * 60 * hnum) - (60 * mnum); 
    snum = Math.round(seconds); if(String(snum).length ==1 ){snum = "0" + snum;} 
    document.getElementById("timeDate").innerHTML =dnum+"&thinsp;天"; 
    document.getElementById("times").innerHTML = hnum + "&thinsp;时" + mnum + "&thinsp;分" + snum + "&thinsp;秒"; 
} 
setInterval("createtime()",250);
</script>
```

再打开 `\themes\next\layout\_third-party\analytics\` 文件夹下的 `busuanzi-counter.swig` 文件，删除全部内容，粘贴如下代码：

``` xml
{% if theme.busuanzi_count.enable %}
<div class="busuanzi-count">
  <script src="https://busuanzi.ibruce.info/busuanzi/2.3/busuanzi.pure.mini.js"></script>

  {% if theme.busuanzi_count.total_visitors %}
    <font color=DarkSlateGray face=STLiti><span class="site-uv" title="访问人数">
      <i class="fa fa-{{ theme.busuanzi_count.total_visitors_icon }}"></i>
      <span class="busuanzi-value" id="busuanzi_value_site_uv"></span>人次
    </span><span class="post-meta-divider">|</span></font>
    <font color=DarkSlateGray face=STLiti>
    <span title="总字数"><i class="fa fa-edit"></i>&ensp;<span class="post-count">{{ totalcount(site) }}</span>字,</span>
    <span id="timeDate" title="网站运行时间">载入天数...</span><span id="times" title="网站运行时间">载入时分秒...</span><span class="post-meta-divider">|</span>
    </font>
  {% endif %}

  {% if theme.busuanzi_count.total_views %}
    <font color=DarkSlateGray face=STLiti><span class="site-pv" title="总访问量">
      <i class="fa fa-{{ theme.busuanzi_count.total_views_icon }}"></i>
      <span class="busuanzi-value" id="busuanzi_value_site_pv"></span>次
    </span></font>
  {% endif %}
</div>
{% endif %}
```

> *注：这里同上一样，使用了「华文隶书」字体。*   

最后在打开 next 主题配置文件 `_config.yml` 找到 busuanzi_count，修改为如下：

``` xml
busuanzi_count:
  enable: true
  total_visitors: true
  total_visitors_icon: user #图标
  total_views: true
  total_views_icon: eye
  post_views: false
  post_views_icon: eye
```

记得 enable 设置为 true。

**(3) 备案信息**

打开 `/themes/next/layout/_layout.swig` 文件，添加如下代码：

![](https://img-1256179949.cos.ap-shanghai.myqcloud.com/20190216161815.png)

> *注：如上，左侧是之前的，右侧是添加的代码。* 

现把添加后的代码摘入如下，方面复制：

``` xml
<div class="footer-inner">
    {% include '_partials/footer.swig' %}
    {% include '_third-party/analytics/analytics-with-widget.swig' %}
    <!--备案等自定义↓-->

    <div style="font-family:STLiti;display:inline-block;height:20px;line-height:20px;">
        <a target="_blank" href="" ><img src="/images/gov.png" style="float:left;"/>赣公网安备 xxxxxxxxxxxx号</a>
        <span class="post-meta-divider" style="color: #555;">|</span><span><a href="http://www.miitbeian.gov.cn" target="_blank">赣ICP备xxxxx号</a></sapn>
    </div> 

    {% block footer %}{% endblock %}
</div>
```

*其中，备案信息开头的图片存放在 `\themes\next\source\images\` 文件夹下。*

效果：![](https://img-1256179949.cos.ap-shanghai.myqcloud.com/20190216162228.png)

!!!最后的博客底部效果，如下图： 

![](https://img-1256179949.cos.ap-shanghai.myqcloud.com/20190216174015.png)

如果没有备案，不想底部显示备案信息，可以考虑显示其他，比如相同位置添加如下代码：

``` xml
<!--版权等自定义↓-->

<div style="font-family:Courier New;display:inline-block;height:20px;line-height:20px;">
    Powered by <a target="_blank" href="https://hexo.io/zh-cn/index.html">Hexo</a>,Theme by 
    <a target="_blank" href="https://theme-next.iissnan.com/">NexT</a>. 
    Hosted by <a target="_blank" href="https://pages.github.com/">GitHub Page</a>
</div>
```

**!!!最后博客底部效果，如图：**

![](https://img-1256179949.cos.ap-shanghai.myqcloud.com/20190216185828.png)

**(4) 修改底部的桃心**

打开 `\themes\next\layout\_partials\footer.swig` 文件，修改：

``` html
<span class="with-love">
    <i class="fa fa-{{ theme.footer.icon }}"></i>
</span>
```

修改为：

``` html
<span class="with-love" id="animate" style="font-size: 13px">
	<i class="fa fa-heart"></i>
</span>
```

然后再打开 `\themes\next\source\css\_common\components\footer\footer.styl` 文件，在相应处添加或修改为如下：

``` css
if hexo-config('footer.icon.animated') {
	#animate {
    animation: iconAnimate 1.88s ease-in-out infinite;
	}
}

.with-love {
  display: inline-block;
  margin: 0 5px;
  color: #9a6eac;
}
```



### (20) 左侧添加社交链接和协议

打开 next 主题配置文件`_config.yml` ，找到 social_icons，设置 icons_only 和 transition 为 true：

``` xml
social_icons:
  enable: true
  icons_only: true # false
  transition: true  # false
```

然后 `hexo s` 预览可以看到：

![](https://img-1256179949.cos.ap-shanghai.myqcloud.com/20190216165239.png)

再打开 `\themes\next\layout\_macro\` 文件夹下的 `sidebar.swig` 文件，在如下两处添加代码：

![](https://img-1256179949.cos.ap-shanghai.myqcloud.com/20190216165438.png)

![](https://img-1256179949.cos.ap-shanghai.myqcloud.com/20190216165514.png)

> *注：如上，左侧是之前的，右侧是修改后的。* 

先把两处改动摘入如下：

``` xml
<span class="links-of-author-item">
    <! --增加的下面这行 悬浮显示文字-->
    {% set sidebarURL = link.split('||')[0] | trim %} 
    <a href="{{ link.split('||')[0] | trim }}" target="_blank" title="{{ name + ' &rarr; ' + sidebarURL }}">
```

```xml
{% endif %}

<! --增加的下面这部分，知识共享协议 -->
{% if theme.sidebar.copyright %}
<div class="cc-license motion-element" itemprop="license"><a href="https://creativecommons.org/licenses/by-nc-sa/4.0/" class="cc-opacity" rel="external nofollow noopener noreferrer" target="_blank"><img src="/images/cc-by-nc-sa.svg" alt="Creative Commons"></a></div>
{% endif %}

{# Blogroll #}
```

其中，svg 文件存放在 `\themes\next\source\images\` 文件夹下。

效果：![](https://img-1256179949.cos.ap-shanghai.myqcloud.com/20190216171849.png)

### (21) 关于页面样式的修改，如链接的颜色、回顶部按钮样式、底部页码等等

打开 `\themes\next\source\css\_custom\` 文件夹下的 `custom.styl` 文件，添加如下内容，修改内容已有注释写明：

``` 
// 更改文中链接的颜色
.post-body a {
  color: $orange;
  text-decoration: none;
  border-bottom: 1;
  &:hover {
    color: $blue;
    //text-decoration: underline;
  }
}

// 右下角返回顶部按钮样式
.back-to-top:hover {
    color: rgb(136, 255, 13);
	background-color: rgba(0, 0, 0, 0.75); //black
}

// 文章```代码块顶部样式
.highlight figcaption {
    margin: 0em;
    padding: 0.5em;
    background: #eee;
    border-bottom: 1px solid #e9e9e9;
}
.highlight figcaption a {
    color: rgb(80, 115, 184);
}


//修改文章内code样式
code {color:#c7254e;background:#f9f2f4;border:1px solid #d6d6d6;}

// [Read More]按钮样式: 黑底绿字
.post-button .btn:hover {
	
    color: rgb(136, 255, 13) !important;
	background-color: rgba(0, 0, 0, 0.75); //black
}

// 页面底部页码
.pagination .page-number.current {
	
    border-radius: 100%;
    background-color: rgba(100, 100, 100, 0.75);
}
// 页面底部页码, 去除鼠标置于上方时，数字上方的线
.pagination .prev, .pagination .next, .pagination .page-number {
    margin-bottom: 10px;
    border: none;
	color: rgb(1, 1, 1);
}

// 页面底部页码，鼠标置于上方，黑底绿字
.page-number:hover,.page-number:active{
	color: rgb(136, 255, 13);
	border-radius: 100%;
    //background-color: rgba(255, 0, 100, 0.75); //品红
	background-color: rgba(0, 0, 0, 0.75); //black
}
```

关于页面的很多设置都可以在此设置。

除了上面这些，我还设置了其他很多，比如页面底部页码、网页加载条、返回顶部按钮、左侧信息栏等样式。可参考：[Vincentqyw的custom.styl](https://github.com/Vincentqyw/blog-code/blob/master/themes/next/source/css/_custom/custom.styl)、[Lruihao的custom.styl](<https://github.com/Lruihao/lruihao.github.io/blob/hexo/themes/next/source/css/_custom/custom.styl>)。

另外在网上有看到别人的博客有个页面效果——文章之间、以及文章与下面分页之间有隔横，这个效果样式一直想拿到，觉得那样的更好看。后面联系到了博客作者，问了这事，他说是用的最新版的 NexT 主题，默认就是这样。再然后我找到了 NexT 版本更新说明的博客网站 [NexT – Theme for Hexo](https://theme-next.org/) 发现它也是那样的效果（最新源码：[hexo-theme-next](https://github.com/theme-next/hexo-theme-next/tree/v6.0.6)），看来真是新版 NexT 默认样式。前端我只会一点，不会改啊，只能这样了，日后有时间在探究吧~

> 2019-06-16 更新：现在知道了，只需要在主题配置文件设置 scheme 为 Gemini 即可。

### (22) 更换博客背景图

打开 `\themes\next\source\css\_custom\` 文件夹下的 `custom.styl` 文件，添加如下代码：

``` css
//背景图
body { 
    background-image: url(/images/background.jpg);
    background-attachment: fixed; // 不随屏幕滚动而滚动fixed,scroll,inherit
    background-repeat: no-repeat; // 如果背景图不够屏幕大小则重复铺，改为no-repeat则表示不重复铺
    background-size: cover; // contain等比例铺满屏幕 //cover拉伸铺满
    background-position: bottom;//x,y轴调整
    +mobile(){
      //background-position: 0% -20%;https://i.loli.net/2018/12/29/5c270a0523154.jpg
      //https://i.loli.net/2018/12/29/5c270fc2bfcad.png
      background-image: url(https://ziyuan.lruihao.cn/images/bg_cell.png);
      background-size: cover;
    }
}
```

其中，背景图片为 background-image 后面的 url 地址，即存放在 `\themes\next\source\images\` 文件夹下。

### (23) 设置博客的图标favicon

第一步：首先要有一个常见格式名（如`.jpg`, `.png`等）的图片作为备选 favicon，选择一个 favicon 制作网站完成制作，例如 [FavIcon from Pics](http://favicon.htmlkit.com/favicon/)、[比特虫](http://www.bitbug.net/)、[favicon制作 - 在线工具](https://tool.lu/favicon/)，最好设置为 32x32，除了自己制作，当然也可以去一些网站上找，如：[EasyIcon](http://www.easyicon.net/)。

第二步：将`favicon.ico`文件放在网站根目录下的 source 文件夹，如 `/themes/next/source/images` 文件夹下，并且修改配置文件：

``` xml
favicon:
  small: /images/favicon-16x16-next.png #小图标 默认的NexT
  medium: /images/favicon.ico	#中图标 默认NexT
  apple_touch_icon: /images/apple-touch-icon-next.png #苹果触摸图标
  safari_pinned_tab: /images/logo.svg #safari固定标签
```

可以看到有四种效果，一般我们只需将 medium 换成我们自己图标路径就行了。然后刷新网站，就可以看到效果了。效果：<img src="https://img-1256179949.cos.ap-shanghai.myqcloud.com/20190218151352.png"/>

参考：[关于Hexo6.0搭建个人博客(进阶篇)](https://segmentfault.com/a/1190000014676320)

### (24) 文章标题下显示评论或Comments字样

打开：`\themes\next\layout\_macro\post.swig` 文件，搜索 `<span class="post-meta-item-icon">`，在所有搜索到的该 span 标签下添加：

``` html
<span class="post-meta-item-text">评论：</span>
```

或者：（看自个想要中文还是英文字眼显示）

``` html
<span class="post-meta-item-text">Comments：</span>
```

因为我用的是 valine 评论，所以我也可以只在 valine 下添加如上代码。

```html
{% elseif theme.valine.enable and theme.valine.appid and theme.valine.appkey %}
<span class="post-comments-count">
    <span class="post-meta-divider">|</span>
    <span class="post-meta-item-icon">
        <i class="fa fa-comment-o"></i>
    </span>
    <span class="post-meta-item-text">Comments：</span>
    <a href="{{ url_for(post.path) }}#comments" itemprop="discussionUrl">
        <span class="post-comments-count valine-comment-count" data-xid="{{ url_for(post.path) }}" itemprop="commentCount"></span>
    </a>
</span>
{% endif %}
```

不过还是建议在搜索到的该标签下都添加，以防今后换别的评论系统不显示。

### (25) 设置文章标题下的发表、分类、访问次数、文章字数、阅读时间等为英文

打开 `\themes\next\languages\zh-Hans.yml`，在 post 下相应处修改为如下：

``` xml
post:
  created: Post created #创建于
  modified: Post modified #更新于
  sticky: 置顶
  posted: Posted on #发表于
  visitors: Visitors #阅读次数 
  in: In #分类于
  read_more: 阅读全文
  untitled: 未命名
  toc_empty: 此文章未包含目录
  wordcount: Words #字数统计
  min2read: Reading time #阅读时长
  totalcount: Site words total count
```

注：`#` 为注释。

### (26) 设置文章加密

参考：[next 主题添加密码访问 | YouForever](<https://www.zhyong.cn/posts/68c4/>)，使用的插件 hexo-blog-encrypt  地址：<https://github.com/MikeCoder/hexo-blog-encrypt>



### (99) 第三方服务整合的比较全面的DEMO欣赏

- [博採眾長](https://lruihao.cn/)

  > 「关于」页面特别地还有个网易音乐播放，不错，另外，博客最底部的优化的不错，打算借鉴。

- [Vincent Qin](https://www.vincentqin.tech/)

- [wustxiao's blog](http://wustxiao.cn/)

- [Zack's Blog](http://www.aisun.org/)

- [进击的学霸的博客](https://l-cw.github.io/)



## 三、博客速度/SEO优化

### (1) SEO

参考：[hexo 博客 seo 优化](https://segmentfault.com/a/1190000009254968)

### (2) 速度优化

*注：关于访问速度优化，本人还未实践…* 

参考：

- [Hexo博客-Next性能优化之路 | Waber's Blog](http://waberyang.com/2017/03/12/Hexo%E5%8D%9A%E5%AE%A2-Next%E6%80%A7%E8%83%BD%E4%BC%98%E5%8C%96%E4%B9%8B%E8%B7%AF/)
- [Hexo博客之速度优化 - 简书](https://www.jianshu.com/p/93b63852f0b3)
- [hexo next主题深度优化(六)，使用hexo-neat插件压缩页面，大幅度提升页面性能和响应速度](https://blog.csdn.net/dataiyangu/article/details/84963491)



## 四、主题制作

- [从零开始制作 Hexo 主题](http://www.ahonn.me/2016/12/15/create-a-hexo-theme-from-scratch/)
- [写一个自己的Hexo主题](https://segmentfault.com/a/1190000006057336)



## 附录-配置文件说明

Hexo 的各种通用的配置都是在博客根目录行下的 `_config.yml` 文件中设置的。下面介绍一些常用的配置项：

``` xml
# Site 基本信息
title: Ruikye                      # 博客标题，如左上角显示
subtitle: ruikye 的个人博客         # 博客副标题
description: 移动开发技术分享博客     # 用于搜索引擎搜索到的描述信息
author: 零雨の夜                    # 博客署名，一般会现在在博客的最下方，rg: &copy;2014 零雨の夜
email: xxx@xxx.com                # 可不填
language: zh-CN                   # 让博客支持中文
...
# Writing
...
highlight:              # 代码高亮
  enable: true          # 开启代码高亮
  line_number: false    # 是否显示行号
  tab_replace: true     # 是否替换 tab 为空格
...
# Pagination
## Set per_page to 0 to disable pagination
per_page: 1             # 文章分页时，每页最多显示文章数，eg: 我的博客在首页和归档页最多只显示一篇文章
pagination_dir: page    # 分页目录
...
# Extensions
## Plugins: https://github.com/hexojs/hexo/wiki/Plugins
## Themes: https://github.com/hexojs/hexo/wiki/Themes
theme: bs-light         # 这里配置博客的主题风格，主题安装在 themes/ 目录下，这里的值就是主题的文件夹名字 
exclude_generator:
plugins:
- hexo-generator-feed   # 安装、启用的插件，这里是启动 RSS 订阅的插件
# Deployment
## Docs: http://hexo.io/docs/deployment.html
deploy:
  type: github                                                  # 博客托管服务器类型
  repository: https://github.com/rakkang/rakkang.github.io.git  # 托管服务器地址
  brach: master                                                 # 博客使用的代码分支
```

除了 Hexo 的通用配置外，每个主题还有各自的配置文件，主题的配置文件放在：`themes/[xxx]/_config.yml`, 如：`themes/bs-light/_config.yml`，下面以 `bs-light` 为例：

``` xml
# 导航栏，如右上角的显示，Tips: RSS 栏是插件添加的不再这里
menu:
  首页: /                 # 格式是：[显示标签]:[索引目录]
  存档: /archives
# 文章右边的小部件
widgets:
# search/tag/category/recent_posts/tagcloud   ----> 这里是 bs-light 的可用小部件
- search                 # 搜索框
- recent_posts           # 最近发布的文章
- category               # 存档目录
- tagcloud               # 文章的标签集合
# 如果在文章的 *.md 中使用 <!-- more -->，那么之后的内容不会在首页显示，而是显示 阅读全文 的链接，显示可以更改
# 如：更多，查看原文等
excerpt_link: 阅读全文
# 博客的社交分享，eg: 博客底部的两个图标
social:
# key weibo/twitter/google/github/stackoverflow/rss
# value url
# e.g github: https://github.com/DaiXiang
  github: https://github.com/rakkang
  rss: /atom.xml
...
cnzz_analytics: true     # 博客的访问统计，这里使用 CNZZ 的统计
# google_analytics:
# rss:
# comment_provider:      # 评论功能，一般使用国内的 多说评论
# Facebook comment
```



---

*update：2018-01-30*

*update：2019-02-13 标题由「Hexo之NexT主题的配置及遇到的问题」改为了「NexT主题的优化定制修改指南.」；增加了很多内容，如「2.第三方服务及其他修改」这节内容；其他地方做了一些删减和修改。* 

*update：2019-02-14 补充完善和添加了很多内容。*  

*update：2019-02-15 添加了「添加RSS订阅功能」、「取消文章目录对标题的自动编号和取消目录」等小节、以及站点底部和页面样式的一些修改等*

*update：2019-02-17 修改了一点页面样式；增加了「三、博客速度/SEO优化」节；增加了博客 favicon*  

*update：2019-06-16*

> 1、设置了 scheme: Gemini。注：新版的 NexT 主题源码早已转移在了这个仓库 *<https://github.com/theme-next/hexo-theme-next>*  
>
> 2、修改 `/themes/source/css/_custom/custom.styl`：取消了「网页加载进度条」；设置了顶部条 `height: 2px`；设置底部页码 `border-radius: 0%`；
>
> 3、注释了 `source/css/_variables/custom.styl` 中的这两行代码：
>
> ``` xml
 $main-desktop = 1200px
 $content-desktop = 950px
> ```
> 在 `source/css/_variables/Gemini.styl` 文件中设置 `$main-desktop ` 为 75%：`$main-desktop=75%`

*update：2019-07-04* 

> 1、打开 `/themes/source/css/_custom/custom.styl`：①侧边栏信息样式 border-radius 修改为了 0， `border-radius: 0px;`，②更换了博客背景图，③ 修改尾部 .footer 的 +mobel() 下的样式 bottom 为 120 px，用来解决手机端底部的显示阻挡页面翻页的按钮。④设置了 body 样式，从而在手机端不显示背景图 ⑤设置了顶部条在手机端显示白色，高度为0px。⑤修改了顶部条样式 ⑥去除了标题颜色等样式，添加了点别的样式 ⑦设置了 body 样式下的手机端字体大小为 14 px ⑧以及一些其他小的修改
>
> 2、打开 `/themes/next/layout/_layout.swig`，设置底部版声明的字体样式为黑色 `color:black`
>
> 3、添加了「禁用打赏文字抖动」

*update：2019-07-07*

> 1、添加了文章标题下的评论字样的显示。
>
> 2、修改了文章标题下的发表、分类、访问次数、文章字数、阅读时间等为英文。
>
> 3、增加了菜单