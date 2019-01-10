# Spark简介
1.Spark通过SparkContext对象访问Spark这个对象代表对计算集群的一个链接，一旦有了SparkContext就可以用它来创建RDD。
2.完成应用与spark的连接之后，就需要在程序中导入Spark包并且创建SparkContext，通过创建一个sparkContext对象配置应用，然后基于这个对象创建SparkContext。
```java
// spark配置
    val sparkConf = new SparkConf()
      .setAppName(KAFKA_APPLICATION_ID)
    .set("spark.streaming.kafka.consumer.poll.ms", "5000")
 ```
 # RDD 
 1. rdd——弹性分布式数据集，在Spark中对数据的所有操作就是创建RDD，转化已有的RDD，调用RDD操作进行求值
 2. 每个RDD分为多个分区，这些分区运行在集群的不同的节点上，使用sc.textFile()可以创建一个字符串的RDD
 3. 创建出来RDD之后，RDD支持转化操作transformation（生成一个新的RDD）和行动操作action（计算出一个RDD的结果）
 ## 创建RDD
 1.读取外部数据集或者对一个集合进行并行化 
 ```java
 val lines = sc.parallelize(List("hello","world"))
 ```
2. collect()函数可以用来获取整个RDD中的数据
 ## transformation和action操作
 1. transformation： map()操作，接收一个函数，将这个函数作用于RDD中的每一个元素。filter()操作，接收一个函数，将RDD中满足该函数的元素放入新的RDD中返回
 。flatmap()操作，对每个输入元素生成多个输出元素，返回的各列表的元素组成的RDD而不是一个由列表组成的RDD（map操作）
 2. persist()持久化，使用Spark持久化存储一个RDD时，计算RDD的节点会分别保存他们所求出的分区数据，有一个持久化数据的节点发生故障，spark会在需要用到缓存的数据
 时重新重算丢失的分区数据。默认情况下会将数据以序列化的形式缓存在JVM堆中，unpersist()手动将持久化的RDD从缓存中移除。
 
 # SparkStreaming
 1. 创建StreamingContext，流计算的入口，可指定多长时间处理一次新数据的批次间隔batch interval，调用start（）方法开始接收数据，执行会在另一个线程中进行，
 需要调用awaitTermination（）等待流计算的完成，防止应用的退出。
 ```java
  // 设置spark streaming的配置信息，以及时间颗粒度
    val ssc = new StreamingContext(sparkConf, Seconds(KAFKA_Spark_Circle))
 ```
 
 
