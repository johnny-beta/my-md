## Johnny 个人学习笔记

#### 1 与memcached区别

​	mem是**多线程，非阻塞IO复用**  redis是**单线程多路IO复用**

#### 2 redis持久化

#### 3 redis内存淘汰机制

​	redis数据结构

​	常用数据类型：

#### 4ThreadLocal模式synchronized关键字

　　ThreadLocal模式synchronized关键字都用于处理多线程并发访问变量的问题，只是二者处理问题的角度和思路不同。

　　1）ThreadLocal是一个java类，通过对当前线程中的局部变量的操作来解决不同线程的变量访问的冲突问题。所以，ThreadLocal提供了线程安全的共享对象机制，每个线程都拥有其副本。

　　2）Java中的synchronized是一个保留字，它依靠JVM的锁机制来实现临界区的函数或者变量的访问中的原子性。在同步机制中，通过对象的锁机制保证同一时间只有一个线程访问变量。此时，被用作“锁机制”的变量时多个线程共享的。

　　同步机制(synchronized关键字)采用了“**以时间换空间**”的方式，提供一份变量，让不同的线程排队访问。而ThreadLocal采用了“**以空间换时间**”的方式，为每一个线程都提供一份变量的副本，从而实现同时访问而互不影响。

```javascript
function a() {
    alert(1);
}
```



#### 5 threadlocal synchronize volatile三个关键字的区别

1. threadlocal是针对的单例模式下，不同线程使用不同局部变量的折衷办法，属于空间换时间（是线程安全的）--实现原理。threadlocal.map，属于每一个线程Thread类下面的一个方法
2. synchronize是jvm采用的加锁机制，将该资源或对象同一时刻，只能由同一线程去访问，等执行完释放锁以后，才能执行其他的
3. volatile是不保证的原子性的一个操作（所以仍然不是线程安全的），他具有可见性-能避免脏读，同时避免了jvm的执行顺序重排

#### 6 相关进阶知识点：

消息队列：

- 高可用

- 顺序执行

- 架构设计

分布式搜索引擎

- 设计原则、分布式
- 海量级优化查询性能
- 生产环境的部署

redis

- redis线程模型

SERVER SOCKET -> SOCKET事件 -> I/O多路复用程序 -> 事件queue -> 文件事件分配器 ->{连接应答处理器、命令请求处理器、命令回复处理器}

高性能高并发的原因：

1. 纯内存操作
2. 非阻塞式I/O多路复用
3. 单线程避免了多线程的上下文切换

- redis数据类型和使用场景
- 过期策略，手写LRU
- 如何保证高可用
- redis持久化
- reids cluster集群

1. redis架构，
2.  **单机版**

![](https://img2018.cnblogs.com/blog/1481291/201809/1481291-20180925142100480-1152515615.png)

###### 特点：简单

问题：

1、内存容量有限 2、处理能力有限 3、无法高可用。

单机redis能够承载QPS大概在上万，到几万不等

**主从复制**

![](https://img2018.cnblogs.com/blog/1481291/201809/1481291-20180925142118041-1727225479.png)

**哨兵**

![s](https://img2018.cnblogs.com/blog/1481291/201809/1481291-20180925142143478-1454265814.png)

**集群（proxy 型）：**

![](https://img2018.cnblogs.com/blog/1481291/201809/1481291-20180925142206124-913246424.png)

**集群（直连型）：**

![](https://img2018.cnblogs.com/blog/1481291/201809/1481291-20180925142304757-1498788186.png)



- 应对缓存雪崩

dubbo





hash算法 -> 一致性hash算法 -> hash slot 算法

1. #### 双重加锁机制：参考spring源码

```java
/**
     * Return the (raw) singleton object registered under the given name.
     * <p>Checks already instantiated singletons and also allows for an early
     * reference to a currently created singleton (resolving a circular reference).
     * @param beanName the name of the bean to look for
     * @param allowEarlyReference whether early references should be created or not
     * @return the registered singleton object, or {@code null} if none found
     */
    protected Object getSingleton(String beanName, boolean allowEarlyReference) {
        Object singletonObject = this.singletonObjects.get(beanName);
        if (singletonObject == null && isSingletonCurrentlyInCreation(beanName)) {
            synchronized (this.singletonObjects) {
                singletonObject = this.earlySingletonObjects.get(beanName);
                if (singletonObject == null && allowEarlyReference) {
                    ObjectFactory<?> singletonFactory = this.singletonFactories.get(beanName);
                    if (singletonFactory != null) {
                        singletonObject = singletonFactory.getObject();
                        this.earlySingletonObjects.put(beanName, singletonObject);
                        this.singletonFactories.remove(beanName);
                    }
                }
            }
        }
        return (singletonObject != NULL_OBJECT ? singletonObject : null);
    }
```





mysql存储结构是页 16K--

- **FILE HEADER - PAGE HEADER - .... USER RESCORDS - PAGE DIRECTORY - FREE SPACE  -FILE TAILER**
- **这些数据页组成了双向链表  这些数据页内的用户数据又组成了单项链表**



#### 字段

- 尽量使用`TINYINT`、`SMALLINT`、`MEDIUM_INT`作为整数类型而非`INT`，如果非负则加上`UNSIGNED`
- `VARCHAR`的长度只分配真正需要的空间
- 使用枚举或整数代替字符串类型
- 尽量使用`TIMESTAMP`而非`DATETIME`，
- 单表不要有太多字段，建议在20以内
- 避免使用NULL字段，很难查询优化且占用额外索引空间
- 用整型来存IP

#### 索引

- 索引并不是越多越好，要根据查询有针对性的创建，考虑在`WHERE`和`ORDER BY`命令上涉及的列建立索引，可根据`EXPLAIN`来查看是否用了索引还是全表扫描
- 应尽量避免在`WHERE`子句中对字段进行`NULL`值判断，否则将导致引擎放弃使用索引而进行全表扫描
- 值分布很稀少的字段不适合建索引，例如"性别"这种只有两三个值的字段
- 字符字段只建前缀索引
- 字符字段最好不要做主键
- 不用外键，由程序保证约束
- 尽量不用`UNIQUE`，由程序保证约束
- 使用多列索引时主意顺序和查询条件保持一致，同时删除不必要的单列索引



> - MYISAM INNODB
> - 只有表级所 没有行级所
> - 没没有事务
> - 没有外键
> - 崩溃后的安全恢复



1. **为什么要用MYBATIS:Mybatis就是面向sql语句的**，便于sql优化

2. 图片存储使用FASTDFS 分布式存储

3. 使用静态server:nginx+f5

4. seo:**添加一个关键词**、做网页的**伪静态化或者是纯静态化**等处理。还有就是在页面的关键词中中添加一些链接等。

5. 广告 搜索面板 购物车需要加优化

6. 设置有效期  LRU

7. redis cluster 或 redis 主从+sentinal哨兵监测

8. 集群的登陆问题 CAS框架 与shiro或spring security集成

   

![](http://mmbiz.qpic.cn/mmbiz_png/tibrg3AoIJTtt5WD7PStDP8xn9FCAqN0Hc2PLZUxDUsebS6dLW6fKHyGVfosuX3XeLwClNP3GWNGvw0dicv8mficw/0?wx_fmt=png)

**查询缓存 --> 解析器 (解析语法-->预处理器) --> 查询优化器 --> 执行计划 --> 查询引擎**

