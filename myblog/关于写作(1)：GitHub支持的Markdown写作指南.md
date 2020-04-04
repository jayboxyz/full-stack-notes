---
title: Git&GitHub 学习4：GitHub支持的Markdown写作指南
date: 2019-02-13 20:01:08
categories: 版本控制
tags: [Blog,Markdown,GitHub] 
---

GitHub 的 MarkDown 语法在标准的 Markdown 语法基础上做了扩充，称之为 GitHub Flavored Markdown，简称 GFM，GFM 在 GitHub 上有广泛应用，除了 README 文件外，issues 和 wiki 均支持 Markdown语法。<!-- more -->

## 一、Markdown最常用格式

### 0. 标题

标题是每篇文章必备而且最常用的格式。在 Markdown 中，如果想将一段文字定义为标题，只需要在这段文字前面加上 #，再在 # 后加一个空格即可。还可增加二、三、四、五、六级标题，总共六级，只需要增加 # ，增加一个 # ，标题字号相应降低一级。如图：

![](http://note.youdao.com/iyoudao/wp-content/uploads/2016/09/2-0-%E6%A0%87%E9%A2%98.png)

### 1. 列表（有序、无序列表）

列表格式也很常用，它可以让你的文稿变得井井有条。在 Markdown 中，你只需要在文字前面加上 - 就可以了；如果你希望是有序列表，在文字前面加上 1. 2. 3. 即可。*注：-、1.和文字之间要保留一个字符的空格。*

![](http://note.youdao.com/iyoudao/wp-content/uploads/2016/09/2-1-%E5%88%97%E8%A1%A8.png)

### 2. 引用

如果你需要在文稿中引用一段别处的句子，那么就要用到「引用」格式。在引用文字前加上 > 并与文字保留一个字符的空格，即可。

![](http://note.youdao.com/iyoudao/wp-content/uploads/2016/09/2-2%E5%BC%95%E7%94%A8.png)

### 3. 粗体和斜体

Markdown 的粗体和斜体也非常简单：用两个 * 包含一段文本就是粗体的语法；用一个 * 包含一段文本就是斜体的语法；用三个 * 包含一段文本就是粗体+斜体的语法。

![](http://note.youdao.com/iyoudao/wp-content/uploads/2016/09/2-3-%E7%B2%97%E4%BD%93%E6%96%9C%E4%BD%93.png)

### 4. 链接与图片

链接：在 Markdown 中，插入链接只需要使用 `[显示文本](链接地址)` 即可。

图片：在 Markdown 中，插入图片只需要使用 `![显示文本](图片链接地址)` 即可。

*注：插入图片的语法和链接的语法很像，只是前面多了一个 ！*

![](http://note.youdao.com/iyoudao/wp-content/uploads/2016/09/2-4%E9%93%BE%E6%8E%A5%E4%B8%8E%E5%9B%BE%E7%89%87.png)

### 5. 分割线

分割线的语法只需要另起一行，连续输入三个星号 *** 即可分割两段文字内容。如图：

![](http://note.youdao.com/iyoudao/wp-content/uploads/2016/09/2-5-%E5%88%86%E5%89%B2%E7%BA%BF.png)

### 6. 表格

当你需要在 Markdown 文稿中键入表格，示例如下：

![](http://note.youdao.com/iyoudao/wp-content/uploads/2016/09/2-6-7.png)



## 二、Markdown还可以做什么？

### 1. 代码高亮

![](http://note.youdao.com/iyoudao/wp-content/uploads/2016/09/1-1%E4%BB%A3%E7%A0%81%E9%AB%98%E4%BA%AE.png)



### 2. 制作待办事项To-do List

待办事项和清单在日常工作、生活中经常被使用。在 Markdown 中，只需要在待办的事项文本或者清单文本前加上 - [ ]、- [x] 即可。

\- [ ] 表示未完成，- [x] 表示已完成。

*注：键入字符与字符之间都要保留一个字符的空格。*

![](http://note.youdao.com/iyoudao/wp-content/uploads/2016/09/1-2%E5%BE%85%E5%8A%9E%E4%BA%8B%E9%A1%B9.png)



### 3. 高效绘制 流程图、序列图、甘特图、表格

#### 流程图：

在 Markdown 中，一段流程图语法以 “\` 开头，以 “` 结尾。

在 “` 后另起一行，书写graph XX，用以确定将要绘制的流程图及其类型（XX表示流程图类型）。

流程图分为竖向和横向两大类，竖向包括自上而下和自下而上两种顺序，横向包括从右到左和从左到右两种顺序。

其对应语法分别为：graph TB/graph BT/graph RL/graph LR。

- TB - top bottom（自上而下）
- BT - bottom top（自下而上）
- RL - right left（从右到左）
- LR - left right（从左到右）

示例如图：

![](http://note.youdao.com/iyoudao/wp-content/uploads/2016/09/%E6%B5%81%E7%A8%8B%E5%9B%BE.png)

**①对框线形状的调整，如，** 

![](http://note.youdao.com/iyoudao/wp-content/uploads/2016/09/++.png)

**②对箭头的调整，如，** 

![](http://note.youdao.com/iyoudao/wp-content/uploads/2016/09/+++.png)

#### 序列图：

![](http://note.youdao.com/iyoudao/wp-content/uploads/2016/09/%E5%BA%8F%E5%88%97%E5%9B%BE.png)

#### 甘特图：

我们在工作中用甘特图作计划进度表、项目进度表再合适不过了。与流程图一样，Markdown 中，甘特图的语法也是以 “\` 开头，以 “` 结尾。

在 “` 后另起一行，书写 gantt ，用以确定将要绘制的是甘特图。

![](http://note.youdao.com/iyoudao/wp-content/uploads/2016/09/%E7%94%98%E7%89%B9%E5%9B%BE.png)

#### 表格：

![](http://note.youdao.com/iyoudao/wp-content/uploads/2016/09/1-3%E8%A1%A8%E6%A0%BC.png)



### 4. 书写数学公式（注：GitHub不支持）

![](http://note.youdao.com/iyoudao/wp-content/uploads/2016/09/%E6%95%B0%E5%AD%A6%E5%85%AC%E5%BC%8F.png)



## 三、补充：GitHub支持的Markdown

一、二节 Markdown 语法格式以及图片链接都是摘自有道云笔记官方的 Markdown 指南。大部分 Markdown 写作平台应该基本都能支持的上面的语法 ，部分不支持再参考下面的内容。

### 1. 目录索引

使用 `[TOC]`自动生成目录，即不支持如下格式生成目录：

``` xml
[TOC]

### 技术
#### Java
#### Python
```

目前 CSDN、有道云笔记、Typora 等都是支持的，掘金、GitHub 不支持。对于在 GitHub 写作来说，可以利用锚记手动写一个目录，示例代码如下：

``` xml
<!-- TOC -->

- [编程技术](#编程技术)
  - [Java编程](#Java编程)
  - [Python编程](#Python编程)
- [编程之外](#编程之外)

<!-- /TOC -->
```

其中，注意的地方，也是正确的操作姿势：

> 这里的格式：`[这里写上你要显示的目录名称](#这里是标题名称)`，# 后面的标题名称不能完全复制粘贴标题名称，实质需要修改，这样修改：如果标题中含有逗号`,`、顿号`、`、句号`。`、点`.`、括号`(`、`)`、引号`“ ”`、问号`?`等这样的符号（包括全角、半角）都去除掉，空格符号用`-`代替，这样就可以目录索引了。（注：标题中含有英文的话，不管是大写小写，在 # 后都可以随意大小写，不一定要一样。）
>
> PS：我也是使用该项目：[CyC2018/GFM-Converter](https://github.com/CyC2018/GFM-Converter) 发现这些的。该项目可以直接把 [TOC] 格式生成的目录转换为 GitHub 支持的目录， **推荐使用！** 使用步骤：
>
> 1. 先编译：`javac App.java`；
> 2. 在运行：`java App`，然后会提示输入文件的路径；
> 3. 输入需要转换的文件的完整路径（带文件名的那个路径，且包含后缀），点击“Enter”即可转换完成。
>
> PS：该项目还有些符号没考虑到，比如代码还未对问号做去除处理，2019-01-31。我 fork 了一份，哈哈，考虑今后或许我要是有能力修改呢：[strivebo/GFM-Converter](https://github.com/strivebo/GFM-Converter)。
>
> 另外该项目还支持把 LaTex 转换为 GitHub 支持的形式，赞。


### 2. 返回顶部

①如返回到文章开头的标题：`GitHub支持的Markdown的语法使用指南`，直接使用 Markdown 方式：

``` xml
[回到顶部](#GitHub支持的Markdown的语法使用指南)
```

效果：[回到顶部](#GitHub支持的Markdown的语法使用指南)

②或是使用 HTML 方式：

``` xml
<div align="center">
        <a href="#GitHub支持的Markdown的语法使用指南">回到顶部</a>
</div>
```

效果：

<div align="center">
        <a href="#GitHub支持的Markdown的语法使用指南">回到顶部</a>
</div>
注意的地方，也是正确的操作姿势：

> 这里的格式：`[这里写上你要显示的目录名称](#这里是标题名称)`，# 后面的标题名称不能完全复制粘贴标题名称，实质需要修改，这样修改：如果标题中含有逗号`,`、顿号`、`、句号`。`、点`.`、括号`(`、`)`、引号`“ ”`、问号`?`等这样的符号（包括全角、半角）都去除掉，空格符号用`-`代替，这样就可以目录索引了。（注：标题中含有英文的话，不管是大写小写，在 # 后都可以随意大小写，不一定要一样。）



### 3. 定义锚点实现页面随处跳转

锚点（英文名：anchor）：是网页制作中超级链接的一种，又叫命名锚记。命名锚记像一个迅速定位器一样是一种页面内的超级链接，运用相当普遍。

锚点用法：锚点用 id 属性来设置，一个标签如果有 id 属性（或者 name 属性），那么就是页面的一个锚点。如：

``` html
<a id="anchor">我的作品</a>  
或者
<a name="anchor">我的作品</a> 
或者使用别的标签也都可以
<p id="anchor">我的作品</p>  
```

①那么实现页面内跳转，这样即可：

``` html
<a href="#anchor">查看我的作品</a>	    //超级链接，链接的该页面的锚点
```

②跨页面跳转：

``` html
<a href="页面.html#anchor">点击查看我的作品</a>      //超级链接，链接的事另一个界面的锚点
```

GitHub 是支持可以这样做的。这样话，假设想要在页面 B 处返回到 A 处，可以在 A 处定义一个没有文字的锚记，如：

``` html
<a id="mao"></a>
```

注：A 处可以是任何地方，包括标题处，只要是没有文字，文档 Push 到 GitHub 页面也不会显示的。

然后 B 处：

``` html
<a href="#mao">返回到前文</a>
```

这样就可以点击 B 处的「返回到前文」返回到 A 处。当然在 B 处定义锚记（添加个 id 属性即可）：

``` html
<a href="#mao" id="bottom">返回到前文</a>
```

然后 A 处想要返回到 B 处来，形式类似。前面小节关于目录索引、返回顶部实质也是利用的锚记。

### 4. 代码折叠

折腾效果，使用格式：

``` xml
<details>
    <summary><b>示例：Hello World 程序</b></summary> 

?``` java
代码
?```

</details>
```

示例如下：

``` xml
<details>
    <summary><b>示例：Hello World 程序</b></summary> 

?``` java
public class Hello{
    public static void main(String[] args){
        System.out.println("Hello World!");
    }
}
?```
    
</details>
```

<details>
    <summary><b>示例：Hello World 程序</b></summary> 

``` java
public class Hello{
    public static void main(String[] args){
        System.out.println("Hello World!");
    }
}
```

</details>

*注：`<details>`为 HTML5 标签，与`<summary>`配合使用可以为 details 定义标题。标题是可见的，用户点击标题时，会显示出 details。*

### 5. LaTex数学公式（GitHub不支持）

在前面有提到该项目：[CyC2018/GFM-Converter](https://github.com/CyC2018/GFM-Converter) 代码，可以支持把 LaTex 书写的数学公式转换为 GitHub 支持的形式。另外，推荐下这个软件：[Mathpix](https://mathpix.com/)，可以将方程式截图转为 LaTex 格式。

### 6. 文字高亮（GitHub不支持）

文字高亮显示，有道云笔记、Typora 支持，格式：`==需要高亮的文字==`。有道云笔记效果：

![](https://img-1256179949.cos.ap-shanghai.myqcloud.com/20190127205122.png)

### 7. 文字下划线（GitHub不支持）

①为文字添加下划线，格式：`++需要下划线的文字++`，有道云笔记支持，Typora、GitHub 不支持。有道云笔记效果：

![](https://img-1256179949.cos.ap-shanghai.myqcloud.com/20190127205207.png)

②为文字添加下划线，格式：`<u>需要下划线的文字</u>`，有道云笔记、Typora 支持，GitHub 不支持。

### 8. 文字添加删除线

为文字添加删除线，格式：`~~需要添加删除线的文字~~`。效果：~~需要添加删除线的文字~~。

### 9. GitHub支持的表情符号

每个表情的符号码，可以查询 GitHub 官方网页：<http://www.emoji-cheat-sheet.com>

查看：[Emoji表情中文翻译版](./Emoji表情中文翻译版.md)。



## 参考资料

- GitHub：[guodongxiaren/README](https://github.com/guodongxiaren/README#%E6%A8%AA%E7%BA%BF)
- [【简明版】有道云笔记Markdown指南](http://note.youdao.com/iyoudao/?p=2411)
- [【进阶版】有道云笔记Markdown指南](http://note.youdao.com/iyoudao/?p=2445)

