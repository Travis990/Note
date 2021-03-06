# 1、说明

一直有一个疑问，就是在网络开发的时候，什么场景下使用一个连接一个线程，什么时候使用多路复用，虽然也知道，多路服用适用于大量的短连接的场景，而少量的长连接用多线程更合适，但是一直没有一个系统的了解，直到今天和部门的大神聊到Node.js时提到几个名词，才知道，这些东西在Java里面，已经是一整套的系统的知识点了。

Java 的 IO 编程中有 ***BIO、NIO*** 和 ***AIO*** 的概念，这三种概念其实对于我们并不陌生，只是概念名词不知道而已

## 1.1、BIO

即 ***Block IO***，阻塞式 IO，表现为一个连接一个线程，独立处理 IO，互不干扰

缺点：

1. 新连接时需要创建线程，而线程的创建和销毁的成本很高；
2. 线程本身占据的内存也不小；
3. 线程切换成本高；
4. 容易造成锯齿状的系统负载；

一般这类的编程中，会引入线程池避免一些问题，没有 IO 时，线程阻塞着，有 IO 时间发生时，线程开始工作

## 1.2、NIO

即 ***Non-block IO***，非阻塞式 IO，即使用多路复用实现，当有一个新的IO事件时，去查看该IO的事件去处理

## 1.3、AIO

即 ***Asynchronous IO***，异步 IO，和 ***NIO*** 的区别在于，当有新的事件时，启动线程异步处理事件