# Homework 6

张琦 2013301510086

## 摘要

完成一个“辅助精确打击系统”。

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
![](https://github.com/newton2ndlaw/computationalphysics_N2013301510086/blob/master/Homework6/Homework6-5.png)

[第二版程序链接](https://github.com/newton2ndlaw/computationalphysics_N2013301510086/blob/master/Homework6/Code1-3.md)


### 作业L2

2.10 Generalize the program developed for the previous problem so that it can deal with situations in which the target is at a different altitude than the cannon. Consider cases in which the target is higher and lower than the cannon. Also investigate how the minimum firing velocity required to hit the target varies as the altitude of the target is varied.
大概的意思是？概括项目开发之前的问题,以便它可以处理情况下,目标是在一个不同的高度比大炮。考虑的情况下,目标是高于和低于大炮。还研究如何达到目标所需的最小发射速度不同高度的目标是不同的。

我的理解是要求最小速度与目标位置的关系。程序实现：输入一个高度便能自动得到所需的最低速度和出射角度。经过分析可以知道，最小速度的时候，炮弹到达目标的时候，恰好垂直方向上的速度为0。

要得到射到指定高度上的目标，先制作了一个简易的程序，效果如图：

![](https://github.com/newton2ndlaw/computationalphysics_N2013301510086/blob/master/Homework6/Homework6-6.png)

数据部分：


> * Initial theta = 5 deg     dt= 0.001 s     Landing point x = 3729.78608099 m     Landing point y = 171.233405637 m     Total steps = 5767
> * Initial theta = 10 deg     dt= 0.001 s     Landing point x = 6530.81474873 m     Landing point y = 624.79692499 m     Total steps = 10814
> * Initial theta = 15 deg     dt= 0.001 s     Landing point x = 8706.56332415 m     Landing point y = 1295.9757895 m     Total steps = 15362
> * Initial theta = 20 deg     dt= 0.001 s     Landing point x = 12712.9631596 m     Landing point y = 1999.99763227 m     Total steps = 24966
> * Initial theta = 25 deg     dt= 0.001 s     Landing point x = 17514.5284415 m     Landing point y = 1999.9052618 m     Total steps = 39100
> * Initial theta = 30 deg     dt= 0.001 s     Landing point x = 20125.6054058 m     Landing point y = 1999.87741431 m     Total steps = 49297
> * Initial theta = 35 deg     dt= 0.001 s     Landing point x = 21818.1101445 m     Landing point y = 1999.81466149 m     Total steps = 58180
> * Initial theta = 40 deg     dt= 0.001 s     Landing point x = 22819.6233024 m     Landing point y = 1999.97705333 m     Total steps = 66210
> * Initial theta = 45 deg     dt= 0.001 s     Landing point x = 23198.8105218 m     Landing point y = 1999.99977243 m     Total steps = 73547
> * Initial theta = 50 deg     dt= 0.001 s     Landing point x = 22967.8650832 m     Landing point y = 1999.97166764 m     Total steps = 80243
> * Press any key to continue . . .


可以看出某些角度度下，根本无法达到目标的高度。同时也可以看出，达到目标高度的时候，所达到最大的高度时，只有水平方向上的速度。

**重大更新，完成了输入打击点的位置，给出速度和角度的功能**

更改了大量代码之后，考虑到实际炮弹的运行速度，因此具体执行过程是速度计算从500-1000m/s，对应每个角度扫遍0-90°。初步定出最低速度后，再减小角度的间隔，找出最佳角度。为了保证计算效率，因此速度的精度选择在10m/s，角度的精度在0.1°。考虑到运算时间较长，因此保留了每计算一次输出的信息。
运行了几次之后，发现结果误差均在5m以内，考虑到炮弹爆炸的范围比5m大，因此根据该模型炮弹可以精确打击到目标。

* 只需要更改代码中的luodian_x与luodian_y的数值，即可得到要打击地点所需求的发射速度和初始角度。
* 更改要求速度和角度数值的最小间隔，即可更改最后计算精度。
* 时间间隔选为0.01s已经足够精确了，它引起的误差在1m以内。


以下例子选取的打击点为
**x=20000m，y=1000m**

效果图：所求得的轨迹用蓝色线表示，要打击的点用蓝色圆点表示。

![](https://github.com/newton2ndlaw/computationalphysics_N2013301510086/blob/master/Homework6/Homework6-2-1.png)

误差图：
> * Final result is:
> * min velocity =  620 m/s
> * The best theta =  50.2 deg
> * error x =  2.34366446801 m
> * error y =  0.489940326464 m


![](https://github.com/newton2ndlaw/computationalphysics_N2013301510086/blob/master/Homework6/Homework6-2-2.png)

完整的输出内容太多，因此给出链接：
[结果的链接](https://github.com/newton2ndlaw/computationalphysics_N2013301510086/blob/master/Homework6/data2.txt)

代码链接：
[Code](https://github.com/newton2ndlaw/computationalphysics_N2013301510086/blob/master/Homework6/Code2-1.md)

其他的例子结果如图：

**x=15000m y=1500m**
> * Final result is:
> * min velocity =  510 m/s
> * The best theta =  48.4 deg
> * error x =  0.16015657806 m
> * error y =  1.18356369012 m

![](https://github.com/newton2ndlaw/computationalphysics_N2013301510086/blob/master/Homework6/Homework6-2-3.png)


**x=23456m y=1234m**
> * Final result is:
> * min velocity =  700 m/s
> * The best theta =  49.6 deg
> * error x =  3.54463554191 m
> * error y =  0.944241171886 m

![](https://github.com/newton2ndlaw/computationalphysics_N2013301510086/blob/master/Homework6/Homework6-2-4.png)

* 如果要继续提高精度，直接减小角度的间隔与速度的间隔即可，但会导致运行时间很长，暂时没有想到特别好的优化计算速度的方法。
* 考虑到扫遍500-1000m/s，0-90°，所花的时间比较长，可以单独将其结果输出为一个文件，之后只用查阅该文件就可以了，这个方法可以节省大量时间。并且可以将节省出来的时间花在更精细的其他运算上，以提高精度和效率。

同样是选取的打击点为**x=20000m，y=1000m**，将精确度调为速度2m/s，角度0.02deg，所得结果对比如下：

精确度 10m/s 0.1deg 用时 1:20
> * Final result is:                     
> * min velocity =  620 m/s  
> * The best theta =  50.2 deg        
> * error x =  2.34366446801 m          
> * error y =  0.489940326464 m     


精确度 10m/s 0.1deg 用时 8:30
> * Final result is:
> * min velocity =  614 m/s  
> * The best theta =  47.16 deg
> * error x =  0.378643408018 m     
> * error y =  0.160188358397 m



### 作业L3

考虑炮弹初始发射的时候发射角度误差1%，速度有5%的误差，风阻误差10%

暂时先只考虑发射角度的变化1°左右，速度变化5%。更改最后部分的代码，即可得到各种误差速度和角度的组合所求得的曲线。

以下例子选取的打击点为
**x=20000m，y=1000m**
结果图：

![](https://github.com/newton2ndlaw/computationalphysics_N2013301510086/blob/master/Homework6/Homework6-3-1.png)

所得的数据如下：
> * Final result is:
> * min velocity =  620 m/s
> * The best theta =  50.2 deg
> * error x =  2.34366446801 m
> * error y =  0.489940326464 m
> * Initial velocity = 589.0 m/s     Initial theta = 49.2 deg     Landing point x = 18747.5936833 m     y = 999.16025653 m     Total steps = 7185     dt = 0.01 s
> * Initial velocity = 589.0 m/s     Initial theta = 50.2 deg     Landing point x = 18644.6093633 m     y = 998.761294321 m     Total steps = 7295     dt = 0.01 s
> * Initial velocity = 589.0 m/s     Initial theta = 51.2 deg     Landing point x = 18522.3090066 m     y = 997.776985987 m     Total steps = 7403     dt = 0.01 s
> * Initial velocity = 620 m/s     Initial theta = 49.2 deg     Landing point x = 20108.4695368 m     y = 996.94047375 m     Total steps = 7487     dt = 0.01 s
> * Initial velocity = 620 m/s     Initial theta = 50.2 deg     Landing point x = 19997.6563355 m     y = 999.510059674 m     Total steps = 7600     dt = 0.01 s
> * Initial velocity = 620 m/s     Initial theta = 51.2 deg     Landing point x = 19868.2598149 m     y = 998.224137667 m     Total steps = 7712     dt = 0.01 s
> * Initial velocity = 651.0 m/s     Initial theta = 49.2 deg     Landing point x = 21470.9066587 m     y = 998.907980567 m     Total steps = 7779     dt = 0.01 s
> * Initial velocity = 651.0 m/s     Initial theta = 50.2 deg     Landing point x = 21356.8769746 m     y = 998.121805234 m     Total steps = 7897     dt = 0.01 s
> * Initial velocity = 651.0 m/s     Initial theta = 51.2 deg     Landing point x = 21219.4571796 m     y = 999.741794601 m     Total steps = 8012     dt = 0.01 s
> * Landing point x min is  18522.3090066 m    max is  21470.9066587 m
> * The maximum error is  1477.69099344 m


代码链接：
[Code](https://github.com/newton2ndlaw/computationalphysics_N2013301510086/blob/master/Homework6/Code2-3.md)

根据图中可以看出速度误差5%造成的影响远远比角度误差1%造成的影响要大得多。1%角度的误差范围内尚能保证炮弹命中目标，但是5%的速度误差将会导致炮弹在大部分的结果中偏离目标1000m以上。因此实际应用中要连续发射多枚炮弹才能击中目标。

程序暂时写到这里，科里奥利力和风阻随后再加入。

## 结论

可以利用python编写“辅助精确打击系统”，在一个比较简答的模型下来计算炮弹的轨迹，以及通过打击点来获得初始速度和角度。但本次作业所使用方法的效率太低，尽管经过了优化，但是运行时间仍然需要一分钟以上。增加精度只需要减少扫描的间隔即可，但是考虑到运算时间将大幅度增加。过长的运算时间将在实际应用中将失去意义。

## 致谢

以上内容均为原创，未参考任何同学的程序和思路。



