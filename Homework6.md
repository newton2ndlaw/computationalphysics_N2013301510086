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

效果如图：
![](https://github.com/newton2ndlaw/computationalphysics_N2013301510086/blob/master/Homework6/Homework6-1.png)

编写为程序： [程序代码链接](https://github.com/newton2ndlaw/computationalphysics_N2013301510086/blob/master/Homework6/Code1-1.md)


## 结论

## 致谢
