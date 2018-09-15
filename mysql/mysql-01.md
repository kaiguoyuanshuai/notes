### 时间复杂度


> 在数据结构与算法中，通常会使用`时间复杂度`来描述一个算法的性能，或者一种数据结构的检索性能，这里面不会详细的去描述如何计算时间复杂度，只是给一个认识 。 `O(1)` `O(n)` `O(log(n))` 等常见的时间复杂度直观的认识



![原理图](/resources/mysql/time-complexity.png)


![原理图](/resources/mysql/exsample.png)


### mysql 应用结构图



### B+tree 简单的理解

### MYSAM、InnoDB 区别

### MYSAM、InnoDB 数据存储结构 

#### 索引、联合索引 的存储过程 
#### 索引
 1. 非独立的列 
 2. 前缀索引  [前缀索引](http://www.cnblogs.com/gomysql/p/3628926.html) ```sql  alter table city_demo add key (city(6)); ```
 3. 多列索引和索引顺序  


### InnoDB 数据插入、查询


**问题**
- 为什么索引很多的时候，会影响插入更新的性能
- 为什么要使用 B+tree



### InnoDB 查询原理
