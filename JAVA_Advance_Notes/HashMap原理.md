

### HashMap  实现原理

  #### HashMap 数据结构

##### 1.7 版本的数据结构


![原理图](/resources/hashMap/HashMap_数据结构存储原理图.png)





##### 1.8 版本的数据结构




#### 如何取出 get put 数组 的下标



##### 1、计算hash

```java
   static final int hash(Object key) {
        int h;
        return (key == null) ? 0 : (h = key.hashCode()) ^ (h >>> 16);
    }
```

##### 2、计算下标i

```java
n = tab.length
i = (n - 1) & hash
```

##### 3、效果图如下
![原理图](/resources/hashMap/hashcode.png)

**附加知识 ：**

![原理图](/resources/javaBase/Java_基础之位运算.png)

##### 4、什么是Hash碰撞 
`Hash碰撞`表示 key 最终计算(通过上面的计算方法计算)出来的值`index`下标的数组已经被占用了

#### 如何进行自动扩容

##### 1、什么时候自动扩容 

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

##### 2、自动扩容的方式

 ```java
 void resize(int newCapacity) {
        Entry[] oldTable = table;
        int oldCapacity = oldTable.length;
        if (oldCapacity == MAXIMUM_CAPACITY) {
            threshold = Integer.MAX_VALUE;
            return;
        }

        //创建新的长度的数组 
        Entry[] newTable = new Entry[newCapacity];
        transfer(newTable, initHashSeedAsNeeded(newCapacity));
        //将引用修改为新的数组
        table = newTable;
        threshold = (int)Math.min(newCapacity * loadFactor, MAXIMUM_CAPACITY + 1);
    }

 ```
  	
#### put HashMap 的数据

##### put 数据的过程  
1. 对key的hashCode()做hash，然后再计算index;
2. 如果没碰撞直接放到bucket里；
3. 如果碰撞了，以链表的形式存在buckets后；



4. 如果碰撞导致链表过长(大于等于TREEIFY_THRESHOLD)，就把链表转换成红黑树；
如果节点已经存在就替换old value(保证key的唯一性)
5. 如果bucket满了(超过load factor*current capacity)，就要resize。




```java
public V put(K key, V value) {
        if (table == EMPTY_TABLE) {
            inflateTable(threshold);
        }
        if (key == null)
            return putForNullKey(value);
        //计算index的值
        int hash = hash(key);
        int i = indexFor(hash, table.length);

        //替换所有的新的值 如果key 相同
        for (Entry<K,V> e = table[i]; e != null; e = e.next) {
            Object k;
            if (e.hash == hash && ((k = e.key) == key || key.equals(k))) {
                V oldValue = e.value;
                e.value = value;
                e.recordAccess(this);
                return oldValue;
            }
        }

        modCount++;
        addEntry(hash, key, value, i);
        return null;
    }
```

```java
 void addEntry(int hash, K key, V value, int bucketIndex) {
   //如果size 大于 容量*负载因子 则扩容 
        if ((size >= threshold) && (null != table[bucketIndex])) {
            resize(2 * table.length);
            //计算出扩容后的hash
            hash = (null != key) ? hash(key) : 0;
            //重新计算 index
            bucketIndex = indexFor(hash, table.length);
        }

        createEntry(hash, key, value, bucketIndex);
    }
```

```java
    void createEntry(int hash, K key, V value, int bucketIndex) {
      //获取出当前数据的链表
        Entry<K,V> e = table[bucketIndex];
      // 将当前的值加入到链表中
        table[bucketIndex] = new Entry<>(hash, key, value, e);
        size++;
    }

```



