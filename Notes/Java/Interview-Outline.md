# Java 程序员面试知识大纲

> 学历代表过去，财力代表现在，学习能力代表将来。

## 基础算法

- 排序
- 查找

## 操作系统和常用协议

- 进程、线程、协程
- 编译原理
- TCP 协议
  - 三次握手
  - 四次挥手
  - 确认机制、滑动窗口
- HTTP 协议
  - HTTP Method
  - HTTP Header
  - Keep Alive
  - Websocket
  - HTTPS
  - HTTP2
- Linux
  - User Space, Kernel Space
  - Shell

## 程序设计

- OO, AOP, Functional
- 封装、多态
- 面向对象设计六大原则
- 设计模式
- 代码风格
- 代码重构
- 单元测试

## Java 集合框架

- List: ArrayList, LinkedList
- Set: HashSet, LinkedHashSet
- Map: HashMap, LinkedHashMap, ConcurrentHashMap, TreeMap

## Java 扩展

- IO
- NIO, Netty, Mina
- Servlet
- JMX
- Java 8
  - Lambda
  - Stream

## Java 并发

- volatile, synchronized
- Thread, ThreadLocal, Runnable, Callable
- Lock, ReadWriteLock, ReentrantLock, StampedLock
- CountDownLatch, CyclicBarrier, Semaphore, Exchanger
- Executor, ExecutorService, Future, CompletableFuture
- Fork-Join
- AQS, CAS, ABA 问题
- Java Memory Model

## JVM

- 虚拟机组成结构
- 虚拟机堆内存结构
- 垃圾收集算法、垃圾收集器
- 虚拟机调优

## 框架和语言

- Spring, Spring Boot, Struts
- MyBatis, Hibernate
- jQuery, React, Vue.js
- JavaScript, Node.js, Scala, Python...

## 数据库相关

- 表设计经验
- 事务 ACID 特性、事务四个隔离级别
- 索引原理以及运用
- 分页、分库、分表、读写分离
- 分布式事务的典型处理方式：两阶段型（2PC）、补偿型（TCC）、异步确保型、最大努力通知型

## 高并发、分布式、中间件、微服务、容器

- 并发编程模型
- Map/Reduce，Master/Slave
- Tomcat
- Nginx
- Redis
- Kafka
- Dubbo
- Hadoop, HDFS, Zookeeper, HBase
- MongoDB
- Spark, Storm
- Docker、K8s

## 应用题

- 如何用 Java 多线程模拟现实生活中的场景？例如：多辆车自驾旅游，在加油站会和休息，最终又一起达到目的地。
- 如何实现大文本的敏感词汇过滤功能？
- 如何实现代码语法高亮功能？
- 如何实现一个短链接服务？
- 如何设计下载大量 MP3 歌曲的分布式可容错系统？
- 如何设计抢红包功能？
- 如何设计秒杀系统？
- 如何设计网络爬虫系统？
- 如何设计存储海量的小文件（大小都是几百K~几M）？
- 有两个大文本文件，文件中的数据按行存放，如何实现找到两个文件中彼此不相同的行？

## 软素质

- 工作习惯
- 学习习惯
- 职业规划
- 兴趣爱好