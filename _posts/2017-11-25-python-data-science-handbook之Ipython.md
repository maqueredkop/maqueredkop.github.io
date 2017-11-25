---
layout: post
title: 《Python-Data-Science-Handbook》之Ipython
date: 2017-11-25 16:00:00
categories: python
tag: [python, 笔记]
---


* content
{:toc}


最近python 用的不多，而且总感觉python 没什么长进，对数据分析常用的包也不怎么熟悉，所以打算学学并且做做笔记，主要是一些需要注意的地方。也算是督促自己吧。
这本书是《Python-Data-Science-Handbook》，而且是开源免费的，项目主页在[github](https://github.com/jakevdp/PythonDataScienceHandbook), 格式是ipynb，但是直接打开比较慢，甚至很难打开，发现了一个在线工具[nbviewer](http://nbviewer.jupyter.org/), 把github项目地址复制一下就可以很方便的打开ipynb文件了，所以我现在主要在[links](http://nbviewer.jupyter.org/github/jakevdp/PythonDataScienceHandbook/blob/master/notebooks/Index.ipynb)这个地址学习。

这一章主要是关于Ipython, 很强大的交互式python, 比自带的python 解释器要强大的多，但是我个人的体会是，它的局限性也不小，比较适合交互，尝试一些demo, 查看一下帮助文档，还是很好的。但是真正的项目的话，IDE肯定更好，比如pycharm, spyder 等等。另外，jupyter notebook 很强大，比较适合写tutorial , blog 等等。

* 开启jupyter notebook

    jupyter notebook

* save the code with %%file

    %%file test.py # 下一行的代码就会overwriting 到test.py(if exists)
    %%file -a test.py # means append, 会附加到已存在的 test.py上。

* Accessing Documentation with ?

    len?
    L = [1,2,3]
    L.insert?

* Accessing Source Code with ??

    len??

但是python 里面C写的源码是看不到的，而python 写的动辄上千行，所以这个功能不是很常用。

* Exploring Modules with Tab-Completion

    L.<TAB>
    L.co<TAB>
    from itertools import co<TAB>

这个功能我觉得还是很好用的。
   
* wildcard matching

    str.*find*?

* Miscellaneous Shortcuts

1. ctrl-l  clear terminal screen
2. ctrl-c interrupt python command
3. ctrl-d exit ipython session

* Pasting Code Blocks: %paste and %cpaste

使用时先复制好代码，带>>> 也没关系， 然后第一行为%paste，Enter 后就自动粘帖好代码了。
%cpaste 支持多次复制，适合长的代码。

* Running External Code: %run

    python test.py # 在ipython 中会报错
    %run test.py  # 正确执行

这一功能也是很有帮助的。

* Timing Code Execution: %timeit
%timeit 可以给出单行代码的运行时间，%%timeit 支持多行代码

    %timeit L = [n ** 2 for n in range(1000)]

* Help on Magic Functions: ?, %magic, and %lsmagic
在ipython 中，带有%的是一些magic function,对于这些函数的帮助文档，可以使用？查看：

    %timeit?
    %magic # access a general description of available magic functions, including some examples
    %lsmagic # For a quick and simple list of all available magic functions

% magic 的用法是ipython的一大特色，很有创意的想法。大大扩展了它的灵活性。

* Suppressing Output

    sum([1,2]); # 加上分号，不会显示结果

* Profiling Full Scripts: %prun

    %prun sum_of_lists(1000000) # 整个函数的性能分析

* Line-By-Line Profiling with %lprun
    
    # 逐行的性能分析
    $ pip install line_profiler
    %load_ext line_profiler
    %lprun -f sum_of_lists sum_of_lists(5000)

* Profiling Memory Use: %memit and %mprun
    
    # 代码内存分析
    $ pip install memory_profiler
    %load_ext memory_profiler
    %memit sum_of_lists(1000000)

以上这几个功能很强大，但是一般可能也不会用到。

最后，可以参考Ipython 的网站[Ipython](http://ipython.org/)。



