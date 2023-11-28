# Python基础

## for循环

### for in 遍历

```python
colors = ["red", "green", "blue"]
for color in color:
	print color
# out: red \n green...
```

### for in range()

```python
colors = ["red", "green", "blue"]
for i in range(0, len(colors)): # 倒序遍历range(len(colors), -1, -1)
	print i, colors[i]
# out: 0 red \n 1 green...
```

### for in enumerate()

```python
s = [1, 2, 3, 4, 5]
# 语法: enumerate(sequence, [start=0])
for index, value in enumerate(s):
    print('%s, %s' % (index, value))
# out: 0, 1 \n 1, 2

# 指定索引从1开始
for index, value in enumerate(s, 1):
    print('%s, %s' % (index, value))
# out: 1, 1 \n 2, 2
```

## 条件判断

### or或 and与

对应java：or == ||， and == &&

## ACM输入输出

### 输入输出接收

```python
# 输入
a, b = map(int,input().split())# map函数(func, *iterables)使用可迭代对象中的每一个元素作为参数调用func函数，返回一个迭代器

print(a, b) # 打印多个变量，默认以空格隔开，可以通过sep参数修改：print(a, b, sep='-')
print(a, b, end = ' ') # end默认以换行符结尾，多个print不在同一行
print(f"a = {a}") #格式化字符串，可以在字符串里面加{}打印变量，类似str.format()
# format用法
print('name is {}, age is {}'.format('peter',25))
print('name is {1}, age is {0}'.format(25, 'peter'))
print('name is {name}, age is {age}'.format(name='peter',age='25'))
```

### 数据处理

```python
# 数据对齐
S = '1'
S.rjust(10, '0') # 字符串右对齐，即在左补0，0000000001。10:width，总长度，不足才补
S.ljust(10, '0') # 1000000000

# 进制转换
int('0xE', 16) # 16进制转10进制
bin(10) # 10进制转2进制  0b1010
oct(10) # 10进制转8进制  0o12
hex(10) # 10进制转16进制  0xa

# 前缀和
from itertools import accumulate
s = list(accumulate(nums, initial=0))  # nums 的前缀和，python3.8之后提供

# 统计词频
from collections import Counter
nums = [1, 1, 1, 6, 6, 6, 7, 8]
count = Counter(nums)  

# 数字处理
int(3.75) # 向下取正
round(3.48) # 四舍五入
import math
math.ceil(3.48) # 向上取整
a = 2 ** 5 # 2的5次方
```

## 字符相关

声明字符：`str = "" or ''`。python中，单引号和双引号使用完全相同。\用来转义，使用r可以让\不发生转义，如`r"this is \n"`

```python
str1.isdigit() # 判断是否数字
str1.isalpha() # 判断是否字母
str1.isalnum() # 判断是否为数字和字母的组合
punc = string.punctuation # 判断是否标点符号
if str1 in punc:
    print('is punctuation')
   
print(ord('c') - ord('a')) # 字符相加减
print(chr(99)) # ASCII码转字符
str1.lstrip() # 去除左边字符，默认空格，可指定字符
```

## Sorted排序

语法`sorted(iterable, key=None, reverse=False) `默认升序排序。

- iterable：可迭代对象。
- key：主要是用来进行比较的元素，只有一个参数，具体的函数的参数就是取自于可迭代对象中，指定可迭代对象中的一个元素来进行排序。
- reverse：排序规则，reverse = True 降序 ， reverse = False 升序（默认）。

