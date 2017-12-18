---
layout: post
title: R_for_data_science_ggplot2
date: 2017-12-18 21:30:00
categories: R
tag: [R, 笔记]
---


* content
{:toc}


前段时间感觉R忘的差不多了，想再温习下，尤其是一些目前流行的一些库，希望用到的时候能马上捡起来，我个人是一度很痴迷R这门很独特的语言的。感觉的确异常的强大。Garrett Grolemund 与 Hadley Wickham 出了一本开源书《R for data science》,看上去很不错，而且在线就可以免费去阅读，[地址](http://r4ds.had.co.nz/index.html)。虽然比较懒，但是未来还不算明朗，仅仅靠兴趣还是不足以提高技能，还是要整理学过的，读过的东西。也算督促自己去完成一些这样的事吧。作为一个事业，不能像读小说一样随性，还是要push下自己的。

这一章主要总结下R里面的ggplot2 绘图的要点。不会很详细的记录，因为很多在线的文档已经很好了，也很方便去作为参考。

ggplot2 来做图还是很方便，比如画一个散点图：

        ggplot(data = mpg) + geom_point(mapping = aes(x=displ, y=hwy))

比较简单的模板可以这样套用：

        ggplot(data = <DATA>) + <GEOM_FUNCTION>(mapping = aes(<MAPPINGS>))

Note: Each geom function in ggplot2 takes a mapping argument. This defines how variables in your dataset are mapped to visual properties. The mapping argument is always paired with aes(), and the x and y arguments of aes() specify which variables to map to the x and y axes. 也就是说，aes() 里面的变量控制了图的特征，比如x,y，color,shape, size 等等。

另外,不同类型的图使用了不同的*geom*, A geom is the geometrical object that a plot uses to represent data. People often describe plots by the type of geom that the plot uses. For example, bar charts use bar geoms, line charts use line geoms, boxplots use boxplot geoms, and so on. 

因此，不同的geom 具有不同的或者特有的aes() 变量，比如 *linetype* 可以在geom_smooth 里面使用，但是不可以在geom_point里使用。

另外，如果想在一个图里面使用多个geom叠加的效果，可以简洁的写成：

```
    ggplot(data = mpg, mapping = aes(x = displ, y = hwy)) + 
    geom_point() + 
    geom_smooth()

```

ggplot2的坐标系统(Coordinate systems)里面可能常用的有 *coord_flip()* ,用来翻转x,y轴。 而*coord_fixed()* 用来固定x,y的坐标对应关系，这样图片的放大也不会改变图中x,y的长宽比例。

综合下来，在ggplot2里面，可以对图施加影响的主要就是这几个，另外，还有 *theme*, *label*这些不是核心的组件。一般的模板就可以套用如下：

```

    ggplot(data = <DATA>) + 
      <GEOM_FUNCTION>(
        mapping = aes(<MAPPINGS>),
        stat = <STAT>, 
        position = <POSITION>
      ) +
    <COORDINATE_FUNCTION> +
    <FACET_FUNCTION>

```

其中，stat 可以改变做图是数值转换的计算方法，比如stat_count等，position(已经忘了做什么的了。。。), facet就是切面图，可以分成很多小图来展示，一般也不会用到。


最后，ggplot2 需要多查看文档，记忆我是肯定记不住的，知道去那里找到答案也挺好。以下是一些文档等的链接：

[本书的该节 Data visualisation](http://r4ds.had.co.nz/data-visualisation.html), 篇幅不大，建议用到就粗略看一边。

[Data Visualization with ggplot2 : : CHEAT SHEET](https://github.com/rstudio/cheatsheets/raw/master/data-visualization-2.1.pdf), rstudio 上面总结的表格，简直不能更赞，非常方便去快速查看用法。

[ggplot2 documention](http://ggplot2.tidyverse.org/reference/), ggplot2 官方文档，应该是最可信的文档之一。

[ggplot2 extensions](http://www.ggplot2-exts.org/gallery/), 里面相当于ggplot2的各种神奇的插件，可以完成很多匪夷所思的画图，各路大神的作品，极大的丰富了ggplot2的灵活性。

[R Graphics Cookbook](http://www.cookbook-r.com/Graphs/), 这是该书的开源在线版(感谢开源！)，作者Winston Chang, 据说评价也不错，可以作为补充的文档。

估计这些对于初学者应该够了，常用常查常新吧！
