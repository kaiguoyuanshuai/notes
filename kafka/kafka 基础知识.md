

### 基本概念 

- 消息总是会持久化到磁盘中 （默认保存7天）



#### Kafka API 配置说明

** ProducerConfig 消息发送端配置 **

- ProducerConfig.ACKS_CONFIG (asks)
0 消息发送给broker之后，不需要确认 （）

- ProducerConfig.BATCH_SIZE (batch.size) 


** ConsumerConfig 消费端配置 **


** 同步发送与异步发送 **









### 集群 

#### 集群配置 
- 连接 zookeeper
- 设置唯一的broker 
- 设置listener

#### 集群选举
master 选举规则 ： 注册到集群的broker最小的节点为master

