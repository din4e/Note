# STL源码剖析（The annotated STL Sources）

C++作为一个面向对象程序设计语言，具有一个同样重要的思维模式：泛型。  
STL入门specialize之路:  
C++ template学习泛化以及深入理解STL第一道门槛：class template、function template、member template、specialization、partial specialization。STL大量使用了operator overloading。
运用STL，了解泛型技术和STL学理、最终扩充STL。

## 3 迭代器以及``traits``编程技法

``iterator``定义：依序巡访某个聚合物（容器）所含的元素，但不暴露聚合物内部表达方式的方法。

### 3.1 迭代器设计思想

STL中心思想：将容器和算法分开。
容器和算法的泛化，用class template和function template就可以实现，如何设计粘合剂。

以``find()``为例展示效果。
```cpp
template <class Iterator, class T>
```
迭代器依附于容器之下，是否存在独立泛用的迭代器？

### 3.2 迭代器是一种``smart pointer``



迭代器是一种行为类似于指针的对象。指针最常用的是内容提领（dereference）和成员访问（member access）。

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