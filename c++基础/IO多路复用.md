# select、epoll、poll的学习
- 同步IO需要在读写事件就绪后自己负责读写，也就是说这个过程是阻塞的。select/epoll/poll都是同步IO，

- 异步IO是不需要自己负责读写的，只负责把数据从内核拷贝到用户空间。
----
## IO多路复用
普通IO只能监听一个socket，但是io多路复用可以同时监听多个socket

内核一旦发现进程指定的一个或者多个IO条件准备读取时，他就通知该进程。
适用的场景
1. 客户处理多个文件描述字符时，必须用多路复用
2. 客户处理多个套接口的时候
3. 一个TCP服务器既要监听套接口，又要处理已经连接的套接口
4. 一个服务器既要处理TCP又要处理UDP的时候
5. 一个服务器处理多个协议或者多个服务的时候

与多进程相比，**优点** 在于：**系统开销小**，系统不需要创建新的进程，也不用在这些进程之间进行切换和维护，大大减小了系统开销


-----
## select
select 函数
```
int select(int maxfdp1,fd_set *readset,fd_set *writeset,fd_set *exceptset,const struct timeval *timeout)
```
返回值：就绪描述符的数目，超时返回0，出错返回-1

缺点：
- 每次调用select的时候都需要把文件描述符的集合从用户态复制到内核态，开销很大。
- 检测到sock有数据，就返回，但是不会告知是哪个sock。需要在内核遍历所有的文件描述符，开销很大。
- 支持的文件描述符数量太小了，默认是1024
- 不是线程安全的
- 会修改传入的数组  

-----
## poll
```
int poll()
```
改进：
- 修改了1024个链接的限制，变成了无限制
- 不会修改传入的数组

缺点：
- 仍然是线程不安全的

-----
## epoll
提供了三个函数
- `epoll_create`创建epoll句柄，
- `epoll_ctl`注册要监听的事件类型
- `epoll_wait`等待事件的产生

改进：
- epoll_ctl函数，每次注册新的事件到epoll句柄时，会把所有的fd拷贝到内核，不会在epoll_wait的时候重复拷贝。epoll保证每个fd在整个过程只会拷贝一次
- 会告知是哪个sock有数据，不用自己去找
- epoll没有文件描述符FD的限制
缺点：
- 只支持linux

-----
## 总结
- select和poll需要不断地轮询所有的fd集合，期间可能有多次睡眠和唤醒的交替。而epoll只需要判断一下就绪链表是否为空即可，可以省下大量的CPU时间。
- select和poll每次调用时，需要将fd集合从用户态复制到内核态，而epoll只需要复制一次。

[知乎上看到的解释（简单版）]
>
  epoll和select/poll最大区别是
  1. epoll内部使用了mmap共享了用户和内核的部分空间，避免了数据的来回拷贝
  2. epoll基于事件驱动，epoll_ctl注册事件并注册callback回调函数，epoll_wait只返回发生的事件避免了像select和poll对事件的整个轮寻操作

------
参考链接：
https://www.cnblogs.com/creazylinux/p/7364685.html
http://www.cnblogs.com/Anker/archive/2013/08/14/3258674.html
https://www.zhihu.com/question/32163005
