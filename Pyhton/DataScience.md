# DataScicence

## Jupyter

```bash
jupyter notebook # 启动jupyter
jupyter nbconvert --to script demo.ipynb # .ipynb转.py
crtl+c ctrl+c # 关闭jupyter
```

## Numpy

### 安装使用

``` python
import numpy  as np
```

### 基本类型

### 基本操作

#### [```numpy.argmax()```用法](https://www.cnblogs.com/touch-skyer/p/8509217.html)

argmax返回的是最大数的索引，argmax有一个参数axis，默认是0，表示第几维的最大值。

```python
import numpy as np
a = np.array([[1, 5, 5, 2],
              [9, 6, 2, 8],
              [3, 7, 9, 1]])
print(np.argmax(a, axis=0)) // [1,2,2,1]

a = np.array([[1, 5, 5, 2],
              [9, 6, 2, 8],
              [3, 7, 9, 1]])
print(np.argmax(a, axis=1)) // [1,0,2]
```

#### 设置完整输出数组

```python
np.set_printoptions(threshold=np.inf) # 完整输出numpy数组
```

## Pandas

### Pandas安装使用

``` python
import pandas as pd
import numpy  as np
```

### Pandas基本类型

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

### Pandas基本操作

#### 数据读取保存

```py
df=pd.read_csv(inputfilename,sep='\t',encloding='utf-8')
df.to_csv(inputfilename)
```

#### Pandas设置现实行列

```py
pd.options.display.max_columns = None
pd.options.display.max_rows = None
```

#### 获取Pandas的列属性

```py
[column for column in df]
df.columns.values # array
list(df)
df.columns # Index 可以通过 tolist(), 或者 list（array） 转换为list
```

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

#### [Pandas循环更高效](https://towardsdatascience.com/how-to-make-your-pandas-loop-71-803-times-faster-805030df4f06)

1. 使用```.apply()```方法；
2. 使用numpy的```.values```矢量化，具体原因来源于[访问局部性](https://en.wikipedia.org/wiki/Locality_of_reference)。

---

#### df.describe()

#### df.nunique()

#### [.drop()](https://blog.csdn.net/nuaadot/article/details/78304642)

## 数据分析

## .unique()

```python
unlist=np.unique(df["colume"])
df.nunique()
```

## 可视化

### [Bar Chart Race in Python with Matplotlib](https://towardsdatascience.com/bar-chart-race-in-python-with-matplotlib-8e687a5c8a41)

## LightingBGM

### LightingBGM评价函数设置为f1_score

二分类问题的F1数值计算

```python
params{
       metric:"None",
},

def f1_scorer(pred, train_data):
    return "f1_score", f1_score(train_data.get_label(), np.round(pred), average="weighted"), True
# pred是一个维度数组，train_data是一个LightingBGM.Dataset。

bst = lgb.train(params, dtrain, num_boost_round = 30000, valid_sets = dvalid,verbose_eval = 400,early_stopping_rounds = 200, feval = f1_scorer )
```

参考:  
[feval in lgb.cv giving unexpected results](https://github.com/microsoft/LightGBM/issues/1483)  
[f1_score metric in lightgbm](https://stackoverflow.com/questions/50931168/f1-score-metric-in-lightgbm)  
[sklearn.metrics.f1_score](https://scikit-learn.org/stable/modules/generated/sklearn.metrics.f1_score.html)

## 参考资料

[蓝鲸网站使用python进行数据清洗](http://bluewhale.cc/2016-08-21/python-data-cleaning.html)  
[Pandas数据清洗](https://www.cnblogs.com/BoyceYang/p/8182053.html)  
[BiliBili数值处理](https://www.bilibili.com/video/av52783056/?p=3)  
[pandas-profiling](https://www.zhihu.com/question/24590883/answer/782584888)  
[BiliBili PCA的使用](https://www.bilibili.com/video/av28790123?from=search&seid=15676878223827506884)
