## NumPy 操作

+ 数组的算数和逻辑运算
+ 傅里叶变换和用于图形操作的例程
+ 与线性代数有关的操作。NumPy拥有线性代数和随机数生成的内置函数。

NumPy 通常与 SciPy（Scientific Python）和 Matplotlib（绘图库）一起使用。

### 一. NumPy-Ndarry 对象

NumPy 中定义的最重要的对象是称为 `ndarray` 的 N 维数组类型。 它描述相同类型的元素集合。 可以使用基于零的索引访问集合中的项目。

```python
numpy.array(object, dtype = None, copy = True, order = None, subok = False, ndmin = 0)
a = np.array([1,2,3])
```
| 序号 | 参数及描述                                                   |
| ---- | ------------------------------------------------------------ |
| 1.   | `object` 任何暴露数组接口方法的对象都会返回一个数组或任何（嵌套）序列。 |
| 2.   | `dtype` 数组的所需数据类型，可选。                           |
| 3.   | `copy` 可选，默认为`true`，对象是否被复制。                  |
| 4.   | `order` `C`（按行）、`F`（按列）或`A`（任意，默认）。        |
| 5.   | `subok` 默认情况下，返回的数组被强制为基类数组。 如果为`true`，则返回子类。 |
| 6.   | `ndimin` 指定返回数组的最小维数。                            |

### 二. NumPy 数据类型

| 序号 | 数据类型及描述                                               |
| ---- | ------------------------------------------------------------ |
| 1.   | `bool_` 存储为一个字节的布尔值（真或假）                     |
| 2.   | `int_` 默认整数，相当于 C 的`long`，通常为`int32`或`int64`   |
| 3.   | `intc` 相当于 C 的`int`，通常为`int32`或`int64`              |
| 4.   | `intp` 用于索引的整数，相当于 C 的`size_t`，通常为`int32`或`int64` |
| 5.   | `int8` 字节（-128 ~ 127）                                    |
| 6.   | `int16` 16 位整数（-32768 ~ 32767）                          |
| 7.   | `int32` 32 位整数（-2147483648 ~ 2147483647）                |
| 8.   | `int64` 64 位整数（-9223372036854775808 ~ 9223372036854775807） |
| 9.   | `uint8` 8 位无符号整数（0 ~ 255）                            |
| 10.  | `uint16` 16 位无符号整数（0 ~ 65535）                        |
| 11.  | `uint32` 32 位无符号整数（0 ~ 4294967295）                   |
| 12.  | `uint64` 64 位无符号整数（0 ~ 18446744073709551615）         |
| 13.  | `float_` `float64`的简写                                     |
| 14.  | `float16` 半精度浮点：符号位，5 位指数，10 位尾数            |
| 15.  | `float32` 单精度浮点：符号位，8 位指数，23 位尾数            |
| 16.  | `float64` 双精度浮点：符号位，11 位指数，52 位尾数           |
| 17.  | `complex_` `complex128`的简写                                |
| 18.  | `complex64` 复数，由两个 32 位浮点表示（实部和虚部）         |
| 19.  | `complex128` 复数，由两个 64 位浮点表示（实部和虚部）        |

数据类型对象描述了对应于数组的固定内存块的解释，取决于以下方面：

- 数据类型（整数、浮点或者 Python 对象）
- 数据大小
- **字节序（小端或大端）**
- 在结构化类型的情况下，字段的名称，每个字段的数据类型，和每个字段占用的内存块部分。
- 如果数据类型是子序列，它的形状和数据类型。

 字节顺序取决于数据类型的前缀`<`或`>`。 `<`意味着编码是小端（最小有效字节存储在最小地址中）。 `>`意味着编码是大端（最大有效字节存储在最小地址中）。

#### np.dtype()应用(结构化数据类型的使用)

```python
# 首先创建结构化数据类型。  
import numpy as np 
dt = np.dtype([('age',np.int8)])  
print dt 
```

```
[('age', 'i1')] 
```

将其应用在**ndarry**对象，比较下面两个实例

