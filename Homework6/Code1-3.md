```python
#作业2.9
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
Initial_velocity = 700.0
Initial_theta = 0.0


print 'Exercise 2.9 The trajectory V2.0'
print 'Designed by Roach'
print 'Please input the following conditions:'

#输入
def initialize(Initial_theta):
    global Initial_velocity,dt,c_vx,c_vy,c_x,c_y,theta,m
    Initial_theta = Initial_thetas[m]
    dt = 0.0001
    c_vx.append(Initial_velocity * cos(Initial_theta*pi/180))
    c_vy.append(Initial_velocity * sin(Initial_theta*pi/180))
    c_x.append(0.0)
    c_y.append(0.0)
    theta=Initial_theta
    print 'Initial theta =',theta,'deg    ',
    print 'dt=',dt,'s    ',
    return 0

#计算
def calculate(c_vx,c_vy,c_x,c_y,c_v,dt,Constant_Bm,Constant_a,Constant_alpha,Constant_T0,Constant_g):
    i = 0
    while c_y[i] >= 0:
        rho_ratio = ( 1 - Constant_a * c_y[i] / Constant_T0 ) ** Constant_alpha
        c_v.append(( c_vx[i] ** 2 + c_vy[i] ** 2) ** 0.5)
        c_vx.append( c_vx[i] - Constant_Bm * rho_ratio * dt * c_v[i] * c_vx[i])
        c_vy.append( c_vy[i] - Constant_g * dt - Constant_Bm * rho_ratio * dt * c_v[i] * c_vy[i])
        c_x.append( c_x[i] + c_vx[i] * dt)
        c_y.append( c_y[i] + c_vy[i] * dt)
        i=i+1
    print 'Landing point x =',c_x[i],'m    ',
    print 'Total steps =',i,
    return 0

print ''
print ''
print 'The constant numbers are:'
print 'B/m =',Constant_Bm,'m^-1'
print 'a =',Constant_a,'K/m'
print 'alpha =',Constant_alpha,''
print 'T0 =',Constant_T0,'K'
print 'g =',Constant_g,'m/s^2'
print 'velocity =',Initial_velocity,'m/s'
print ''
print ''

Initial_thetas=[43.0,43.1,43.2,43.3,43.4,43.5,43.6,43.7,43.8,43.9]

for m in range (10) :
    c_x = None
    c_y = None
    c_vx = None
    c_vy = None
    c_v = None
    c_x = []
    c_y = []
    c_vx = []
    c_vy = []
    c_v = []
    Initial_theta = 0.0
    print ''
    initialize(Initial_theta)
    calculate(c_vx,c_vy,c_x,c_y,c_v,dt,Constant_Bm,Constant_a,Constant_alpha,Constant_T0,Constant_g)

print ''
```