```python
sorted([5, 2, 3, 1, 4])# 默认为升序 ans:[1, 2, 3, 4, 5]
a=[5,2,3,1,4]
a.sort() # list.sort()只适用list，会修改原始list。效率稍微高一点

example_list = [5, 0, 6, 1, 2, 7, 3, 4]
result_list = sorted(example_list, key=lambda x: x*-1) # 利用key，倒序排序 [7, 6, 5, 4, 3, 2, 1, 0]
sorted(example_list, reverse=True) # 也可以这样倒序排序 [7, 6, 5, 4, 3, 2, 1, 0]

# 利用key对数组/字典排序
array = [{"age":20,"name":"a"},{"age":25,"name":"b"},{"age":10,"name":"c"}]
array = sorted(array,key=lambda x:x["age"])
# ans [{'age': 10, 'name': 'c'}, {'age': 20, 'name': 'a'}, {'age': 25, 'name': 'b'}]

# 多列排序：先按照成绩降序排序，相同成绩的按照名字升序排序
d1 = [{'name':'alice', 'score':38}, {'name':'bob', 'score':18}, {'name':'darl', 'score':28}, {'name':'christ', 'score':28}]
l = sorted(d1, key=lambda x:(-x['score'], x['name']))
# [{'name': 'alice', 'score': 38}, {'name': 'christ', 'score': 28}, {'name': 'darl', 'score': 28}, {'name': 'bob', 'score': 18}]
```

## 列表推导式

1. [表达式 for 变量 in 列表]  / [out_exp_res for out_exp in input_list]
2. [表达式 for 变量 in 列表 if 条件]  / [out_exp_res for out_exp in input_list if condition]

**表达式**：列表生成元素表达式，可以是有返回值的函数。

**for 变量 in 列表**：迭代将变量传入表达式中

**if 条件**：条件语句，过滤列表中不合条件的值

同理，有字典推导式{ key_expr: value_expr for value in collection }/{ key_expr: value_expr for value in collection if condition }、集合推导式、元组推导式

## Counter

可以非常方便的统计词频，**统计可迭代对象中每个元素出现的次数，返回一个字典**

```python
from collections import Counter
nums = [1, 1, 1, 6, 6, 6, 7, 8]
count = Counter(nums)  # 统计词频
for k, v in count.items():
    print(k, v)
print(count)
"""
out: 1 3 \n 6 3 \n 7 1 \n 8 1
"""
```

## 类

### 基础概念

Python设计之初就是一门**面向对象**的语言。

```python
# 类的定义
class MyClass:
  i = 12345
  # 两个下划线开头，声明私有属性，类外部无法直接访问。
  __my = 0
  def f(self):
    return "hello world"
  # 两个下划线开头，声明私有方法，类外部无法直接访问。
  def __myMethod(self):
    print("myMethod")
  
m = MyClass()
print(m.i, m.f()) # 访问属性和方法
```

类有默认的构造方法`__init__()`，可以有参数。

**类的方法与普通的函数有一个特殊的区别：必须有一个额外的第一个参数名称，惯例它的名称是self。**

```python
class Complex:
    def __init__(self, realpart, imagpart):
        self.r = realpart
        self.i = imagpart
    def prt(self):
        print(self)
        print(self.__class__)
x = Complex(3.0, -4.5)
print(x.r, x.i)   # 输出结果：3.0 -4.5
x.prt()
```

类的继承（如果一种语言不支持继承，类就没什么意义）python支持多继承

```python
# 单继承
class DerivedClassName(BaseClassName):
  def myMethod(self): # 子类可以重写父类方法
      print ('调用父类方法')
# 多继承
class DerivedClassName(Base1, Base2, Base3):
```

### **类的专有方法**

- **__init__ :** 构造函数，在生成对象时调用
- **__del__ :** 析构函数，释放对象时使用
- **__repr__ :** 打印，转换
- **__setitem__ :** 按照索引赋值
- **__getitem__:** 按照索引获取值
- **__len__:** 获得长度
- **__cmp__:** 比较运算
- **__call__:** 函数调用
- **__add__:** 加运算
- **__sub__:** 减运算
- **__mul__:** 乘运算
- **__truediv__:** 除运算
- **__mod__:** 求余运算
- **__pow__:** 乘方

### 运算符重载

Python同样支持运算符重载，我们可以对类的专有方法进行重载，实例如下：

