# Numpy常用数据结构： 

## 【ndarray - N维数组】

 

Numpy中的数据结构比python中自带的数据结构，如列表、元组、字典等，要快很多。

在Python中，尽量要避免写for循环，因为python和C语言相比，其运算效率较低，尽量要使用numpy里的数据结构。

 

numpy常用函数包括： 

*array() arange() linspace() zeros()*

*np.array()*

 

用法：

import numpy as np

 

np.arange()

np.linspace()

np.zeros()

np.array()

 

\1. array()用法

import numpy as np

np.array(*列表或元组*)

```python
import numpy as np

# - 1
arr1 = np.array([-9,7,4,3])
print(type(arr1))
# 打印arr1得类型，为numpy.ndarray对象：array([-9，7，4，3])

# - 2
arr2 = np.array([-9,7,4,3], dtype= ‘str' ) 
# dype设定数组内数据的类型，dype可以是，str, float, int, ... 不用加引号

# - 3
arr3 = np.array([[1,2,3,4],[5,6,7,8],[9,10,11,12]])
# 使用嵌套列表的方式创建二位数组
```

 

\2. arange()用法 - 创建数组

用法同python中的迭代器：

```python
# arange()的用法同python中的迭代器：

for i in range(0,10,1):  # 左取右不取
    print(i)
```

np.arange(起始值，终止值，步长），也是左取右不取

```python
a = np.arange(0,11,2)
print(a)

# 创建一个起始值为0，终值为10，步长为2的数组
```

 

\3. linspace() 用法 - 创建等差数组

np.linspace(初始值，终止值，元素个数，endpoint=True)

endpoint = True，包含终值；endpoint = False，不包含终值

```python
a = np.linspace(0,11,6,endpoint=False)
print(a)

# 创建一个初始值为0，终值为10，包含6个元素的等差数组
```

 

\4. zeros()用法 - 创建二维数组

np.zeros(行数a，列数b)，产生一个行数为行数a，列数为列数b的二维数组：

```python
a = np.zeros([4,5])
print(a)
#  创建一个4行5列的二位数组
```

 

np.zeros(数字a)，产生一个一行，包含数字a个数字的一维数组：

```python
a = np.zeros(4)
print(a)
# 产生一个1行，4个元素的数组
```

np.ones(行数a,列数b)，产生一个行数为列数a，列数为列数b的二维数组。

```python
np.ones([2,3])
```

 注意：

Numpy的底层是用C语言写的，所以做数学运算时是并行运算，arr2 + 1 是对每一个元素同时加1：

```python
arr2 = np.array([[1,3,5,7,9],[8,3,5,4,2],[11,53,4,68,10]])

arr3 = arr2 + 1.5

print(arr3)
```

运算会比python的for循环迭代器快很多。所以还是尽量用Numpy里面的数据结构做数据清洗，因为其清洗效率高。

 

\5. 数组的属性

1）arr3.ndim - 查看数组维度

2）arr1.shape - 查看数组形状（几行几列）

输出为(4,)时，为1维数组

3）arr3.size - 查看数组中的元素个数

3行4列的数组，输出为12

4）arr3.dtype - 查看数组的数据类型

 

\6. 数组的访问

1）数据的索引方式：

array[a,b] - a:代表行索引；b:代表列索引
 

```python
# 这是一个嵌套元组

data2 = ((8.5,6.4,1.2,0.7),(1.5,3.2,4.8,9,3),(0.9,4.4,7.2,1.5))

arr2 = np.array(data2)


# 访问第1行

c = arr2[0] 

# 访问1-3行

d = arr2[0:3]

# 取第2行、第3列的元素

e1 = arr2[1,2]

e2 = arr2[1][2]

# 对行数不做限制，选择第2-3列

f = arr2[:,1:3]

print('c:\n'+c, 'd:\n'+d, 'e1:\n'+e1, 'e2:\n'+e2, 'f:\n'+f)
```