### Topic&Partition的概念



### 消息分区分发

#### 自定义分区策略 
默认情况下 ：对key进行hash取模算法 如果key 为空的话 ，则进行随机运算 

### 消息消费

- 消费者可以指定消费某一个/多个分区  TopicPartition  consumer.assign
- 