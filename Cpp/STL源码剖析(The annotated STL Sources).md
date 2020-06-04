# STL源码剖析（The annotated STL Sources）

C++作为一个面向对象程序设计语言，具有一个同样重要的思维模式：泛型。  
STL入门specialize之路:  
C++ template学习泛化以及深入理解STL第一道门槛：class template、function template、member template、specialization、partial specialization。STL大量使用了operator overloading。
运用STL，了解泛型技术和STL学理、最终扩充STL。

## 2 空间配置器

### 2.3 内存基本处理工具

三个函数都有commit or rollback构造所有必须元素，否则不构造任何函数。

`uninitialized_copy()` 包含两步：

+ **配置空间区块**
+ 在真个区块上构造元素  

`uninitialized_fill()`

`uninitialized_fill_n()`

POD必然拥有trivial ctor/dtor/copy/assignment函数，可以高效初值填充。  

## 3 迭代器以及`traits`编程技法

`iterator`定义：依序巡访某个聚合物（容器）所含的元素，但不暴露聚合物内部表达方式的方法。

### 3.1 迭代器设计思想

STL中心思想：将容器和算法分开。
容器和算法的泛化，用class template和function template就可以实现，如何设计粘合剂。

以`find()`为例展示效果。

```cpp
template <class Iterator, class T>
```

迭代器依附于容器之下，是否存在独立泛用的迭代器？

### 3.2 迭代器是一种``smart pointer``

**迭代器是一种行为类似于指针的对象**。指针最常用的是内容提领（dereference）和成员访问（member access）。

#突然想起来之前看到的``sizeof(iterator)=4``。  
#有点理解这个问题了[C 语言中，「.」与「->」有什么区别？](https://www.zhihu.com/question/49164544)

### 3.3 迭代器相应型别

获取迭代器相应型别（associated type）的解决方法``function template``的参数推导（argument deduction）机制。编译器自动会对template进行参数推导。相应型别有五种，不全依赖推导机制来获取。
```cpp
template <class I, class T>
void func_impl(I iter, T t){
    T tmp;
    //...
};
template <class I>
inline void func(I iter){
    func_impl(iter, *iter);
}

int main(){
    int i;
    func(&i);
}
```
## 3.7 `__type_traits` 

`iterator_traits`负责萃取迭代器的特性，`__type_traits`负责萃取型别的特性。

# 4

**vector满载后的空间配置策略。**

## `list`

list的节点、迭代器、数据结构设计  
在尾部添加空白节点就符合前闭后开的要求  

## 4.6 `queue`

STL中queue是一个container adapter，而不算container。默认的情况下以deque作为底层结构，当然也可以用list作为底层结构，list也是双向开口的数据结构。
操作包含：`empty()`、`size()`、`front()`、`back()`、`push()`、`pop()`。
```cpp
tamplate <class T, class Sequence=deque<T> >
queue<int,list<int>>  q;//使用list作为低层结构；
```

# 5

## 5.3 `set`

`set`和`list`有类似的性质，插入或删除操作后依然有效。**但不是说没有迭代器失效的问题了。`erase(it++)`防止对`void*`进行操作。**

# 6 

算法：分为质变算法和非质变算法。

## `sort()`

关系型容器自带排序功能；  
序列式容器stack，queue，priority-queue都有特定入口，不允许排序；  
vector，deque是随机访问的，适用泛型sort()；  
list或slist不适合sort() 容器内部实现了成员函数sort()；  

## `reverse()`  

由使用了iter_swap()；  
迭代器的双向或随机定位能力影响了算法的效率。