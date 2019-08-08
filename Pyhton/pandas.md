[TOC]

# Pandas

## 安装使用

``` python
import pandas as pd
import numpy  as np
```

## 基本类型

### DataFrame 

DataFrame本质是一种带行标签和列标签、支持相同类型数据和缺失值的多维数组。Pandas建立在Numpy之上。重点是**数据添加标签**，**处理缺失值**。

### Series

Series对象将一组数据和一组索引绑定在一起。可以使用```values```和```index```属性获取数据。```values```返回结果和Numpy一致。

## 基本操作

### 数据保存读取

### 修改数据

#### 对某一列赋值

``` python
df=pd.DataFrame(ts.get_zz500s()) 
df["cloume"] = 0.0 # 初始化 
```
