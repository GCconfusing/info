---
 layout: post
 title: 2020电子部简易Markdown教程
 date: 2020-9-10
 author: multicoloredstone
 permalink: /blog/2020/Simple-Guide-Markdown
 categories:
     - blog
 tags: Markdown

---

<!--more-->

## 给萌新的三连

#### 什么是Markdown？

&emsp;&emsp;Markdown是一种**轻量级**的文本标记语言，通过一些简单的标记语法，它可以使普通的文本具有一定的格式。

&emsp;&emsp;Markdown的语法非常简单，所以最终呈现的效果也往往是简洁、单一的。它无法用于复杂的排版，但缺点就是优点——Markdown的使用者得以专注于内容本身，无需调整格式就能获得不错的阅读体验，你们现在阅读的文档就是使用Markdown编写的。

&emsp;&emsp;同时，Markdown格式简洁轻量的特性让它能够很容易地被分享，容易渲染之后在网页上显示，也可以方便地转换为各种格式。

#### 为什么学习Markdown？

&emsp;&emsp;Markdown在技术工作者群体当中正得到越来越广泛的应用——Github、SourceForge、reddit等网站使用Markdown编写帮助文档（github的readme.md很多人应该都见过，.md就是Markdown文档的意思）；知乎、简书、思否、掘金等软件支持Markdown格式的内容；而如果想要自己搭建博客的话，大多数个人博客的博文也是使用Markdown编写的。

&emsp;&emsp;总之，Markdown的轻量和跨平台特性使之成为一种非常易用的东西。同时，由于它所使用的标记符号很少，所以学习起来也是很快的，我认为每一个技术工作者都该学习一下Markdown。我保证，花一个小时你就能学会基本的使用，而且你一定会喜欢它的简洁。

#### 如何学习Markdown

&emsp;&emsp;关于Markdown的使用，网络上现有的资源已经非常好了，我们无意再制造一份全面的教程来进行无意义的讲解，关于Markdown的基本知识请大家通过以下链接进行学习：

* https://www.runoob.com/markdown/md-tutorial.html
* https://www.jianshu.com/p/191d1e21f7ed
* https://guides.github.com/features/mastering-markdown/  （全英，慎入哦（其实挺简单的））
* https://github.com/younghz/Markdown

&emsp;&emsp;然后，我们推荐的编写工具为[Typora](https://typora.io/)，日常的笔记如果可以公开的话推荐大家使用[思否](https://segmentfault.com/)发布（当然也可以自己搭博客），保存笔记时选择Markdown格式即可。

### Markdown在电子部日常中的使用

&emsp;&emsp;如果你全面地浏览了我们给出的链接中的内容，那么你可能会觉得“好像Markdown学习来还有一点复杂？”

&emsp;&emsp;错觉，绝对是错觉。

&emsp;&emsp;下面笔者来给大家总结一下电子部日常里Markdown的使用。

&emsp;&emsp;首先，说一下最常用的元素——其实就五个——标题、列表、图片、超链接、代码。

### 最常用元素解析

#### 一、标题

&emsp;&emsp;在Typora里面（之后的说明都默认在Typora中进行），敲一个`#`出来，然后敲一下空格，接下来输入的一行就算是标题文字了，`#`号的多少用于区分标题的层级，支持六级标题。

#### 二、列表

&emsp;&emsp;列表可以分为有序列表和无序列表。

&emsp;&emsp;无序列表是这样的：

* 条目一
* 条目二
* 条目三

&emsp;输入一个`*`号然后敲下**空格或Tab**就可以开始一个无序列表，输入一个条目的内容后回车可以开始下一个条目，不进行下一条目的内容输入而再次按空格的话可以结束当前的列表；不进行输入而按BackSpace退格的话可以删掉小圆点但仍在条目内容起始处进行输入。

&emsp;&emsp;有序列表是这样的：

1. 条目一
2. 条目二
3. 条目三

&emsp;&emsp;输入一个数字 + `.`(英文句号)然后**"空格/Tab"**可以开始一个有序列表，其他操作与无序列表相同。

#### 三、图片

&emsp;&emsp;推荐使用这样的方式插入图片：输入`![]()`（注意是英文括号），然后将图片路径输入到圆括号中，为了方便管理，推荐在本地书写文档时为每份笔记分配一个文件夹，然后在其下建立一个图片文件夹（比如“Picture” “Image”什么的），然后，使用相对路径插入图片。

&emsp;&emsp;比如这样：`![](./Picture/P1.jpg)`

#### 四、超链接

&emsp;&emsp;插入超链接的方法是输入`[]()`，然后，把你希望显示的文字放进方括号，实际链接放进圆括号。比如，如果你输入`[谷歌](https://www.google.com)`，那么显示效果是这样的：[谷歌](https://www.google.com)

&emsp;&emsp;稍微要注意一下的地方是：在向括号中粘贴链接的时候，请先按Ctrl + / 切换到源代码模式（可以比较一下两种模式下粘贴链接后最终的源码）。

#### 五、代码

&emsp;&emsp;写技术文章当然少不了放代码啦，但是Markdown编辑器（例如Typora）会对原始内容进行渲染，所以不能直接输入。代码输入的话，有单行和多行之分，都需要使用反引号  \`（一般在你键盘左上角，Esc下面，记得使用英文模式），用一对反引号包起来的内容被视为单行代码，将按照原始内容显示，比如这样：`printf(Hello!);`

&emsp;&emsp;而插入多行代码的方式是——在一行的开头敲三个反引号然后回车，显示效果如下：

```c
#include <stdio.h>
int main()
{
	printf("Hello World!");
	return 0;
}
```

### 一点补充

&emsp;&emsp;总的来说，会用上面的五个元素的话，平常写文档就没问题了，不过，为了改善阅读体验，你可能偶尔会需要使用以下几个元素：

> 这一般表示引用，英文模式输入一个>然后空格即可

`**内容**`-----这样可以给内容**加粗**

`$$`----输入这个然后回车可以插入公式，一般大家使用Latex语法来描述公式，相关内容很多，但是能做出很不错的效果，如下：
$$
\sum_{k=\frac{1}{2}}^{N^2}\frac{1}{k}
$$
&emsp;&emsp;另外，Markdown里直接输入空格的话，如果导出为PDF，那么这些空格当中处于一行文字起始位置的空格将不会被保留，如果希望文字开头有空格效果的话，使用`&emsp;`（英文分号）来显示一个空格。

&emsp;&emsp;更多的小技巧，请大家在使用的过程中探索。

<p align="right">by multicoloredstone</p>

