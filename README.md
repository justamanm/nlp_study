## nlp从0到1

学习过程的记录

---



### week1(7.29)

| day                                      | content                                                      |                                                              |
| ---------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| es环境搭建                               |                                                              | 见ElasticSearch.md                                           |
| es搜索                                   |                                                              |                                                              |
| word2vec了解<br>gensim实现word2vec词向量 | jieba分词<br>根据数据生成词向量模型<br> 加载模型获取相似词<br> 句子相似度比较（词向量直接相加后求cosine），效果很差 | 词向量.md<br>[[NLP] 秒懂词向量Word2vec的本质 - 知乎 ](https://zhuanlan.zhihu.com/p/26306795) <br>  [word2vec是如何得到词向量的？ - crystalajj的回答 - 知乎](https://www.zhihu.com/question/44832436/answer/266068967)<br>[word2vec 中的数学原理详解](https://www.cnblogs.com/peghoty/p/3857839.html)<br> [Python gensim库word2vec 基本用法](https://www.cnblogs.com/Allen-rg/p/10589035.html)<br> [skip-gram结构图问题](https://zhuanlan.zhihu.com/p/65633189) |

### week2(8.03)

| day                                                          | content                                                      |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| 了解hanlp                                                    | 相关书籍：《自然语言处理入门》，hanlp作者写的<br> 讲了nlp相关的各个任务，但好像深度学习的东西不多，所以还没看 |
| [bert-as-service](https://github.com/hanxiao/bert-as-service) 开源库使用 | bert模型的实现<br> 可以获取句向量，然后求余弦比较相似度<br> (属于表示型，但bert是可以直接输入两个句子比较相似度的） |
| 了解cnn                                                      | 李宏毅机器学习课程<br> 书：python深度学习<br> cnn之前了解过，也是深度学习入门就会学的，从图像任务理解比较直观 |
| 了解lstm                                                     | 李宏毅机器学习课程<br> [人人都能看懂的LSTM介绍及反向传播算法推导（非常详细） - 陈楠的文章 - 知乎 ](https://zhuanlan.zhihu.com/p/83496936) <br> [LSTM神经网络输入输出究竟是怎样的？ - lonlon ago的回答 - 知乎](https://www.zhihu.com/question/41949741/answer/309529532)<br> [RNN的梯度消失指的是权重停止更新吗？ - 耶律齐的回答 - 知乎](https://www.zhihu.com/question/356489098/answer/900999182)<br> [LSTM如何来避免梯度弥散和梯度爆炸？ - Towser的回答 - 知乎](https://www.zhihu.com/question/34878706/answer/665429718) |
| 了解attention/transformer                                    | 李宏毅机器学习课程<br> attention出现的背景 & encoder-decoder：[【经典精读】Transformer模型深度解读 - 潘小小的文章 - 知乎](https://zhuanlan.zhihu.com/p/104393915)<br> [详解Transformer （Attention Is All You Need） - 大师兄的文章 - 知乎 ](https://zhuanlan.zhihu.com/p/48508221) <br> [Attention机制详解（二）——Self-Attention与Transformer - 川陀学者的文章 - 知乎](https://zhuanlan.zhihu.com/p/47282410)<br> |
| note                                                         | 模型总结：模型综述.md                                        |

### week3(8.10)

| day                                                          | content                                                      |                                                              |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 了解bert                                                     | 就是transformer的encoder的叠加                               | [github-bert](https://github.com/google-research/bert)<br> [图示详解BERT模型的输入与输出](https://www.cnblogs.com/gczr/p/11785930.html)<br>  [【NLP】Google BERT详解 - 李如的文章 - 知乎](https://zhuanlan.zhihu.com/p/46652512) |
| [github-bert-utils](https://github.com/terrifyzhao/bert-utils)开源库 | 获取句向量                                                   |                                                              |
| bert预处理-fine-tuning                                       |                                                              | [b站-2019 NLP(自然语言处理)之Bert课程]( <https://www.bilibili.com/video/BV1NJ411o7u3 ) |
| bert预训练开源库：                                           | 中文句子相似度比较                                           | [github-chinese-bert-similarity](https://github.com/policeme/chinese-bert-similarity) |
| 了解文本分类模型：TextCNN/fastText                           | 没有非监督的方法，即需要有标签的数据<br>这样就转换为了文本分类问题 |                                                              |

### week4(8.17)

| day                                                          | content                                                      |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| 1.bert输入理解：单个句子/两个句子<br> 2.思考：两种方式比较句子相似度<br> 3.了解到有albert：精简版的bert<br> 4.思考:不相关问题接一层意图识别（两种：专业问答、闲聊） | 问答模型选择时的输入问题，即要找一个input为两个句子的模型<br>bert既可以输入单个句子做分类，也可以输入两个句子做相似度比较，而最后都是用cls来做输出的，为什么可以做到？<br> 其实是想从bert模型中找到获取句子相似度的思路；<br> BERT有两个预训练的任务：MLM和NSP；即单个句子是根据语言模型训练，两个句子的训练其实是next sentence的训练，而不是相似度的训练，使用sep，对句子concat后加入句子位置信息，模型会学到sep |
| 1.文本匹配模型分两种：基于表示和基于交互<br>2.可以参考大厂的实现方式 |                                                              |
|                                                              |                                                              |
|                                                              |                                                              |
|                                                              |                                                              |



阶段

- 深度学习基础和主要模型
  - [李宏毅2020机器学习深度学习(完整版)国语](https://www.bilibili.com/video/BV1JE411g7XF )
- nlp相关内容
  - 零散的搜索，主要是知乎和博客上的文章，github上的代码
  - [CS224n 斯坦福深度自然语言处理课](https://www.bilibili.com/video/BV1pt411h7aT)
  - [李宏毅老师2020新课深度学习与人类语言处理](https://www.bilibili.com/video/BV1RE411g7rQ)
  - 还没怎么看
- 落地案例了解，实战



notes

- ElasticSearch.md
- 词向量.md
- 模型综述.md
- 



points

- 句子的语义相似度问题
- 相似度问题本质是分类问题（即要有带标签的数据 8.14）
- 两种方式，一种是产生句向量求距离，另一种是直接输入两个句子输出相似度（8.17）
  - 实际验证了这一点：文本匹配模型分两种，基于表示和基于交互（8.18）

















