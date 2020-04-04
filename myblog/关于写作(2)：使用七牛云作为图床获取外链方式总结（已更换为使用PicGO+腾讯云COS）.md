---
title: 关于写作(2)：使用七牛云作为图床获取外链方式总结（已更换为使用PicGO+腾讯云COS）
date: 2019-02-13 20:01:08
categories: Blog
tags: [Blog,PicGo,腾讯云] 
---

使用七牛云作为图床获取外链方式总结。注：已更换为使用 腾讯云 COS 做图床，上传工具使用的 PicGo。<!-- more -->

# 一、图床的选择

## 1. 什么是图床？

很多技术人写作都有在用 Markdown 轻量级标记语言进行博客写作，这种写作让我们不用像使用 Word 那么麻烦调整排版和格式，而只需专心写作照样完成排版的一种写作方式。但是，基本所有支持 Markdown 本地写作工具都只能采用导入本地图片引用的方式，对于一篇需要大量图片阐述的文章，或者是文章发布于网络后图片丢失问题，这不得不是经常要面对的问题。

那么有什么比较好的解决方式吗？哈哈，有的。很多人采用的图片寄存于网络，用服务厂商作为图片存储的地方，大家称为图床。好了，那像 CSDN 博客、简书平台不是都可以做到图片存储吗？是的，在这些平台写文章的时候可以通过上传图片然后得到一个图片网络地址，但当图片数量多，一张一张上传，这也是非常麻烦，另外，也是担心万一人家平台做防盗链呢（不了解防盗链话自行谷歌下~）。其实我们想要图床功能，有很多专业的服务商免费提供一定容量和流量可以让我们方便干这些事情，比如七牛云。

## 2. 图床种类

谷歌搜索下图床能搜到很多图床网站，列举一些供参考使用：

