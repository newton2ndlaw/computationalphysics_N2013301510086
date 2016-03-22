# Homework 4

## 摘要

- [x] 完成第一章的练习题（自己任选一题）
- [x] 使用matplotlib完成图片的各种细节，认真写报告


## 背景介绍

练习运用python来解决物理问题。利用python的进行数值运算来解微分方程，并做出解的图像。

## 正文

选择的题目是Exercise 1.6。

这道题的背景是人口增长模型，要解出方程的数值解。运用书中1.2节介绍的方法，可以得到递推公式。最后用python进行运算即可。

###第一版
该版本暂时先提供简单的输入、计算、输出、存储、作图功能。
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


程序代码如下：
```python
#作业1.6

from pylab import *
import pickle

N = []
t = []
a = 0
b = 0
dt = 0
n = 0
time = 0

#输入
def initialize(N, t, _a, _b, _dt, _n):
    global a, b, dt, n, time
    print 'Initial population N -> ',
    N.append(float(raw_input()))
    print 'Constant a -> ',
    a = float(raw_input())
    print 'Constant b -> ',
    b = float(raw_input())
    print 'Total time t -> ',
    time = float(raw_input())
    print 'Time step dt -> ',
    dt = float(raw_input())
    t.append(0)
    n = int(time / dt)
    return 0

#计算
def calculate(N, t, a, b, dt, n):
    print 'N=',N
    print 't=',t
    print 'a=',a
    print 'b=',b
    print 'dt=',dt
    print 'n=',n
    for i in range(1,n):
        N.append(N[i-1] + (a * N[i-1] - b * N[i-1] * N[i-1]) * dt)
        t.append(t[i-1] + dt)
    return 0

#存储
def store(N, t, n):
    mfile = open('notes'+' N='+Nstr+' a='+astr+' b='+bstr+' t='+timestr+'.txt','a')
    for i in range(n):
        print >> mfile, i ,t[i], N[i]
    mfile.close()

    pickle_file = open('pickled_data.pkl','w')
    pickle.dump(t, pickle_file)
    pickle.dump(N, pickle_file)

    return 0

#读取
def read():
    pickle_file = open('pickled_data.pkl','r')
    t = pickle.load(pickle_file)
    N = pickle.load(pickle_file)
    print t
    print N

initialize(N, t, a, b, dt, n)
calculate(N, t, a, b, dt, n)

#将初始值转化为字符串用于文件名
Nstr = '%f' %N[0]
astr = '%f' %a
bstr = '%f' %b
timestr = '%f' %time

#清空文件 碰到同名文件就将其清除掉
mfile = open('notes'+' N='+Nstr+' a='+astr+' b='+bstr+' t='+timestr+'.txt','a')
mfile.truncate()
mfile.close()

store(N, t, n)
plot(t, N, label='$N(t)$',color='red',linewidth=3)
xlabel('t')
ylabel('N')
title('Exercise 1.6 Population growth problems')

show()
savefig('notes'+' N='+Nstr+' a='+astr+' b='+bstr+' t='+timestr+'.png')
```

### 第二版
* 可以根据输入的信息来改变输出的图像。
* 添加了程序后输出所有计算过程的功能，利用了read函数。


## 结论

待会弄个图片上去。

## 致谢

* 参考了老师编写的程序。