```python
class Vector:
   def __init__(self, a, b):
      self.a = a
      self.b = b
 
   def __str__(self):
      return 'Vector (%d, %d)' % (self.a, self.b)
   
   def __add__(self,other):
      return Vector(self.a + other.a, self.b + other.b)
 
v1 = Vector(2,10)
v2 = Vector(5,-2)
print (v1 + v2)
```

## 异常处理

异常捕捉`try...except...`/`try...except...else...`/`try...except...else...finally...`

```python
while True:
    try:
        x = int(input("请输入一个数字: "))
        break
    except ValueError as err:
        print("您输入的不是数字，请再次尝试输入！")
		except (RuntimeError, TypeError, NameError):# 一个 try 语句可能包含多个except子句
    		pass
    except:
      	print("Unexpected error")
        raise # raise语句抛出一个指定的异常。语法格式raise [Exception [, args [, traceback]]]
        # e.g. raise Exception('x 不能大于 5。x 的值为: {}'.format(x))
```

## 正则表达式使用

### 规则

| **模式**    | 描述                                                         |
| ----------- | ------------------------------------------------------------ |
| ^           | 匹配字符串的开头                                             |
| $           | 匹配字符串的末尾。                                           |
| .           | 匹配任意字符，除了换行符，当re.DOTALL标记被指定时，则可以匹配包括换行符的任意字符。 |
| [...]       | 用来表示一组字符,单独列出：[amk] 匹配 'a'，'m'或'k'          |
| [^...]      | 不在[]中的字符：`[^abc]` 匹配除了a,b,c之外的字符。           |
| re*         | 匹配0个或多个的表达式。                                      |
| re+         | 匹配1个或多个的表达式。                                      |
| re?         | 匹配0个或1个由前面的正则表达式定义的片段，非贪婪方式         |
| a\|b        | 匹配a或b                                                     |
| \w          | 匹配字母数字及下划线                                         |
| \W          | 匹配非字母数字及下划线                                       |
| \s          | 匹配任意空白字符，等价于 [\t\n\r\f].                         |
| \S          | 匹配任意非空字符                                             |
| \d          | 匹配任意数字，等价于 [0-9].                                  |
| \D          | 匹配任意非数字                                               |
| \A          | 匹配字符串开始                                               |
| \Z          | 匹配字符串结束，如果是存在换行，只匹配到换行前的结束字符串。c |
| \z          | 匹配字符串结束                                               |
| \G          | 匹配最后匹配完成的位置。                                     |
| \b          | 匹配一个单词边界，也就是指单词和空格间的位置。例如， 'er\b' 可以匹配"never" 中的 'er'，但不能匹配 "verb" 中的 'er'。 |
| \B          | 匹配非单词边界。'er\B' 能匹配 "verb" 中的 'er'，但不能匹配 "never" 中的 'er'。 |
| \n, \t, 等. | 匹配一个换行符。匹配一个制表符。等                           |

### 使用

1. 导入re模块。
2. 使用re模块里的`match(正则表达式，要匹配的字符串)`方法匹配。对匹配到的结果用`group()`方法提取出来。

