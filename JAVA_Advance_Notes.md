##Java 进阶知识 

####集合

ArrayList、LinkedList、Hashtable、HashMap、ConcurrentHashMap、HashSet 实现原理

- HashMap
  - HashMap  实现原理 

    ##### 如何取出 get put 数组 的下标

    先将key 进行 hashCode 然后将 hashCode 进行hash然后再与长度取&位运算



    ![原理图](resources/hashMap/hashcode.png)





    ##### HashMap put 的位运算规则原理:

    - hashcode 计算方法 
    - index 计算方法

    ![原理图](resources/javaBase/Java 基础之位运算.png)





  - HashMap 1.7-1.8的变化区别 

  - 线程不安全的问题(死循环)

    [美团：Java 8系列之重新认识HashMap](https://tech.meituan.com/java_hashmap.html)
    [Java HashMap原理解析](https://yikun.github.io/2015/04/01/Java-HashMap%E5%B7%A5%E4%BD%9C%E5%8E%9F%E7%90%86%E5%8F%8A%E5%AE%9E%E7%8E%B0/)


![原理图](resources/hashMap/HashMap 数据结构存储原理图.png)



- HashTable 实现原理 

- ConcurrentHashMap 实现原理  
- ConcurrentHashMap 1.7-1.8的区别

- HashTable与ConcurrentHashMap的区别






####多线程 

- ThreadLocal 实现原理、应用场景、避免的问题


- 



