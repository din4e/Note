[TOC]

# Jupyter

 ```bash
# 启动jupyter
jupyter notebook
# .ipynb转.py
jupyter nbconvert --to script demo.ipynb 
# 关闭jupyter
crtl+c ctrl+c
```

# Numpy

## 安装使用

``` python
import numpy  as np
```

## 基本类型

## 基本操作

### 设置

#### 完整输出数组

```python
np.set_printoptions(threshold=np.inf) # 完整输出numpy数组
```

# Pandas

## Pandas安装使用

``` python
import pandas as pd
import numpy  as np
```

## Pandas基本类型

```python
df[["weight"]] # DataFrame
df["weight"] # Series
```

输出结果对比：

```bash
       weight
0    0.133333
1    0.316667
2    0.216667
3    0.366667
4    0.433333
..        ...
495  0.150000
496  0.733333
497  0.300000
498  0.816667
499  0.083333

[500 rows x 1 columns]

0      0.133333
1      0.316667
2      0.216667
3      0.366667
4      0.433333
         ...   
495    0.150000
496    0.733333
497    0.300000
498    0.816667
499    0.083333
Name: weight, Length: 500, dtype: float64
```

### DataFrame 

DataFrame本质是一种带行标签和列标签、支持相同类型数据和缺失值的多维数组。Pandas建立在Numpy之上。重点是**数据添加标签**，**处理缺失值**。

### Series

Series对象将一组数据和一组索引绑定在一起。可以使用```values```和```index```属性获取数据。```values```返回结果和Numpy一致。

## Pandas基本操作

### 数据保存读取

```python
df=pd.read_csv(inputfilename)
df.to_csv(inputfilename)
```

#### 获取Pandas的列属性

```python
[column for column in df]
df.columns.values # array
list(df)
df.columns # Index 可以通过 tolist(), 或者 list（array） 转换为list
```

### 修改数据

#### 对某一列赋值

``` python
df=pd.DataFrame(ts.get_zz500s()) 
df[index] = 0.0 # index是未初始化的列 
```

#### 对某一列做归一化操作

```python
max_min_scaler = lambda x : (x-np.min(x))/(np.max(x)-np.min(x))
df[index] = df[[index]].apply(max_min_scaler)
```

### 包函数

#### df.describe()

#### df.nunique()

#### [.drop()](https://blog.csdn.net/nuaadot/article/details/78304642)

# 数据分析

## .unique()

```python
unlist=np.unique(df["colume"])
df.nunique()
```

# 参考资料

[蓝鲸网站使用python进行数据清洗](http://bluewhale.cc/2016-08-21/python-data-cleaning.html)  
[Pandas数据清洗](https://www.cnblogs.com/BoyceYang/p/8182053.html)  
[BiliBili数值处理](https://www.bilibili.com/video/av52783056/?p=3)  
[pandas-profiling](https://www.zhihu.com/question/24590883/answer/782584888)  
[BiliBili PCA的使用](https://www.bilibili.com/video/av28790123?from=search&seid=15676878223827506884)
