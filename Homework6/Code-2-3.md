```python
#作业2.10
from math import *
from pylab import *
from matplotlib.pylab import *
import pickle
import matplotlib.pyplot as plt
import numpy as np
import pylab as pl

dt = 0
c_x = []
c_y = []
c_vx = []
c_vy = []
c_v = []
Constant_Bm = 4.0*10**(-5)
Constant_a = 6.5*10**(-3)
Constant_alpha = 2.5
Constant_T0 = 300
Constant_g = 9.794
Initial_velocity = 0.0
Initial_theta = 0.0

luodian_x = 20000
luodian_y = 1000

#版本信息
print 'Exercise 2.9 The trajectory V3.0'
print 'Designed by Roach'
print 'Please input the following conditions:'

#输入函数
def initialize(Initial_theta,Initial_velocity):
    global dt,c_vx,c_vy,c_x,c_y,theta,m,velocity
    Initial_theta = Initial_thetas[m1]
    Initial_velocity = Initial_velocitys[m2]
    dt = 0.01
    c_vx.append(Initial_velocity * cos(Initial_theta*pi/180))
    c_vy.append(Initial_velocity * sin(Initial_theta*pi/180))
    c_x.append(0.0)
    c_y.append(0.0)
    velocity=Initial_velocity
    theta=Initial_theta
    print 'Initial velocity =',velocity,'m/s    ',
    print 'Initial theta =',theta,'deg    ',
    return 0

#计算函数
def calculate(c_vx,c_vy,c_x,c_y,c_v,dt,Constant_Bm,Constant_a,Constant_alpha,Constant_T0,Constant_g):
    i = 0
#上升阶段
    while c_y[i] >= 0 and c_vy[i]>0:
        rho_ratio = ( 1 - Constant_a * c_y[i] / Constant_T0 ) ** Constant_alpha
        c_v.append(( c_vx[i] ** 2 + c_vy[i] ** 2) ** 0.5)
        c_vx.append( c_vx[i] - Constant_Bm * rho_ratio * dt * c_v[i] * c_vx[i])
        c_vy.append( c_vy[i] - Constant_g * dt - Constant_Bm * rho_ratio * dt * c_v[i] * c_vy[i])
        c_x.append( c_x[i] + c_vx[i] * dt)
        c_y.append( c_y[i] + c_vy[i] * dt)
        i=i+1
#下降阶段
    while c_y[i] >= luodian_y :
        rho_ratio = ( 1 - Constant_a * c_y[i] / Constant_T0 ) ** Constant_alpha
        c_v.append(( c_vx[i] ** 2 + c_vy[i] ** 2) ** 0.5)
        c_vx.append( c_vx[i] - Constant_Bm * rho_ratio * dt * c_v[i] * c_vx[i])
        c_vy.append( c_vy[i] - Constant_g * dt - Constant_Bm * rho_ratio * dt * c_v[i] * c_vy[i])
        c_x.append( c_x[i] + c_vx[i] * dt)
        c_y.append( c_y[i] + c_vy[i] * dt)
        i=i+1
    print 'Landing point x =',c_x[-1],'m    ',
    print 'y =',c_y[-1],'m    ',
    print 'Total steps =',i,
    print '    dt =',dt,'s',
    return 0

print ''
print ''
print 'The constant numbers are:'
print 'B/m =',Constant_Bm,'m^-1'
print 'a =',Constant_a,'K/m'
print 'alpha =',Constant_alpha,''
print 'T0 =',Constant_T0,'K'
print 'g =',Constant_g,'m/s^2'
print ''
print ''

#要求的角度0-90
Initial_thetas=[]
for i_theta in range (19):
    Initial_thetas.append(i_theta*5)

#要求的速度500-1000
Initial_velocitys=[]
for i_velocity in range (51):
    Initial_velocitys.append(i_velocity*10+500)

result_velocity=[]
result_theta=[]
result_x=[]
result_y=[]


for m2 in range (51) :
    for m1 in range (19):
#每一次计算之前，清除数组
        c_x = None
        c_y = None
        c_vx = None
        c_vy = None
        c_x = []
        c_y = []
        c_vx = []
        c_vy = []
        c_v = []
        print ''
        initialize(Initial_theta,Initial_velocity)
        calculate(c_vx,c_vy,c_x,c_y,c_v,dt,Constant_Bm,Constant_a,Constant_alpha,Constant_T0,Constant_g)
        result_velocity.append(Initial_velocitys[m2])
        result_theta.append(Initial_thetas[m1])
        result_x.append(c_x[-1])
        result_y.append(c_y[-1])
print ''

xabs=[]
yabs=[]
result_velocity1=[]
result_theta1=[]

#删掉达不到目标点的数据
for n in range (len(result_x)):
    if abs(result_y[n] - luodian_y) < 10 and result_x[n] - luodian_x > 0:
        yabs.append(abs(result_y[n] - luodian_y))
        xabs.append(abs(result_x[n] - luodian_x))
        result_velocity1.append(result_velocity[n])
        result_theta1.append(result_theta[n])

#找出最小的可以到达目标的速度
for n in range (len(xabs)):
    if min(result_velocity1) == result_velocity1[n]:
        minlabel = n

print 'min velocity',result_velocity1[minlabel]
print 'theta',result_theta1[minlabel]
print 'xabs',xabs[minlabel]
print 'yabs',yabs[minlabel]

#进一步细化要求的角度
Initial_thetas=None
Initial_thetas=[]
for i_theta in range (100):
    Initial_thetas.append(i_theta*0.1+result_theta1[minlabel]-5)
print Initial_thetas

#固定速度
Initial_velocitys=None
Initial_velocitys=[]
Initial_velocitys.append(result_velocity1[minlabel])
velocityresult1=result_velocity1[minlabel]

result_x = None
result_y = None
result_theta = None
result_x = []
result_y = []
result_theta = []
xabs = None
yabs = None
result_velocity1 = None
result_theta1 = None
xabs = []
yabs = []
result_velocity1 = []
result_theta1 = []

#这一次只对角度进行循环
for m1 in range (100):
#每一次计算之前，清除数组
    c_x = None
    c_y = None
    c_vx = None
    c_vy = None
    c_x = []
    c_y = []
    c_vx = []
    c_vy = []
    c_v = []
    print ''
    m2=0
    initialize(Initial_theta,result_velocity)
    calculate(c_vx,c_vy,c_x,c_y,c_v,dt,Constant_Bm,Constant_a,Constant_alpha,Constant_T0,Constant_g)
    result_theta.append(Initial_thetas[m1])
    result_x.append(c_x[-1])
    result_y.append(c_y[-1])
print ''

for n in range (len(result_x)):
    if abs(result_y[n] - luodian_y) < 100 :
        yabs.append(abs(result_y[n] - luodian_y))
        xabs.append(abs(result_x[n] - luodian_x))
        result_velocity1.append(result_velocity[n])
        result_theta1.append(result_theta[n])


for n in range (len(xabs)):
    if min(xabs) == xabs[n]:
        minlabel = n

#输出最好的发射速度和角度：
print ''
print 'Final result is:'
print 'min velocity = ',velocityresult1,'m/s'
print 'The best theta = ',result_theta1[minlabel],'deg'
print 'error x = ',xabs[minlabel],'m'
print 'error y = ',yabs[minlabel],'m'

#速度误差5%与角度误差5%的时候：
m1=0
m2=0

Initial_velocitys=None
Initial_velocitys=[velocityresult1*0.95,velocityresult1,velocityresult1*1.05]
Initial_thetas=None
Initial_thetas=[result_theta1[minlabel]-1,result_theta1[minlabel],result_theta1[minlabel]+1]

result_x = None
result_y = None
result_theta = None
result_x = []
result_y = []
result_theta = []
xabs = None
yabs = None
result_velocity1 = None
result_theta1 = None
xabs = []
yabs = []
result_velocity1 = []
result_theta1 = []

for m2 in range (3) :
    for m1 in range (3):
#每一次计算之前，清除数组
        c_x = None
        c_y = None
        c_vx = None
        c_vy = None
        c_x = []
        c_y = []
        c_vx = []
        c_vy = []
        c_v = []
        print ''
        initialize(Initial_theta,Initial_velocity)
        calculate(c_vx,c_vy,c_x,c_y,c_v,dt,Constant_Bm,Constant_a,Constant_alpha,Constant_T0,Constant_g)
        result_velocity.append(Initial_velocitys[m2])
        result_theta.append(Initial_thetas[m1])
        result_x.append(c_x[-1])
        result_y.append(c_y[-1])
        plot(c_x,c_y)
print ''

#找出误差值
for n in range (len(result_x)):
    if abs(result_y[n] - luodian_y) < 100 :
        yabs.append(abs(result_y[n] - luodian_y))
        xabs.append(abs(result_x[n] - luodian_x))
        result_velocity1.append(result_velocity[n])
        result_theta1.append(result_theta[n])

print 'Landing point x min is ',min(result_x),'m    max is ',max(result_x),'m'
print 'The maximum error is ',max(xabs),'m'

plt.scatter(luodian_x,luodian_y)
xlabel('x (m)')
ylabel('y (m)')
title('Problem 2.10')
show()
```
