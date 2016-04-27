```python
import matplotlib.pylab as plt
import time
from math import *

start_time = time.time()

print 'Exercise 3.29 V1.0'
print 'Designed by roach'

Constant_b = 8.0/3.0
Constant_sigma = 10.0
dt = 0.0001


def Calculate():
    c_x.append(initial_x)
    c_y.append(initial_y)
    c_z.append(initial_z)
    c_t.append(0)
    for i in range(500000):
        c_x.append(c_x[i]+Constant_sigma*(c_y[i]-c_x[i])*dt)
        c_y.append(c_y[i]+(-c_x[i]*c_z[i]+r*c_x[i]-c_y[i])*dt)
        c_z.append(c_z[i]+(c_x[i]*c_y[i]-Constant_b*c_z[i])*dt)
        c_t.append(c_t[i]+dt)
    return 0

c_x = []
c_y = []
c_z = []
c_t = []
initial_x = 1.0
initial_y = 0.0
initial_z = 0.0
r = 163

Calculate()


plt.plot(c_t,c_z)
plt.xlabel('time')
plt.ylabel('z')
plt.title('Exercise 3.29 r=160')

print 'Time used',time.time()-start_time,'s'

plt.show()
```