- [极简图床](https://jiantuku.com/#/)
  默认公共图床使用 sm.ms、微博图床，可以自定义支持七牛，界面简洁美观，支持 [Chrome 插件](https://chrome.google.com/webstore/detail/heebflcbemenefckkgfnnklbhdbdkagg)，注册后还可以同步上传历史。
- [路过图床](https://imgchr.com/)
- [Qchan图床](http://tuchuang.org/)
- [小贱贱图床](http://pic.xiaojianjian.net/)
- [SM.MS](https://sm.ms/) - SM.MS 由 V2EX @[Showfom](https://www.v2ex.com/member/Showfom) 自建的，无外链限制，无流量限制的图床，支持 HTTPS，速度不错。
- [微博图床](http://weibo.com/minipublish)



**(1) 图床分类**

- 公共图床
- 自建图床：云服务（如七牛云、又拍云、阿里云 OSS）
- 自建图床：开源方案 （如 Lychee 开源方案、树洞外链）

目前图床可以分为两种，一种是**公共图床，一种是自建图床。**

公共图床也就是利用公共服务的图片上传接口，来提供图片外链的服务，比如「微博图床」。自建图床，也就是利用各大云服务商提供的存储空间或者自己在 VPS 上使用开源软件来搭建图床，存储图片，生成外链提供访问，比如七牛云、Lychee 开源自建图床方案。

目前自建图床方案有两种，一种是利用云服务商提供的存储服务来作为图床，通过 API 来管理图片，另一种是在 VPS 上安装开源的图片或文件管理程序，只要能提供外链，基本都可以作为图床来用。

> 图床服务最重要的是稳定性，大厂的云服务也都比较有保障，大家只要考虑下价格和易用性就可以了。就我个人而言，我首先推荐七牛，它的价格比较厚道，免费用户也有一定额度，数据可以自己掌控，另外各大平台的图床工具也基本都支持，易用性很高。其次推荐微博图床，对于不是很重要的图片，都可以存到微博图床，毕竟流量存储都免费，速度也不错。至于图床工具，就看自己的喜好了，只要顺手就行。但是不论选择哪一个服务或者工具，我觉得首先要自己可以掌控数据。
>
> 总之，适合自己的才是最好的。

**(2) 图床工具**   

虽然图床选择好，但是对普通用户来说，直接使用图床 API 很麻烦，我们可以借助一些工具方便的上传图片，下面就根据 macOS、Windows、Web 分别推荐几款工具。

macOS： 
- [iPic - Markdown 图床、文件上传工具](https://itunes.apple.com/cn/app/id1101244278?ls=1&mt=12)

- [MWeb](https://zh.mweb.im/)（Markdown 写作工具，也支持上传图片）


Windows： 
- [MPic-图床神器]( http://mpic.lzhaofu.cn/)

Web：

- 比如「极简图床」插件、「微博图床」等等



# 二、七牛云图床使用

关于七牛云的介绍：七牛是一个云存储服务商，注册并实名认证之后，你将免费享有 10GB 存储空间，每月 10GB 下载流量、100 万次 GET 请求、 10 万次 PUT/DELETE 请求。七牛的定位不是像百度云一样的网盘 ，也不是同坚果云一般的同步云 ，而是 CDN，让你在浏览网页的时候最快的接收到页面中的图片、音频等文件，所以非常适合个人、企业用户用来储存站点资源。对于个人博主来说，你可以把博客中的图片、音频、视频等媒体上传到七牛，在博客中引用；也可以将站点需要加载的 CSS、JS 等文件上传到七牛，以加速网站。

## 1. 最原始上传

①到 [七牛云](https://www.qiniu.com/) 网站注册；

②实名认证（实名认证了才能享受 免费 10Gb 存储空间；**实名认证需要「本人手持身份证」的正反面两张照片，请提前准备好**）；

③点击「管理控制台」；

④「资源主页」--> 点击「对象存储」，立即添加（即创建存储空间，七牛云把这个叫作”Bucket“），其中包括以下三个项：

- 存储空间名称：存储空间名称作为唯一的 Bucket 识别符
- 存储区域：区域选择自己附近的
- 访问控制：作为图床的话，访问控制只能选择为「公开空间」

点击创建，Ok。

⑤然后打开存储空间，选择内容管理，点击上传文件，上传你所需要用到的图片；

⑥上传完成后，在存储空间文件列表中点击某一文件的右侧按钮，可以看到外链地址，复制粘贴即可用。

现在来梳理下一张图片上传图片所经历的步骤：

``` 
1. 登录打开七牛云网页个人存储空间
2. 上传图片
3. 复制外链
4. 粘贴到 Markdown
```

一张图片用了四步呐，要是图片很多，那不是作死嘛。有什么方法解决方便快捷上传吗？当然有，方法有三个：

1. 七牛云插件上传：简单

2. 使用 dropzone 上传：方便
   - [使用Dropzone和七牛优化博客图床](http://yansu.org/2015/01/10/use-dropzone-and-qiniu-to-store-blog-images.html)
   - [Mac OS 图床运用优化模式 - Microdust](http://azeril.me/blog/How-To-Use-Image-Hosting-Quickly.html)

3. 使用命令行上传：快捷，尤其适合需要目录及协作的团队

   官方有个「开发者工具」页面，提供一些工具进行上传，包括后面讲的 [qshell](https://developer.qiniu.com/sdk#official-tool )， 其中有个「QSunSync」的 Windows 版本图片同步上传客户端。

## 2. 七牛云插件上传：简单

浏览器插件 ~~[qiniu upload files](https://chrome.google.com/webstore/detail/qiniu-upload-files/emmfkgdgapbjphdolealbojmcmnphdcc)~~
> 七牛云插件，像使用桌面系统一样管理你的七牛云空间；支持拖拽上传，批量操作，文件处理等功能
>
> 如何操作：https://www.jianshu.com/p/44d818f781a7

还可以利用在线「极简图床」工具，默认使用的为公共图床 sm.ms，但是也可以自定义的，自定义图床为七牛云图床，方法如下：

``` 
在最前面有关七牛云的注册等等操作，前面已经讲了，不絮叨了，之后：

1. 在“个人面板”->“密钥管理”中查看 AccessKey/SecretKey；
2. 在储存空间的“空间概览”里，记住这里的“测试域名”；
3. 在「极简图床」上配置上刚才七牛储存的“空间名称”、“AccessKey”、“SecretKey”、“域名”后，保存。然后就可以上传到自己专属的七牛空间上了。

“AccessKey”、“SecretKey”：在“个人面板”->“密钥管理”中查看AccessKey/SecretKey；

“域名”：在储存空间的“空间概览”里可以看到。
```




## 3. 使用 dropzone 上传：方便

参考文章：

- [使用Dropzone和七牛云存储来优化博客图床](http://yansu.org/2015/01/10/use-dropzone-and-qiniu-to-store-blog-images.html)
- [Mac OS 图床运用优化模式 - Microdust](http://azeril.me/blog/How-To-Use-Image-Hosting-Quickly.html)

## 4. 使用命令行上传

**(1) qshell**

使命命令行方式，可以不用手动上传文件到七牛，它会自动帮你将本地目录的文件同步到七牛之前设定的存储空间下。

详细教程，参考「参考资料」②文章的方法三，但是参考资料②中所说的 qrsync  已经失效，现在使用的 qshell 命令行，操作方式其实类似。

先引用官方的 qshell 介绍：qshell 是利用七牛文档上公开的 API 实现的一个方便开发者测试和使用七牛 API 服务的命令行工具。该工具设计和开发的主要目的就是帮助开发者快速解决问题。目前该工具融合了七牛存储，CDN，以及其他的一些七牛服务中经常使用到的方法对应的便捷命令，比如 b64decode，就是用来解码七牛的 URL 安全的 Base 编码用的，所以这是一个面向开发者的工具，任何新的被认为适合加到该工具中的命令需求，都可以在 [ISSUE列表](https://github.com/qiniu/qshell/issues) 里面提出来，我们会尽快评估实现，以帮助大家更好地使用七牛服务。

配置教程：[官方文档](https://developer.qiniu.com/kodo/tools/1302/qshell) | [官方GitHub](https://github.com/qiniu/qshell)，同时官方也有视频教程：[视频教程--命令行工具使用](https://developer.qiniu.com/kodo/kb/3858/video-of-how-to-use-qrs-tools)。

**(2) hexo-qinqiu-sync**  

~~网上看到有通过命令安装 `hexo-qiniu-sync` 插件的方式：http://skyhacks.org/2017/08/02/UseQiniudnToStorePic/、 https://yuchen-lea.github.io/2016-01-21-use-qiniu-store-file-for-hexo/~~

GitHub 上也有教程：[gyk001/hexo-qiniu-sync](https://github.com/gyk001/hexo-qiniu-sync)

## 5. 图片优化

图片搜身、水印处理、自动旋正解决照片莫名其妙发生旋转：[Hexo博客(19)使用七牛云图床 | masikkk](http://masikkk.com/article/hexo-19-qiniu-cloud/)



# 三、图片上传方案选择

由于笔者用的 Windows，并且目前对图片上传的要求不大，只要能保证方便上传图片就行，目前有考虑以下几种方式。

1. 第一种：使用本文一开始提到的谷歌搜索出来的那些在线图床进行上传就是，比如 [SM.MS](https://sm.ms/)，不过可能会有某些限制，比如「小贱贱图床 」每日上传图片限制数：20张。

2. 第二种：使用本文提到 Chrome 浏览器插件 ~~[qiniu upload files](https://chrome.google.com/webstore/detail/qiniu-upload-files/emmfkgdgapbjphdolealbojmcmnphdcc) 插件~~，填写空间名称、AK、SK、域名等设置即可从电脑拖拽图片至浏览器即可完成上传，得到外链地址。

3. 第三种：使用本文提到的 ~~[极简图床](https://jiantuku.com/#/)~~，设置七牛云为图床，填写空间名称、AK、SK、域名、样式，上传图片即可得到外链地址。PS：其中，样式为可选设置，其作用是 [通过添加七牛样式后缀，实现水印、缩略图功能，查看使用说明](https://shimo.im/docs/IUQsi7cDPOwL9aZc)

4. 第四种：使用上传工具 [MPic](http://mpic.lzhaofu.cn/) 。操作步骤：

   ```
   1. 打开文件，启动程序请点击 MPic.exe，为方便启用可点击右键发送到‘桌面快捷方式’。
   2. 使用前先设置七牛云存储账号，即输入七牛云空间名、AK、SK、域名，保存；
   3. 然后就可以直接拖拽图片至客户端就能上传。
   
   说明：下载的文件中包含的 CSkin.dll 文件，它是程序的核心文件，请与 MPic.exe 文件保持在同一目录中；需要查看历史上传记录请点击“我的上传”即可查看。
   ```

5. 第五种：①使用官网 [开发者工具页面](https://developer.qiniu.com/sdk#official-tool) 的「QSunSync」同步上传 Windows 客户端，亲测了下，没有成功，还不知道哪的问题；②或者使用官网的开发者工具页面的 qshell 工具（基于七牛 API 服务的命令行工具），教程都在官网。


考虑到可以绑定七牛云，我最后考虑的是第二、第三、第四种方式（这几种方式都可以绑定七牛云为图床），也都差不多，都可以选择。当然若只是偶尔上传图片而已，可以考虑公共图床，如使用 [SM.MS](https://sm.ms/)  也 Ok。

参考：

- 利用「极简图床」网站页面上传图片至七牛云存储：[使用七牛云存储markdown用的图片](http://blog.csdn.net/itvincent/article/details/54292591)
- 这篇文章关于把七牛云作为图床的教程写的很详细、全面：[如何使用七牛云做为图床？](http://www.cnfeat.com/blog/2015/11/30/cli-qiniu/)
- [使用七牛云作为博客的图床](https://justin94lee.github.io/2016-11-02/Use-Qinyin-As-Image-Host.html)



# 四、目前使用的方法  [荐]

## 1. 腾讯云 COS

一开始我使用的是七牛云，但七牛云后来改了规则，测试域名使用 30 天需要绑定自己备案的域名才能继续使用，我觉得麻烦，后来知道腾讯 COS 有免费存储，于是干脆选择了腾讯 COS 做图床。

![](https://img-1256179949.cos.ap-shanghai.myqcloud.com/20190201174237.png)

当时看官方说明，腾讯云 COS 有 50G 的永久免费存储空间，不过截止到现在 2019-02-01 登陆了官网查看，才发现了 2019-01-25 腾讯云对象存储 COS 免费额度已经发生了变更，变成了这样：

| 用户类型 | 免费额度         | 有效期 |
| -------- | ---------------- | ------ |
| 个人用户 | 50GB标准存储容量 | 6个月  |
| 企业用户 | 1TB标准存储容量  | 6个月  |

个人用户免费额度有效时间 6 个月。不过发现站内信给我的通知，我未受此次变更影响，也就是说我还是能享受 50G 的永久免费存储空间，突然有种「早就是优势」的赶脚。

## 2. 上传工具 PicGo 

使用 PicGo 工具，配置自定义的快捷键，上传图片简直不能太方便了，墙裂推荐。

GitHub 地址：[Molunerfinn/PicGo](https://github.com/Molunerfinn/PicGo)，如何使用 PicGo 可以参考该文：[PicGo：基于 Electron 的图片上传工具 - 少数派](https://sspai.com/post/42310)。该工具支持微博图床、七牛图床、腾讯云 COS、GitHub 等等。

使用 PicGo 上传图片到腾讯云 COS，参考：[图床上传工具PicGo v1.5更新：支持腾讯云COSv5版本、支持GitHub图床、支持上传前重命名文件等等 - 少数派](https://sspai.com/post/44495)

另外 PicGo 还支持微博图床、阿里云OSS、又拍云等作为图床，甚至 GitHub 图床。如果不嫌图片加载速度可能不那么快，可以考虑一下 GitHub 作为图床，记得我在哪里看到过，GitHub 单个仓库存储容量可以达到 1000G，所以放心用吧，我觉得也考虑把这个作为文件备份的地方。

具体如何配置参考：[传送门](https://sspai.com/post/44495)。我有实际操作了一遍，有几点要说的：

1. 在 <https://github.com/settings/tokens> 中生成的 token，记得复制以下存放在其他地方留着备用，因为这个 token 只会显示一次；

2. PicGo 设置中，域名为空即可，另外，如果需要把图片存放在图床仓库 img 文件夹，则先第一步，在仓库新建 img 文件夹（如何在 GitHub 仓库新建文件夹相信你有办法的），然后在 PicGo 的存储路径指定为 `img/` 即可，这样得到的地址如下格式：

   ``` xml
   https://raw.githubusercontent.com/strivebo/backup/master/img/20190218004624.png
   ```

3. 使用 GitHub 作为图床，图床仓库不要去设置为私有，如果设置为了私有仓库，在其他人浏览器不会显示；

   

---

*update：2019-07-21*



 