```python
import numpy as np 

dt = np.dtype([('age',np.int8)]) 
a = np.array([(10,),(20,),(30,)], dtype = dt)  
print a
```

```
[(10,) (20,) (30,)]
```

 ```python
# 文件名称可用于访问age列的内容
import numpy as np 

dt = np.dtype([('age',np.int8)]) 
a = np.array([(10,),(20,),(30,)], dtype = dt)  
print a['age']
 ```

```
[10 20 30]
```

定义student结构化数据类型

```python
import numpy as np

student=np.dtype([('name','a20'),('age','i1'),('masks','>f4')])
class_1 = np.array([('abc',21,50),('xyz',15,78)],dtype=student)
print(class_1)
print(class_1['age'],class_1['name'],class_1['masks'])
```

```
[(b'abc', 21, 50.) (b'xyz', 15, 78.)]
[21 15] [b'abc' b'xyz'] [50. 78.]
```

$\color \red FixMe：这里的输出结果怎么总是多个b$

每个内置类型都有一个唯一定义他的字符代码：

- `'b'`：布尔值
- `'i'`：符号整数
- `'u'`：无符号整数
- `'f'`：浮点
- `'c'`：复数浮点
- `'m'`：时间间隔
- `'M'`：日期时间
- `'O'`：Python 对象
- `'S', 'a'`：字节串
- `'U'`：Unicode
- `'V'`：原始数据（`void`）

### 三. NumPy 数组特性

```python
# 这会调整数组大小  
import numpy as np 

a=np.array([1,2,3,4,5,6])
a.shape=(2,3)
print(a)
b = a.reshape(3,2)
print(b)
```

```
[[1 2 3]
 [4 5 6]]
[[1 2]
 [3 4]
 [5 6]]
```

```python
a.ndim() # 返回数组维度
a.itemsize() # 返回数组中每个元素的字节单位长度
np.shape() np.reshape() # 改变数组维度
```

```python
# np.flags() # 展示数组当前的标志
import numpy as np 
x = np.array([1,2,3,4,5])  
print x.flags
```

```
C_CONTIGUOUS : True 
F_CONTIGUOUS : True 
OWNDATA : True 
WRITEABLE : True 
ALIGNED : True 
UPDATEIFCOPY : False
```
#### np.flags() 
| 序号 | 属性及描述                                                   |
| ---- | ------------------------------------------------------------ |
| 1.   | `C_CONTIGUOUS (C)` 数组位于单一的、C 风格的连续区段内        |
| 2.   | `F_CONTIGUOUS (F)` 数组位于单一的、Fortran 风格的连续区段内  |
| 3.   | `OWNDATA (O)` 数组的内存从其它对象处借用                     |
| 4.   | `WRITEABLE (W)` 数据区域可写入。 将它设置为`flase`会锁定数据，使其只读 |
| 5.   | `ALIGNED (A)` 数据和任何元素会为硬件适当对齐                 |
| 6.   | `UPDATEIFCOPY (U)` 这个数组是另一数组的副本。当这个数组释放时，源数组会由这个数组中的元素更新 |

### 四. NumPy 数组创建 

#### 1. np.empty()

创建指定形状和dtype的未初始化数组。使用以下构造函数：

```python
numpy.empty(shape, dtype = float, order = 'C')
```

构造器接受下列参数：

| 序号 | 参数及描述                                                   |
| ---- | ------------------------------------------------------------ |
| 1.   | `Shape` 空数组的形状，整数或整数元组                         |
| 2.   | `Dtype` 所需的输出数组类型，可选                             |
| 3.   | `Order` `'C'`为按行的 C 风格数组，`'F'`为按列的 Fortran 风格数组 |

 注意：构造的数组元素为随机数，因为他们未初始化。

#### 2. np.zeros()

返回特定大小，以0填充的数组，默认类型为float

```python
numpy.zeros(shape, dtype = float, order = 'C')
```

构造器接受下列参数：

