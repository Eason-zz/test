# **选择排序python版（课堂笔记)**



```python 
my_list = [5,6,9,8,3,2,1,4,7,10,464,55,9,55,68454,86,22] 
for i in range(len(my_list)): 
    min_idx = i 
    for j in range(i+1, len(my_list)): 
        if my_list[min_idx] > my_list[j]: 
            min_idx = j 
    my_list[i], my_list[min_idx] = my_list[min_idx], my_list[i]  
print ("排序后的数组：") 
for i in range(len(my_list)): 
    print("%d" %my_list[i])
```

