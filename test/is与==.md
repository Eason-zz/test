# 写在前面

*这是笔者的在python学习过程中的一些笔记，如有误，还请谅解。*

## python学习心得（四）



### is 与 == 

#### 区别：

```python
a = [1,2,3]
b = [1,2,3]
print(a,b)
print(id(a),id(b))
print(a == b) # a和b的值相等，使用==会返回True
print(a is b) # a和b不是同一个对象，内存地址不同，使用is会返回False
```



```python
>>> a =[1,2,3]
>>> b =[1,2,3]
>>> print(a,b)
[1, 2, 3] [1, 2, 3]
>>> print(id(a),id(b))
64781768 58309008
>>> print(a == b)
True
>>> print(a is b)
False
```

