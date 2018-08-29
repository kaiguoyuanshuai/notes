## Java 进阶知识 

#### 集合

ArrayList、LinkedList、Hashtable、HashMap、ConcurrentHashMap、HashSet 实现原理

- **HashMap**

  - **HashMap  实现原理**

    ##### HashMap 数据结构

    1.7 版本 

    ![原理图](resources/hashMap/HashMap 数据结构存储原理图.png)

    1.8 版本



    ##### 如何取出 get put 数组 的下标

    1、计算hash

    ```java
       static final int hash(Object key) {
            int h;
            return (key == null) ? 0 : (h = key.hashCode()) ^ (h >>> 16);
        }
    ```

    2、计算下标i

    ```java
    n = tab.length
    i = (n - 1) & hash
    ```



    3、效果图如下

    ![原理图](resources/hashMap/hashcode.png)



    **附加知识 ：**

    ![原理图](resources/javaBase/Java 基础之位运算.png)





  ##### 如何进行自动扩容

  	1、什么时候自动扩容 

  ```java
  // 判断是否需要自动扩展
  threshold = (int) Math.min(capacity * loadFactor, MAXIMUM_CAPACITY + 1);
  (size >= threshold) && (null != table[bucketIndex])
      
  //扩容大小
  resize(2 * table.length);
  ```

  `capacity` 表示容器大小 

  `loadFactor` 表示 负载因子 



  **结论 ：**

  - 当HashMap内转载大小 大于  `capacity * loadFactor`  的时候就会进行自动扩容 ；

  - 扩容大小为 当前大小的`2倍` 


  	2、自动扩容的方式

  	













  - HashMap 1.7-1.8的变化区别 

  - 线程不安全的问题(死循环)

    [美团：Java 8系列之重新认识HashMap](https://tech.meituan.com/java_hashmap.html)
    [Java HashMap原理解析](https://yikun.github.io/2015/04/01/Java-HashMap%E5%B7%A5%E4%BD%9C%E5%8E%9F%E7%90%86%E5%8F%8A%E5%AE%9E%E7%8E%B0/)






- HashTable 实现原理 

- ConcurrentHashMap 实现原理  
- ConcurrentHashMap 1.7-1.8的区别

- HashTable与ConcurrentHashMap的区别






####多线程 

- ThreadLocal 实现原理、应用场景、避免的问题


- 



