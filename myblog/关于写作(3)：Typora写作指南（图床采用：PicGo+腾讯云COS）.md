---
title: 关于写作(3)：Typora写作指南（图床采用：PicGo+腾讯云COS）
date: 2019-02-13 20:01:08
categories: 版本控制
tags: [Blog,Typora,GitHub] 
---

Markdown 写作软件 Typora 的介绍和使用。<!-- more -->

### (1) Typora介绍

Markdown 这种格式被许多写作网站支持，可以说技术人写作必备。本人目前一直在用的 Markdown 编辑器如那件为 Typora，虽然也很多在线编辑器，但总觉得有些不方便，想一想没联网的时候呢。[Typora](https://typora.io/) 是一款非常好用跨平台 Markdown 编辑器，编写过程中所见及所得，当然也能切换到源码方式，非常方便。

Typora 在安装后默认的主题有这么几个：

``` markdown
Github
Newsprint
Night
Pixyll
Whitey
```

**美化Typora的中文字体——设置为「微软雅黑」**

不管切换哪一个主题，中文字体都默认显示为“宋体”，觉得丑可以考虑更改为其他字体。操作：打开“文件” --> “偏好设置” --> 找到「主题」栏，“打开主题文件夹”，该路径默认为`C:\Users\用户名\AppData\Roaming\Typora\themes`，你也可以直接找到该路径打开，然后就是修改 CSS 了。

打开`github.css`，仅在 body{} 模块的"font-family"后面增加`Microsoft YaHei`：

``` css
body {
    font-family: "Microsoft YaHei","Open Sans","Clear Sans","Helvetica Neue",Helvetica,Arial,sans-serif;
    color: rgb(51, 51, 51);
    line-height: 1.6;
}
```

重启 Typora 即可。

### (2) Typora快捷键

- `Ctrl+Shitf+L`：左侧显示和隐藏目录
- `Ctrl+/`：切换到源码模式
- 

### (3) Typora安装新主题

首先进入 Typora 官网 Themes 页面：[Typora主题](https://theme.typora.io/)，然后选择一个中意的主题，比如 Catfish 主题，然后点击该主题的名称。点击对应主题后进入主题介绍和下载界面，我们然后点击 Download 下载该主题，下载好的主题存放在本地磁盘。然后我们打开下载的压缩包，可以看到：

![](https://img-1256179949.cos.ap-shanghai.myqcloud.com/20190201171633.png)

把其中`catfish`、`catfish.css`、`catfish.styl`拷贝到主题所在的文件夹下即可，当然把压缩包所有文件全部拷贝也可以。最后打开 Typora 可以看到主题菜单栏多出了 Catfish 主题，选择即可使用该主题。

### (4) Typora引入图片地址（采用PicGo+腾讯云COS）[荐]

作为一个比较常用 Markdown 写文章、博客的人，在 Markdown 里插入图片是经常操作的一件事，虽然可以采用把图片放在本地然后引入的方式，但觉得非常不方便，比如图片多了的时候，就烦恼了。

后来我了解到了网络图床，可能你不知道图床是什么，简单说，就是可以把你需要的图床上传到图床网站，然后 Markdown 文档中引入图片的网络地址即可。

之后我就选择了七牛云作为图床，因为听说有免费的 10G 免费存储空间，我觉得也够了，另外也听说很多人在用。配合上传工具（我使用的是浏览器插件「极简图床」）进行上传，还是非常方便的。但在使用期间出现过了「极简图床」不能登录的情况，另外，七牛云也出现了变化，官方发邮件提示测试域名要被回收，测试域名回收后以前那些上传的图片地址就失效了。

![](https://img-1256179949.cos.ap-shanghai.myqcloud.com/20190201174237.png)

这就非常尴尬了。

于是，我考虑着得找个比较好的解决方式。在与别人交流相关问题后，有让我了解到了腾讯 COS 和 PicGo 工具，后面我就实操了，哈哈，简直不能太方便。

另外，当时看官方说明，腾讯云 COS 有 50G 的永久免费存储空间，不过截止到现在 2019-02-01 登陆了官网查看，才发现了 2019-01-25 腾讯云对象存储 COS 免费额度已经发生了变更，变成了这样：

| 用户类型 | 免费额度         | 有效期 |
| -------- | ---------------- | ------ |
| 个人用户 | 50GB标准存储容量 | 6个月  |
| 企业用户 | 1TB标准存储容量  | 6个月  |

个人用户免费额度有效时间 6 个月。不过发现站内信给我的通知，我未受此次变更影响，也就是说我还是能享受 50G 的永久免费存储空间，突然有种「早就是优势」的赶脚。

GitHub 地址：[Molunerfinn/PicGo](https://github.com/Molunerfinn/PicGo)，如何使用 PicGo 可以参考该文：[PicGo：基于 Electron 的图片上传工具 - 少数派](https://sspai.com/post/42310)。该工具目前支持微博图床、七牛图床、腾讯云 COS 等等。

使用 PicGo 上传图片到腾讯云 COS，参考：[图床上传工具PicGo v1.5更新：支持腾讯云COSv5版本、支持GitHub图床、支持上传前重命名文件等等 - 少数派](https://sspai.com/post/44495)