| 序号 | 参数及描述                                                   |
| ---- | ------------------------------------------------------------ |
| 1.   | `Shape` 空数组的形状，整数或整数元组                         |
| 2.   | `Dtype` 所需的输出数组类型，可选                             |
| 3.   | `Order` `'C'`为按行的 C 风格数组，`'F'`为按列的 Fortran 风格数组 |

 #### 3. np.ones()

```python
numpy.ones(shape, dtype = None, order = 'C')
```

构造器接受下列参数：

| 序号 | 参数及描述                                                   |
| ---- | ------------------------------------------------------------ |
| 1.   | `Shape` 空数组的形状，整数或整数元组                         |
| 2.   | `Dtype` 所需的输出数组类型，可选                             |
| 3.   | `Order` `'C'`为按行的 C 风格数组，`'F'`为按列的 Fortran 风格数组 |

### 五. NumPy 来自现有数据的数组

#### 1.numpy.asarray()

**将列表，列表的元组，元组等返回为ndarray**

```python
numpy.asarray(a, dtype = None, order = None)
```

构造器接受下列参数：

| 序号 | 参数及描述                                                   |
| ---- | ------------------------------------------------------------ |
| 1.   | `a` 任意形式的输入参数，比如列表、列表的元组、元组、元组的元组、元组的列表 |
| 2.   | `dtype` 通常，输入数据的类型会应用到返回的`ndarray`          |
| 3.   | `order` `'C'`为按行的 C 风格数组，`'F'`为按列的 Fortran 风格数组 |

```python
# 设置了 dtype  
import numpy as np 

x =  [1,2,3] 
a = np.asarray(x, dtype =  float)  
print a
```

```
[ 1.  2.  3.]
```

```python
# 来自元组列表的 ndarray
import numpy as np 

x =  [(1,2,3),(4,5)] 
a = np.asarray(x)  
print a
```

```
[(1, 2, 3) (4, 5)]
```

#### 2. numpy.frombuffer()

**将字符串返回为ndarray**

```python
numpy.frombuffer(buffer, dtype = float, count = -1, offset = 0)
```

构造器接受下列参数：

| 序号 | 参数及描述                                           |
| ---- | ---------------------------------------------------- |
| 1.   | `buffer` 任何暴露缓冲区借口的对象                    |
| 2.   | `dtype` 返回数组的数据类型，默认为`float`            |
| 3.   | `count` 需要读取的数据数量，默认为`-1`，读取所有数据 |
| 4.   | `offset` 需要读取的起始位置，默认为`0`               |

```python
import numpy as np 
s =  'Hello World' 
a = np.frombuffer(s, dtype =  'S1')  
print a
```

```
['H'  'e'  'l'  'l'  'o'  ' '  'W'  'o'  'r'  'l'  'd']
```

#### 3. numpy.fromiter()

**将任何可迭代对象返回为一个ndarray**

```python
numpy.fromiter(iterable, dtype, count = -1)
```

构造器接受下列参数：

| 序号 | 参数及描述                                           |
| ---- | ---------------------------------------------------- |
| 1.   | `iterable` 任何可迭代对象                            |
| 2.   | `dtype` 返回数组的数据类型                           |
| 3.   | `count` 需要读取的数据数量，默认为`-1`，读取所有数据 |

```python
# 使用 range 函数创建列表对象  
import numpy as np 
list = range(5)  
print list
```

 ```
range(5)
[0,  1,  2,  3,  4]
 ```

```python
# 从列表中获得迭代器  
import numpy as np 
list = range(5) 
it = iter(list)  
# 使用迭代器创建 ndarray 
x = np.fromiter(it,dtype=float)
print(x)
```

$ \color \red fix me : 迭代器，输出结果不对$

### 六. NumPy 来自数值范围的数组

#### 1. numpy.arange()

**返回给定开始截止和步长的ndarray**

```python
numpy.arange(start, stop, step, dtype)
```

构造器接受下列参数：

| 序号 | 参数及描述                                                   |
| ---- | ------------------------------------------------------------ |
| 1.   | `start` 范围的起始值，默认为`0`                              |
| 2.   | `stop` 范围的终止值（不包含）                                |
| 3.   | `step` 两个值的间隔，默认为`1`                               |
| 4.   | `dtype` 返回`ndarray`的数据类型，如果没有提供，则会使用输入数据的类型。 |

 ```python
import numpy as np
a = np.arange(2,10,2,dtype=np.float32)
print(a)
 ```

