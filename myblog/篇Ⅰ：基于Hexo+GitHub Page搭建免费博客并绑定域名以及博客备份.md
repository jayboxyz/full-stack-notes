---
title: 篇Ⅰ：基于Hexo+GitHub Page搭建免费博客并绑定域名以及博客备份
date: 2019-02-14 20:01:08
categories: Blog
tags: [Blog,GitHub,Hexo] 
---

基于 Hexo+GitHub Page 搭建免费博客并绑定域名，以及博客备份。<!-- more -->

# 写在前面

这里引用阮一峰老师网络日志里说的，对于喜欢写博客的人，会经历三个阶段：

``` 
第一阶段，刚接触 Blog，觉得很新鲜，试着选择一个免费空间来写。
第二阶段，发现免费空间限制太多，就自己购买域名和空间，搭建独立博客。
第三阶段，觉得独立博客的管理太麻烦，最好在保留控制权的前提下，让别人来管，自己只负责写文章。
```

大多数博客作者，都停留在第一和第二阶段，因为第三阶段不太容易到达：你很难找到俯首听命、愿意为你管理服务器的人。

但是其实该情况早已改变，很多程序员早已在 [GitHub](https://github.com/) 网站上搭建 Blog。他们既拥有绝对管理权，又享受 GitHub 带来的便利——不管何时何地，只要向主机提交 commit，就能发布新文章。更妙的是，这一切还是免费的，GitHub 提供无限流量，世界各地都有理想的访问速度。

好了，本文就来讲如何在 GitHub 上搭建博客及采用 Git 分支进行文章备份。

基于 Hexo+GitHub Page 搭建博客的教程，网上这样的文章很多，在这之前我也记录过一篇 [基于Hexo+GitHub Page搭建免费个人博客教程](http://blog.csdn.net/u012195214/article/details/72454346)。网上相关文章也很多：

- [hexo从零开始到搭建完整](https://www.cnblogs.com/visugar/p/6821777.html)
- [利用GitHub Pages建立项目或个人网站](https://github.com/uolcano/blog/issues/11) 
- [在win7中一步一步安装Hexo搭建个人博客](http://www.lzblog.cn/2016/04/06/%E5%9C%A8win7%E4%B8%AD%E4%B8%80%E6%AD%A5%E4%B8%80%E6%AD%A5%E5%AE%89%E8%A3%85Hexo%E6%90%AD%E5%BB%BA%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2/) 
- [了解githubPages+hexo搭建博客的原理](http://blog.csdn.net/sunshine940326/article/details/57413678)
- [利用GitHub Pages建立项目或个人网站](https://github.com/uolcano/blog/issues/11)
- ......

本文主要是梳理搭建步骤，特别地，本文主要特点有采用 Git 分支进行对博客源文章进行备份。 



# 一、博客搭建

在搭建过程之前，先了解下 npm。

先简单介绍下 npm：npm 是 Node 的模块管理器，功能极其强大。它是 Node 获得成功的重要原因之一。正因为有了 npm，我们只要一行命令，就能安装别人写好的模块 。`npm install`命令用来安装模块到 node_modules目录。

> NPM 是随同 NodeJS 一起安装的包管理工具，能解决 NodeJS 代码部署上的很多问题，常见的使用场景有以下几种：
>
> - 允许用户从 NPM 服务器下载别人编写的第三方包到本地使用。
> - 允许用户从 NPM 服务器下载并安装别人编写的命令行程序到本地使用。
> - 允许用户将自己编写的包或命令行程序上传到 NPM 服务器供别人使用。
>   由于新版的 nodejs 已经集成了 npm，所以之前 npm 也一并安装好了。同样可以通过输入 "npm -v" 来测试是否成功安装。命令如下，出现版本提示表示安装成功。
>
> —— *From： [菜鸟教程](http://www.runoob.com/nodejs/nodejs-npm.html)*  

npm 的包安装分为本地安装（local）、全局安装（global）两种，从敲的命令行来看，差别只是有没有 -g 而已，比如：

``` 
npm install express	# 本地安装
npm install express -g   # 全局安装
```

本地安装：

> 将安装包放在 ./node_modules 下（运行 npm 命令时所在的目录），如果没有 node_modules 目录，会在当前执行 npm 命令的目录下生成 node_modules 目录。可以通过 require() 来引入本地安装的包。
>

全局安装：

> 将安装包放在 /usr/local 下或者你 node 的安装目录。可以直接在命令行里使用。
>

如果你希望具备两者功能，则需要在两个地方安装它或使用 npm link。

## 1. 搭建步骤 

**(1) 第一步：Github Pages** 

> Github Pages 免费的静态站点，其特点：免费托管、自带主题、支持自制页面等。

创建 Github Pages 比较简单，只要你有一个 GitHub 账号在创建一个仓库就行了，但是这个仓库是有规则的，其格式必须为：`yourusername.github.io`。然后根据提示一直下一步即可，非常简单。比如我的账户名为`strivebo`，则格式为`strivebo.github.io`。（这里在 GitHub 上创建仓库我就不多讲了吧？）

**(2) 第二步：Hexo相关操作**

我把用到的命令先记录在此：
```python
hexo new "postName" #新建文章，缩写为：hexo n
hexo new page "pageName" #新建页面
hexo generate #生成静态页面至public目录,,缩写为：hexo g
hexo server #开启预览访问端口（默认端口4000，'ctrl + c'关闭server）,缩写为：hexo s  
hexo s -p 8080  #本地预览的时候修改端口为8080 
hexo s -debug #本地预览调试
hexo deploy #部署到GitHub，缩写为：hexo d
hexo clean  # 清除缓存文件 db.json 和已生成的静态文件 public 
hexo help  # 查看帮助
hexo version  #查看Hexo的版本
---------------以下为组合命令----------------------------------
hexo s -g  #生成并本地预览
hexo d -g  #生成并上传
```

**具体的操作步骤：** 

1. 安装 [Git](https://git-scm.com/download/win) 和 [node.js](https://nodejs.org/zh-cn/)（笔者实践使用的 `Git-2.15.0-64-bit.exe` 和 `node-v9.4.0-x64.msi` 版本）；

2. 新建目录，如名称为 blog 的文件夹，然后在该目录下的`Git Bash` （安装了 Git 就有这个，鼠标右键会出现）下输入`npm install -g hexo` 
    > 基于上面对 npm 的了解，此命令为全局安装 hexo；也有看到教程写的是：`npm install -g hexo-cli`这个（**并且官方文档也是用的这个命令说是安装 hexo**）；或者好像也可以使用`npm install hexo --save`进行安装（**亲测：不可以先使用这个命令！**），安装完毕生成了`node_node_modules `文件夹（莫非这个命令才是此版本 node.js 对应的安装方式？），然后再执行`hexo`或者是后面的需要用到的`hexo g`命令，都会生成`db.json`文件，我现在还不知道其作用，当然`hexo g`还会生成 public 文件内容（文章被编译形成的文件夹）。

    去网上找了下解释：[hexo和hexo-cli的关系？](https://segmentfault.com/q/1010000009487303)

    > ① hexo 本身是一个静态博客生成工具，具备编译 Markdown、拼接主题模板、生成 HTML、上传 Git 或 FTP 等基本功能。将这些功能封装为命令，提供给用户通过 hexo server / hexo deploy 等命令调用的模块，就是 hexo-cli 了。CLI = Command Line Interface 命令行界面。
    >
    > ② 后者是前者的命令行模式，即 `hexo-cli`为`hexo`的命令行模式。

3. 再在该目录下，Git Bash 下敲`hexo init`，会自动下载如下文件及文件夹到这个目录，但不包括 public 文件夹。

    ```python
    node_node_modules 文件夹（纳闷：按道理不是在npm install -g hexo生成吗？）
    scaffolds 文件夹
    source 文件夹
    themes 文件夹
    .gitignore 
    _config.yml 
    package.json 
    package-lock.json 
    ```

    备注：public 文件夹为 `hexo generate`或`hexo g`（其实是这个「编译过程」）生成静态页面才会生成的文件夹。

4. 然后  `hexo generate` 或 `hexo g`生成 `public` 文件夹（该文件夹下为 `.md` 文件编译后生成的静态文件，包括html/css/js/图片等等）和`db.json`文件

    > `public`文件夹下为`.md`文件编译后形成的文件，也正是被 `hexo deploy`部署到 GitHub 上的文件。

5. 可以`hexo s`开启本地预览端口，输入 <http://localhost:4000/> 进行预览，可以看到默认主题下的博客，如果遇到 4000 端口被占用的问题，可以使用比如 `hexo s -p 8080` 指定 8080 端口预览。**好了！ 本地搭建的活干完了！** 

    现在可以试试写文章了实践了，执行`hexo new "第一篇博客.md"`，这样就在 source 目录下生成该博客文章了，然后可以进行写作了，再去执行`hexo g`编译和`hexo s`预览了，另外如果文章写错了需修改，可以重新生成；网站显示异常时，可以先使用`hexo clean`清除缓存文件 `db.json` 和已生成的静态文件目录 public，再`hexo g`重新生成。

6. 本地预览完毕，则`hexo deploy `或 `hexo d` 发布至 GitHub，访问地址格式如：https://yourname.github.io

    > 注：若在发布至 GitHub 提示 `Deployer not found: github 或者 Deployer not found: git` , 原因是需要安装一个插件，命令是：`npm install hexo-deployer-git --save`（网上搜了下，这步的含义说是在安装 git 插件）

    发布之后，该文件下该目录下生成了 **`.deploy_git`** 文件夹（目测了下：该文件有一个`.git`文件夹；其他文件和`public`文件夹下内容一样）。**那该文件夹干嘛的？** 

    网上看到的解释 1：
    > .deploy_git： 这个应该是 git 部署用的文件。比如你写好的博客想部署到 GitHub Pages 上去的话，可以用 git 部署插件，那个插件会创建这个目录

    网上看到的解释 2：
    > 注意，使用这种方式，只会将 hexo 编译后生成的 html、css、js 等上传到 github.io 代码库中，并不会将本地的其它源码提交；
    > 同时，在本地生成一个 .deploy_git 目录，表示是 hexo 专用的 git 库；

    我在部署，即上传至 GitHub 完毕之后，查看到 master 分支上的文件和`.deploy_git`文件夹下的文件相同，所以我的猜测正如网上看到的解释的意思：**hexo d 只会发布编译后生成的文件，`.deploy_git`目录表示 hexo 专用的 git 库，在 `hexo d` 进行发布部署的时候，会拷贝 `public` 文件夹所有内容至 `.deploy_git` 目录下，再把该文件内容推送到 GitHub 仓库。**在后面的实践中，证实了这点！  

    这里有个思考的地方？`hexo d` 发布的时候为什么就会发布到仓库下 master 的分支（我仓库下明明还有 backup 分支）呢？哈哈，我**猜测**是在设置`_config.yml`该文件的时候：
    ```
    deploy: 
    type: git
    repository: git@github.com:strivebo/strivebo.github.io.git
    branch: master
    ```
    我这里 branch 设置的为 master，所以默认部署到 master 分支。

    其中这里的配置我解释下：如`repository`配置为`git@github.com:strivebo/strivebo.github.io.git` 写上这样的表示采用的 ssh 方式，若为`https://github.com/strivebo/strivebo.github.io.git`表示采用 https 方式提交。注意的地方，type 值这里为 git，我看网上很多人说之前很多人设置的值为 github，被坑了。

**(3) 更换主题** 

对于默认主题我们不喜欢怎么办？不着急，是可以换主题的，可以到官网推荐的主题选择：https://hexo.io/themes/，或者到 GitHub 上搜索关键字「hexo-theme」也能搜到很多；然后就是直接下载下来就行，解压出来里面文件夹复制粘贴到博客根目录的 themes 文件夹下，最后配置好`主题配置文件_config.yml`和`站点配置文件_config.yml`(即博客根目录下的`_config.yml`)，其中站点配置文件只要把`theme`值改为复制粘贴过来的主题的那个文件夹名称就行。

然后编译、发布、预览就可以看到效果了！

## 2. 域名绑定

不绑定域名肯定也是可以的，就用默认的 xxx.github.io 来访问，如果想更个性一点，想拥有一个属于自己的域名，那也是 OK 的。

分两大步骤：先到服务商比如[阿里云](https://cn.aliyun.com/)旗下[万网](https://wanwang.aliyun.com/)进行的操作；然后在仓库项目的操作。

关于域名的注册，以前域名的注册总是推荐去国外的 [godaddy](https://sg.godaddy.com/zh/offers/domains?isc=gennlcn08&currencytype=CNY&mkwid=sqRPKLZmr_pcrid_229777822940_pkw_godaddy_pmt_e_pdv_c_&gclid=EAIaIQobChMIkvWy89Xy2AIVxgQqCh2yNQ3hEAAYASAAEgK9e_D_BwE) , 但是现在国内的 [阿里云旗下万网](https://wanwang.aliyun.com/?utm_content=se_980922&gclid=EAIaIQobChMI7ouSmqKT1wIViAgqCh3jEAOkEAAYASAAEgK87vD_BwE) 也很多人在使用，价格也不贵，一般首次注册使用还是很便宜的，但据大家说在万网注册 .cn 等后缀域名是需要在国内备案的，如果在国外服务商注册，如  [godaddy](https://sg.godaddy.com/zh/offers/domains?isc=gennlcn08&currencytype=CNY&mkwid=sqRPKLZmr_pcrid_229777822940_pkw_godaddy_pmt_e_pdv_c_&gclid=EAIaIQobChMIkvWy89Xy2AIVxgQqCh2yNQ3hEAAYASAAEgK9e_D_BwE)  注册，就不用备案。

*关于备案问题，我有在网上了解了下，以下摘自网上：*

> 域名的备案根据你的服务器主机而定，主机在哪就在哪里备案；
>
> 只有中国国内的空间才要求备案，接入商会严格把关的，不备案的网站是绝对不能访问的；
>
> 网站备案主要是看你的网络主机是哪家公司的，就在哪家公司做备案；
>
> 备案与域名注册商无关，与服务器有关，也就是说你的域名可以接入其他任何一家 IDC，但如果你的服务器在万网，那么万网作为服务器接入商，你的备案信息就必须先经过万网的审核后才能递交工信部终审；
>
> 注册 cn 域名做网站并不是一定需要备案的，主要还是看用的是哪时主机。如果用的是国内主机，那么就必须备案，如果用的是国外的空间，那么就不需要备案，直接使用即可。不过需要注意的是，根据 CN 域名管理机构 CNNIC 的规定，cn 域名在注册时需要注册人提交身份证扫描件进行审核，在审核通过后才能正常使用，否则就会注册失败；
>
> 其实是一句话，域名如果绑定指向到国内网站空间就要备案。也就是说如果你这个域名只是纯粹注册下来，用作投资或者暂时不用，是无需备案的。域名指向到国外网站空间，也是无需备案的。但是 CN 域名是特例，CN 域名指向到国外网站空间也要备案，不备案就是暂停解析状态，无法指向到任何 IP。由于域名备案基本取决于网站空间的情况，所以备案也是空间服务商提供备案，不是域名注册商。
>
> .......

看了网上一些解释，我大概明白了，是否备案与域名无关，得看购买的主机/服务器在哪，在国内的才需要备案。我想我利用的是 GitHub Page 服务，相当于服务器在国外，所以不用备案吧。下面以在万网注册为例。

**(1) 万网的操作——域名解析设置** 

登入万网购买域名。然后：管理控制台 → 域名与网站（万网） → 域名；在购买的那个域名处，点击「解析」，进行如下设置。

绑定域名分 2 种情况：带 www 和不带 www 的。

域名配置最常见有 2 种方式，CNAME 和 A 记录，CNAME 填写域名，A 记录填写 IP，由于不带 www 方式只能采用 A 记录，所以必须先 ping 一下你的 `用户名.github.io` 的 IP，然后到你的域名 DNS 设置页，将 A 记录指向你 ping 出来的 IP，将 CNAME 指向你的 `用户名.github.io`，这样可以保证无论是否添加 www 都可以访问，如下：

| 记录类型 | 主机记录 | 解析线路 | 记录值             |
| -------- | -------- | -------- | ------------------ |
| A        | @        | 默认     | 103.245.222.133    |
| CNAME    | www      | 默认     | strivebo.github.io |

**(2) 对仓库的操作——添加CNAME文件**

在 GitHub 博客仓库 master 分支根目录创建一个 `CNAME` 文件(无后缀)，里面填写你的域名，加不加 `www` 看自己喜好，因为经测试：

- 如果你填写的是没有 www 的，比如 mygit.me，那么无论是访问 `http://www.mygit.me` 还是 `http://mygit.me`，都会自动跳转到 `http://mygit.me`
- 如果你填写的是带 www 的，比如 `www.mygit.me` ，那么无论是访问 `http://www.mygit.me` 还是 `http://mygit.me`，都会自动跳转到 `http://www.mygit.me`
- 如果你填写的是其它子域名，比如 abc.mygit.me，那么访问 `http://abc.mygit.me` 没问题，但是访问 `http://mygit.me` ，不会自动跳转到 `http://abc.mygit.me`

关于添加 `CNAME` 文件简单提下，如果你不想如上直接在远程仓库创建 `CNAME` 文件，可按如下操作在本地添加完再部署：

> 在博客目录的 source 文件夹下添加 `CNAME` 文件，`hexo g` 编译会自动生成这个文件于 public 中，`hexo d` 部署的时候会把 public 文件夹下文件复制于 `.deploy_git` 目录下进行发布。

参考资料：[使用hexo+github搭建免费个人博客详细教程](http://www.cnblogs.com/liuxianan/p/build-blog-website-by-hexo-github.html)  

## 3. 域名绑定个人实践

(1) 域名注册和解析

一开始我使用的都是阿里云的，包括购买域名、域名解析，后来域名快要到期了，准备续费三年，发现有点小贵，于是想着买一个新的域名会不会更便宜呢？然后有在腾讯云下搜了下相同名称但后缀为 `.com` 的域名发现比在阿里云续费三年价格还便宜一点点，遂直接在腾讯云买了个新的域名（[购买传送门](https://dnspod.cloud.tencent.com/)），解析用的是腾讯云的免费解析套餐（[云解析套餐 - 腾讯云](https://buy.cloud.tencent.com/cns) 可以了解下）。以下是我的解析设置：

| 主机记录 | 记录类型 | 线路类型 | 记录值              |
| -------- | -------- | -------- | ------------------- |
| www      | CNAME    | 默认     | strivebo.github.io. |
| @        | CNAME    | 默认     | strivebo.github.io. |

![](https://img-1256179949.cos.ap-shanghai.myqcloud.com/20190214160616.png)

从上图可以了解到，添加 www、@ 记录，CNAME 的类型，这样话，不管地址栏输入的是带 www 的`www.strivebo.com` ，还是不带 www 的 `strivebo.com` 都是可以访问到目标网页。

(2) 创建CNAME文件

在本地博客根目录下的 `source` 文件夹中，新建一个名为 `CNAME` 的文件，注意这个文件不带 `任何后缀名`。打开 `CNAME` 文件，在里面填写你购买的域名，加不加`www`看前文的说明，就不赘述了。

~~(3) SSL证书~~  

什么是 SSL 证书？

> 首先说明 SSL（安全套接层，Secure Sockets Layer）是一种安全协议，目的是为互联网通信，提供安全及数据完整性保障。SSL 证书遵循 SSL 协议，可安装在服务器上，实现数据传输加密。
>
> CA（数字证书认证，Certificate Authority）机构，是承担公钥合法性检验的第三方权威机构，负责指定政策、步骤来验证用户的身份，并对 SSL 证书进行签名，确保证书持有者的身份和公钥的所有权。CA 机构为每个使用公开密钥的用户发放一个 SSL 证书，SSL 证书的作用是证明证书中列出的个人/企业合法拥有证书中列出的公开密钥。CA 机构的数字签名使得攻击者不能伪造和篡改证书。
>
> SSL 证书实际上就是 CA 机构对用户公钥的认证，内容包括电子签证机关的信息、公钥用户信息、公钥、权威机构的签字和有效期等。

简单看，安装了 SSL 证书，可以让你的网站支持 HTTPS 地址形式，地址栏不再提示连接不安全。了解下：[SSL证书\_SSL数字证书_HTTPS加密 - 腾讯云](https://cloud.tencent.com/product/ssl)。

腾讯云提供免费 SSL 证书申请，如何申请：[SSL 证书 域名型（DV）免费SSL证书 - 腾讯云](https://cloud.tencent.com/document/product/400/8422)。申请到后的证书可下载到本地，或者部署到云服务。

SSL 证书如何安装和部署指引：[SSL 证书 证书安装指引 - 腾讯云](https://cloud.tencent.com/document/product/400/4143)、[hexo 博客开启 https (SSL 证书)](https://blog.csdn.net/StaunchKai/article/details/82901437)。

其实对于 GitHub Page  现在可以对自定义域名支持 HTTPS：

> GitHub 官方在 2018 年5 月 1 号宣布，GitHub Pages 的自定义域名获得对 HTTPS 的支持。
>
> 设置操作：打开仓库的Settings，找到 GitHub Pages 项，找到 Enforce HTTPS，打上勾即可。

## 4. 问题汇总 

**问题 1：** 执行 hexo deploy 命令，README 文件就消失，有什么解决方法吗？

在 Hexo 目录下的 source 目录下新建一个 `README.md`文件，修改 Hexo 目录下的配置文件`_config.yml`，将`skip_render`参数的值设置为上。即 `skip_render: README.md`保存退出即可。使用 hexo d 命令就不会渲染 README.md 这个文件了。

参考资料：[怎么用hexo上传一个README.md到github?](https://www.zhihu.com/question/28058973) 



# 二、博客备份 

## 1. 备份详解

博客搭建完毕，就可以通过 `https://strivebo.github.io` 类似这样的格式访问了。如果要绑定了域名就可以使用域名访问了。


这里有个问题是：部署上去的，即发布到 GitHub 的都是编译后的文件，如 `html`、`css`，`js`等文件，但是自己写的 `.md` 文章实际是没有上传至 GitHub 的，**如果需要备份这些源文件，该怎么备份呢？或者换了别的电脑该怎么更新博客呢？**

**(1) 如果备份分支 backup 为默认分支** 

如果备份分支 backup 为默认分支：在完成上面部署至 GitHub 之后，可以把该博客目录于 GitHub 博客这个仓库进行关联（即绑定），这样就在该根目录生成记录版本控制信息的`.git`目录，这里这块知识就是 git 有关知识了，自行网上了解下 `.git` 目录作用。同时也能注意到博客根目录下有个`.gitigore`文件，就是可以**设置文件要还是不要 push 到 GitHub 仓库去**。 

因为首次 GitHub 上没有非默认分支，使用如下命令：

```
git push origin backup:backup
```
这条命令的作用是：把本地 backup 分支推送到名字为 origin 的远程服务器的 backup 分支上，但因为远程服务器没有 backup 分支，会自动新建该同名分支，**然后在 GitHub 网站的 setting 页面设置 backup 为默认分支。**  其中，这步操作，就把需要备份文件比如 source 文件夹下的的博客「源文件」已经上传至分支 backup。

然后下次就算换电脑了，可以直接 clone 该博客仓库，得到 backup 分支的数据（即得到了 GitHub 默认分支 backup 数据），然后再如最开始安装 nodejs、Git 以及安装 hexo，最后再执行相关命令得到编译后的文件（即 public 目录），最后`hexo d`部署至 GitHub 博客仓库的 master 上。

**(2) 如果部署分支 master 为默认分支** 

如果部署分支 master 为默认分支 ：换了电脑之后，clone 仓库后默认显示 master 分支数据，然后执行格式 `git checkout -b <本地分支名称> origin/<远程分支名称>`，如 `git checkout -b backup orgin/backup` 该语句作用是在本地创建新的分支，分支的名称是 backup，第二个 backup 也是我想要 clone 的远程分支的名字，这样 GitHub 上非默认分支的数据也 clone下来了，而且还进行了绑定；

再`git checkout backup` 这样就切换到本地 backup 分支了，然后进行写文章，编译，部署等操作，因为部署只会部署`.deloper_git`文件夹下文件内容，所以这样的方式也是可行的。

但是这里有个问题是，备份分支 backup 并没有备份「node_modules」文件夹，所以需要重新安装`hexo`，即执行一开始讲到的`npm install -g hexo`，如果不行，则用这个`npm install -g hexo-cli`试试来安装 hexo，然后可以用 hexo 命令进行一系列如编译、部署等操作了。

这里又有个问题出现了，`hexo g`编译文章后，使得`package.json`和`package-lock.json`文件改动了，如果担心这里的变动引起不必要的问题，可以干脆在`.gitignore`文件中设置忽略这两个文件不被提交。

实际操作中，发现每次 add 命令把修改提交到暂缓区后，还是会提示`package.json`文件的已修改，同时也切换不了到本地 master 分支，得了，commit 一次，然后切换到本地 master 分支查看，发现比远程 master 分支多了`node_modules`文件夹和`db.json`文件。

然后`hexo d`就可以发布部署`public`文件夹内容至 GitHub 上了，OK。

最后，进行 Git 有关操作 `git push origin backup:backup` 进行备份源文件（不包括`.gitgnore`设置的那些被忽略提交的文件和目录，哈哈，比如`node_modules`这个目录就不会被提交到备份分支 backup 啊）！

**相关学习：** 

- [npm install 生成的package-lock.json是什么文件？有什么用？](https://www.zhihu.com/question/62331583) 

    > 大致意思是，如果改了 package.json，且 package.json 和 lock 文件不同，那么执行`npm i`时 npm 会根据 package 中的版本号以及语义含义去下载最新的包，并更新至 lock。
    >
    > 如果两者是同一状态，那么执行`npm i `都会根据 lock 下载，不会理会 package 实际包的版本是否有新。

- [.npmignore文件的干嘛的](http://front-ender.me/architecture/npmignore.html) 

## 2. 备份实战

本人 GitHub 博客那个仓库设置的是 master 为默认分支；另外我本机安装版本为 Git v2.15.0，nodejs v9.4.0。

1. `git clone git@github.com:strivebo/strivebo.github.io.git`克隆默认分支 master 分支数据；

2. 使用`git branch -a`可以查看到本地只有 master 分支以及远程有 master 和 backup 分支，于是`git checkout -b backup origin/backup` 可以本地自动新建了 backup 分支并且与远程 backup 分支绑定了，同时切换到了本地 backup 分支，并且可以看到本地分支内容和远程一样，内容如下：

   ```
   scaffolds 文件夹
   source 文件夹
   themes 文件夹
   .gitignore 
   _config.yml 
   package.json 
   package-lock.json 
   ```

3. 使用`npm install -g hexo`或者`npm install -g hexo-cli`安装 hexo，完毕之后未在博客根目录生成`node_modules`文件夹，并且继续敲`hexo init`提示：

   ```
   ERROR Local hexo not found in G:\strivebo.github.io
   ERROR Try running: 'npm install hexo --save'
   ```

   于是敲`npm install hexo --save`，可以看到博客根目录生成了`node_modules`文件夹及内容，然后可以使用`hexo init`来生成一些文件了，但是因为我远程的备份分支 backup 本来就是备份了这个步骤生成的文件（除了 node_modules 文件夹内容未备份），比如 themes 文件等都是远程备份了的；

4. 然后`hexo g`编译 source 中的博客文章，生成 public 文件夹，编译后的 html/css/js 等文件也存于此，`hexo s`本地预览；

5. 然后本地在 source 新增博客文章，以及文章修改，`hexo g`、`hexo g`即可，最后 `hexo d`发布部署至 GitHub（其实 `hexo d`会自动生成一个`.deploy_git`文件夹，并且实质是把 public 文件夹内容复制于该文件夹进行发布的，该文件夹下有个隐藏文件夹`.git`维护着 **发布** 这个过程的版本控制信息。）

---

*update：2019-07-21*