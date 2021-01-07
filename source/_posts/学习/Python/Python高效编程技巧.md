---
title: Python高效编程技巧
date: 2020-10-24 13:30:04
author: 乔亚峰
top: true
toc: true
mathjax: false
summary: Python 中有很多内置函数帮你提高工作效率！
categories: Python
tags:
  - Python
  - 博客
---

工作中经常要处理各种各样的数据，遇到项目赶进度的时候自己写函数容易浪费时间。
Python 中有很多内置函数帮你提高工作效率！
一：在列表，字典中根据条件筛选数据

1.假设有一个数字列表 data, 过滤列表中的负数
列表推导式


```

result = [i for i in data if i >= 0]

filter
result = filter(lambda x: x>= 0, data)
```


2.学生的数学分数以字典形式存储，筛选其中分数大于 80 分的同学




```
d = {x:randint(50, 100) for x in range(1, 21)}
{k: v for k, v in d.items() if v > 80}
```

二：对字典的键值对进行翻转

使用 zip() 函数

    zip() 函数用于将可迭代的对象作为参数，将对象中对应的元素打包成一个个元组，然后返回由这些元组组成的列表。

```
>>> s1 = {x: randint(1, 4) for x in sample('abfcdrg', randint(1,5))}
>>> s1
{'b': 1, 'f': 4, 'g': 3, 'r': 1}
>>> d = {k:v for k, v in zip(s1.values(), s1.keys())}
>>> d
{1: 'r', 4: 'f', 3: 'g'}
```


二. 统计序列中元素出现的频度
1.某随机序列中，找到出现次数最高的3个元素，它们出现的次数是多少？

随机序列如下：

```
data = [randint(0,20) for _ in range(20)]
```



方法1: 可以使用字典来统计，以列表中的数据为键，以出现的次数为值


```
from random import randint

def demo():
    data = [randint(0, 20) for _ in range(30)]
    # 列表中出现数字出现的次数
    d = dict.fromkeys(data, 0)
    for v in li:
        d[v] += 1
    return d
```


方法2：直接使用 collections 模块下面的 Counter 对象


```
>>> data = [randint(0, 20) for _ in range(30)]
>>> data
[7, 8, 5, 16, 10, 16, 8, 17, 11, 18, 11, 17, 15, 7, 2, 19, 5, 16, 17, 17, 12, 19, 9, 10, 0, 20, 11, 2, 11, 10]
>>> c2 = Counter(data)
>>> c2
Counter({17: 4, 11: 4, 16: 3, 10: 3, 7: 2, 8: 2, 5: 2, 2: 2, 19: 2, 18: 1, 15: 1, 12: 1, 9: 1, 0: 1, 20: 1})
>>> c2[14]
4
>>> c2.most_common(3)  # 统计频度出现最高的3个数
[(17, 4), (11, 4), (16, 3)]
```


2. 对某英文文章单词进行统计，找到出现次数最高的单词以及出现的次数

通过上面的练习，我们知道可以用 Counter 来解决


```
import re
from collections import Counter

# 统计某个文章中英文单词的词频

with open('test.txt', 'r', encoding='utf-8')as f:
    d = f.read()

total = re.split('\W+', d)  # 所有的单词列表
result = Counter(total)
print(result.most_common(10))
```


三.根据字典中值的大小，对字典中的项进行排序

比如班级中学生的数学成绩以字典的形式存储：

```
{"Lnad": 88, "Jim", 71...}
```



请按数学成绩从高到底进行排序！

方法1: 利用 zip 将字典转化为元祖，再用 sorted 进行排序


```
>>> data = {x: randint(60, 100) for x in "xyzfafs"}
>>> data
{'x': 73, 'y': 69, 'z': 76, 'f': 61, 'a': 64, 's': 100}
>>> sorted(data)
['a', 'f', 's', 'x', 'y', 'z']
>>> data = sorted(zip(data.values(), data.keys()))
>>> data
[(61, 'f'), (64, 'a'), (69, 'y'), (73, 'x'), (76, 'z'), (100, 's')]
```



方法2: 利用 sorted 函数的 key 参数


```
>>> data.items()
>>> dict_items([('x', 64), ('y', 74), ('z', 66), ('f', 62), ('a', 80), ('s', 72)])
>>> sorted(data.items(), key=lambda x: x[1])
[('f', 62), ('x', 64), ('z', 66), ('s', 72), ('y', 74), ('a', 80)]
```


四. 在多个字典中找到公共键

实际场景：在足球联赛中，统计每轮比赛都有进球的球员

    第一轮： {"C罗": 1, "苏亚雷斯":2, "托雷斯": 1..}
    第二轮： {"内马尔": 1, "梅西":2, "姆巴佩": 3..}
    第三轮： {"姆巴佩": 2, "C罗":2, "内马尔": 1..}

模拟随机的进球球员和进球数


```

>>> s1 = {x: randint(1, 4) for x in sample('abfcdrg', randint(1,5))}
>>> s1
{'d': 3, 'g': 2}
>>> s2 = {x: randint(1, 4) for x in sample('abfcdrg', randint(1,5))}
>>> s2
{'b': 4, 'g': 1, 'f': 1, 'r': 4, 'd': 3}
>>> s3 = {x: randint(1, 4) for x in sample('abfcdrg', randint(1,5))}
>>> s3
{'b': 4, 'r': 4, 'a': 2, 'g': 3, 'c': 4}
```


首先获取字典的 keys，然后取每轮比赛 key 的交集
由于比赛轮次数是不定的，所以使用 map 来批量操作


```
map(dict.keys, [s1, s2, s3])
```

然后一直累积取其交集， 使用 reduce 函数

```

reduce(lambda x,y: x & y, map(dict.keys, [s1, s2, s3]))
```

一行代码搞定！
