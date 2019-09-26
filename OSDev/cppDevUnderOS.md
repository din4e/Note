# 在Mac OSX下使用C++

## [GNU C编译器的gnu11和c11](https://blog.csdn.net/weixin_34205076/article/details/85966460)

国际标准组织发布c11后，gnu为自己的编译器发布两种标准gnu11和c11
**gnu11：**带gnu c扩展的c11标准，如果你的代码包含了typeof，__attribute__等等gnu的扩展，就必须用这个。
**c11：**这个就是纯c11的标准，不带gnu扩展。
可以在Makefile中声明：
`CFLAGS=-std=gnu11 -g -Wall`或者，纯标准的c11，玩linux的要慎用，因为linux代码到处都是gnu的痕迹哦，哈哈.`CFLAGS=-std=c11 -g -Wall`

## [编译器GCC与Clang的异同](https://blog.csdn.net/fengbingchun/article/details/79252110)

Clang：是一个C、C++、Objective-C和Objective-C++编程语言的编译器前端。**它采用了底层虚拟机(LLVM)作为其后端。**

## [Use of undeclared identifier 'DBL_MAX'](https://stackoverflow.com/questions/28427495/error-c2065-dbl-max-undeclared-identifier-in-vs2008-but-not-in-vs2010)

```cpp
#include <math.h>
#include <float.h>
```

stackoverflow太好用了，google太好用了。
