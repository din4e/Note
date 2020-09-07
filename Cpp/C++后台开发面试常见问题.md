能力基础，简历，面试的心态和技巧，都很重要。

参考资料
[牛客网——C++后台开发面试常见问题](https://www.nowcoder.com/discuss/59394?type=post&order=time&pos=&page=2&channel=&source_id=1)

## 数据结构

## 算法

+ 动态规划的核心思想（我说数学归纳，自底向上，大问题切割成小问题）
+ 快排的核心思想和时间复杂度（我说基于基准数的冒泡的，复杂度说了个logn 好像错了应该是nlogn
+ 做个题吧，二叉树的按层遍历，注意换行
+ top k 堆的各种时间复杂度
+ 手撕代码 两个链表找交点

## 操作系统

+ 在单线程中 i++（++i） ，都是使用三个指令来实现的：1. 将值从内存拷贝到寄存器； 2. 寄存器自增；3. 将值从寄存器拷贝到内存；
+ 进程和线程的区别
+ 进程间的通信方式
+ epoll怎么实现的，和poll，select有啥区别

## 计算机网络

+ [TCP和UDP的区别](https://www.cnblogs.com/williamjie/p/9390164.html)
  + TCP面向连接（如打电话要先拨号建立连接）；UDP是无连接的，即发送数据之前不需要建立连接；
  + TCP提供可靠的服务。也就是说，通过TCP连接传送的数据，无差错，不丢失，不重复，且按序到达;UDP尽最大努力交付，即不保   证可靠交付；
  + TCP面向字节流，实际上是TCP把数据看成一连串无结构的字节流；UDP是面向报文的，UDP没有拥塞控制，因此网络出现拥塞不会使源主机的发送速率降低（对实时应用很有用，如IP电话，实时视频会议等）；
  + 每一条TCP连接只能是点到点的；UDP支持一对一，一对多，多对一和多对多的交互通信；
  + TCP首部开销20字节；UDP的首部开销8个字节，较小；
  + TCP的逻辑通信信道是全双工的可靠信道，UDP则是不可靠信道；
  + TCP和UDP都支持全双工，在发送信息的同时，可以接收信息。
  1. 基于连接与无连接；
  2. 对系统资源的要求（TCP较多，UDP少）；
  3. UDP程序结构较简单；
  4. 流模式与数据报模式 ，拥塞控制；
  5. 保证数据正确性，保证数据顺序；不保证，可能丢包。->UDP安全性。
+ 半双工(Half Duplex)数据传输指数据可以在一个信号载体的两个方向上传输，但是不能同时传输。
+ 为啥是四次而不是三次
+ get和post的区别？幂等性问题？post怎么解决幂等性问题？
+ cookie和session区别

## C++

+ [c++this指针](https://blog.csdn.net/qq_41035588/article/details/83216792)

+ 面向对象思想的核心和优缺点（这问题真的，就多讲讲吧）
+ 重载和虚函数的理解，[底层实现](https://blog.csdn.net/Li_suhuan/article/details/100008326)；
+ c++的类型转换函数
+ c++智能指针是本身是线程安全的
+ [7类智能指针](https://www.cnblogs.com/greatverve/p/smart-ptr.html)
+ c++ new一个对象背后发生了什么
+ RAII（Resource Acquisition Is Initialization，资源获取就是初始化） 是C++一个非常好的特性：当一个对象初始化时自动调用构造函数，当一个对象到达其作用域结尾时，自动调用析构函数。所以我们可以利用这个特性解决锁的维护问题：把锁封装在对象内部！此时，在构造函数时获得锁，在语句返回前自动调用析构函数释放锁。其实这种做法有个专有的名称，叫做RAII。根据RAII对资源的所有权可分为常性类型和变性类型，代表者分别是`boost::shared_ptr<>`和`std::auto_ptr<>`，从所管资源的初始化位置上可分为外部初始化类型和内部初始化类型。
+ **RTTI（Runtime type Identification，运行阶段类型识别）只适用于包含虚函数的类。**
+ 数据库：
+ [malloc和new的区别](https://blog.csdn.net/weixin_39411321/article/details/89311059)
+ [malloc和new的区别](https://blog.csdn.net/zhong29/article/details/80930919)
  1. malloc与free是c++/c语言的标准函数，new/delete是C++的运算符。
  2. 他们都可用于申请动态内存和释放内存。new/delete比malloc/free更加智能，其实底层也是执行的malloc/free。为啥说new/delete更加的智能？因为new和delete在对象创建的时候自动执行构造函数，对象消亡之前会自动执行析构函数。既然new/delete的功能完全覆盖了malloc和free，为什么C++中不把malloc/free淘汰出局呢？因为c++程序经常要调用c函数，而c程序智能用malloc/free管理动态内存。
  3. new返回指定类型的指针，并且可以自动计算出所需要的大小。如 ：
   `int *p;    p = new int; //返回类型为int*类型，大小为sizeof(int);int *pa; pa = new int[50];//返回类型为int *，大小为sizeof(int) * 100`;malloc必须用户指定大小，并且默然返回类型为void*,必须强行转换为实际类型的指针。
  
数据库：

+ redis有哪些数据结构？项目中用到了哪些？说一下redis中的字典是怎么实现的？

设计模式：

+ [设计模式笔记](https://blog.csdn.net/bzehong/article/details/89193708)
+ [设计模式笔记 带图](https://www.cnblogs.com/kaoleba/p/11189065.html)

[STL中的sort函数实现原理](https://blog.csdn.net/vanturman/article/details/81706538)
