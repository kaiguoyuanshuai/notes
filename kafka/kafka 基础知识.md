

### 基本概念 

#### 相关知识

- 消息总是会持久化到磁盘中 （默认保存7天）
- 每一个消费group都是能够重新开始消费所有已经发出的topic 消息
- producer 是主动将消息push 到kafka消息队列中 consumer 主动从kafka消息队列中pull 消息进行消费



![image](https://user-images.githubusercontent.com/42650061/45919615-b38f8a00-beca-11e8-9ca1-c4186462591d.png)


#### Kafka API 配置说明

**ProducerConfig 消息发送端配置**

- ProducerConfig.ACKS_CONFIG (asks)
0:消息发送给broker之后，不需要等待 broker 的确认。（性能最高，但是当server 宕机的时候会导致数据丢失）
1:表示producer 只需要获取kafka集群节点的leader节点确认即可，延时较小，同时可以确保leader 节点的数据不会丢失
all(-1) : 需要ISR中所有的Replica给予接受确认，速度最慢，安全性最高 


- ProducerConfig.BATCH_SIZE (batch.size) 
consumer可以通过批量的方式来提交消息，可以通过一这个参数来控制批量提交的字节数大小，默认16kb 
- linger.size 
![image](https://user-images.githubusercontent.com/42650061/45919712-6ca29400-becc-11e8-8a5e-2655c0eed52b.png)

- max.request.size 
设置请求消息的最大数量，为了防止较大的数据包影响到吞吐量，默认值为1M 

** ConsumerConfig 消费端配置 **
- group.id 
consumer group 是kafka提供的具有容错性的消费者机制，组内可以存在多个消费者共享一个公共的ID，即 group id ，组内的所有消费者协调在一起订阅主题（topic）的所有分区（partition） 

![image](https://user-images.githubusercontent.com/42650061/45919750-f2beda80-becc-11e8-8dad-dced028555c4.png)

- enable.auto.commit
设置自动提交，可以通过consumer.commitSync 方式实现手动提交 

- enable.auto.reset
laster 新的消费者将会从其他的消费者最后消费的offerset开始消费topic 
earlist 新的消费者会从最早未消费过的消息进行消费 
none 新的消费者加入的时候，由于之前不存在offser 会抛出异常

** 同步发送与异步发送 **









### 集群 

#### 集群配置 
- 连接 zookeeper
- 设置唯一的broker 
- 设置listener

#### 集群选举
master 选举规则 ： 注册到集群的broker最小的节点为master


