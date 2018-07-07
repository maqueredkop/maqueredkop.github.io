
---
layout: post
:title: RNA-Seq QC note
date: 2018-07-07 14:36
categories: RNA-Seq
tag: [RNA-Seq 笔记]
---


* content
{:toc}



> 有一会子没有写博客了，一方面是自己懒，还有就是事情也比较多，好在暂时这几天有点时间，自己也放松下来想总结总结，学点新东西吧。而且最近感觉其他各行各业都有转行到生信的趋势。。。 看来我们饭碗不保了。。。 而且行业变化也比较快，新技术也比较多，不主动学习的话还是不行。尤其是在职场上面，硬实力是对技术人员最有效的加成。闲话少说，这个RNA-Seq 分析系列的笔记算是自己的一些心得，总结，包括书中，文章中学到的知识点吧。主要是一方面记录自己到底是不是真的理解了，学到了什么;另一方面也是记下来后面可以看看，免得过几天就忘了。尤其是我发现这两年记忆力真的是不行了。

---

> RNA-Seq 分析的话，一般就是从下机数据开始分析，做一下质量控制，去接头序列，去低质量值，还要一些比如重复序列，low-complexed 等等。本文主要跟QC 有关。

### 软件选择

QC 的话，[fastqc](https://www.bioinformatics.babraham.ac.uk/projects/fastqc/) 是非常流行好用的软件，速度也挺快，对于快速的了解原始数据是非常有帮助的。虽然用法简单，但真的很强大，各种QC图一目了然。

其次就是去adapter序列，经验发现[cutadapt](https://github.com/marcelm/cutadapt) 确实是比较好用的，去的也比较干净。一般如果是illumina 通用接头的话,只输入前13bp 即可，如AGATCGGAAGAGC, 当然最好能确定是什么接头，虽然有软件可以自动识别，但是最好还是明确什么接头序列。 cutadapt 的问题主要是python写的，如果样本多，数据量大，耗时太惊人。 尤其是python2 下还不能多线程运行。

去完接头序列之后一般就是从序列两端开始去低质量值的碱基。这方面[trimmomatic](https://github.com/timflutre/trimmomatic)表现相当不错，速度快，属于多面手。虽然也可以去adapter,但是有的时候会去不干净。

一种策略就是 'cutadapt + trimmomatic' , 还有一种就是最近测试感觉还不错的 [fastp](https://github.com/OpenGene/fastp),不到一年，目前github上面的star已经有250了，可见虽然这些工作已经非常成熟了，软件几十个肯定有了，但是如果有更好的工具，大家还是会欢迎的。更重要的是，还是国产软件，OpenGene 出品。试了一下，好不错，c++ 写的，速度很快。可以兼顾去adapter 和 trimm base ，而且还有其他功能，下文会提到。

### 存在的问题

有一个问题我觉得可以去思考，就是去adapter 或者低质量值的时候，或者设定最低保留长度，如果read1被过滤到，那么对应的read2一般也会删除，不管read2质量如何，那么这种情况是不是会损失很多有意义的reads? 如何处理？

还有就是fastqc报告里面，'Per base sequence content',如果是随机引物建库的话，可能会出现前面几个碱基的 sequence-specific bias. 这种偏好性肯定会影响对于基因表达的定量，因为这样一来转录本之间就不是uniform coverage了。这种是不能通过去adapter等来弥补的。

还有就是，随机引物会造成测序开始时的错配，最多会影响到前7个碱基。即使是这些碱基的base quality 也很高。所以最好还是去掉的好。这个虽然有[文章](https://www.ncbi.nlm.nih.gov/pubmed/24386481)报道，但是还需要再验证下。而且这也只适用于RNA-Seq.

另外，有的时候原始数据会出现low-complexity sequences或者ployA/G/N tails ，前者可能全为'AAAAAAAAAAAAAAAAAAAA'或者'TAGCTAAAAAAAAAAAAAAAAAAAAAA'，这种序列应该提前过滤掉，可以使用前面提到的fastp 去处理，该软件也可以处理各种polyN/A 等的情况。

> 总之好的输入数据才能生成好的分析结果，所以QC还是很重要的，如果出现了异常，一般fastqc的结果报告里会体现出来，建议多了解一下。


