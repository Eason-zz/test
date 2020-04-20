# 解决win10 cmd下运行python弹出windows应用商店问题



## 问题描述：

​	win10系统下，环境变量已配置，然而在cmd下或powershell下运行python，均弹出应用商店，不能正常工作。



## 原因分析：

![image-20200222154901982](C:\Users\86177\AppData\Roaming\Typora\typora-user-images\image-20200222154901982.png)

将path中python的环境变量提升，使其优先级高于应用商店的环境变量（应该是这个**C:\Users\87717\AppData\Local\Microsoft\WindowsApps**）的优先级即可。



*不行的话就删了C:\Users\hongc\AppData\Local\Microsoft\WindowsApps，记得备份，万一有用呢*

再运行python，一切OK，不知道是不是就我遇到这个问题了。。。。。。