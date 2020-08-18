双数组trie树

> 双数组Trie (Double-Array Trie)结构由日本人JUN-ICHI AOE于1989年提出的，是Trie结构的压缩形式，仅用两个线性数组来表示Trie树，该结构有效结合了数字搜索树(Digital Search Tree)检索时间高效的特点和链式表示的Trie空间结构紧凑的特点。双数组Trie的本质是一个确定有限状态自动机（DFA），每个节点代表自动机的一个状态，根据变量不同，进行状态转移，当到达结束状态或无法转移时，完成一次查询操作。在双数组所有键中包含的字符之间的联系都是通过简单的数学加法运算表示，不仅提高了检索速度，而且省去了链式结构中使用的大量指针，节省了存储空间。 

参考：

- [hanlp--双数组Trie树](https://www.hankcs.com/program/java/%e5%8f%8c%e6%95%b0%e7%bb%84trie%e6%a0%91doublearraytriejava%e5%ae%9e%e7%8e%b0.html)
- [双数组Tire树(DART)详解](https://www.bbsmax.com/A/Ae5RyEj7JQ/ )  - 很详细
- [DoubleArrayTrie（DAT）双数组字典树原理解读](https://zhuanlan.zhihu.com/p/113262718 )



trie树为什么占用内存？双数组trie树为什么说是对trie进行了压缩？























