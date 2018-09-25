### Topic&Partition的概念



### 消息分区分发

#### 自定义分区策略 

#### 默认分区策略 
默认情况下 ：对key进行hash取模算法 如果key 为空的话 ，则进行随机运算 

### 消息消费

- 消费者可以指定消费某一个/多个分区  TopicPartition  consumer.assign
- 



消费者与partion 的数量 
消费者 > partion 多出来的消费者不工作，浪费资源
消费者 < partion 消费者会同时消费多个partion（建议：整数倍）



### 重新分区
增减 consumer、broker、partition 会导致 Rebalance

#### 分区分配策略 
Range(范围) -》默认 
    按照字母的顺序进行排序，

案例 ：
    10分区 - 3消费者 
    C1、C2、C3
    range = 10 /3  
    C1 ： 0,1,2,3，


RoundBobin(轮训) 


#### 轮训策略触发时机 
- 对于 consumer group 新增消费者会触发 rebalance 
- 消费者离开 consumer groupp 
- topic 中新增了分区 
- 消费者主动取消订阅topic

#### Rebabance 执行&管理 
Coordination  管理器 


