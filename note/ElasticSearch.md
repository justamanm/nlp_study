### 概述

- 类似于一个搜索引擎
- 使用ES必须先安装java
- [各版本介绍](https://www.elastic.co/guide/en/elasticsearch/reference/index.html )，可用于查看支持的java版本



### [ES原理](https://zhuanlan.zhihu.com/p/62892586 )

- 分词
- 倒排索引（索引：与mysql的like对比，速度快）
  - 正向索引，书的目录，根据章节名称找内容
  - 倒排索引，根据内容，找章节标题/页码/所在位置，如果有搜索到多个则根据tf/idf评分
- tf-idf：衡量一个词在一个文档中的重要程度
- tf：关键词在某一个文档中出现的频率
- IDF的主要思想是：如果包含词关键词的文档越少，也就是n越小，IDF越大，则说明关键词具有很好的类别区分能力 



### 类型

| ES               | Mysql  |      |
| ---------------- | ------ | ---- |
| 索引 - index     | 数据库 |      |
| 类型 - type      | 表     |      |
| 文档 -  document | 记录   |      |



### 安装

[参考](https://blog.csdn.net/feifanhanmc/article/details/77432061 )

0. 存放路径问题：es 如果装了插件，路径文件夹不能有空格或者汉字；所以es目录不要有空格

1. [下载zip](https://www.elastic.co/cn/downloads/past-releases )

   - java-1.8 对应下载es-5.5.3，再高的版本测试无法启动
   - 如果闪退使用其他低版本的es

2. 解压后配置

   - config目录下elasticsearch.yam，增加：

     ```
     http.cors.enabled: true 
     http.cors.allow-origin: "*"
     ```

3. 执行elasticsearch.bat即可

   - 可以打开```http://127.0.0.1:9200/```即可

4. 安装可视化head插件

   - 与es独立，即放在单独目录中进行执行（且不能放到默认的plugs目录下）

   - 先安装依赖的grunt
     - ```npm install -g grunt-cli ```，使用```grunt -version```验证
   - [下载head插件](https://github.com/mobz/elasticsearch-head/releases )
     - 注意不能放在es目录的plugs文件夹下，单独创建文件夹存放
   - 解压后，进入插件目录，执行```npm install```
     - 注意命令不能加-g
   - 完成后，执行```grunt server```启动即可

5. kibana

   - 启动：es安装目录下的kibana目录/bin/kibana.bat
   - 访问localhoust:5601 即可

6. 自定义分词器

   - [安装](https://blog.csdn.net/gaoyan601/article/details/106905575 )
     - 下载：[elasticsearch-analysis-ik](https://github.com/medcl/elasticsearch-analysis-ik)
     - 配置分词器插件
     - 配置自定义词库
   - ik分词器使用：
     - ik_max_word：最细粒度的拆分 
       - 中华人民共和国人民大会堂 --》中华人民共和国、中华人民、中华、华人、人民共和国、人民、共和国、大会堂、大会、会堂 
     - ik_smart：最粗粒度的拆分
       - 中华人民共和国人民大会堂 --》中华人民共和国、人民大会堂 
     - 两种分词器使用的最佳实践是：索引时用ik_max_word，在搜索时用ik_smart
       - 即：索引时最大化的将文章内容分词，搜索时更精确的搜索到想要的结果
     - 参考：[ik_max_word和 ik_smart的区别 - 传智燕青的文章 - 知乎](https://zhuanlan.zhihu.com/p/52543633)

7. 注

   - 先启动es，再启动head插件（grunt）
   - [elasticsearch安装踩过的那些坑](https://blog.csdn.net/u013641234/article/details/80792416 )

8. 配置为服务

   - 执行bin目录下: elasticsearch-service.bat install 



### API使用

#### 7.x之后移除type类型

- 因为lucene的原因
- [Elasticsearch7.X为什么移除类型(type)](https://www.cnblogs.com/wangzhen3798/p/10765202.html )
- 相当于每个index只有一个type（_doc），一个数据库只能有一张表



#### [并发控制](https://www.cnblogs.com/loujiang/p/12686607.html )

- if_seq_no与if_primary_term，请求时带上这两个值，如果相同则更新，否则不更新

#### shards-分片

- 当一个index占用的存储空间过大，需要进行分片，每一个或每几个分片可以放在同一个node

- 可以实现读写并发

- 一般都会设置备份

- 例，index01有5个shard，每个shard备份一个

  ```python
  # 当写入一条记录时，返回
  "_shards" : {
      "total" : 2, # 所要写入的shard及其备份，所以为2
      "successful" : 1,	# 没有设置备份node，所以为1
      "failed" : 0	
    }
  ```



#### 创建index

- 直接指定到记录，会自动创建index
- put，必须指定文档id
- post，可以不指定文档id，不指定时文档id自动生成

#### 更新index(记录)

- 更新后对应记录的version会+1

- 注：全覆盖，而不是字段更新

  ```python
  PUT index01/_doc/1
  {
    "title1":"1、VMware Workstation虚拟机软件安装图解"
  }
  ```

- _create 防止覆盖已存在的文档 

  - ```index01/_doc/1/_create，```如果存在不会创建或更新
  - 不加_create，则会更新



### [mapping](https://www.elastic.co/guide/en/elasticsearch/reference/current/mapping.html )

- 创建：index时指定mapping

  ```python
  PUT /index01
  {
    "mappings": {
      "properties": {
        "age":    { "type": "integer" },  
        "email":  { "type": "keyword"  }, 
        "name":   { "type": "text"  }     
      }
    }
  }
  ```

- 增加：给存在mapping增加字段

  ```python
  PUT /index01/_mapping
  {
    "properties": {
      "employee-id": {
        "type": "keyword",
        "index": false	# 此字段不建立索引，不会被搜索
      }
    }
  }
  ```

- 更新：

  ```python
  create a new index with the correct mapping and reindex your data into that index
  ```

- 查询index的所有mapping

  ```python
  GET /index01/_mapping
  返回：
  {
    "index01" : {
      "mappings" : {
        "properties" : {
          "age" : {
            "type" : "integer"
          },
          "email" : {
            "type" : "keyword"
          }
        }
      }
    }
  }
  ```

- 查询index指定字段的mapping

  ```python
  GET /index01/_mapping/field/employee-id
  返回：
  {
    "index01" : {
      "mappings" : {
        "employee-id" : {
          "full_name" : "employee-id",
          "mapping" : {
            "employee-id" : {
              "type" : "keyword",
              "index" : false
            }
          }
        }
      }
    }
  }
  ```

  

### 更新字段

- 仅post

```python
POST index01/_update/1
{
  "script": {
    "source": "ctx._source.content=\"从官网下载VMware-workstation，双击可执行文件进行安装...\""  
  } 
}
```



### 分词

```python
GET _analyze
{
  "analyzer" : "ik_max_word",
  "text" : "补换证办理流程是什么？？"
}
```





### 查询

```python
GET /_search			# 所有索引
GET /index01/_search	 # index01索引
{
    "query": {
        "match_all": {}		# match_all 查询所有
    }
}

GET index01/_search
{
  "query": {
    "match": {		# match 模糊查询，只要包含一个或多个的文档就会被搜索出来
      "title1": {		
        "query": "软件"
      }
    }
  }
}

GET index01/_search
{
  "query": {
    "term": {		# term 全匹配
      "author": "chengyuqiang"
    }
  }
}
```



### 路由机制

- 对于分片的index，添加路由参数，指定在那个分片中创建/查找

- 优点：可以节省时间

- 缺点：自定义routing值可以造成数据分布不均的情况 

  ```python
  PUT blog/_doc/1?routing=haron
  {
    "title":"1、VMware安装",
    "author":"hadron",
    "content":"VMware Workstation虚拟机软件安装图解...",
    "url":"http://x.co/6nc81"
  }
  ```



### refresh

- 默认情况下每个分片会每秒自动刷新一次 

- index，update，delete和bulk API支持设置刷新，以控制此请求所做的更改何时对搜索可见

  ```python
  POST /_refresh 	# 刷新所有索引
  POST /blogs/_refresh  # 仅刷新blogs索引
  ```

- 通过设置配置刷新时间，可能不需要默认的每秒刷新一次

  ```python
  PUT /my_logs
  {
    "settings": {
      "refresh_interval": "30s"  # 每30秒刷新 my_logs 索引
    }
  }
  ```

  

- 精确控制每一个记录的刷新时间，一般不需要

- 空字符串或true

  - 立即显示在搜索结果中
  - 只有在从索引和搜索角度进行仔细考虑并验证它不会导致性能不佳之后，才能进行此操作 
    ```python
    PUT test/_doc/1?refresh
    PUT test/_doc/2?refresh=true
    ```

- wait_for

  - 在回复之前，请等待刷新请求所做的更改

    ```python
    PUT test/_doc/1?refresh=wait_for
    ```

- false

  - 不采取与刷新相关的操作

    ```python
    PUT test/_doc/4?refresh=false
    ```

    

参考：[Elasticsearch 7.x：3、文档管理](https://blog.csdn.net/chengyuqiang/article/details/86015411 )



### python

- [文档](https://elasticsearch-py.readthedocs.io/en/master/api.html )





### 基本使用总结

- 查询过程

  ```python
  # 对问题分词
  补换证办理流程是什么	
  ['补', '换证', '办理', '流程', '是什么']
  证书遗失灭失补证事项是否可以网上办理	
  ['证书', '遗失', '灭失', '补', '证', '事项', '是否', '可以', '网上', '办理']
  ```

  - 要自定义分词的词语，如：补换证，补证

- 首先，几种匹配情况：

  - 完全命中，无歧义（返回唯一答案）
  - 命中
    - 问题包含了多个含义
    - 不是正常的问题
    - 如：怎样办理，登记流程是什么，使用权怎么办理（返回相近含义的问题供选择）
  - 未命中
    - 应该要回答，但库里没有（返回 "暂时无法回答" ，进一步处理，如加入问题库）
    - 应该要命中，但没有命中；如细分问题：提问的内容不光针对库中的问题，还包含了答案中的内容
      - 如：登记所以依据的法律有哪些？
      - 返回：房产继承诉讼的法律依据有哪些，虽然命中，但命中推荐问题中并不是想要的
    - 完全不相关，（需要进行识别区分，且调用chatrobot进行对话，通常是没有意义的对话，如对诗）

- es的问题是只能应对完全命中的情景，其他均无法处理
  - 类似于关键词搜索

- 什么问题可以回答，哪些不能回答（分离不相关查询功能）
  - 如完全不相关的查询：今天天气怎么样-13.5，吃了吗-11，办-0.6 (score)
  - 会强行返回结果，且分数波动返回较大，无法通过分数判断
  - 是因为其评分机制比较死板

- 无法区分歧义问题
  - 即问题含义模糊，可对应多种含义
  - 什么时候应该是确定唯一的答案，什么时候返回可选问题答案
  - 还是依赖与匹配的程度，而匹配度在es中由评分体现