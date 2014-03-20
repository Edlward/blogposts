title: 中文分词（一）
date: 2013-12-25 20:49:20
categories: 机器学习
tags:
---
* [《中文分词（一）》](http://zipperary.com/2013/12/25/chinese-segmentation/)
* [《中文分词（二）》](http://zipperary.com/2013/12/27/chinese-segmentation-2/)
* [《中文分词（三）》](http://zipperary.com/2013/12/27/chinese-segmentation-3/)



这两天忙 NLP 课程的大作业，我们组的题目是「中文分词」，要求是可以使用任何现有的资料，我们采用的是@TeapDB 的**结巴分词**，项目主页是：<https://github.com/fxsjy/jieba> 。

今晚刚刚做完 presentation，不知不觉在台上扯了四十分钟，在空调吹暖气烤的屋里出了一身的汗。汗还没干，把内容整理一下：

###为什么要进行中文分词？

* 词是最小的能够独立活动的有意义的语言成分。

* 汉语是以字为基本的书写单位，词语之间没有明显的区分标记。

* 正确分词是中文信息处理的基础与关键。

###中文分词的难点

1. 交集型歧义：    
 结婚的和尚未结婚的   =>   
 结婚／的／和／尚未／结婚／的    
 结婚／的／和尚／未／结婚／的  
 
2. OOV(Out of Vocabulary)识别：  
 云计算、创新办、好用
 
<!--more-->
 
###基于规则的分词：最大匹配

e.g. "南京市长江大桥"

词典的最大词长是5

**正向最大匹配：**从左向右，依次扫描。比如"南"，扫描前5个，"南京市长江"，词典中并没有这个词；扫描前4个，"南京市长"，词典中有这个词，Okay。然后从"江"开始，后面一共就剩3个了，但词典中木有，那么缩短，"江大"，也木有，只能是"江"了。依次继续，可以得到"大桥"。最后我们就得到了按照正向最大匹配得到的词序：

南京市长/江/大桥


**逆向最大匹配：**我们都知道，中文的重心一般在后面，所以按照从右向左的扫描方式，取得的效果会更好一些。分词的方式跟上面是一样的，除了扫描顺序。最后得到的词序是：

南京市/长江大桥

###基于统计的分词

1. 基于 DAG(有向无环图)和 Dict(词典)的中文分词。
2. 基于HMM的 Viterbi 算法

结巴分词正是使用这种思想。该分词程序的**主要功能**有：

* **分词**
* 关键词提取：TF/IDF
* 词性标注（pos）
* Tokenize：返回词语在原文的起始位置


**代码**有：

* Python 版，作者所写
* C++
* Java

后两种为其他人做的 commit。


程序的**性能**：

* 1.5 MB / Second in Full Mode
* 400 KB / Second in Default Mode
* Test Env: Intel(R) Core(TM) i7-2600 CPU @ 3.4GHz；《围城》.txt

###演示


输入文本： “这是一个伸手不见五指的黑夜。我叫孙悟空，我爱北京，我爱Python和C++。”

程序执行结果：

![](http://ww4.sinaimg.cn/large/5e8cb366jw1ebw9jdi6mjj20k00egwg1.jpg)

###基于 DAG 和 Dict 的中文分词

分词步骤：

1. 根据 dict 生成 trie，提高词典查询速度
2. 文本预处理，生成中文短语
3. 生成词图（DAG），并求最大概率路径

咦，文章不短了，马上下课，今天先到这儿，明天继续！

*附我 Presentation 的 ppt： [点我下载](http://pan.baidu.com/s/1jG1DcFk)*

Merry Christmas!







