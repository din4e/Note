[TOC]

# Jupyter

#### .ipynb转.py

 ```bash
 jupyter nbconvert --to script demo.ipynb 
 ```

#### 启动 

```bash
jupyter notebook
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

### 数据保存读取

### 修改数据

#### 对某一列赋值

# Pandas

## 安装使用

``` python
import pandas as pd
import numpy  as np
```

## 基本类型

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

## 基本操作

### 数据保存读取

```python
df=pd.read_csv(inputfilename)
df.to_csv(inputfilename)
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
