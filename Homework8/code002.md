```python
import matplotlib.pyplot as plt
import numpy as np
from math import *
from pickle import *

print 'Exercise 3.8 The relationship between the amplitude and period V2.1'
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
    print 'Period =',t_thetamax[10]/10,'s'

    print ''
    strtheta = str(Initial_thetasdeg[m1])
    plt.plot(c_t,c_theta,label=strtheta +'deg')

plt.xlabel('t (s)')
plt.ylabel('theta (rad)')
plt.title('Exercise 3.8')
plt.legend()
plt.show()
```