```python
import re  # 导入re 模块
 
str_content = "Python is a good language"  # 要匹配的内容, 对应match 里面的string
str_pattern = "Python"  # patterPn 匹配的规则
# re_content = re.match("python", str_content)
re_content = re.match("python", str_content, re.I) # (pattern, str, flag)
if re_content: # 为None时调用为报错
    print(re_content.group()) #re_content.span() 为匹配到的下标
else:
    print("没有匹配到内容")
"""
flag的使用：
re.I 忽略大小写
re.L 表示特殊字符集 \w, \W, \b, \B, \s, \S 依赖于当前环境
re.M 多行模式
re.S 即为 . 并且包括换行符在内的任意字符（. 不包括换行符）
re.U 表示特殊字符集 \w, \W, \b, \B, \d, \D, \s, \S 依赖于 Unicode 字符属性数据库
re.X 为了增加可读性，忽略空格和 # 后面的注释
"""
    
    
# eg2 搜索
S = "To hello ni wo ta"
print(re.findall('[a-z]*o[a-z]*', S, re.I)) # 找到所有带o的单词

"""
.*：表示匹配除换行符以外任何单字符，贪婪匹配，如a.*b，搜索aabab，会匹配整个字符串
.*?：懒惰模式/非贪婪模式，匹配尽可能少的字符，如a.*?b，搜索aabab，匹配aab
.+?：懒惰模式/非贪婪模式。如a.+?b，搜索ababccaab，匹配abab
"""


"""
替换
re.sub(pattern, repl, string, count=0, flags=0)

pattern：同findall函数中的pattern。

repl：指定替换成的新值。

string：同findall函数中的string。

count：用于指定最多替换的次数，默认为全部替换。

flags：同findall函数中的flags。
"""

"""
分割
re.split(pattern, string, maxsplit=0, flags=0)

pattern：同findall函数中的pattern。

maxsplit：用于指定最大分割次数，默认为全部分割。

string：同findall函数中的string。

flags：同findall函数中的flags。

"""

```

# 常用集合

## 列表list（数组）可用作堆/队列

```python
a = [] # 创建
a = [0] * 10
a = list()

a.append(1) # 末尾添加
a.insert(0, 2) # 指定位置插入

print(a[1]) # 访问
idx = a.index(2) # 查找某个元素，存在返回下标
copied_a = a.copy() #拷贝1
copied_a1 = list(a) #拷贝2
copied_a2 = a[:] #拷贝3
copied_a3 = [v for v in a] #拷贝4

a[1] = 3 # 修改

a.remove(2) # 删除指定值的元素，O(n)
a.pop(0) # 删除指定位置的元素，O(n)
a.pop() # 删除末尾元素，O(1)

# 排序
a.sort()
a.sort(reverse=True)
"""
dcdcdcdce
dcdcdcdce
"""
# 元素拼接
a = [1,0,1,0,1]
# ''.join 中的''可以理解为元素间的连接符号，如果是'-'就变成1-0-1-0-1
print(''.join([str(i) for i in a])) 
```

### 嵌套列表声明

```python
# 第一种
a = [[]] * 3
a[1].append('x')
# 第二种
b = [[] for _ in range(3)] # ans = [[0 for _ in range(N)] for _ in range(N)]
b[1].append('x')
```

不能用第一种，第一种内层子列表[]实际引用了同一个可变对象，结果是`[['x'], ['x'], ['x']]`

## 字典

就是hashmap，不过这里不同键值对间的k，v可以不一样。

### 查询

```python
dict1 = {1: 10, 2: 5, 3: 15}
dict2 = dict() # 声明一个空字典
dict3 = {} # 空字典
print(dict1[1])
dict1[4] = 6 # 没有的赋值就是添加，有的就是覆盖
```

### 遍历

```python
# 第一种
for k, v in dict1.items():
	print(k, v)
# 第二种
for k in dict1:
	print(k, dict1[k])
```

### 判断值是否存在

```python
dict1 = {1: 10, 2: 5, 3: 15}
for k, v in dict1.items():
  # 推荐
	print(k + 1 in dict1)
	# 第二种
  print(k + 1 in dict1.keys())
```

### 删除

```python
# 删除键值对
del dict1[2]
```

## 集合Set

set是一个无序的不重复元素序列

```python
 # 创建
s = {v1,v2,...}
s = set(value)
s = set() #空集合只能这样创建，{}是创建空字典
# 添加, x可以是列表、元组、字典等
s.add(x)
s.update(x)
# 移除元素
s.remove(x) # 没有x会报错
s.discard(x) # 不会报错
s.pop()# 随机删除
s.clear() # 清空
# 查找
if x in s:
```

## 堆

### 使用heapq

