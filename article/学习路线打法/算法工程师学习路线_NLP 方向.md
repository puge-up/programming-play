- [一、传统 NLP](#一传统-nlp)
  - [1、文本相似度算法](#1文本相似度算法)
  - [2、text similarity](#2text-similarity)
- [二、深度学习 NLP](#二深度学习-nlp)
  - [1、词向量发展过程，及相应 papers](#1词向量发展过程及相应-papers)
  - [2、词向量讲解的相关文章 + 博客](#2词向量讲解的相关文章--博客)
- [三、视频 + 库 + 书籍](#三视频--库--书籍)
- [四、说明](#四说明)

对于算法工程师，常见方向有：NLP、搜索推荐、知识图谱、CV、机器学习算法工程师等等，不同领域在求职时岗位是会细化的。

NLP 技术主要是和数据打交道，通过 SQL + Python 写脚本处理简单文本内容，复杂问题需要跑模型进行处理，常用在搜索召回链路、用户语义识别等场景。

我个人比较熟悉 NLP + 推荐相关技术，本文只谈 NLP 相关技术栈，会推荐相关学习资料。

## 一、传统 NLP

- 中文分词技术
- 词性标注
- 命名实体识别
- 词汇权重计算技术：TFIDF、SIF等
- 搜索相关，索引方法：倒排索引，query 与文档相似度计算方法：BM25，文档排序方法：PageRank
- 文本相似度衡量方法：LCS、Levenshtein 距离、杰卡德指数、w2v、wmd 等

### 1、文本相似度算法

**最长公共子序列**（LCS：动态规划思想，与最长公共子串有些不一样）

- http://www.kancloud.cn:8080/digest/pieces-algorithm/163624
- 得到公共子序列长度后，相似度 = 公共子序列length/min(length(x), length(y))，之所以要除以两个串中短串的长度，是因为需要将相似度进行 normalize，而且当串 y 完全包含 x 时，相似度为 1，所以要除以短串的长度。
- 适用于计算简称和全称之间的相似度。

**最小编辑距离**（Levenshtein距离，动态规划思想）

- https://www.dreamxu.com/books/dsa/dp/edit-distance.html
- 可以使用 python Levenshtein 包的 Levenshtein.ratio()

**jaccard index**（杰卡德指数）

- 度量两个集合之间的相似性，它被定义为两个集合交集的元素个数除以并集的元素个数。
- 若 A、B 两个集合都为空，则指数为 1。
- 将两个文本进行分词，分词后的集合，计算 jaccard index

**bm25**

- https://www.jianshu.com/p/1e498888f505

**w2v**

- 对文本进行分词，分词后的每个词，查询词向量表得到词向量，文本词向量为单词词向量的平均。可利用 TFIDF 或者 SIF 等方法对单词进行加权，得单词词向量的加权平均，最后计算两个文本词向量的相似度，可以用 cosine similarity 等方法。

### 2、text similarity

**Jaccard Similarity**

做法
- size of intersection divided by size of union of two sets

具体做法

- lemmatization：单词变成 root 形式，譬如has，have，had均变成have形式；
- 计算两个 text 中，交集的单词量/并集的单词量。

例子

- Sentence 1: AI is our friend and it has been friendly
- Sentence 2: AI and humans have always been friendly
- after lemmatization, Jaccard Similarity = 5/(5+3+2)

**bag of words**

做法
- 将所有 texts 所出现的词汇整理成词汇表，利用词汇表表达 text，text 出现过某个词，特征对应维度为 1（出现多次可为 n，为 n 的方式叫做 bag of words + tf ，也叫 Count Vectorizer 方法）

具体做法

- text preprocessing：去除特殊字符，空格等，然后进行word的tokenize；
- preprocessing后的 words，整理成词汇表；
- 利用词汇表，每个 text 表达为 len(词汇表)长度的向量，出现word 的坐标为 1（多次为n）。
- 计算相似性：利用 bag of words + cosine similarity，计算相似性即可。

**bag of ngram**

做法
- 将连续 n 个 words 作为一个 word，然后做 bag of words。

具体做法

- text preprocessing：去除特殊字符，空格等，然后进行 word 的 tokenize；
- 对每个处理后的 text，连续 n 个 words 看做一个 word，加入词汇表；
- 利用词汇表，每个 text 表达为 len(词汇表)长度的向量，出现 word 的坐标为 1（多次为n）。
- 计算相似性：利用 bag of words + cosine similarity，计算相似性即可。

**TF-IDF**

做法

- 将所有 texts 中所出现的词汇整理成词汇表，利用词汇表表达 text，其中 text 出现过某个词，则计算该词的 tf-idf 作为特征值。

具体做法

- text preprocessing：去除特殊字符，空格等，然后进行 word的 tokenize；
- preprocessing 后的 words，整理成词汇表；
- 针对text中每个出现在词汇表中的词，计算该词的 tf-idf；
- tf：词频（term frequency，tf）指的是某一个给定的词语在该 text 中出现的频率。这个数字是对词数（term count）的归一化，以防止它偏向长的 text

<div align=center><img src='https://mmbiz.qpic.cn/mmbiz_png/iaumSdLKJXtQo9dczlcjwafo3NtxmC8tw2ichULia8ldpWrYIKa5Lv2ryqy9AlISSTQsg38OicLbMMYxTEWQTmd2UA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1' width="50%" height="50%"></div>

- 其中分子 nij 表示词 ti 在 textj 中出现的次数，分母表示 textj 所有词出现的次数之和。
- idf：逆向文件频率（inverse document frequency，idf）是一个词语普遍重要性的度量。某一特定词语的 idf，可以由总文件数目除以包含该词语之文件的数目，再将得到的商取以 10 为底的对数得到
<div align=center><img src='https://mmbiz.qpic.cn/mmbiz_png/iaumSdLKJXtQo9dczlcjwafo3NtxmC8tw0C58GiaKiafs8EGK03xmMPvSGKkKpdXTwQyYEUs5tQIb95KXnJSiatZhw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1' width="50%" height="50%"></div>

- 其中分子表示语料库中的 texts 的总数，分母表示出现过词汇 ti 的 texts 的数量。
- tf-idf：tf * idf，tf-idf 倾向于过滤掉常见的词语，保留重要的词语。
- 计算相似性：利用 bag of words + cosine similarity，计算相似性即可。

**SIF(Smooth Inverse Frequency)**

做法

- 利用预测的词频，计算每个 word 的权重，根据词的权重，加权求得 text 的 embedding，针对多个 texts 组成的矩阵，计算第一个主成分向量，计算每个 text embedding 在该主成分向量上的投影，并减去投影的值，得到最终的 embedding。

具体做法

- 既可以用从海量文本中统计的词频，也可以使用自身应用的 texts，统计每个词的词频。词频是词的出现次数除以所有词出现的总次数。
- 算出 text 的 embedding 之后，针对多个 texts，计算一个主成分向量，然后计算每个 text embedding 在这个主成分的投影，减去投影值，得到最终每个 text 的 embedding。
- https://github.com/PrincetonML/SIF
- 计算相似性：利用 bag of words + cosine similarity，计算相似性即可。

**WMD(word mover distance)**

- 直接计算texts之间的similarity，需要利用word embedding。
- 做法：找出 textA 向 textB 迁移的最小花费。

具体做法

- textA和textB表示成 normalized bag of words（nBow），分别为dA,dB，其中

<div align=center><img src='https://mmbiz.qpic.cn/mmbiz_png/iaumSdLKJXtQo9dczlcjwafo3NtxmC8tw5K4kziaChQTnziaoXl4VE5VIJ6UPBtric77lv8BGYSLIGHGXF1rX1sG3w/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1' width="50%" height="50%"></div>

- 计算 textA 和 textB 中每个单词 xi 与 xj 之间的距离 cij

<div align=center><img src='https://mmbiz.qpic.cn/mmbiz_png/iaumSdLKJXtQo9dczlcjwafo3NtxmC8twDrJ8JpzMOibyG6GibZkl7Fe2HcpqnRYn7OwABB9aNDXLAdicfKQ06ePMw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1' width="50%" height="50%"></div>

- 其中单词之间的距离是利用 word embedding 的欧氏距离衡量的。

- WMD 的目标是从 dA 迁移到 dB，其中花费最小，其中 Tij 表示从 dA 中的 wordi 迁移到 dB 中的 wordj 的量，因此问题的数学形式为

<div align=center><img src='https://mmbiz.qpic.cn/mmbiz_png/iaumSdLKJXtQo9dczlcjwafo3NtxmC8twtw2dK7a8je9tzonmia7LPlvt7Nyhxbw8ic7SjbkFZkCdH03RnLoJLymA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1' width="50%" height="50%"></div>

- WMD 算法是 earth mover distance 的一个特例，缺点是解法的时间复杂度高。但是可以通过减少一定的下界近似和剪枝的方式加快求解。

## 二、深度学习 NLP

### 1、词向量发展过程，及相应 papers

- NNLM：📎2003-NNLM.pdf
- CBOW、Skip-gram：📎skipgram.pdf
- Glove:📎glove.pdf
- ELMO：📎ELMO.pdf
- GPT：📎GPT.pdf
- Bert: 📎BERT Pre-training of Deep Bidirectional Transformers for Language Understanding.pdf

### 2、词向量讲解的相关文章 + 博客

- 从 Word Embedding 到 Bert 模型—自然语言处理中的预训练技术发展史：https://zhuanlan.zhihu.com/p/49271699

- 语言模型演化历史：从 N-gram 到 BERT。

- Transformer 图解：http://fancyerii.github.io/2019/03/09/transformer-illustrated/#layernorm

- Transformer 代码阅读：http://fancyerii.github.io/2019/03/09/transformer-codes/

## 三、视频 + 库 + 书籍

- stanford cs224n：https://web.stanford.edu/class/cs224n/
- Allennlp open library：https://allennlp.org/
- 李宏毅的机器学习中文课程：https://www.youtube.com/channel/UC2ggjtuuWvxrHHHiaDH1dlQ/videos
- NLP town：https://github.com/nlptown/nlp-notebooks
- Snorkel：帮助做弱监督的库
- 传统NLP：统计自然语言处理基础
- NLP实战：Python自然语言处理实战核心技术与算法

文中给出了很多链接以及视频资料，**有些是需要 google 才能访问**，对于这部分内容需要认真去看、去消化下。

## 四、说明

原创文章链接：[算法工程师学习路线（NLP 方向）](https://mp.weixin.qq.com/s?__biz=MzU4MjQ3NzEyNA==&mid=2247484978&idx=1&sn=4ad2361454fd613f125a8e77e233c5ea&chksm=fdb6f219cac17b0fd713e1bb9231a6ed569ce3620cc56138e7abada2996f78952addcc54eac6&token=1698861862&lang=zh_CN#rd)
