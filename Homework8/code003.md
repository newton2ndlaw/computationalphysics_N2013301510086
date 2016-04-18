```python
import matplotlib.pyplot as plt
import numpy as np
from math import *
from pickle import *

print 'Exercise 3.8 The relationship between the amplitude and period V4.0'
print 'Designed by Roach'

c_t = []
c_theta = []
c_omega = []
Initial_theta = 0
Initial_omega = 0
dt = 0.001

Constant_g = 9.794
Constant_l = 1

def Initialize(Initial_theta,Initial_omega):
    global c_theta,c_omega
    c_theta.append(Initial_theta)
    c_omega.append(Initial_omega)
    c_t.append(0)
    print 'Initial theta =',c_theta[0],'rad    ',
    return 0

def Calculate(c_theta,c_omega,c_t,dt):
    i = 0
    for i in range(26000):
        c_omega.append(c_omega[i] - (Constant_g/Constant_l)*sin(c_theta[i])*dt)
        c_theta.append(c_theta[i] + c_omega[i+1]*dt)
        c_t.append(c_t[i]+dt)
        i=i+1
    print 'Total steps =',i,'    ',
    print 'dt =',dt,'s    ',
    return 0

Initial_thetasdeg = []
Initial_thetas = []
for m in range(18):
    Initial_thetasdeg.append( m*5+5 )
    Initial_thetas.append( (m*5+5)*pi/180 )

Initial_omegas = [0]

print 'theta list(deg)',Initial_thetasdeg
print 'theta list(rad)',Initial_thetas

periodlist=[]

for m1 in range(18):
    c_theta = None
    c_omega = None
    t_thetamax = None
    c_t = None
    c_theta = []
    c_omega = []
    t_thetamax = [0]
    c_t = []
    Initial_theta = Initial_thetas[m1]
    Initial_omega = Initial_omegas[0]

    Initialize(Initial_theta,Initial_omega)
    Calculate(c_theta,c_omega,c_t,dt)

    for i in range(1,25999):
        if c_theta[i] > c_theta[i-1] and c_theta[i] > c_theta[i+1]:
            t_thetamax.append(c_t[i])
    sum_y=t_thetamax[0]+t_thetamax[1]+t_thetamax[2]+t_thetamax[3]+t_thetamax[4]+t_thetamax[5]+t_thetamax[6]+t_thetamax[7]+t_thetamax[8]+t_thetamax[9]+t_thetamax[10]
    ave_y=sum_y/11
    sum_x=0+1+2+3+4+5+6+7+8+9+10
    ave_x=sum_x/11
    sum_xy=t_thetamax[1]+2*t_thetamax[2]+3*t_thetamax[3]+4*t_thetamax[4]+5*t_thetamax[5]+6*t_thetamax[6]+7*t_thetamax[7]+8*t_thetamax[8]+9*t_thetamax[9]+10*t_thetamax[10]
    sum_x2=1+2**2+3**2+4**2+5**2+6**2+7**2+8**2+9**2+10**2
    b = (sum_xy-11*ave_x*ave_y)/(sum_x2-11*(ave_x**2))
    a = ave_y - b*ave_x
    r1= (0-ave_x)*(t_thetamax[0]-ave_y)+(1-ave_x)*(t_thetamax[1]-ave_y)+(2-ave_x)*(t_thetamax[2]-ave_y)+(3-ave_x)*(t_thetamax[3]-ave_y)+(4-ave_x)*(t_thetamax[4]-ave_y)+(5-ave_x)*(t_thetamax[5]-ave_y)+(6-ave_x)*(t_thetamax[6]-ave_y)+(7-ave_x)*(t_thetamax[7]-ave_y)+(8-ave_x)*(t_thetamax[8]-ave_y)+(9-ave_x)*(t_thetamax[9]-ave_y)+(10-ave_x)*(t_thetamax[10]-ave_y)
    r2= (((0-ave_x)**2+(1-ave_x)**2+(2-ave_x)**2+(3-ave_x)**2+(4-ave_x)**2+(5-ave_x)**2+(6-ave_x)**2+(7-ave_x)**2+(8-ave_x)**2+(9-ave_x)**2+(10-ave_x)**2)*((t_thetamax[0]-ave_y)**2+(t_thetamax[1]-ave_y)**2+(t_thetamax[2]-ave_y)**2+(t_thetamax[3]-ave_y)**2+(t_thetamax[4]-ave_y)**2+(t_thetamax[5]-ave_y)**2+(t_thetamax[6]-ave_y)**2+(t_thetamax[7]-ave_y)**2+(t_thetamax[8]-ave_y)**2+(t_thetamax[9]-ave_y)**2+(t_thetamax[10]-ave_y)**2))**0.5
    r = r1/r2
    print ''
    print '        T(s) =',b,'* times + ',a,
    print '        r =',r
    periodlist.append(b)
    strtheta = str(Initial_thetasdeg[m1])

print 'Initial theta list',Initial_thetasdeg
print 'period list',periodlist

plt.xlabel('theta (deg)')
plt.ylabel('period (s)')
plt.title('Exercise 3.8 The relationship between the amplitude and period V3.0')
plt.plot(Initial_thetasdeg,periodlist,label='theta')
plt.show()

```
