---
title: Python语法糖
date: 2025-12-16 15:38:31
tags: Python
categories: Pyhon
---

![img](/images/PythonSyntaticSugar.png)

# 圣诞到了！想要糖吗？来点Python语法糖！

`语法糖是指一些小操作，使编程变得更简单和高效。`

<!-- more -->

## 1. 切片

> 所有py初学者都会惊叹的**py切片**！

```python
>>> a = [0, 1, 2, 3, 4, 5, 6, 7, 8 , 9]
>>> a[::-1] # 逆序
[9, 8, 7, 6, 5, 4, 3, 2, 1, 0]

>>> b = "Beautiful is better than ugly."
>>> b[13:19] # 切片出13-19个字符
'better'
```


## 2. 推导式

> 非非非非非非非非非非非非常好用！

```python
>>> a = [0, 1, 2, 3, 4, 5, 6, 7, 8 , 9] # 传统的顺序序列赋值
>>> a
[0, 1, 2, 3, 4, 5, 6, 7, 8 , 9]

>>>  b = [i for i in range(10)] # 用列表推导式的顺序序列复制
>>>  b
[0, 1, 2, 3, 4, 5, 6, 7, 8 , 9]

>>> c = [i for i in range(10) if i % 2 == 1] # 用判断推导式的顺序序列复制
>>> c
[1, 3, 5, 7, 9]

>>> dic = {i : chr(i + 65) for i in range(10)} # 用字典推导式的顺序序列复制
>>> dic
{0: 'A', 1: 'B', 2: 'C', 3: 'D', 4: 'E', 5: 'F', 6: 'G', 7: 'H', 8: 'I', 9: 'J'}
```

## 3. 链式比较

> 不用写很多and，但其实有些时候写了更明白

```python
if 5 < x < 10: # 链式比较
    pass

if 1 < x < y < 10: # 多个参数比较
    pass
```


## 4. 上下文管理

> 离开with自动关闭文件

```python
with open("a.txt", "r") as f1, \
     open("b.txt", "w") as f2:
    data = f1.read()
    f2.write(data.upper())
```

## 5. 装饰器

> 装饰器是学习***Python绕不过去的坎***

```python
def decorator(func): # 装饰函数
    def wrapper():
        print("Before Function")
        func()
        print("After Function")
    return wrapper
    
@decorator
def hello():
    print("Hello!")

# 多个装饰器
@decorator1
@decorator2
def my_func():
    pass
# 等价于 my_func = decorator1(decorator2(my_func))
```
---
```terminal
Before Function
Hello!
After Function
```

## 6. 格式化

> f-string，只能说比printf好用太多了，也更优雅

```python
print(f"Result: {3 + 4 * 2}")

print(f"Name: {'alice'.upper()}")

pi = 3.14159
print(f"Pi: {pi:.2f}")

print(f"|{'text':^10}|") # :<左对齐 :>右对齐 :^居中
```

## 7.参数解包

> 将序列或字典拆解为单独的参数

```python
def sum_3(a, b, c):
    return a + b + c

args = [3, 5, 7]
print(sum_3(*args)) # = sum_3(4, 5, 7)

kwargs = {'a': 6, 'b': 8, 'c': 10}
print(sum_3(**kwargs)) # = sum_3(a=5, b=8, c=10)
```
---
```terminal
15
24
```

## 8. 动态参数

> 解包的应用，可以输入任意数量的参数

```python
def dynamic_args(*args, **kwargs): 
    print(args)
    print(kwargs)

dynamic_args(1,'2', True, name='alex', age=18)

l = [4,'8',False]
d = {'name': 'alice', 'age': '16'}
dynamic_args(*l, **d) # = dynamic_args(4,'8', False, name='alice', age=18)
```
---
```terminal
(1, '2', True)
{'name': 'alex', 'age': 18}
(1, '2', False)
{'name': 'alice', 'age': '16'}
```

## 9， 下划线语法

> 增强可读性，同时用于忽略变量

```python
num = 1_000_000  # 等价于 1000000
pi = 3.141_592_653_589_793

# 在循环中忽略变量
for _ in range(10):
    do_something()

# 解包时忽略不需要的值
data = (1, 2, 3, 4, 5)
first, _, third, _, fifth = data
```

## 10. Lambda

> 匿名函数，一种编写简洁的小型函数的方式

```python
x = lambda a: a + 10
print(x(5)) # 输出: 15

# 通常与内置函数如 map()、filter() 和 reduce() 一起使用，以便在集合上执行操作
list = [1, 2, 3, 4, 5]
squared = list(map(lambda x: x**2, list))
print(squared)  # 输出: [1, 4, 9, 16, 25]
```