---
title: Python快速预览
date: 2015-08-22 23:18:04
tags: [Python, note]
categories: Python
---
## 数据类型和变量
python语言是动态语言

## 字符串和编码
* UTF-8是可变长编码，用来转化Unicode编码，UTF-8一个Unicode字符根据不同的数字大小编码成1-6个字节。
* 在python中，Unicode表示的字符串用u'...'表示.
* 将Unicode字符转化为UTF-8字符用`encode('utf-8')`:

```python
u'ABC'.encode('utf-8')
```
* 将UTF-8字符转化为Unicode字符用`decode('utf')`:

```python
'abc'.decode('utf-8')
```
* 让python解释器按照UTF-8编码读取文件,需要在文件开头写上如下:
 `#-*- coding:utf-8 -*-`
* python的格式化方法与C 语言一致,用%实现,如:

```python
'hello, %s' %'world'
hello, world
'Hi, %s, you have $%d.' %('Michael', 10000)
Hi, Michael, you have $1000.
```
* 有几个%占位符,后面就跟多少个变量,顺序要对应好,如果只有一个%,可省略括号.
    - 常见的占位符有,%d整数, %f浮点数,%s字符串,%x十六进制数.
    - 格式化整数和浮点数还可以指定是否补0和整数与小数的位数.
    - 在格式化字符串中,需要转义%时,可用%%表示.
* 在python 3.x中,'xxxx'和u'xxxx' 统一成Unicode编码.

## 使用list和tuple
### list的使用
list里面的元素类型可以不同，也可以添加另外一个list   

```python
classmates = ['Box', 'Ads'] #创建list变量
classmates[0] #访问list中的元素
output:'Box'
#访问list最后一个元素
classmates[-1] 
output: 'Ads'
#添加元素到末尾
classmates.append('and')
#插入元素到指定位置
classmates.insert(1, 'sdd')
#删除末尾的元素
classmates.pop()
#删除指定位置的元素
classmates.pop(i)
#获得list的长度
len(classmates)
```
### tuple
tuple类似与list，只是tuple一旦初始化就不可以修改。tuple没有append和insert方法，  获得元素的方法与list一样。

```python
#创建一个tuple
classmates= (1,2,3)
#需要注意的是，当创建只有一个元素的tuple时，需要这样作来消除歧义：
classmates = (1,)
```
tuple可以包含list元素，tuple所包含的list元素中的元素内容可以更改。

### dict
dict类似与其他编程语言中的map

```python
#创建一个dict
d={'misc':93,'sds':82}
#还可以通过key来放入value：
d['misc'] = 23
#判断key是否存在
'sidh' in d
#当key不存在时，用get方法返回的是None，或者自己指定的返回值
d.get('sd', -1)
```

### set  
set类似与dict，但是只有key，没有对应的value，在set没有重复的key，创建set需要提供一个list

```python
s= set([1,23,4,5])
#在set重复的元素会自动被过滤，可以通过add(key)来添加元素，但是添加重复的元素没有效果。
#可以通过remove(key)来移除元素。
# set可以作数学意义上的交集、并集等操作
s1 = set([1,2,3])
s2 = set([3,4,5])
s1 & s2
s1 | s2
```      
set和dict不可放入可变对象，另外对于不可变对象，调用自身任何方法都不会改变自己,而是会创造一个新的对象并返回。  

## 条件判断和循环
### if表达式格式

```python
if <条件判断1>:
    <执行1>
elif <条件判断2>:
    <执行2>
else:
    <执行3>
```
### for循环格式  
```python            
for x in range(4):  #range()可以生成整数序列
       
```
### while 循环格式
```python
while <条件判断> :
```


## 函数
python的函数相当与一个对象的引用。因此，可以将函数赋予一个变量，相当于给函数起了一个       别名。  

```python
#函数定义
def function_name(parameter1, parameter2...) :
    <函数体>
```

没有写return的函数会返回None。定义一个空函数可以用pass语句

