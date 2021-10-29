---
title: Python机器学习入门
date: 2021.10.21
author: Aik
img: /source/images/xxx.jpg
top: true
hide: false
cover: true
coverImg: /images/1.jpg
password: 
toc: true
mathjax: true
summary: 记录了自己入门机器学习的过程
categories: 机器学习
tags:
  - Python
  - 机器学习
---

# Python机器学习入门

机器学习就是通过算法让计算机能够从数据中提取出有用的信息，并且能够按我们的需要对它进行决策判断，最后得到我们希望得到的结果，也就是从数据-模型-预测的一个过程。

## 机器学习概述

### 算法分类

- 监督学习

  - 定义：输入数据是由输入特征值和目标值所组成。函数的输出可以是一个连续的值（称为回归），或输出是有限个离散值（称作分类）。

  - 目标值：类别 —— 分类问题
    - k-近邻算法、贝叶斯分类、决策树与随机森林、逻辑回归
  - 目标值：连续型的数据 —— 回归问题
    - 线性回归、岭回归

- 无监督学习

  - 定义：输入数据是由输入特征值所组成。
  - 目标值：无 —— 无监督学习
    - 聚类 k-means

例：

1. 预测明天的气温是多少度？  回归
2. 预测明天是阴、晴还是雨？  分类
3. 人脸年龄预测？  回归/分类
4. 人脸识别？  分类

### 开发流程

1. 获取原始数据 - 数据集
2. 数据预处理
3. 特征工程 - 处理成能被算法使用的数据
4. 选择合适的机器学习算法训练，得到模型
5. 模型评估，查看训练的效果
6. 模型应用

### 学习库和使用框架

- sklearn

- PyTorch

- TensorFlow

## 特征工程

### 数据集

数据集分为训练集和测试集，通常在进行模型训练时会将数据集的训练集和测试集进行7：3分或者8：2分。

初学时可以使用sklearn里自带的数据集，它的数据量较小，方便学习。也可以通过去Kaggle等平台上进行寻找别人提供的数据集，最终大部分情况还是需要自己进行数据集的构建，利用爬虫等进行数据采集。

- sklearn数据集的简单使用：

  安装库：`` pip install Sklearn``

  然后在.py文件开头导入包：``from sklearn.datasets import load_iris``

  ```
  from sklearn.datasets import load_iris
  from sklearn.model_selection import train_test_split
  
  # 鸢尾花数据集查看
  def getDataSource():
      iris = load_iris()
      # 返回的是一个Bunch类型(继承自字典的类型)，所以可以用调用字典的方式去获取到相应的键值对数据
      print("鸢尾花数据集：\n", iris)
      print("查看数据集描述：\n", iris["DESCR"])
      print("查看特征值的名字：\n", iris.feature_names)
      print("查看特征值：\n", iris.data, iris.data.shape)
  
      # 数据集划分
      x_train, x_test, y_train, y_test = train_test_split(iris.data, iris.target, test_size=0.2)
      print("训练集的特征值:\n", x_train, x_train.shape)
      return None
  ```

### 特征工程介绍

**数据和特征决定了机器学习的上限，而模型和算法只是逼近这个上限而已。**

特征工程是使用专业背景知识和技巧处理数据，使得特征能在机器学习算法上发挥更好的作用的过程。（会直接影响机器学习的效果）

- pandas：用于数据清洗、数据处理
- sklearn：用于特征工程处理

特征工程包含下面三个内容：

1. 特征提取
2. 特征预处理
3. 特征降维

### 特征提取

首先，机器学习算法就是一些统计方法，即一个一个的数学公式。但是这些数学公式不能直接处理例如文本的字符串数据、类型数据、图像等，所以需要把这些数据转换成数值类型。怎么样去完成这一过程就是特征提取所该做的事情。

特征提取的API：``sklearn.feature_extraction``

#### 字典特征提取

作用：对字典数据进行特征值化

- sklearn.feature_extraction.DictVectorizer(sparse=True,...)
  - DictVectorizer.fit_transform(X)	X:字典或者包含字典的迭代器返回值	返回值：返回sparse矩阵
  - DictVectorizer.inverse_transform(X)    X:array数组或者sparse矩阵    返回值：转换之前数据格式
  - DictVectorizer.get_feature_names()    返回类别名称

下面为字典特征提取的一个例子

```
from sklearn.feature_extraction import DictVectorizer

def dict_demo():
    # 字典特征提取       ->one-hot编码
    data = [{'city': '北京', 'temperature': 100}, {'city': '上海', 'temperature': 60}, {'city': '深圳', 'temperature': 30}]
    # 实例化一个转换器类
    transfer = DictVectorizer(sparse=False)  # 默认返回的是sparse稀疏矩阵（用下标来表示位置，不表示0的位置，可以节省内存，提高加载效率），False则返回二维数组
    # 调用fit_transform()
    data_new = transfer.fit_transform(data)
    print("data_new：\n", data_new)
    print("特征名字：\n", transfer.get_feature_names())

    return None
```

one-hot编码就是对类别进行二进制化的操作，在数据集中有多少个类别特征就分成多少列，每份数据占一行，例如对下面数据进行one-hot编码：

| city | temperature |
| ---- | ----------- |
| 北京 | 100         |
| 上海 | 60          |
| 深圳 | 30          |

最后编码后的结果就是一个二维数组：

| city=上海 | city=北京 | city=深圳 | temperature |
| --------- | --------- | --------- | ----------- |
| 0         | 1         | 0         | 100         |
| 1         | 0         | 0         | 60          |
| 0         | 0         | 1         | 30          |

#### 文本特征提取

作用：对文本数据进行特征值化

- sklearn.feature_extraction.text.CountVectorizer(stop_words=[])	返回词频矩阵
- CountVectorizer.fit_transform(X)    X:文本或者包含文本字符串的可迭代对象    返回值：返回sparse矩阵
- CountVectorizer.inverse_transform(X)    X:array数组或者sparse矩阵    返回值：转换之前数据格式
- CountVectorizer.get_feature_names()    返回值：单词列表
- sklearn.feature_extraction.text.TfidfVectorizer

一般是把一个个单词作为特征