heapq默认创建的是小根堆

```python
arr = [10,8,9,4,6,3,5]
heap = []
# 第一种，heapq.heappush创建堆结构
for num in arr:
	heapq.heappush(heap, num)
  
# 创建最大堆的话，把数取反，弹出的时候再取反，就能得到从大到小的数
arr1 = [-arr[i] for i in range(len(arr))]
  
# 第二种，heapq.heapify创建堆结构
heapq.heapify(arr)

# 堆排序，小 => 大
heap_sort = [heapq.heappop(heap) for _ in range(len(heap))]
print("heap sort result: ", heap_sort)
```

### 获取堆顶元素

1. `heapq.heappop(heap)` 
2. 单纯获取的话直接 `heap[0]`heap为对应的堆名

### 获取堆t个最大值或最小值

时间复杂度应该是n*log(t)，n为数组大小，t为获取的个数

```python
array = [10, 17, 50, 7, 30, 24, 27, 45, 15, 5, 36, 21]
heapq.heapify(array)
print(heapq.nlargest(2, array) # 获取最大的2个数
print(heapq.nsmallest(3, array)) # 获取最小的3个数
"""
[50, 45]
[5, 7, 10]
"""
```

### 合并有序列表

```python
a = [3, 1, 6, 8]
b = [5, 9, 2, 1]
merge = heapq.merge(sorted(a), sorted(b))
# merge返回的结果是迭代器 所以要输出list(merge)
print(list(merge))
```

### 替换数据

有两种，`heapq.heappushpop()`和`heapq.heapreplace()`

```python
heap = [5,6,7,8,9]
gen = heapq.heappushpop(heap, 3)
print("先把3加入堆再弹出的根，弹出值：", gen) # 弹出3

gen2 = heapq.heapreplace(heap, 3)
print("先弹出根在把3加入到堆中，弹出值：", gen2) # 弹出5
```

### 比较问题

1. 如果heapq放入的是元组，那么**元组第一个元素会用于比较大小**
2. 堆中放的是自定义类，可以通过实现`__lt__`来比较元素大小

```python
def __lt__(self, other):
    return self.value < other.value
ListNode.__lt__ = __lt__
```

## 队列

### 双端队列

声明：`collections.deque([iterable[, maxLen]])`

#### 方法速查表

| 方法                      | 说明                                                         |
| ------------------------- | ------------------------------------------------------------ |
| append(x)                 | 从 deque 最右端加入元素 x                                    |
| appendleft(x)             | 从 deuqe 最左端加入元素 x                                    |
| extend(iterable)          | 使用可迭代对象 iterbale 中的元素扩展 deque 右端              |
| extendleft(iterable)      | 使用可迭代对象 iterbale 中的元素扩展 deque 左端              |
| insert(i, x)              | 在 index=i 的位置插入元素 x (若导致 deque 长度超过 maxlen，引发 IndexError) |
| pop()                     | 弹出 deque 最右端的一个元素 (若无元素引发 IndexError)        |
| popleft()                 | 弹出 deque 最左端的一个元素 (若无元素引发 IndexError)        |
| remove(x)                 | 移除从左到右找到的第一个 x (若无 x 引发 ValueError)          |
| clear()                   | 清空 deque 中的所有元素，使之为空 deque (长度归0)            |
| copy()                    | 创建一份当前 deque 的浅拷贝                                  |
| count(x)                  | 计算 deque 中 x 的个数                                       |
| index(x[, start[, stop]]) | 返回在 [start, stop] 之间从左到右找到的第一个 x 的 index (未找到引发 ValueError) |
| reverse()                 | 将当前 deque 逆序排列，返回 None                             |
| rotate(n=1)               | n 为正数向右循环移动 n 步，n 为负数向左循环移动 n 步，若 deque 非空<br />向右循环移动 1 步等价于 d.appendleft(d.pop())<br />向左循环移动 1 步等价于 d.append(d.popleft()) |