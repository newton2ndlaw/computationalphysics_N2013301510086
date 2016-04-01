# Homework 6

## 摘要

第六次作业
- 作业L1 2.9题
- 作业L2 2.10题强化版（引入风阻）————“辅助精确打击系统”
- 作业L3 发展“超级辅助精确打击系统”（考虑炮弹初始发射的时候发射角度误差1%，速度有5%的误差，风阻误差10%，可以考虑引入Coriolis force等，以炮弹落点与打击目标距离差平方均值最小为优胜）


## 背景介绍

## 正文

### 作业L1

炮弹发射的过程是一个绝热过程，根据课本P30，空气密度与海拔高度的关系：

![](http://latex.codecogs.com/gif.latex?%5Crho%20%3D%20%5Crho_0%20%281-%5Cfrac%7Bay%7D%7BT_0%7D%29%5E%5Calpha)

空气阻力和空气密度的关系：

![](http://latex.codecogs.com/gif.latex?F_%7Bdrag%7D%5E*%3D%5Cfrac%7B%5Crho%7D%7B%5Crho_0%7DF_%7Bdrag%7D%28y%3D0%29)

于是，可以得到递推关系：

![](http://latex.codecogs.com/gif.latex?%5Cleft%5C%7B%5Cbegin%7Bmatrix%7Dv_%7Bx%2Ci&plus;1%7D%3Dv_%7Bx%2Ci%7D-%5Cfrac%7B%5Crho%20B_2%20v_i%20v_%7Bx%2Ci%7D%7D%7B%5Crho_0%20m%7D%20%5C%5C%20v_%7By%2Ci&plus;1%7D%3Dv_%7By%2Ci%7D-%5Cfrac%7B%5Crho%20B_2%20v_i%20v_%7By%2Ci%7D%7D%7B%5Crho_0%20m%7D%20%5C%5C%20v_i%3D%5Csqrt%7Bv_%7Bx%2Ci%7D%5E2&plus;v_%7By%2Ci%7D%5E2%7D%20%5C%5C%20%5Cfrac%7B%5Crho%7D%7B%5Crho_0%7D%3D%281-%5Cfrac%7Bay%7D%7BT_0%7D%29%5E%5Calpha%20%5C%5C%20x_%7Bi&plus;1%7D%3Dx_i&plus;v_%7Bx%2Ci%7D%20%5CDelta%20t%20%5C%5C%20y_%7Bi&plus;1%7D%3Dy_i&plus;v_%7By%2Ci%7D%20%5CDelta%20t%20%5Cend%7Bmatrix%7D%5Cright.)

为了更方便直观的观察轨迹，固定了横纵坐标。所有的常数都是使用课本上的数值，重力加速度选用的是武汉当地数值9.794m/s^2，在以下效果图中有显示。

#### 第一版

先写了一个基本的代码。

运行的效果如图：
![](https://github.com/newton2ndlaw/computationalphysics_N2013301510086/blob/master/Homework6/Homework6-1.png)

基本的程序代码： [链接](https://github.com/newton2ndlaw/computationalphysics_N2013301510086/blob/master/Homework6/Code1-1.md)

为了比较不同的参数所带来轨迹的区别，添加了部分代码。

如图，对比不同角度之间的轨迹与落点的位置，可以得到最远距离的抛射角度。
![](https://github.com/newton2ndlaw/computationalphysics_N2013301510086/blob/master/Homework6/Homework6-3.png)
单独保存的坐标图如下：
![](https://github.com/newton2ndlaw/computationalphysics_N2013301510086/blob/master/Homework6/Homework6-4.png)

如图，对比相同角度，不同步长对最后结果的区别。根据结果可以推断出，时间间隔在0.001s时，精度已经可以达到1m了。
![](https://github.com/newton2ndlaw/computationalphysics_N2013301510086/blob/master/Homework6/Homework6-2.png)

程序代码： [链接](https://github.com/newton2ndlaw/computationalphysics_N2013301510086/blob/master/Homework6/Code1-2.md) 

求最远距离：将时间间隔定为0.001s，可以发现最大值在43deg到45deg之间。
> * theta(deg)  x(m)
> * theta=41    x=24458.8885085
> * theta=42    x=24503.0416323
> * theta=43    x=24525.8416870
> * theta=44    x=24527.1081447
> * theta=45    x=24506.6490545
> * theta=46    x=24464.0696149

继续缩短时间间隔为0.0001s，以此求出43.0deg-45.0deg角度之间的落点位置。
> * theta(deg)     x(m)
> * theta=43.0     x=24525.7873230
> * theta=43.2     x=24527.7863969
> * theta=43.4     x=24528.8941009
> * theta=43.5     x=24529.1310545
> * theta=43.6     x=24529.1497062
> * theta=43.7     x=24528.9700753
> * theta=43.8     x=24528.5515402
> * theta=44.0     x=24527.0778260

经过分析可知最远射程的角度在43.6deg（误差0.1deg），落点位置为24529m（误差0.5m）。

#### 第二版
优化程序之后，可以自动进行批量运算，更加方便地求出结果。
* 删除了输出图像
* 简化了文字的输出
* 提供了更高的精度
* 只需更改源代码中所要求的角度即可

效果图：
!()[]

[第二版程序链接](https://github.com/newton2ndlaw/computationalphysics_N2013301510086/blob/master/Homework6/Code1-3.md)


### 作业L2



### 作业L3




## 结论


## 致谢



