## Redis 相关内容





#### Redis 持久化方案
##### 快照持久化 

> 快照持久化方案会将某一时刻的所有数据都写入到硬盘中


`redis.conf`
```
save 60 1000 
dbfilename dump.rdb 
dir 
```

###### 缺陷 
- 会丢失部分数据 例如 ：如果redis宕机会导致 最后一次快照执行之后的数据丢失 

###### 创建快照的方法
- 客户端发送`BGSAVE`命令创建快照， `redis`嗲用fork来创建一个子线程复制将快照写入硬盘，**父进程则继续处理命令**
- 客户端发送`SAVE`命令创建快照，在创建完快照之前 ，**父进程不接受任何命令** 
- 在`redis.conf`设置 save 的配置选项 例如 save 60 10000 ，则表示 在最近一次创建快照之后开始算起 **60秒之内有10000次写入** 则 redis 会自动触发`BGSAVE` 命令 ，如果设置多个，满足其中一个就会被执行
- 当Aredis服务器连接Bredis服务器，向B服务器发送SYNC的命令来开始一次复制操作的时候，如果主服务器没有执行`BGSAVE`，那么主服务器就会执行`BGSAVE`命令




##### AOF 持久化(Append Only file)

> 只追加文件持久化方案,会在执行`写命令`的时候，将`写命令`命令复制到硬盘中

###### 缺点 
- AOF文件体积大 
- 重写和压缩的过程中会影响性能 



###### 一些东西
- `redis.conf` 修改 appendonly yes 开启  aof 
- 文件同步流程 3个步骤 :  写入文件内容 ->缓冲区 -> 将缓冲区写入硬盘(某个时候) redis 提供三个选项去将缓存区的内容写入硬盘: `always` 每个写命令都同步写入硬盘 ; `everysec` 每秒钟同步一次 ;`no` 由操作系统觉得何时进行同步(容易丢失数据)

###### 重写和压缩AOF文件
随着redis 不断运行，不断的执行写命令道AOF文件，AOF的文件体积会不断的增长，增大了还原操作执行时间，降低磁盘的剩余容量 。

为了解决AOF文件体积不断增大的问题：
- 用户可以向redis 发送`BGREWRITEAOF`命令，这个命令会移除AOF文件的冗余命令来重写 AOF文件 。
- 设置阈值自动执行`BGREWRITEAOF`命令 `auto-aof-rewrite-percentage` `auto-aof-rewrite-min-size` 两个条件同事触发的时候将会自动执行


#### 复制


##### 主从复制开启
- 通过配置文件  slaveof 指定一个 slaveof host port 选项的配置文件
- 运行中的redis服务器 SLAVEOF no one  终止复制  SLAVEOF host port 开始复制

##### 主从复制启动

![原理图](/resources/redis 主从复制.png)





#### Redis如何淘汰过期的keys

- 主动 
    > 当客户端访问某一个key的时候，如果key过期了，则会被删除 
    > 缺点：如果一些key不被访问则内存占用越大
- 被动 
    > 为了节省内容，redis 使用了被动模式，
    > 即：redis 每10秒钟做的事情
    > 1.测试随机的20个keys进行相关过期检测。
    > 2.删除所有已经过期的keys。 
    > 3.如果有多于25%的keys过期，重复步奏1.


#### Redis 内存淘汰策略
在 `redis.conf`中存在一行配置 `maxmemory-policy volatile-lru` 用来配置 内存淘汰策略 
 - noeviction 内存不足以容纳写入的数据，新写入的操作会报错
 - allkeys-lru  内存不足以容纳写入的数据，移除最近最少使用的key(推荐使用)
 - allkeys-random  内存不足以容纳写入的数据 随机删除key
 - volatile-lru 内存不足以容纳写入的数据，在设置了过期时间的key空间中，移除最少使用的key
 - volatile-random 内存不足以容纳写入的数据，在设置了过期时间的key空间中，随机删除某个key 
 - volatile-ttl 内存不足以容纳写入的数据，在设置了过期时间的key空间中 移除快要过期的key 




#### Redis 使用单线程的优劣式，已经为什么单线程性能还比较高
-  redis 高效原因 
    - 基于内存，网络 
    - 多路复用机制 
    - 单线程 避免cpu切换，锁操作

- 为什么使用单线程性能还高 
    - 基于内存操作，性能很高，不需要多线程操作 
    - 不使用多线程，减少了cpu的切换操作
    - 单线程不需要考虑线程安全，避免锁、死锁的情况


#### Redis 内存回收策略







