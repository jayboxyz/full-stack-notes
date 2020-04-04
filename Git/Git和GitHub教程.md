# Git/GitHub 教程

## 一、Git

### 1.1 Git 基础

#### Git 命令

- `git init`： 初始化一个目录，其实初始化完毕然后本地多出了一个 `.git`的隐藏目录，这个目录管理着一个代码库的版本信息。

- `git add`： 把一个文件从`untracked`（未被追踪）状态转为到 `staged`状态，直白的讲，就是把文件提交到`暂缓区`，这个时候还没真正意义上的代码提交。格式为：`git add .`提交所有改动，`git add hello.txt`提交指定文件的改动。

- `git commit`： 这步才是真正的代码提交到仓库，格式为：`git commit`或者加参数`git commit -m “这次的提交说明信息”`，前者会进入一个页面，输入 i 可以进入编辑界面，再写上这次的提交的注释说明信息（一般用来记录本次提交的主要意图），然后按 ESC 键退出编辑返回到命令模式，然后连续输入两个大写的 “Z”（用 Shift 键或 Capslock 键都可以），就保存并退出了；后者的话直接可以写上提交的注释说明信息。

  如果在提交的时候出现提示设置邮箱和用户名，是为了保证提交的准确性，在提交的时候 user.name 和 user.email 会进入日志，这些信息，是追踪代码变更的关键，比如是谁修改的。以后会随更新内容一起被永久纳入历史记录。

  注：在设置用户名的时候，可以使用任意的字符。Git 实际上是使用 email 进行关联每次提交的，只不过使用 username 作为标示符来进行显示。当你的 email 地址和 github上的 email 地址一致时，则会使用 GitHub 上面的 name 来进行显示。

- `git status`： 查看仓库文件状态。可以加参数 -s，即`git status -s`，加个 -s 用简洁模式查看当前修改和仓库里面差别多少，可以看到有多少文件被新增了，多少被修改了，多少被删除了。

- `git log`： 查看提交历史记录，即版本历史信息，比如谁提交的，什么时间提交的。

- ...待续

配置 Git 提交的用户名和邮箱：

如果工作中只涉及一个 Git 服务器，用一个全局配置就可以了。

``` xml
git config --global user.name "strivebo"
git config --global user.email "ishuzb@gmail.com"
```

非全局配置，某个项目下的配置：(去掉`--global`)

``` xml
git config user.name "strivebo"
git config user.email "ishuzb@gmail.com"
```

查看修改后的配置：

``` xml
git config --global user.name 或 git config user.name
git config --global user.email 或 git config user.email
```

取消全局配置：

``` xml
git config --global --unset user.name
git config --global --unset user.email

git config --global user.name    #(查看)全局配置账户是否已经移除
git config --global user.email   #(查看)全局配置邮箱是否已经移除
```



### 1.2 Git 进阶



### 1.3 Git GUI 客户端

#### GitHub Desktop

- [GitHub Desktop图文教程 - 简书](<https://www.jianshu.com/p/a6fc842f501d>)

建议还是使用下面的 SourceTree 吧。

#### SourceTree

SourceTree 是 Windows 和 Mac OS X 下免费的 Git 和 Hg 客户端，拥有可视化界面，容易上手操作。同时它也是 Mercurial 和 Subversion 版本控制系统工具。支持创建、提交、clone、push、pull 和 merge 等操作。

1、安装

- [SourceTree安装（小白特别详细教程） - 云+社区 - 腾讯云](<https://cloud.tencent.com/developer/article/1369196>) - 本人使用的 Google 账号。
- [SourceTree 免注册免登陆防坑法（windows版本）- SegmentFault 思否](<https://segmentfault.com/a/1190000012104165>) - 免注册的办法，可以试试。

2、使用

- [SourceTree的基本使用 - 天字天蝎 - 博客园](<https://www.cnblogs.com/tian-xie/p/6264104.html>)
- [Sourcetree安装与使用 - 掘金](<https://juejin.im/post/5a54e1976fb9a01ca32527fd>)



## 二、GitHub 

GitHub Trending：<https://github.com/trending>

GitHub 全球排名：<https://gitstar-ranking.com/>

GitHub 帮助文档：<https://help.github.com/en>(英文) | <https://help.github.com/cn>(简体中文)

学习资料：

- [github-cheat-sheet](<https://github.com/tiimgreen/github-cheat-sheet>) - 含 GitHub 的各种使用和技巧。  [荐]
- 



### 2.1 GitHub 基本使用

1、添加 SSH

打开 Bash：`ssh-keygen`。生成私钥公钥，默认保存在 C 盘的用户目录下。



Wiki 的使用：

- [GitHub Wiki 页面的添加和设置 - LPD-iOS](<https://lpd-ios.github.io/2017/07/11/GitHub-Wiki-Introduction/>)



### 2.2 GitHub 进阶使用



如何高效管理 GitHub Star？

1、Astral：<https://github.com/astralapp/astral>

> 一款优雅便捷的 GitHub Star 管理工具。它主要具备以下功能：
>
> - 简便的标签系统
> - 过滤 & 搜索
> - 文档快速阅读
> - 便签备注功能
> - 完全免费且开源

2、The Fucking GitHub：<https://github.com/lvxianchao/the-fucking-github>

> 可以很方便的查看、整理、搜索在 GitHub Star 过的项目。它主要具备以下功能：
>
> - 标签系统
> - 项目目录系统
> - 快速检索
> - 多端数据同步
> - 免费且开源

3、Remu：<https://github.com/zenghongtu/Remu>

> 该插件在兼具前面两款插件功能的情况下，针对 Star 标签添加这一操作做了优化：用户在 Star 完一个项目之后，可以随手给项目打上标签。
>
> 值得一提的是，由于 Chrome 浏览器自带的 storage.sync 数据同步接口仅有 100KB 的存储容量，因此作者采用 gists 来完成同步功能，顺带能查看历史记录，也算是开发上的一个小 trick。