```python
def nothing():
    pass
```
pass语句什么都不作，可以用来当占位符使用。   函数不会检查参数类型，我们可以自己加上类型检查，使用`isinstance`函数实现

```python
def my_abs(x):
    if not isintance(x,(int,float)):
        raise TypeError('bad operand type')
    if x >=0:
        return x
    else :
        return -x
```
python函数可以返回多个返回值：

```python
x,y = move(x,y)
```
实际上，返回的只是一个tuple，只是写法上简化了。

### 默认参数

```python
def call_city(x,y, city='beijing',age=12):
    pass
```
默认参数原则：默认值写在最后面,也可以不按顺序提供部分默认参数，当需要指名参数名：

```python
call_city(x,y, age=12)
```
默认参数，最好指向不变对象。

### 可变参数
可变参数与定义list参数的区别就是在参数前面加个*，例如：

```python
def calc_sum(*numbers):
    sum =0
    for n in numbers:
           sum += n
    return sum
```
对于函数体内部来说，`numbers`接受的是一个`tuple`。   如果有一个list或者tuple变量，要调用可变参数的话，可以在变量前加*，把list和tuple转化为可变参数

### 关键字参数
关键字参数会在函数内部自动组装成一个dict。示例

```python

def person(name, age, **kw)
    print 'name:',name, 'age:',age,'other:', kw
person('Michael', 30,city='beijing')
```
在调用函数时，可以只传入必选参数，也可以传入任意数量的关键字参数。

## 高级特性
### 切片
切片操作可以轻松的切成一段数列,例如`L`是一个`list`

```python
# 取前3个元素
L[0:3]
#或
L[:3]
#取后10个元素
L[-10:]
#前十个数,每个2个取一个
L[:10:2]
#所有数,每隔5个取一个
L[::5]
#字符串同样支持切片操作.
```
### 迭代
dict可以同时迭代key和value:

```python
for k, v in d.iteritems()
```
判断一个对象是否可以迭代,可以用collections模块里的iterable类型:

```python
isinstance('abd', Iterable)
output: True
```
同时迭代索引和元素
```python
for i, value in enumerate(list):  
```           
### 列表生成式
列表生成式可以看成对for循环语句的简化.例如

```python
[x*x for x in range(1,11)]
output:   [1,4,9,16,25,36,4964,81,100]
#将生成的元素x*x放在前面,后面跟for循环.for循环后还可以加上if判断
[x*x for x in range(1,11) if x%2==0]
output:[4,16,36,64,100]
#还可以使用两层循环          
[m+n for m in 'ABC' for n in 'XYZ']
output:['AX','AY','AZ','BX','BY','BZ','CX','CY','CZ']
```
### 生成器
生成器只存储算法,需要时才会将后续的元素计算出来,从而节省大量的空间.将上述列表生成式的[]改成()就创建了一个`generator`.

```python
g = (x*x for x in range(1,11))
```
创建一个`generator`后,可以通过`next()`来打印里面的元素,或者使用`for`循环迭代.还可以使用`yield`关键字,将函数定义成`generator`,例如:    

```python
>>> def odd():
...    print 'step1'
...    yield 1
...    print 'step2'
...    yield 2
...    print 'step3'
...    yield 3
...
>>> o = odd()
>>> o.next()
step1
1
>>> o.next()
step2
2
>>> o.next()
step3
3
```
每当调用`next()`的时候,遇到`yield`语句返回,再次执行时,会从上次返回的`yield`语句处继续执行.

## 函数式编程
所谓高阶函数可以理解为,可以接受另外一个函数作为参数的函数,还可将函数作为返回值.
### 匿名函数

```python
lambda x: x*x
```
lambda表示匿名函数,冒号前面的x表示参数,匿名函数只能有一个表达式.返回值就是该表达式的结果.
### 装饰器
函数也是个对象,赋给变量,函数还有个__name__属性,可以获得函数名称.