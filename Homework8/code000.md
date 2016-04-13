```python
import matplotlib.pyplot as plt
import numpy as np
from math import *
from pickle import *

print 'Exercise '
print 'Designed by Roach'

c_t = []
c_theta = []
c_omega = []
Initial_theta = 0
Initial_omega = 0
dt = 0.001

Constant_g = 9.794
Constant_l = 1

def initialize(Initial_theta,Initial_omega):
    global c_theta,c_omega
    Initial_theta = Initial_thetas[0]
    Initial_omega = Initial_omegas[0]
    c_theta.append(Initial_theta)
    c_omega.append(Initial_omega)
    c_t.append(0)
    print 'Initial theta =',c_theta[0],'rad'
    print 'Initial omega =',c_omega[0],'rad/s'
    return 0

def calculate(c_theta,c_omega,c_t,dt):
    i = 0
    while c_t[i] <= 50:
        c_omega.append(c_omega[i] - (Constant_g/Constant_l)*c_theta[i]*dt)
        c_theta.append(c_theta[i] + c_omega[i+1]*dt)
        c_t.append(c_t[i]+dt)
        i=i+1
    print 'Total steps =',i,'    ',
    print 'dt =',dt,'s'
    return 0

Initial_thetas = [30*pi/180]
Initial_omegas = [0]

initialize(Initial_theta,Initial_omega)
calculate(c_theta,c_omega,c_t,dt)
 
print 'theta max',max(c_theta),'rad'
print 'theta error',(max(c_theta)/Initial_thetas[0]-1)*100,'% rad'


plt.plot(c_t,c_omega)
plt.show()

```
