Spring 循环依赖问题 原理分析 

### 哪些问题 

参考 ： https://segmentfault.com/a/1190000015221968



1、Spring是如何解决循环依赖的

2、Spring对于循环依赖的解决方案是否还有纰漏

3、既然不能完全解决循环依赖，我们该怎么办

#### 何为循环依赖

> 循环依赖：即两个或多个Bean相互之间的持有对方，比如CircleA引用CircleB，CircleB引用CircleC，CircleC引用CircleA，则它们最终反映为一个环。 



#### Spring是如何解决循环依赖的

- Spring getBean() 的过程
- 





#### Spring对于循环依赖的解决方案是否还有纰漏

- 构造方法注入的bean 

- BeanPostProcessor改变了Bean的版本 

  

#### 既然不能完全解决循环依赖，我们该怎么办