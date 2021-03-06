Title: Python学习笔记之Python对象
Date: 2014-05-25 18:51:50
Tags: Python, Python对象

Python 对象拥有三个特性： 身份，类型和值

身份：每一个对象都有一个唯一的身份标识自己，任何对象的身份可以使用内建函数`id()`来得到。这个值可以被认为是该内存对象的内存地址。

类型：对象的类型决定了该对象可以保存什么类型的值，可以进行什么样的操作，以及遵循什么样的规则。可以用内建函数`type()`来查看Python对象的类型。因为在Python中类型也是对象(Python是面向对象的)，所以`type()`返回的是对象而不是简单的字符串。

值：对象表示的数据项

对象属性：某些Python对象有属性、值或相关联的可执行代码，比如方法(method)。
Python用句点(\.) 标记法来访问属性。
属性包括相应对象的名字。
最常用的属性是函数和方法，不过一些Python类型也有数据属性。
含有数据属性的对象包括(但不限于): 类、类实例、模块、复数和文件。

## 标准类型

 * 数字(分为几个子类型，其中有三个是整形)
 * Integer 整形
 * Boolean 布尔型
 * Long integer 长整形
 * Floating point real number 浮点型
 * Complex number 复数型
 * String 字符串
 * List 列表
 * Tuple 元祖
 * Dictionary 字典

## 其他内建类型

 * 类型
 * Null 对象(None)
 * 文件
 * 集合/固定集合
 * 函数/方法
 * 模块
 * 类

## 内部类型

 * 代码 代码对象是编译过的Python源代码片段，他是可执行对象。通过调用内建函数complie()可以得到代码对象。代码对象可以被exec命令或eval()内建函数来执行。
 * 帧   帧对象表示Python的执行栈帧。用到帧对象的一个地方是跟踪记录对象。
 * 跟踪记录 当你的代码出错时，Python就会引发一个异常。当异常发生时，一个包含针对异常的栈跟踪信息的跟踪记录对象被创建。
 * 切片 当使用Python的切片语法时，就会创建切片对象。
 * 省略
 * Xrange   调用内建函数xrang()会生成一个Xrang对象，xrange()是内建函数range()的兄弟版本，用于需要将节省内存使用或range()无法完成的超大数据集场合。

## 标准了额I型操作符

### 对象值的比较

比较操作符用来判断同类型对象是否相等，所有的内建类型均支持比较运算，比较运算返回布尔值True或False.
数字类型根据注释的大小和符号比较，字符串按照字符序列进行比较。

    >>> 2 == 2
    True
    >>> 2.46 <= 8.33
    True
    >>> 'abc' == 'xyz'
    False
    >>> 'abc' > 'xyz'
    False
    >>> 'abc' < 'xyz'
    True
    >>> [3, 'abc'] == ['abc', 3]
    False
    >>> [3, 'abc'] == [3, 'abc']
    True
    >>>
    >>>
    >>> 3 < 4 < 7
    True
    >>> 4 > 3 == 3
    True
    >>> 4 < 3 < 5 != 2 < 7
    False

### 对象身份比较

Python 提供了`is` 和 `is not` 操作符来测试两个变量是否指向同一个对象。

    a is b

等价于

    id(a) == id(b)

举例

    >>> a = [5, 'hat', -9.3]
    >>> b = a
    >>> a is b
    True
    >>> a is not b
    False
    >>>
    >>> b = 2.5e-5
    >>> b
    2.5e-05
    >>> a
    [5, 'hat', -9.3]
    >>> a is b
    False
    >>> a is not b
    True

### 布尔类型

操作符的优先级从高到底是： not(逻辑非), and(逻辑与), or(逻辑或)

    >>> x, y = 3.1415926536, -1024
    >>> x < 5.0
    True
    >>> not (x < 5.0)
    False
    >>> (x < 5.0) or (y > 2.718281828)
    True
    >>> (x < 5.0) and (y > 2.718281828)
    False
    >>> not (x is y)
    True

