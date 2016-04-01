```python
#作业2.9
from math import *
from pylab import *

dt = 0
n = 0
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


print 'Exercise 2.9 The trajectory V1.0'
print 'Designed by Roach'
print 'Please input the following conditions:'

#输入
def initialize(Initial_theta):
    global Initial_velocity,dt,c_vx,c_vy,c_x,c_y
    print 'Initial angle (degree) -> ',
    Initial_theta = float(input())
    print 'Time step dt (second) -> ',
    dt = float(raw_input())
    c_vx.append(Initial_velocity * cos(Initial_theta*pi/180))
    c_vy.append(Initial_velocity * sin(Initial_theta*pi/180))
    c_x.append(0.0)
    c_y.append(0.0)
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
    print ''
    print ''
    print 'The conditions are:'
    print 'theta =',Initial_theta, 'deg'
    print 'dt =',dt,'s'
    print 'B/m =',Constant_Bm,'m^-1'
    print 'a =',Constant_a,'K/m'
    print 'alpha =',Constant_alpha,''
    print 'T0 =',Constant_T0,'K'
    print 'g =',Constant_g,'m/s^2'
    print 'velocity =',Initial_velocity,'m/s'
    print 'The result is:'
    print 'Landing point x =',c_x[i],'m'
    print 'Total steps =',i
    return 0

initialize(Initial_theta)
calculate(c_vx,c_vy,c_x,c_y,c_v,dt,Constant_Bm,Constant_a,Constant_alpha,Constant_T0,Constant_g)

strInitial_theta=str(Initial_theta)

plot(c_x,c_y,linewidth=3,label=strInitial_theta)
xlabel('x (m)',fontsize=20)
ylabel('y (m)',fontsize=20)
title('Exercise 2.9 The trajectory',fontsize=20)
xlim(0, 30000)
ylim(0, 20000)

show()
```