```
[2. 4. 6. 8.]
```

#### 2. numpy.linspace()

**返回给定开始截止和个数的ndarray**

```python
numpy.linspace(start, stop, num, endpoint, retstep, dtype)
```

构造器接受下列参数：

| 序号 | 参数及描述                                                   |
| ---- | ------------------------------------------------------------ |
| 1.   | `start` 序列的起始值                                         |
| 2.   | `stop` 序列的终止值，如果`endpoint`为`true`，该值包含于序列中 |
| 3.   | `num` 要生成的等间隔样例数量，默认为`50`                     |
| 4.   | `endpoint` 序列中是否包含`stop`值，默认为`ture`              |
| 5.   | `retstep` 如果为`true`，返回样例，以及连续数字之间的步长     |
| 6.   | `dtype` 输出`ndarray`的数据类型                              |

```python
import numpy as np
a = np.linspace(10,20,3)
print(a)
a = np.linspace(10,20,3,endpoint=False,retstep=True)
print(a)
```

```
[10. 15. 20.]
(array([10.        , 13.33333333, 16.66666667]), 3.3333333333333335)
```

#### 3. numpy.logspace()

**与linespace(线性空间)对应为对数刻度上的ndarray**

```python
numpy.logspace(start, stop, num, endpoint, base, dtype)
```

`logspace`函数的输出由以下参数决定：

| 序号 | 参数及描述                                                 |
| ---- | ---------------------------------------------------------- |
| 1.   | `start` 起始值是`base ** start`                            |
| 2.   | `stop` 终止值是`base ** stop`                              |
| 3.   | `num` 范围内的数值数量，默认为`50`                         |
| 4.   | `endpoint` 如果为`true`，终止值包含在输出数组当中          |
| 5.   | `base` 对数空间的底数，默认为`10`                          |
| 6.   | `dtype` 输出数组的数据类型，如果没有提供，则取决于其它参数 |

 ### 七. NumPy 切片和索引

`ndarray`对象的内容可以通过索引或切片来访问和修改，就像 Python 的内置容器对象一样。

如前所述，`ndarray`对象中的元素遵循基于零的索引。 有三种可用的索引方法类型： **字段访问，基本切片**和**高级索引**。

基本切片是 Python 中基本切片概念到 n 维的扩展。 通过将`start`，`stop`和`step`参数提供给内置的`slice`函数来构造一个 Python `slice`对象。 此`slice`对象被传递给数组来提取数组的一部分。


```python
import numpy as np
a = np.arange(10)
s = slice(2,7,2)  
print a[s]
```

输出如下：

```
[2  4  6]
```

在上面的例子中，`ndarray`对象由`arange()`函数创建。 然后，分别用起始，终止和步长值`2`，`7`和`2`定义切片对象。 当这个切片对象传递给`ndarray`时，会对它的一部分进行切片，从索引`2`到`7`，步长为`2`。

通过将由冒号分隔的切片参数（`start:stop:step`）直接提供给`ndarray`对象，也可以获得相同的结果。

```
import numpy as np
a = np.arange(10)
b = a[2:7:2]  
print b
```

输出如下：

```
[2  4  6]
```

如果只输入一个参数，则将返回与索引对应的单个项目。 如果使用`a:`，则从该索引向后的所有项目将被提取。 如果使用两个参数（以`:`分隔），则对两个索引（不包括停止索引）之间的元素以默认步骤进行切片。

```python
import numpy as np 
c=np.array([[1,2,3],[4,5,6],[7,8,9]])
print(c)
print(c[1,...])
print(c[1:,...])
print(c[...,1:])
```

```
[[1 2 3]
 [4 5 6]
 [7 8 9]]
[4 5 6]
[[4 5 6]
 [7 8 9]]
[[2 3]
 [5 6]
 [8 9]]
```

https://blog.csdn.net/a373595475/article/details/79580734