Python支持一个表达式进行多种比较操作，其实这个表达式本质上是有多个隐式的and连接起来的多个表达式。

    >>> 3 < 4 < 7   # 与 "(3 < 4) and (4 < 7)"一样
    True

## 标准类型内建函数

`type()`: 接受一个对象为参数，并返回它的类型。他的返回值是一个类型对象。

    >>> type(4)
    <type 'int'>
    >>>
    >>> type('Hello World!')
    <type 'str'>
    >>>
    >>> type(type(4))
    <type 'type'>

`cmp()`: 用于比较两个对象obj1和obj2。

如果obj1小于obj2，则返回一个负整数。
如果obj1大于obj2，则返回一个整数。
如果obj1等于obj2，则返回0。

例子：

    >>> a, b = -4, 12
    >>> cmp(a,b)
    -1
    >>> cmp(b,a)
    1
    >>> b = -4
    >>> cmp(a,b)
    0
    >>> a, b = 'abc', 'xyz'
    >>> cmp(a,b)
    -1
    >>> cmp(b,a)
    1
    >>> b = 'abc'
    >>> cmp(a,b)
    0

`str()`: 得到的字符串可读性好, 无法用于`eval()`求职，但很适合`print`语句输出


`repr()`: 得到的字符串通常可以用来重新获得该对象。 通常情况下  `obj == eval(repr(obj))` 这个等式是成立的。

    >>>str(4.53-2j)
    '(4.53-2j)'
    >>>
    >>> str(1)
    '1'
    >>>
    >>> str(2e10)
    '20000000000.0'
    >>>
    >>> str([0, 5, 9, 9])
    '[0, 5, 9, 9]'
    >>>
    >>> repr([0, 5, 9, 9])
    '[0, 5, 9, 9]'
    >>>
    >>> `[0, 5, 9, 9]`
    '[0, 5, 9, 9]'

`str()`,`repr()`,`\`\``, 运算在特性和功能上非常相似，`repr()`和`\`\``做的是一样的事情，都是返回一个对象的"官方"字符串表示。

注：不是所有`repr()`返回的字符串都能够用`eval()`内建函数得到原来的对象。如：

    >>> eval(`type(type)`)
    Traceback (most recent call last):
      File "<stdin>", line 1, in <module>
      File "<string>", line 1
        <type 'type'>
        ^
    SyntaxError: invalid syntax

虽然`repr()`和`\`\``基本一样，但是更推荐用函数的方式，因为在某些场合下函数会比操作符更适合使用。

## 类型工厂函数

看上去有点像函数，实质上他们是类。

工厂函数(以前称为内建函数)

`int(), long(), float(), complex()
str(), unicode(), basestring()
list(), tuple()
type()`

新式类中新增加的工厂函数：

`dict()
bool()
set(), frozenset()
object()
classmethod()
staticmethod()
super()
property()
file()`

## 标准类型的分类

### 存储模型

 分类 | Python类型
 --- | ---
 标量/原子类型 | 数值(所哟的数值类型),字符串(全部是文字)
 容器雷系先那个 | 列表、元组、字典

### 更新模型

 分类 | python类型
 --- | ---
 可变类型 | 列表，字典
 不可变类型 | 数字、字符串、元组

### 访问模型

 分类 | Python类型
  --- | ---
 直接访问 | 数字
 顺序访问 | 字符串、列表、元组
 映射访问 | 字典

### 标准类型分类汇总

 数据类型 | 存储模型| 更新模型 | 访问模型
 --- | --- | --- | -----
 数字 | 标量 | 不可更改 | 直接访问
 字符串 | 标量 | 不可更改 | 顺序访问
 列表 | 容器 | 可更改 | 顺序访问
 元组 | 容器 | 不可更改 | 顺序访问
 字典 | 容器 | 可更改 | 映射访问

### 不支持的类型

 1. char 或 byte 没有char(单一字符) 或byte(8位整形) 都用商都为1的字符串表示
 2. 指针,Python替你管理内存，没有必要访问指针， `id()`得到的对象的值其实就是接近于指针的地址
 3. int vs short vs long  仅支持int，其余会自动转换
 4. float vs double 不支持单精度

