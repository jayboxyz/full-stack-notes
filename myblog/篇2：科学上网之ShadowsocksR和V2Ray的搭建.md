---
title: 篇2：科学上网之ShadowsocksR和V2Ray的搭建
date: 2019-02-12 20:01:08
categories: 程序人生
tags: [科学上网]
---

该文主要记录 Shadowsocks/ShadowsocksR 和 V2Ray 的搭建过程要点。<!-- more -->

# 一、SS 或 SSR 的搭建

可以先看我写的一篇总结：【篇1：科学上网总结】，该文有记录如何搭建影梭，可以当做先了解下相关知识也可以。

## Step01：安装脚本

### 安装脚本1

参考：[自己搭建ss/ssr服务器教程（适合初学者，最低2.5美元/月）](https://github.com/XX-net/XX-Net/issues/6506)

注：以下操作都是在 CentOS 系统下进行的。当然以防万一，建议大家选择 `CentOS 6`，看网上有人说 `CentOS 7` 默认的防火墙可能会干扰 SSR 的正常连接。【注：如果使用的 Ubuntu 系统也是一样的，不同的可能也就是安装存在安装 wget 的不同，Ubuntu 下使用的 apt-get 命令】

购买好了 VPS，则可以开始搭建了。首先我们需要远程连接上你的 VPS，这里可以使用 Putty、XShell 等客户端工具，也可以使用 Git Bash 下的 ssh 命令（但记得要先配置 SSH，这个就不多赘述了）。

命令：`ssh -p xx user@ip`，xx 为 端口号    user 为用户名   ip 为要登陆的 ip。

使用 Git Bash 连接 VPS 的命令：`ssh -p 22 root@ip`或`ssh root@ip`，其中“ip”替换成 VPS 的 ip，按回车键，然后复制粘贴密码，按回车键即可登录。粘贴密码时有可能不显示密码，但不影响。

``` 
yum -y install wget

wget -N --no-check-certificate https://softs.fun/Bash/ssr.sh && chmod +x ssr.sh && bash ssr.sh

# 下面是备用脚本：

yum -y install wget

wget -N --no-check-certificate https://raw.githubusercontent.com/ToyoDAdoubi/doubi/master/ssr.sh && chmod +x ssr.sh && bash ssr.sh
```

要是想要查看或重新设置输入：`bash ssr.sh`

> PS：亲测，第一个脚本文件已经不可用了，第二个还能使用，以防下次第二个也不正常使用，于是我下载下来了，以及下文提到的 BBR 加速脚本也给下载了。

### 或者安装脚本2

参考：[Vultr最简单的梯子搭建SS教程，只需30分钟，畅游互联网世界](https://segmentfault.com/a/1190000015699248)

``` xml
$ yum install wget -y
$ wget --no-check-certificate https://freed.ga/github/shadowsocksR.sh; bash shadowsocksR.sh
```

这个脚本会自动给你进行所有的设置。

安装锐速：

一键更换内核脚本（Vultr 需先执行此脚本）

``` 
wget -N --no-check-certificate https://freed.ga/kernel/ruisu.sh &&
bash ruisu.sh
```

脚本安装需要 1-3 分钟，耐心等待服务器重启，服务器重启之后，重新连接继续安装就行了。

``` 
wget -N --no-check-certificate https://github.com/91yun/serverspeeder/raw/master/serverspeeder.sh && bash serverspeeder.sh

# 下面这个是备用脚本：

wget -N --n
o-check-certificate https://raw.githubusercontent.com/91yun/serverspeeder/master/serverspeeder-all.sh && bash serverspeeder-all.sh

```

出现这些就算大功告成：![](https://img-1256179949.cos.ap-shanghai.myqcloud.com/20190217004426.png)


- 要深入了解相关「影梭」的 FQ 知识可以看：[科学上网漫游指南](https://lvii.gitbooks.io/outman/content/)

### 或者安装脚本3

关于 SSR 的服务器安装、客户端下载，可以仔细查阅该网站——[SSR中文网](https://ssr.tools/)。

参考：[SSR一键安装脚本 (ShadowsocksR一键安装教程)](https://ssr.tools/31)

``` 
wget --no-check-certificate -O shadowsocks-all.sh https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocks-all.sh
chmod +x shadowsocks-all.sh
./shadowsocks-all.sh 2>&1 | tee shadowsocks-all.log
```

小提示：如果运行上面第一条命令时，出现找不到 wget 之类的提示，则表明系统没有预装 wget，先运行以下命令完成 wget 的安装

``` 
#CentOS：
yum -y install wget
#Ubuntu/Debian：
apt-get -y install wget
```

Putty 连接至 VPS 服务器，分别运行如下各命令：

``` 
#启动SSR：
/etc/init.d/shadowsocks-r start
#退出SSR：
/etc/init.d/shadowsocks-r stop
#重启SSR：
/etc/init.d/shadowsocks-r restart
#SSR状态：
/etc/init.d/shadowsocks-r status
#卸载SSR：
./shadowsocks-all.sh uninstall
```

BBR加速脚本：[VPS服务器Google BBR一键安装脚本](https://ssr.tools/199)，同【第二步：谷歌BBR加速】小节的 BBR 加速脚本。

### ShadowsocksR 推荐协议混淆设置

协议推荐：

- 协议用 auth_chain_a 最佳，此时推荐不使用加密（设置为 none），混淆随意
- 加密选择：若协议用 auth_chain_a，那加密用 none（但不代表密码可以不写或两边不匹配）
- 若协议不是 auth_aes128_md5 或 auth_aes128_sha1，那么不能使用 rc4 加密（可用 rc4-md5）。这时加密可以在 rc4-md5、salsa20、chacha20-ietf 三个里面选择（rc4-md5 可换为 aes 系列，salsa20 可换为 chacha20 或 bf-cfb），
- 如果使用 SSR 还可特别选择 rc4-md5-6。

混淆推荐：

- 如果 QoS 在你的地区明显，混淆建议在 http_simple 与 tls1.2_ticket_auth 中选择，具体选择可以通过自己的试验得出。
- 如果选择混淆后反而变慢，那么混淆请选择 plain。如果你不在乎 QoS，但担心你的个人 vps 能不能持久使用，那么混淆选择 plain 或 tls1.2_ticket_auth，协议选择 auth_chain_a 或 auth_aes128_md5 或 auth_aes128_sha1
- 如果你用于玩游戏，或对连接延迟有要求的情况下，建议不要使用 tls1.2_ticket_auth 混淆，用其它混淆或 plain 服务端里，http_simple 与 http_post 是相互兼容的，没有使用上的区别
- 如果你在公司，或学校，或某些环境下，发现原版 SS 协议不可用，建议你启用 http_simple、http_post 或 tls1.2_ticket_auth 混淆，同时端口相应使用 80 或 443，通常能解决问题。同时能躲避你所在环境下的网络封锁（如禁止访问网盘禁止上传等等）
- 如果使用 tls1.2_ticket_auth 混淆或不开启混淆，那么协议最好不要使用 origin 或 verify_sha1
- 如果使用二重代理，一般你只需要考虑越过防火墙的那一段使用混淆或加强协议，除非为了匿名

参考：

- [当前网络环境，SS及SSR该怎么配置协议混淆才是最佳？ · cg3s/forum Wiki](<https://github.com/cg3s/forum/wiki/%E5%BD%93%E5%89%8D%E7%BD%91%E7%BB%9C%E7%8E%AF%E5%A2%83%EF%BC%8CSS%E5%8F%8ASSR%E8%AF%A5%E6%80%8E%E4%B9%88%E9%85%8D%E7%BD%AE%E5%8D%8F%E8%AE%AE%E6%B7%B7%E6%B7%86%E6%89%8D%E6%98%AF%E6%9C%80%E4%BD%B3%EF%BC%9F>)
- [ShadowsocksR 推荐协议混淆设置 - 开源中国](<https://my.oschina.net/niithub/blog/1812936>)



## Step02：谷歌BBR加速

### BBR加速脚本1

``` 
yum -y install wget

wget --no-check-certificate https://github.com/teddysun/across/raw/master/bbr.sh && chmod +x bbr.sh && ./bbr.sh
```

把上面整个代码复制后粘贴进去，不动的时候按回车，然后耐心等待，最后重启 VPS 服务器即可。重启命令：`reboot`

*关于什么是 BBR 加速，看这篇文章了解下：[SSR开启Google的BBR内核脚本加速TCP（附BBR一键安装脚本）](https://www.moidea.info/archives/445.html)*

> Google 开源了其 TCP BBR 拥塞控制算法，并提交到了 Linux 内核，从 4.9 开始，Linux 内核已经用上了该算法。根据以往的传统，Google 总是先在自家的生产环境上线运用后，才会将代码开源，此次也不例外。  
>
> BBR 是来自于 Google 的黑科技，目的是通过优化和控制TCP的拥塞，充分利用带宽并降低延迟，起到神奇般的加速效果。在BBR之前，比较有名的就是国产的锐速了，不过由于锐速是个国产的闭源软件，所以一直纠结不想装在VPS上。正好，BBR的出现，又成为一个可供折腾的对象。
>
> BBR 这个特性其实是在 Linux 内核 4.9 才计划加入的。所以，要开启BBR，需要内核版本在Linux kernel 4.9以上，根据实地测试，在部署了最新版内核并开启了 TCP BBR 的机器上，网速甚至可以提升好几个数量级。
>
> 查看内核版本：`uname -r`

### 或者安装BBR加速脚本2

**如果前面那个 BBR 加速安装失败！**那么可以看下该文安装这个 BBR 加速：[BBR+BBR魔改+Lotsever(锐速)一键脚本 for Centos/Debian/Ubuntu](https://github.com/XX-net/XX-Net/issues/6506)

> 支持系统：`Centos 6+`/`Debian 8+`/`Ubuntu 14+`
>
> 加速脚本安装，先运行如下命令：
>
> ``` 
wget -N --no-check-certificate "https://raw.githubusercontent.com/chiakge/Linux-NetSpeed/master/tcp.sh" && chmod +x tcp.sh && ./tcp.sh
> ```
> 使用脚本后会出现如下选项：
>
> ![](https://img-1256179949.cos.ap-shanghai.myqcloud.com/20190217004302.png)
>
> 根据自己需求操作，重启后再使用`./tcp.sh`命令接着操作 —> 按 4 或 5 使用 BBR 加速 ---> 基于前面介绍的方法判断是否开启 BBR 加速，比如输入命令：`lsmod|grep bbr`，如果出现 tcp_bbr 字样表示bbr已安装并启动成功。
>
> 关于什么是「魔改版 BBR」解释下：[魔改Google BBR一键安装脚本，比正常版BBR强](https://www.moerats.com/archives/190/)  —> 本方法出自于`hostloc`论坛大佬`Yankee`发布的`BBR`魔改，并由`Vicer`博主制作的一键包。魔改基本就是修改`BBR`源码，调整参数，使其更强劲。
>
> PS：如果在删除内核环节出现这样一张图
>
> ![](https://img-1256179949.cos.ap-shanghai.myqcloud.com/20190217004340.png)
>
> 注意选择`NO`，然后根据提示重启系统。



## Step02：或安装锐速加速

1、安装锐速需降级系统内核，而安装 Google BBR 则需升级系统内核，故两者不能同时安装。
2、安装锐速需降级系统内核，有可能造成系统不稳定，故不建议将其应用在重要的生产环境中。

执行下面命令：

``` 
uname -r
```

回车后输出当前系统内核版本。主要分三种情况：

*1、结果以 2 开头，例如 2.6.32-696.18.7.el6.x86_64。*

这种输出结果说明我们的服务器为 CentOS6 x64 系统。

*2、结果以 3 开头，例如 3.10.0-693.11.6.el7.x86_64。*

这种输出结果说明我们的服务器为 CentOS7 x64 系统。

*3、结果以 4 开头，例如 4.12.10-1.el7.elrepo.x86_64。*

这种输出结果说明我们的服务器已经安装 Google BBR 拥塞控制算法，此时已经无法继续安装锐速。

### 1. 若系统为 CentOS7 x64，如何安装锐速加速

如下图：

![](https://img-1256179949.cos.ap-shanghai.myqcloud.com/20190605200822.png)

以 3 开头，说明使用的 CentOS7 x64 系统，内核版本高。若要安装锐速加速，先降低系统内核：

1、首先更换内核，执行下面命令：

``` 
yum install net-tools -y && wget --no-check-certificate -O appex.sh https://raw.githubusercontent.com/0oVicero0/serverSpeeder_Install/master/appex.sh && bash appex.sh install
```

等待内核更换完毕后系统会自动重启并断开连接。系统重启后，会断开连接。等待 1~2 分钟服务器即可重启完毕，我们重新连接服务器再次连接服务器，输入下面安装命令：

``` 
yum install net-tools -y && wget --no-check-certificate -O appex.sh https://raw.githubusercontent.com/0oVicero0/serverSpeeder_Install/master/appex.sh && bash appex.sh install
```

回车。然后再按回车键继续，系统会自动安装锐速，同时会先后要求我们设置锐速的三项信息。按照下图提示，我们每次都直接回车继续即可。

![](https://img-1256179949.cos.ap-shanghai.myqcloud.com/20190605201351.png)

出现下面信息，就说明锐速安装成功了。

![](https://img-1256179949.cos.ap-shanghai.myqcloud.com/20190605201410.png)

### 2. 若系统为 CentOS6 x64，如何安装锐速加速

若你的系统选择是 CentOS6 x64，不需要更换内核，直接执行下列安装命令

``` 
wget --no-check-certificate -O appex.sh https://raw.githubusercontent.com/0oVicero0/serverSpeeder_Install/master/appex.sh && bash appex.sh install '2.6.32-642.el6.x86_64'
```

安装步骤一路回车就行了。

参考：<https://www.baishitou.cn/1524.html>



---



##  各平台影梭下载

1、各平台 Shadowsocks 客户端下载地址：[Shadowsocks - Clients](https://shadowsocks.org/en/download/clients.html)
2、SSR Mac 客户端下载：[SSR MAC客户端ShadowsocksX-NG-R下载、安装及使用教程](https://ssr.tools/164)

> Shadowsocks 的 MAC 客户端，主要有两个版本：ShadowsocksX 和 ShadowsocksX-NG，其中ShadowsocksX-NG 为ShadowsocksX 的最新版本 。**目前这两个版本仅支持 SS 原版，不支持 SSR 的混淆功能。** 
>
> 目前更建议安装 Shadowsocks-NG-R 版本。
>
> ShadowsocksX-NG-R 目前最新版本为 ShadowsocksX-NG-R8 1.4.4，适用于 iMac/Macbook。
>
> 下载：[ShadowsocksX-NG-R8.dmg](https://github.com/qinyuhang/ShadowsocksX-NG-R/releases/download/1.4.4-r8/ShadowsocksX-NG-R8.dmg)

3、另外这篇文章 [SS/SSR 简介 - 聪聪 Blog](https://congcong0806.github.io/2018/04/20/SS/#%E5%AE%A2%E6%88%B7%E7%AB%AF) 列举了很多各个平台 SS/SSR 客户端并且能点击链接到下载处。下面截图是文章中列举的 SS/SSR 部分 iOS 客户端：

![](https://img-1256179949.cos.ap-shanghai.myqcloud.com/20190228153320.png)

Shadowrocket 下载（需切换到美区下载）：<https://apps.apple.com/us/app/shadowrocket/id932747118>

## VPS推荐

[适合搭建SSR的国外VPS服务器推荐汇总](https://ssr.tools/55)

- 搬瓦工
- Vultr
- Linode
- DigitalOcean

也可以考虑下 Google Cloud，有信用卡可以薅下该羊毛：

- 【1】[谷歌云免费搭建一年SSR服务器](https://freeleox.github.io/2018/11/02/Google%20Cloud%20SSR/) 
- 【2】[10分钟教你用 Google Cloud Platform 搭建自己的VPN](https://elephantnose.github.io/2018/09/24/10%E5%88%86%E9%92%9F%E6%95%99%E4%BD%A0%E7%94%A8%20Google%20Cloud%20Platform%20%E6%90%AD%E5%BB%BA%E8%87%AA%E5%B7%B1%E7%9A%84VPN/)
- 【3】[Google Cloud Platform免费申请&一键搭建SSR & BBR加速教程](https://www.wmsoho.com/google-cloud-platform-ssr-bbr-tutorial/)
  
  > Google 云服务平台对新用户赠送 300 美元，可以免费使用 1 年。并且到期后如果不打算续费，也不会额外收取费用 （像亚马逊AWS就直接扣你费用）。
  >
  > 如果还想继续用，直接新注册个账号，免费 (现在需要新卡了)。用来搭 SS 的话, 最低配置的机型 $5/月, 出口大陆流量 1T 以内为 0.23$/1G，算下来每个月可用 80 多 G 的流量，足够用了, 当然你还可以顺便搭个网站之类的。
  >
  > 注意：需要用到信用卡!!!
  
- 【4】[Google Cloud Platform免费申请&一键搭建SSR & BBR加速](https://allen-feng.github.io/2019/04/24/190424_Google-Cloud-Platform免费申请-一键搭建SSR-BBR加速/)

本人按照【2】搭建，但注意，我看别得文章，在创建防火墙规则的时候“协议和端口”选择“全部运行”就行，并且可以不用进行“负载均衡”配置。

最后就是登陆服务器进行搭建 SSR，为了方便，建议使用 SSH 方式登陆。注意，想要 SSH 方式登录前先配置静态服务器静态 IP，如何配置，参考【4】中操作。配置完成，还需要修改一处，修改参考[用SSH工具XShell连接谷歌云 root用户或普通用户]( https://blog.csdn.net/datadev_sh/article/details/79593360 )，这里也有个地方注意，就是重启服务器，如果发现最后还是登陆不进，请使用 `sudo service sshd restart` 该命令重启试试。注：SSH 客户端推荐 MobaXterm 这个软件。搭建的主要步骤如下：

1、创建防火墙规则
2、创建实例
3、登录服务器搭建 SSR

## 补充：关于DigitalOcean VPS的说明

本人目前一直在用 DigitalOcean。如果你也打算使用这家 VPS，可以考虑使用我这个分享[链接](https://m.do.co/c/632db6a2a3e4)注册。下面是官网给出的：

```
Give $50, Get $25
Everyone you refer gets $50 in credit over 30 days. Once they’ve spent $25 with us, you'll get $25. There is no limit to the amount of credit you can earn through referrals.
```

下面是关于 DigitalOcean 流量和计费方式的问题：

**（1）流量**

*[Digitalocean套餐全面升级，价格不变，内存翻倍：KVM/IPv6/按时付费](https://www.vpsrb.com/735.html)：*

> Digitalocean 2018 年给所有的套餐都升了个级，在价格不变的基础上，所有套餐内存翻倍。从原先的 512M 内存起，变成了 1G 内存起，付费方式依然为按时付费，1G1 核，25G SSD，不限流量的最低套餐每小时 0.007 美元，用多少算多少，用满一个月则需 5 美元。套餐明面上写着月流量 1T 起，实际上是不限流量的。

*[DigitalOcean 对超出流量收费了](https://www.v2ex.com/t/450840)：*

> 之前一直是超出不另外计费，相当于无限流量，从 4 月开始，超出流量开始收费...

**（2）计费** 

*2014-05-15 [DigitalOcean是如何计算费用](http://moe.mwulu.com/digitalocean-feiyong/)*

1) 按月和按小时计费

如果你整月使用 DigitalOcean 的服务器，则按月和按小时计费是没有任何差别。账单中是显示按小时计费，每小时扣费直到每月付款上限。DigitalOcean 按照每个月 672 小时（28天）计算费用，如果你使用不到 672 小时，则按照实际使用小时数计算费用；如果每月使用超过 672 小时，超过 672 小时的部分不收取任何费用，只收取每月付款上限，如 5 美元。具体本人测试大约一小时 0.01 美元。

2) 如何分清扣款

很多使用 DigitalOcean 的同学都不知道 DigitalOcean 到底是怎么计费的，按照官方的最低配置是 5 刀一个月，那么我们充值了 5 刀后直接开通最低配置就扣除账户 5 刀的余额没？答案是：错的！DigitalOcean 的计费是按时计费，按照你开通的云服务器的使用时间来计费，当你删除云服务器液滴后将会停止计费（关机还会在依旧扣费）。他们官方已经有具体的配置价格对照表，而且在开通液滴的时候也有显示每小时计费多少钱，扣除的余额是从您充值的账户里面慢慢扣，非常灵活的计费系统功能。

*[DigitalOcean 扣费方法/DigitalOcean怎么月付？](http://digitalocean.lofter.com/post/2040f2_6c3214)*

DigitalOcean 使用小时计费模式，删除后便不再计费，非常合理。每小时的价格为0.007美元。`0.007美元/小时x每天24小时x每月30天=5.04美元=30.8992人民币`。`0.007x24x365=61.32美元=375.9407人民币`。之前我也奇怪，为什么在购买的时候没有选择按月计费呢？仔细研究下才知道按小时扣费和按月扣费没有区别，反而更节省。

![](https://img-1256179949.cos.ap-shanghai.myqcloud.com/20190112140010.png)

**（3）关于欠费问题**

本人在使用 DigitalOcean 欠费后还能继续使用，欠费好多天后还能用，纳闷了，总觉得要了解清楚，于是发起了一个 Ticket，得到的回复大概意思是，到了一定时间会自动关掉的。

那我便没放在心上，因为觉得再欠费几天就会被自动停掉，但没有想到的是欠费二十多天，欠费 6.73$，依旧能使用，而且每天给我发邮件提示欠费金额。看着每天都在扣费，但又不给我自动关闭，心里着实不够踏实，于是我打开网站准备主动删除 Droplet，发现删不掉，看到网上有人说可以试试注销账号方式，于是试着注销账号，注销不了，很坑啊，再到网上找解决方式，看到有人提到发起 Ticket，于是我第二次发起一个 Ticket，内容如下：

``` html
Hello,I'm your old friend. Last year I heard about Digital Ocean from Github,I also got an exclusive education offer on github.I got a $50 coupon so l used it to buy ur server.I used ur vps to build up my web services ..... That's all reasons that I should thank you!

I usually recommend your service to my classmates and friends, some of them choose to sign up as your paying users..…Due to my recent negligence and I didn't often check my email in time, my account owed $6.73, I thought you would stop my service as long as my account balance runs out. I remember I started a ticket last time and mentioned this problem. Now I am very anxious, and want to stop my service, but it won't work.I don't konw why.

I am not deliberately do that, can you don't ask me pay for the bilng that I overuse, or can you allow me to destroy my service?My account is ishuzb@sina.com. I would appreciate it if you can help me!

One way or another,I love your service and I will recommend Digital Ocean to my friend!
Thanks a lotl!
```

然后过不多久就收到好几封邮件，其中一封：

``` xml
Hello,

I have added a $10 credit to your account to cover the small balance. This should remove the hold on your account and allow you to login. 

Please remove all active services before deactivating the account. 

If you have any further questions or concerns, please feel free to reach back out to us at any time.

Best, 
Wendy
Platform Support Specialist
```

直接给了我账户 10$，DigitalOcean 真是牛逼。哈哈，总算可以删除了。

注：这里多说下我的「经验教训」，如果你是第一次使用，可以使用通过链接（这个网上搜下，我搜到的是这个：<https://try.digitalocean.com/virtual-private-servers/>）注册可以获得对新用户的 100 美刀，但有效期时间 60 天，然后你付款 5 美刀定金就可以使用了 digitalocean 了，但是这个时候如果你要是还有 digitalocean 的优惠码，就不能使用了。所以如果你有优惠码的话，就不要通过那个链接注册，直接进入官网注册账户就好，这样才可以使用优惠码。



# 二、V2Ray 的搭建

## 1. V2Ray介绍

类似影梭代理方式，有个叫 V2Ray 也可以关注下，教程 [V2Ray 配置指南](https://toutyrater.github.io/)。

> V2Ray 是一个与 Shadowsocks 类似的代理软件，可以用来科学上网（翻墙）学习国外先进科学技术。

V2Ray 跟 Shadowsocks 有什么区别？

> 区别还是有的，Shadowsocks 只是一个简单的代理工具，而 V2Ray 定位为一个平台，任何开发者都可以利用 V2Ray 提供的模块开发出新的代理软件。
>
> 了解 Shadowsocks 历史的同学都知道，Shadowsocks 是 clowwindy 开发的自用的软件，开发的初衷只是为了让自己能够简单高效地科学上网，自己使用了很长一段时间后觉得不错才共享出来的。V2Ray 是 clowwindy 被喝茶之后 V2Ray 项目组为表示抗议开发的，一开始就致力于让大家更好更快的科学上网。
>
> 由于出生时的历史背景不同，导致了它们性格特点的差异。
>
> 简单来说，Shadowsocks 功能单一，V2Ray 功能强大。听起来似乎有点贬低 Shadowsocks 呢？当然不！换一个角度来看，Shadowsocks 简单好上手，V2Ray 复杂配置多。

相关教程：

- [科学上网工具 V2Ray 简介及具体搭建流程-SSR中文网](https://ssr.tools/265)
- [V2Ray搭建教程：小白图解版 | 翻个墙翻个墙](https://fangeqiang.com/2030.html)

## 2. 客户端介绍

V2Ray服务器搭建完成后，就可以在本地设备中安装客户端进行连接了。下面我们分别介绍 V2Ray 的各平台客户端的下载和使用，包括：

``` xml
V2Ray Windows客户端
V2Ray 安卓客户端
V2Ray iOS客户端
V2Ray Mac客户端
```

注意：V2Ray 官方仅提供内核，没有图形化界面，所以各平台客户端，为第三方在官方内核基础上发展出的图形化界面，或者是兼容 V2Ray 协议的 APP。

鉴于 V2Ray 版本更新很快，并且 Windows 客户端需要分别下载 V2Ray 内核、V2Ray 图形化界面，所以此处不直接给出下载地址。参考：[V2Ray各平台客户端下载汇总 带图形化界面！-SSR中文网](https://ssr.tools/314)

客户端下载：

![](https://img-1256179949.cos.ap-shanghai.myqcloud.com/20190124153425.png)


# 三、实现路由器科学上网


参考：

- [改造路由器实现“无痛的科学上网”——其实没那么难](<https://jizusun.github.io/openwrt-router-intro>)
- [SSR 路由器客户端下载、安装及使用教程（openwrt ShadowsocksR）-SSR中文网](<https://ssr.tools/136>)





---

*update：2019-04-12*