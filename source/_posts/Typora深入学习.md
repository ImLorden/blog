---
title: Typora深入学习
date: 2024-07-28 17:58:11
categories:
tags:
keywords:
description:
cover:
top_img:
---


# Typora深入学习

> 参考文档
>
> [1.官方文档](https://support.typora.io/)
>
> [2.主题馆](https://theme.typora.io/)
>
> ​	[2.1 如何添加主题](https://blog.csdn.net/weixin_46106283/article/details/109880938)
>
> [3.格式速查表](https://markdown.com.cn/cheat-sheet.html)




[toc]









## 一、Markdown语法



### 1.Block Element元素块

#### paragraph and line breaks段落和换行符

​	英文喜欢的分段就是空一行开始接下一段。这里介绍一个“软换行”和“硬换行”的概念和区别。

|      |                  |                 |
| :--- | :--------------- | :-------------- |
|      | 硬换行           | 软换行          |
| 键位 | `enter`          | `shift + enter` |
| 作用 | 换行，开启下一段 | 换行不开        |



#### headings标题

​	使用#号创建的最多六级标题，可以注意的是许多Markdown编辑器都有设置题目的快捷键(shortcut)，为`command + 1-6,0`但其实markdown的初衷就是纯粹的文字编辑，使用快捷键就有些脱离本质了，但不得不说，类似表格形式麻烦的编辑方式，使用快捷键可以节省不少时间。

​	另外，本笔记是面向有一定markdown基础的，因此类似`如何用#创建标题？`这样的问题可在我的`参考文档3`中可以快速的查阅。这里也可快速点击[链接](https://markdown.com.cn/cheat-sheet.html)进行查阅。





#### blockquotes引用块

> 这是一级引用
> > 这是二级引用
> > > 这是三级引用

这里通过查看引用用法的原始格式发现了：换行复制格式的本质是复制了符号,而删除退格就是删除了一个格式符号， 而格式符号越多，通常级数越低。



#### Lists列表

分为有序列表和无序列表(ordered or unordered)，可以说是最常用的block了

- 无序列表
  - 无序列表子项1
  - 无序列表子项2
  - ...



1. 有序列表
   1. 有序列表子列表1
   2. 有序列表子列表2
   3. ...



#### task list工作表

- 意外的是，task list居然是markdown的通用格式
- [ ] task 1

其实这个东西还蛮难打出来的，`-空格[空格]空格`，需要键入六次

- [x] task done

这个东西又是这样产生的：`-空格[x]空格`，同样需要键入六次，就是把之前括号里的`空格`换成了`x`



#### code block代码块

​	这个我熟，最近用得比较多，用键盘左上角的

``

​	键入就完事儿了，特别注意这个符号不是冒号'





#### Math blocks数学代码块

​	这是本次学习的重点和难点，难在需要熟练才能快速操作，否则每次输入都需要查看大量资料。

$c=mc^2$

$$F=ma$$

$$ \mathbf{V}_1 \times \mathbf{V}_2 =  \begin{vmatrix} \mathbf{i} & \mathbf{j} & \mathbf{k} \\ \frac{\partial X}{\partial u} &  \frac{\partial Y}{\partial u} & 0 \\ \frac{\partial X}{\partial v} &  \frac{\partial Y}{\partial v} & 0 \\ \end{vmatrix} $$

​	使用两个美刀符号和四个美刀符号在Typora中是相同的，后续在Latex语法板块再着重介绍Latex





#### Tables表格

​	Typora提供两种创建表格的方法，一是graphical interface用户界面，二是writing the source code写源代码。

| Jordan | kobe |
|--|--|
|205|203|

​	只能说，source code形式的表格创建非常麻烦以及不规范，因此未来基本上只会使用graphical interface的形式。在Typora中有快捷键`ctrl + t`

|      |       |        |
| ---- | ----- | ------ |
|      | Joran | Bryent |
|      |       |        |
|      |       |        |



#### footnotes脚注

​	Markdown里边居然还有脚注[^fn1]？？

​	似乎用起来还挺方便的[^方便吗]。

​	但注意，区分footnote脚注和endnote尾注，尾注就是全部出现在结尾的注释，类似论文的参考文献。

​	最后，在Typora中使用脚注，可以直接在段落中输入脚注，随后点击该脚注，待注释的脚注就会在文章最后方出现，直接编辑即可。



#### Horizontal Rules平行分割线

​	最喜欢的排版工具，除了三根`-`可以画分割线之外，还可以三个`*`也可以。但前者不需要用到`shift`，更方便。



#### YAML Font Matter

1. YAML是什么？

​	编程免不了要写配置文件，怎么写配置也是一门学问。YAML 是专门用来写配置文件的语言，非常简洁和强大，远比 JSON[^1] 格式方便。	

​	YAML文件的后缀是`.yml`，作为许多工程文件的配置文件，比如这个文件名`_config.yml`就很熟悉，但由于自身写的比较少，在这里先不做过多的深究。

2. Font-Matter是什么

​	Front-matter是文件开头的 YAML 或 JSON 代码块，用于配置写作设置。 以 YAML 格式书写时，Front-matter 以三个破折号结束；以 JSON 格式书写时，Front-matter 以三个分号结束。

```yaml
---
title: Hello World
date: 2013/7/13 20:46:25
---
```

​	类似这样的代码，我在hexo博客制作时就用到了类似的代码。

3. 在Typora中写YAML font-matter有什么特别之处？

​	在文档最顶部输入`---`之后按下`enter`就会出现和其他地方使用`---`产生不一样的效果——会直接让用户编辑。





#### Table of contents内容表、目录

​	就是在文章中插入可跳转的目录，方法是在某个位置输入`[toc]`之后输入`enter`就会自动在该位置自动插入目录(table of contents)。所以一般在文章开端的部分插入就比较科学。

​	在文章开始就创建了toc之后，它会随着后续的编写中自动更新。

​	值得注意的是，该使用方法在其他Markdown编译器中不一定可行，比如在[Notion](https://www.notion.so/)中就无法使用。



#### Callout / Github Style Alert标注内容

​	之前在notion中使用了许多次Callout，但一直不知道它起到的作用是补充和提示，因此在Typora中设置了多种Callout的样式。

​	Callout在Typora中输入不算简单，因为在输入`>`之后就会自动变为[blockquotes格式](# blockquotes引用块)，但无关紧要，输入`>[!tip]`之后，Typora就会自动格式化为Callout了。

​	一下列举一下Typora中支持的Callout类型：

1. note
2. tip
3. important
4. warning
5. caution

> [!TIP]
>
> 1. Callout的使用可以让文章形式丰富。
> 2. 值得一提的是，callout在白色背景中更加好看。



> [!NOTE]
>
> 写callout别忘了中括号里的感叹号`！`





### 2.Span elements跳转元素

#### Links链接

> Markdown支持两种类型的链接：内联inline和引用reference

##### 内联链接

###### 内联网站

​	掏出我们的老测试网站， [百度网](http://baidu.com/ "Title") 。写法就是`[说明字](网站链接)`。这里还提到了带有标题和不带标题的区别，但测试下来似乎差别不大，因此先置之不理

###### 内联本文档

​	用于跳转到本文档内的某个位置，是一个比较常用的功能，就不需要干说：前文某某某地方提到过。

​	在[Callout/Github Style Alert](#Callout / Github Style Alert标注内容)部分其实已经用到了这个格式。和内联网站的差别在于，小括号里的不再是网址，而是`#标题名`充当href（Hypertext Reference）

##### 引用链接

This is [an example][id] reference-style link. Then, anywhere in the document, you define your link label on a line by itself like this: [id]: http://example.com/  "Optional Title Here"

说实话，这一个链接没怎么看懂，但似乎和html有着一部分联系，挖坑挖坑！



#### images图像

​	经常记不住图像和超链接的语法，因为他俩确实有点像...好吧，其实也挺好区分：images的格式会多一个感叹号`！`

​	但不得都不说，Markdown与word相比，很麻烦的点在于插入图片；word插入图片，实则是图片就包含了该word文件中，而markdown中插入图片只是插入了链接，需要很好的文件管理习惯，否则经常出现因为文件夹变动或拷贝给别人出现文档中图片无法显示的问题。

​	对于这一点，好处或许是能保持md文件本事的轻量级。（轻量级是这么用的吗？）

​	一个比较好的解决方式在于：将md文档放在一个文件夹中，该文件夹同时创建一个专门放图片的img文件夹，这样，md文档中的图片链接就会是相对路径，即使改变了该md文件夹的存放路径，也不影响图片的加载。

​	比如我插入我现在工作桌面的图片：

![工作桌面](.\img\img1.png)

 另外，还能使用HTML语法插入图片，示例如下：

<img src=".\img\img1.png" style="zoom:60%;" />



#### 强调语法

​	常用而适用的功能，也是几乎所有文档工具都包含的工具（txt就算了），但由于使用习惯了其他文档工具，大都数人可能都更适应其快捷键或界面工具。比如`ctrl +b`就能快速加粗(Bold)；`ctrl+i`就能快速倾斜(Italics)。

|        |                                                              |                             |
| ------ | ------------------------------------------------------------ | --------------------------- |
| 正常   | 正常                                                         | 正常                        |
| 斜体   | *斜体*                                                       | _斜体_                      |
| 粗体   | **粗体**                                                     | **粗体**                    |
| 删除线 | ~~删除~~                                                     |                             |
| 代码   | `code`                                                       | ```print('hello world!')``` |
| 高亮   | ==highlight==                                                |                             |
| 下标   | 下~标~                                                       |                             |
| 上标   | 上^标^                                                       |                             |
| 颜色   | <span style="color:brown">use HTML to make colored text</span> |                             |
| 下划线 | <u>use HTML to make Underline</u>                            |                             |

​	点击查看源码`ctrl+/`就可以查看具体使用什么符号了。

​	最后，使用这些格式还需要掌握**转义字符**，防止非意愿处理文本。比如我想写5乘以2乘以5，就可以写作：5\*2=2\*5，中间的`2=2`就不会变成斜体。



#### emoji表情包

​	这是一个我用的不多的功能，但还是觉得满炫酷的。让我看看有哪些emoji：

:happy: :haircut: :walking: :question: :wolf: :woman: :man: :basketball: :knife: :gun: :beer: :statue_of_liberty: :trumpet: :turtle: :bird: :helicopter: :video_game: :grin:

OKOK ，确实蛮丰富的，很多词语都有。







## 二、HTML语法

***

看似跑题，其实不然：Typora 中可以使用许多HTML语法来达到一般的md语言无法做到的效果。因此我打算系统地学习HTML语法之后，再来顺手处理掉这些个零碎的效果



### 标签

- HTML 文档由相互嵌套的 HTML 元素构成，HTML元素就是一个个HTML标签。

- HTML标签分为空内容标签和非空内容标签，比如`<p></p>`就是非空内容标签；`<br>`就是一个空内容标签。而空内容标签就不需要结束标签

#### 标签合集

| <h1>标题1</h1>        | <pre>预格式文本</pre> |      |
| --------------------- | --------------------- | ---- |
| <hr>                  | <q>引用语</q>         |      |
| <p>                   | <cite>引证</cite>     |      |
| <!-- -->              | <del>删除线</del>     |      |
| `<br/>`               | <small>小号字</small> |      |
| 加粗                  |                       |      |
| <code>print(1)</code> |                       |      |
| <b></b>               |                       |      |
| <i>斜体</i>           |                       |      |
| <kbd>Enter</kbd>      |                       |      |
| 下<sub>标注</sub>     |                       |      |
| 上<sup>标注</sup>     |                       |      |
| <var>varable</var>    |                       |      |







## 三、Latex语法













[^fn1]: 恭喜你解锁脚注功能！ 
[^方便吗]: 那肯定方便啊！
[^1]:JSON: **J**ava**S**cript **O**bject **N**otation(JavaScript 对象表示法)。JSON 是存储和交换文本信息的语法，类似 XML。

[id]: 
[Google]: 
