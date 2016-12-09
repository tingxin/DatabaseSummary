# 常用NoSQL数据库总结
总结各种数据库的异同,很多内容来自网络,仅供参考

##预览
###Key-Value数据库
* Redis

###Document-based数据库
* MongoDB

###Column-based数据库
* Cassandra

###分布式数据库
* Cassandra
* DynamoDB

##背景
###NoSQL背后的两种模式

NoSQL其实并不是什么妖魔鬼怪，相反，NoSQL的真谛其实应该是Not Only SQL，其产生背景是在数据量和访问量逐渐增大的情况下下，人为地去添加机器或者切分数据到不同的机器，变得越来越困难，人力成本越来越高，于是便开始有了这样的项目，它们的本意是提高数据存储的自动化程度，减少人为干预的时间，让负载更加均匀等。在国际上，真正的代表之作有来自Google的 BigTable 和Amazon 的Dynamo，他们分别使用了不同的基本原理。

###MapReduce

这是历史最久的一种模型，典型的代表是BigTable。Map表示映射，Reduce表示化简。MapReduce通过把对数据集的大规模操作分发给网络上的每个节点实现可靠性（Map）；每个节点会周期性地把完成的工作和状态的更新报告回来（Reduce）。大多数分布式运算可以抽象为MapReduce操作。Map是把输入Input分解成中间的Key/Value对，Reduce把Key/Value合成最终输出Output。这两个函数由程序员提供给系统，下层设施把Map和Reduce操作分布在集群上运行。

###Dynamo

Amazon于2006年推出了自己的云存储服务S3，2007年其CTO公布了S3的设计方案，从此江湖中就不再太平了，开源项目一个个如雨后春笋般地出现了。比较常见的有Facebook开发的Cassandra（如果没有记错，在去年浏览他们项目网页的时候，上面还写着他们之中的一个开发人员是Dynamo的设计人员，现在风头紧，去掉了），还有Linkedin的voldemort，而在国内话，有豆瓣网的beansDB，人人网的nuclear等等。这里我主要讨论的也是Dynamo的方案细节。

入门基础

Dynamo的意思是发电机，顾名思义，这一整套的方案都像发电机一样，源源不断地提供服务，永不间断。以下内容看上去有点教条，但基本上如果你要理解原理，这每一项都是必须知道的。