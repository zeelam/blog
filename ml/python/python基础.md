# Python基础

[TOC]

##  Python简介

### 一些库
#### 深度学习/人工智能

- tensorflow
- pytorch + caffe2
- mxnet
- caffe
- eras TFlearn tensorlayer

#### 机器学习

scikit-learn bumpy/scipy pandas xgboost/LightGBM

### 两个重要函数

- help - 说明文档

  ```
  import pandas as pd
  help(pd)
  ```

- dir - 列出类、方法等

  ```python
  dir(pd)
  ```

## 基本数据类型、变量
- 加减乘除

> +-*/ //
```python
1+1 # 2
1-1 # 0
4*5 # 20
3/2 # python3为1.5 python2为1
3//2 # 1
4**0.5 # 2.0 (次方)
3%2 # 1
```

- int整型
- float浮点类型
- str字符串
- bool布尔型

```python
x = 1 # 整型
type(x) # 返回类型，或者是哪个类的实例
y = -2.11 # float
a = 'xxxxx' # str
b = True # bool
```

**x、y、a、b为变量**

## 表达式

```python
x = 12
x = x + 5
print(x)
```

## 字符串

```python
my_string = 'Zeelam' # 单引号\双引号\三引号初始化都OK
type(my_string) # str
```

```python
help(str)
dir(str)
```

字符串切片

```python
len(my_string) # 长度 6
```

Z  e  e  l  a  m
0  1  2  3 4  5
-5 -4 -3 -2  -1

```python
my_string[4] # a
my_string[-5] # Z
my_string[1:4] # eel 左闭右开
my_string[-5:-2] # Zeel
my_string[2:] # elam 从2到最后
my_string[:3] #Zee
```

字符串函数

```python
my_string.lower() # zeelam
my_string.upper() # ZEELAM
my_string.capitalize() #Zeelam 首字母大写
my_string.startswith('Zee') # True
my_string.endswith('Zee') # False
my_string.strip() # 去掉前后空格
my_string2 = "我 的 名字 叫 张梓霖"
my_string2.split(" ") # 字符串切分 ['我', '的', '名字', '叫', '张梓霖']
my_string2.find("的") # 2 中间有个空格 所以下标是2
my_string2.find("呵呵") # -1 找不到返回负一
```

## 列表(list)

```python
[1,2,3,4,5,6] # list
names = ['zeelam', 'langge', 'hongyang']
len(names) # 3
mix_list = ['zeelam', 2, 1.22, True, ['langge', 'hongyang']] # 可以放入各种类型
len(mix_list) # 5
```

列表切片

```python
names[0] # 'zeelam'
mix_list[4] # ['langge', 'yongyang']
mix_list[4][0] # 'langge'
```

一些方法

```python
'##'.join(names) # 'zeelam##langge##hongyang'
names.append('老司机') # ['zeelam', 'langge', 'hongyang', '老司机']
names2 = ['临时工1', '临时工2']

names + names2 # ['zeelam', 'langge', 'hongyang', '老司机', '临时工1', '临时工2']

names.append(names2) #['zeelam', 'langge', 'hongyang', '老司机', ['临时工1', '临时工2']]

names = ['zeelam', 'langge', 'hongyang', '老司机']
names.extend(names2) # ['zeelam', 'langge', 'hongyang', '老司机', '临时工1', '临时工2']

names.index('zeelam') # 0
names.reverse() # ['临时工2', '临时工1', '老司机', 'hongyang', 'langge', 'zeelam']

# 注意python内置的reversed()函数
# 区别reverse()为成员函数，可以直接改变对象内部的顺序，reversed()只是生成一个倒序的list
```

## 流程语句

### 判断语句

```python
age = 25
if age > 50:
    print('老人')
elif age > 30:
    print('中年人')
else:
    print('年轻人')
# 输出'年轻人'
```

### 循环语句

```python
# while
# for
names = ['zeelam', 'langge', 'hongyang']
for name in names:
    print(name)

# 打印出下标
for i, name in enumerate(names):
    print(i, name)

i = 0
while i < 10:
    print(i)
    i += 1

# break 终止循环
# continue 跳过本次循环
```

列表推导式

```python
names = ['zeelam', 'langge', 'hongyang']
for name in names:
	print('my name is ' + name)

# 使用列表推导式
["my name is " + name for name in names]
'''
结果如下
['my name is zeelam',
'my name is langge',
'my name is hongyang']
'''
num_list = list(range(10))
# [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
[num**3 for num in num_list if (num%2 == 1 and num < 5)]
# [1, 27]
```

## 集合(set)

```python
# {} 为 set
# 不可以重复
names = ['zeelam', 'langge', 'hongyang']
names.append('zeelam')
# names 为 ['zeelam', 'langge', 'hongyang', 'zeelam']
set(names)
# {'zeelam', 'langge', 'hongyang'}
```

## 元组(tuple)

```python
# 元组和list很像，只是不能修改元素内容
num_list = [0, 1, 2, 3]
num_list[1] = 10
# num_list 此时为 [0, 10, 2, 3]
tup1 = (0, 1, 2, 3)
tup1[1] = 10 # 这样做是会报错的
```

## 字典(dictionary)

```python
# Java中的Map类型
legs = {'human':2, 'peppa':4}
type(legs) # dict
legs['hunman'] # 2
legs['bird'] # 报错 KeyError 因为字典里没有这个key
for item_name, item_leg in legs.items():
    print(item_name, leg_num)
```

字典推导式

```python
num_list = [0, 1, 2, 3, 4]
{num:num**3 for num in num_list}
# {0: 0, 1: 1, 2: 8, 3: 27, 4: 64}
```

