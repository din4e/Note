## 位运算 bit-manipulation

+ 位运算主要适用于整型（浮点型八能直接操作，可以分段取出）；
+ 运算符优先级：按位取反 `~` > 左右移 `<<` 、`>>` > 加减 `+` 、`-` > `==` 等于运算符 > 按位与 `&` > 按位异或 `^` > 按位或 `|` ；
+ `&` 、 `|` 是不可逆的单向运算，会造成信息丢失。`<<` 、 `>>` 在数据溢出时也会信息丢失。`^` 不会造成信息丢失。

### 1. 位运算的基本操作

`x&1` 判断奇偶；  
`x&(1<<n)` 判断第 n 位是否为1；    

`x<<n` 乘 2^n ；  
`x>>n` 除以 2^n ；  
`x&((1<<n)-1)` 对 2^n 求模，是对 `x%(1<<n)`的优化；  

`x&-x`、 `x&(~x+1)`、`x^(x&(x-1))` 最后一位 1 所代表的数字，正负数都可以用 ；  
`~x+1` 带符号数交换符号，正变负，负变正，优先级: `~` > `+` ；  

`x|=1<<n` 第 n 位置 1 ；  
`x&=~(1<<n)` 第 n 位置 0 ；   
`x^=(1<<n)` 第 n 位取反；   
`x&(x-1)` 去掉右向左数的第一个 1 ；  
`(!(x&(x-1)) )&&x` 判断 x 是否是 2 的正整数冪 ；  
`x&(x-1)==0` 判断 x 是否是 2 的 n 次幂，如果的结果为 0 则说明是 ；  

#### 1.1 位运算的基本应用  
两数交换
```cpp
void swap(int &a, int &b) {   
  a ^= b, b ^= a, a ^= b;  
}      
a^=b^=a^=b; // 简写后...就nm离谱
```
求绝对值
```cpp
int abs(int x) {   
  int i = x >> 31;    
  return ((x^i) - i);    
}   
```
快速幂
```cpp
int pow(int a,int b){   
    int ans=1;   
    int base=a;   
    while(b){   
        if(b&1) ans*=base;   
        base*=base;   
        b>>=1;   
    }   
    return ans;   
}   
```
快速幂取模
```cpp
int pow_mod(int a,int b,int c){   
    int ans=1;   
    int base=a%c;   
    while(b){   
        if(b&1) ans=(ans*base)%c;   
        base=(base*base)%c;   
        b>>=1;   
    }   
    return ans;   
}   
```   
### 2. 一些位运算的经典问题

2.1 海量数字中，一个数字出现了奇数次，剩余的都出现了偶数次，**异或所有值**后的结果是那个数字。

2.2 统计 x 中 1 的个数
```cpp
int f(int x){   
    int count = 0;   
    while(x){    
        x = x & (x - 1);     
        count++;    
    }   
    return count;  
} // 古老的的微软面试题？！！
```  

二分法粗暴的统计32位无符号整型中 x 中 1 的个数（借鉴一下就好...做题根本背不出来）：
```cpp
int count_one(unsigned long n){     
    //0xAAAAAAAA，0x55555555分别是以“1位”为单位提取奇偶位   
    n = ((n & 0xAAAAAAAA) >> 1) + (n & 0x55555555);   
    //0xCCCCCCCC，0x33333333分别是以“2位”为单位提取奇偶位   
    n = ((n & 0xCCCCCCCC) >> 2) + (n & 0x33333333);   
    //0xF0F0F0F0，0x0F0F0F0F分别是以“4位”为单位提取奇偶位   
    n = ((n & 0xF0F0F0F0) >> 4) + (n & 0x0F0F0F0F);   
    //0xFF00FF00，0x00FF00FF分别是以“8位”为单位提取奇偶位   
    n = ((n & 0xFF00FF00) >> 8) + (n & 0x00FF00FF);   
    //0xFFFF0000，0x0000FFFF分别是以“16位”为单位提取奇偶位   
    n = ((n & 0xFFFF0000) >> 16) + (n & 0x0000FFFF);   
    return n;  
}
```

2.3 枚举出一个集合的子集。设原集合为 index 为 j ，则下面的代码就可以列出它的所有子集。实际解题过程中，也可以用dfs、回溯来代替。
```cpp
for(int j=k;j;j=(j-1)*k) /*...*/ ;    
// k = 101 ; j = 101 => 100 => 001 ;
```

2.4 [n皇后问题的位运算求解（n<32）](https://blog.csdn.net/kai_wei_zhang/article/details/8033194)。
```cpp
void test(int row, int ld, int rd)  {       
    int pos, p;        
    if (row!=upperlim) {            
        pos=upperlim&(~(row|ld|rd));     
        while(pos) {       
            p=pos&(~pos+1); // p=pos&(-pos);         
            pos=pos-p;   
            test(row|p, (ld|p)<<1, (rd|p)>>1);    
        }  
    }  
    else  ++ans;  
}  
// 初始化: upperlim=(1 << n)-1; ans = 0; 调用函数：test(0, 0, 0);   
```

2.5 位掩码：比如用于权限管理，朋友 `chmod 777` 熟悉嘛。

### 3. 位图法 bitmap

位图是一种数据结构，可以用每一位来存放状态。 STL 实现的容器 `bitset` ，可以像使用数组一样使用位。当然可以自己写数据结构比较麻烦。

3.1 位图的缺点：
+ 可读性差；
+ 位图存储的元素个数虽然比一般做法多，但是存储的元素大小受限于存储空间的大小；  

3.2 位图法的应用  

3.2.1 海量数据判断重复：给 40 亿个不重复的 unsigned int 的整数，没有排过序，然后再给一个数，如果快速判断这个数是否在那 40 亿个数当中（腾讯面试题)；

3.2.3 位图法排序：不重复的数据。

## 4. 小结

力扣上的位图法题目一般都会卡时间，特征也比较明显，比如特征数据长度短`data.legth<=16`，超过整型范围就不允许。数据大量，重复性高。


位运算虽然效率高，但是可读性不强。实际写代码的时候，编译器可能自动将一些运算优化成位运算了，做实验有可能看不出效果。

最后，别问，看到神奇代码就是一顿乱背。
```cpp
for (int j=k;j;j=(j-1)*k) /*...*/ ;
```

## 参考资料

[leetcode知乎](https://www.zhihu.com/question/38206659/answer/736472332)     
[斯坦福的整理](http://graphics.stanford.edu/~seander/bithacks.html#OperationCounting)  
[cnblog的一篇整理](https://www.cnblogs.com/thrillerz/p/4530108.html)  