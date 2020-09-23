## nlp从0到1

学习过程的记录

---



### week1(7.29)

| day                                      | content                                                      |                                                              |
| ---------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| es环境搭建                               |                                                              | 见ElasticSearch.md                                           |
| es搜索                                   |                                                              |                                                              |
| word2vec了解<br>gensim实现word2vec词向量 | jieba分词<br>根据数据生成词向量模型<br> 加载模型获取相似词<br> 句子相似度比较（词向量直接相加后求cosine），效果很差 | 词向量.md<br>[[NLP] 秒懂词向量Word2vec的本质 - 知乎 ](https://zhuanlan.zhihu.com/p/26306795) <br>  [word2vec是如何得到词向量的？ - crystalajj的回答 - 知乎](https://www.zhihu.com/question/44832436/answer/266068967)<br>[word2vec 中的数学原理详解](https://www.cnblogs.com/peghoty/p/3857839.html)<br> [Python gensim库word2vec 基本用法](https://www.cnblogs.com/Allen-rg/p/10589035.html)<br> [skip-gram结构图问题](https://zhuanlan.zhihu.com/p/65633189) |
| 总结                                     | es、词向量word2vec                                           |                                                              |

### week2(8.03)

| day                                                          | content                                                      |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| 了解hanlp                                                    | 相关书籍：《自然语言处理入门》，hanlp作者写的<br> 讲了nlp相关的各个任务，但好像深度学习的东西不多，所以还没看 |
| [bert-as-service](https://github.com/hanxiao/bert-as-service) 开源库使用 | bert模型的实现<br> 可以获取句向量，然后求余弦比较相似度<br> (属于表示型，但bert是可以直接输入两个句子比较相似度的） |
| 了解cnn                                                      | 李宏毅机器学习课程<br> 书：python深度学习<br> cnn之前了解过，也是深度学习入门就会学的，从图像任务理解比较直观 |
| 了解lstm                                                     | 李宏毅机器学习课程<br> [人人都能看懂的LSTM介绍及反向传播算法推导（非常详细） - 陈楠的文章 - 知乎 ](https://zhuanlan.zhihu.com/p/83496936) <br> [LSTM神经网络输入输出究竟是怎样的？ - lonlon ago的回答 - 知乎](https://www.zhihu.com/question/41949741/answer/309529532)<br> [RNN的梯度消失指的是权重停止更新吗？ - 耶律齐的回答 - 知乎](https://www.zhihu.com/question/356489098/answer/900999182)<br> [LSTM如何来避免梯度弥散和梯度爆炸？ - Towser的回答 - 知乎](https://www.zhihu.com/question/34878706/answer/665429718) |
| 了解attention/transformer                                    | 李宏毅机器学习课程<br> attention出现的背景 & encoder-decoder：[【经典精读】Transformer模型深度解读 - 潘小小的文章 - 知乎](https://zhuanlan.zhihu.com/p/104393915)<br> [详解Transformer （Attention Is All You Need） - 大师兄的文章 - 知乎 ](https://zhuanlan.zhihu.com/p/48508221) <br> [Attention机制详解（二）——Self-Attention与Transformer - 川陀学者的文章 - 知乎](https://zhuanlan.zhihu.com/p/47282410)<br> |
| 总结                                                         | 各模型寮角                                                   |
| note                                                         | 模型总结：模型综述.md                                        |

### week3(8.10)

| day                                                          | content                                                      |                                                              |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 了解bert                                                     | 就是transformer的encoder的叠加                               | [github-bert](https://github.com/google-research/bert)<br> [图示详解BERT模型的输入与输出](https://www.cnblogs.com/gczr/p/11785930.html)<br>  [【NLP】Google BERT详解 - 李如的文章 - 知乎](https://zhuanlan.zhihu.com/p/46652512) |
| [github-bert-utils](https://github.com/terrifyzhao/bert-utils)开源库 | 获取句向量，获取的是倒数第二层向量<br>参看：原文档或[使用BERT生成句向量](https://blog.csdn.net/u012526436/article/details/87697242) |                                                              |
| bert预处理-fine-tuning                                       |                                                              | [b站-2019 NLP(自然语言处理)之Bert课程]( <https://www.bilibili.com/video/BV1NJ411o7u3 ) |
| bert预训练开源库：                                           | 中文句子相似度比较                                           | [github-chinese-bert-similarity](https://github.com/policeme/chinese-bert-similarity) |
| 了解文本分类模型：TextCNN/fastText                           | 没有非监督的方法，即需要有标签的数据<br>这样就转换为了文本分类问题 |                                                              |
| 总结                                                         | bert及其开源库了解使用，文本分类模型                         |                                                              |

### week4(8.17)

| day                                                          | content                                                      |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| 1.bert输入理解：单个句子/两个句子<br> 2.思考：两种方式比较句子相似度<br> 3.了解到有albert：精简版的bert<br> 4.思考:不相关问题接一层意图识别（两种：专业问答、闲聊） | 问答模型选择时的输入问题，即要找一个input为两个句子的模型<br>bert既可以输入单个句子做分类，也可以输入两个句子做相似度比较，而最后都是用cls来做输出的，为什么可以做到？<br> 其实是想从bert模型中找到获取句子相似度的思路；<br> BERT有两个预训练的任务：MLM和NSP；即单个句子是根据语言模型训练，两个句子的训练其实是next sentence的训练，而不是相似度的训练，使用sep，对句子concat后加入句子位置信息，模型会学到sep |
| 1.文本匹配模型分两种：基于表示和基于交互<br>2.可以参考大厂的实现方式 |                                                              |
| 了解交互类模型：dssm/siamese                                 | 可用于生成问答库中的问题的离线向量，用户输入做实时向量生成，做召回<br> 案例：[苏宁](https://ai.51cto.com/art/201909/603290.htm)<br> 了解到有[聊天模板](https://blog.csdn.net/malefactor/article/details/52166235)：一般有趣的回答都是模板匹配的 |
| 1.继续了解表示型/交互模型<br> 2.了解[SiameseSentenceSimilarity开源库](https://github.com/liuhuanyong/SiameseSentenceSimilarity)<br> 3.了解到有多轮对话这个问题方向 | 1.表示型：Siamese dssm  / siamese lstm，都是把Siamese作为baseline的<br>交互型：esim，attention之前的论文都是以esim作为比较对象的，esim在2017/2018比赛中获得比较好的效果<br> 2.基于dssm模型，具体：两层双向的lstm<br> 确定下一步要做的：从基于交互的匹配模型中选出合适的使用 |
| 1.SiameseSentenceSimilarity库的使用<br>2.测试embedding维度对表现影响 | 1.测试表现，调节超参<br>2.embedding的影响没有想象中的那么大，50-100-200-300，按照需求选即可<br> 参看：[embedding的size是如何确定？ - 知乎](https://www.zhihu.com/question/283167457 ) |
| 总结                                                         | 基于表示型/交互型的两个分支，先了解基础的表示型，使用了dssm模型的开源库 |

阶段路线：

- 机器学习/深度学习基础---》模型原理---》框架学习-落地---》参数调节/模型效果提升---》继续机器学习/深度学习
  - 机器学习基础，如优化器，学习率；对于调节超参数，提高模型表现有用
  - 框架学习，落地模型：keras/tensorflow；模型的实现，如dssm



### week4(8.24)

| day                                                          | content                                                      |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| 跑esim模型demo                                               | 开源库：[text_matching](https://github.com/pengming617/text_matching) |
| esim加入自己训练的词向量，而不是随机初始化<br>embedding层的理解 | 构造词向量矩阵，然后根据句子中各个字的索引去look_up词向量<br> 发现问题，由于数据正负比例是80%，导致最终的acc也是80% |
| 测试数据比例的问题，dssm&esim上测试50%比例的数据             | 正常                                                         |
| 1.在66%比例的数据上测试<br>2.Bert模型的参数大小计算          | 1.正常<br> 2.参看：[Bert/Transformer模型的参数大小计算](https://blog.csdn.net/weixin_43922901/article/details/102602557) |
| 开源库源码，embedding/acc/loss的过程<br>了解albert开源库，bert-for-task |                                                              |
| 1.配置colab的gpu环境<br> 2.跑开源库，albert-tiny             | 1.因为bert-tiny(4M)参数较esim有大幅度的增加(10倍)<br> 所以要用gpu训练<br> 2.与esim差不多，提升1%/2%大概 |
| 总结                                                         | 使用了表示型/交互型模型开源库，dssm/esim，根据源码了解了模型搭建过程，即效果测试对比，解决一些落地问题 |
|                                                              |                                                              |



### week4(8.31)

| day                                             | content                                                      |
| ----------------------------------------------- | ------------------------------------------------------------ |
| 1.在LCQMC数据集上测试各模型表现<br>             |                                                              |
| 1.测试embedding的重要性<br> 2.对3个库使用的总结 | 1.embedding不是那么重要，如果使用错误的embedding，则初始偏离更大一些，后面的网络也能调整过来<br>2.看源码了解模型结构，用的时候要改的就是将输入处理成适合模型的格式，还有就是调试加print，查看各层的shape，loss等<br>其他：keras是对tensorflow的封装，限制了自定义查看训练细节，所以之后用tensorflow或pytorch，tensorflow是首选，用的人比较多 |
| 使用albert-base预训练模型                       | 参数量12M，训练起来速度明显更慢了<br>对显存的限制较大，batch_size需要减少6倍，（大概：参数x倍，batch_size需要减为原来的2x倍）<br> mark：新模型：XLNet、RoBERTa；模型压缩：知识蒸馏<br> 其他：除了白嫖谷歌的gpu，还有可以租用的价格较低的平台，如矩池云、极客云等 |
| 参看实际的落地案例，确定大致的方案              | 离线向量召回 + 预训练模型排序<br> 参看：[贝壳客服](https://www.6aiq.com/article/1590190626464)、[知乎](https://www.6aiq.com/article/1577969687897) |
| 总结                                            | albert-base使用，前面的总结，确定后续：实现demo，召回+排序   |
|                                                 |                                                              |

> 得出了几个结论：
> 训练数据的数量/质量和正负样本的比例对结果很重要
> esim较dssm有较大提升
> esim与albert-tiny很接近，esim参数量较少
>
> 补充：学习率对结果影响也比较大



### week4(9.7)

| day                                                          | content                                                      |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| 任务：随便两个句子，比较相似度                               | 需要全网所有数据的训练，所以不可行                           |
| 1.其中短语/词语相似度：可使用预训练的词向量实现<br>2.测试bert后几层向量求相似度：两个不相似的词相似度都是0.8以上，且越靠近输入的位置就越相似 | 1.找到两个：<br> Chinese-Word-Vectors（130M词量-有字、词、数字等）：词的相似度比较准确<br> 腾讯发布的（800M词量-有字、词、数字等）：更准确些<br> 两者都可以基本满足相似度的任务，但腾讯更准确些，且词量更多 |
| bert的新理解                                                 | 理解预训练语言模型.md                                        |
| elmo源码：预训练获取更好的词向量                             |                                                              |
| esim测试使用预训练词向量：词向量的入库                       | es、milvus（需要较大的内存，所以暂用不了）                   |
| 预训练词向量存到mysql                                        |                                                              |
| 总结                                                         | 基于任务，对词向量、elmo、bert进行对比，深入理解各个模型特点，特别是预训练模型<br> 词的预训练向量入库 |



### week4(9.14)

| day  | content |
| ---- | ------- |
|      |         |
|      |         |
|      |         |
|      |         |
|      |         |
|      |         |
|      |         |



阶段

- 深度学习基础和主要模型
  - [李宏毅2020机器学习深度学习(完整版)国语](https://www.bilibili.com/video/BV1JE411g7XF )

- nlp基础
  - 零散的搜索，主要是知乎和博客上的文章，github上的代码
  - [CS224n 斯坦福深度自然语言处理课](https://www.bilibili.com/video/BV1pt411h7aT)
  - [李宏毅老师2020新课深度学习与人类语言处理](https://www.bilibili.com/video/BV1RE411g7rQ)

- 开源项目的使用

  - github找各个模型的实现
  - 让模型落地，对基本的代码了解，调试
  - 加深对模型的理解

- TODO 落地案例了解，实战

  



notes

- ElasticSearch.md
- 词向量.md
- 模型综述.md
- 问答-表示型&交互型.md
- 理解预训练语言模型.md



对问答任务的理解

- 句子的语义相似度问题
- 相似度问题本质是分类问题（即要有带标签的数据 8.14）
- 两种方式，一种是产生句向量求距离，另一种是直接输入两个句子输出相似度（8.17）
  - 实际验证了这一点：文本匹配模型分两种，基于表示和基于交互（8.18）
- 使用交互型模型（9.14）
  - 由于运算量导致的延时问题，需要先召回，在排序
  - 召回是用离线向量，排序是输入模型进行输出比较
- TODO 补全基础知识，使用其他方式实现，如知识图谱



points

- 不同的任务选不同的模型
- 模型选择：模型太多了，所以必须了解模型出现的背景，往往按照任务类型+时间线就可以梳理出大致的发展流程，梳理出流程后，就能知道具体某一个模型所处的位置，即优缺点，就基本上可以选出所需模型
- update-9.14
  - 使用的方案，落地后的效率(快速响应)



difficult

阶段一：

- 通用的主流模型原理理解，因为有大量的资料，官方的和各博客（李宏毅/知乎，transformer/bert），所以倒不费劲

- d1：对于目标任务如何用nlp解决，找路径；主要是在学习基础知识中逐渐摸索，最终要走到主流的路径上
  - 这一步可以帮助选出合适的模型

- d2：落地，代码，如何把模型用代码复现，需要学习框架知识，如：tensorflow/pytorch/keras
  - 模型有了，怎么实现、落地
  - 实战可学习资料太少，不像理论部分，一抓一大把，主要还是在github搜模型，参考其他人的实现

  ---

阶段二：

- d3：开源项目使用后，真实案例的缺少
  - 虽然知道了大致的几个模型的训练，但真正用在生产环境中的是怎样的
  - 需要在实际的工作中吸收掌握
- d4：现在能做的是基于学过的，但越深入就发现nlp相关知识的不足
  - 一是时间短，只能蜻蜓点水，二是是自学而不是系统的学习，最终的本质还是基础知识的不扎实
  - 基础nlp的知识的了解，包括机器学习
  - 去了解nlp的时间线，去掌握当下的需要的基础知识，一般都会有书的









