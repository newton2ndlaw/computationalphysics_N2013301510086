# Homework 4

## 摘要

- [x] 完成第一章的练习题（自己任选一题）
- [x] 使用matplotlib完成图片的各种细节，认真写报告


## 背景介绍

练习运用python来解决物理问题。利用python的进行数值运算来解微分方程，并利用matplotlib作出解的图像。

## 正文

选择的题目是Exercise 1.6。

这道题的背景是人口增长模型，要解出方程的数值解。运用书中1.2节介绍的方法，可以得到递推公式。最后用python进行运算即可。

###第一版（暂时有3个版本）
该版本暂时先提供简单的输入、计算、输出、存储、作图功能。

**更加丰富的功能请看后面的第二版和第三版**

该程序的一些细节：
* 定义了四个函数：输入、计算、存储、读取。
* 可以根据输入的变量来表示输出的文件名。
* 如果遇到有相同文件名的文本文件，就将其覆盖。
* 反复运行此程序，输入不同的参数，可以得包含每次计算的结果文本文件。
* 输出的图像为红色，线宽为3，并加入了标题和横纵坐标。
* 第一版作一个测试，为提高程序速度，未利用read函数。

程序运行之后的效果如下图：

第一次输入N=10 a=10 b=0.01 t=3 dt=0.001
![](https://raw.githubusercontent.com/newton2ndlaw/computationalphysics_N2013301510086/master/Homework4/Homework4-1.png)
![](https://raw.githubusercontent.com/newton2ndlaw/computationalphysics_N2013301510086/master/Homework4/Homework4-2.png)

第二次输入N=10 a=100 b=0.01 t=3 dt=0.001
![](https://raw.githubusercontent.com/newton2ndlaw/computationalphysics_N2013301510086/master/Homework4/Homework4-3.png)
![](https://raw.githubusercontent.com/newton2ndlaw/computationalphysics_N2013301510086/master/Homework4/Homework4-4.png)

第三次输入N=1000 a=10 b=0.01 t=10 dt=0.01
![](https://raw.githubusercontent.com/newton2ndlaw/computationalphysics_N2013301510086/master/Homework4/Homework4-5.png)
![](https://raw.githubusercontent.com/newton2ndlaw/computationalphysics_N2013301510086/master/Homework4/Homework4-6.png)

程序运行几次之后，产生的文件
![](https://raw.githubusercontent.com/newton2ndlaw/computationalphysics_N2013301510086/master/Homework4/Homework4-7.png)


程序链接：[V1.0](https://github.com/newton2ndlaw/computationalphysics_N2013301510086/blob/master/Homework4/V1.0.md)

### 第二版

该版本丰富了输出的图像，并提供调节功能。

版本说明：
* 可以根据输入的信息来改变输出的图像。
* 暂时只做了线形，线宽，线的颜色，标记点的大小，标记点的颜色几个变量。
* 如有需要，还可以提供更多的选项来作图。
* 添加了程序的介绍，并且让输出信息显示更加工整。
* 仍然没有利用read函数，觉得没有太大意义。
* 第二版程序保留了第一版所有的信息。

第二版程序的效果图

![](https://raw.githubusercontent.com/newton2ndlaw/computationalphysics_N2013301510086/master/Homework4/Homework4-8.png)


程序链接：[V2.0](https://github.com/newton2ndlaw/computationalphysics_N2013301510086/blob/master/Homework4/V2.0.md)

### 第三版

第三版的一些新特性
*删除了选择输出线条类型的部分。
*添加了注释。
*添加了理论值的曲线提供对比。
*增加了单位（时间和人口的单位分别为时间单位和人口单位）。

效果如图：


选取的点较少时：（n比较小）
![](https://raw.githubusercontent.com/newton2ndlaw/computationalphysics_N2013301510086/master/Homework4/Homework4-9.png)

选取的点较多时：
![](https://raw.githubusercontent.com/newton2ndlaw/computationalphysics_N2013301510086/master/Homework4/Homework4-10.png)

选取的点更多时：（n比较大）
![](https://raw.githubusercontent.com/newton2ndlaw/computationalphysics_N2013301510086/master/Homework4/Homework4-11.png)

我们可以看出，随着计算的步长越来越小，计算所得结果越接近理论曲线。


代码如下：[V3.0](https://github.com/newton2ndlaw/computationalphysics_N2013301510086/blob/master/Homework4/V3.0.md)



## 结论

可以利用python来进行微分方程的数值解法，并做出相应的图像。

## 致谢

* 参考了老师编写的程序。
* 参考了课本上的例题。
