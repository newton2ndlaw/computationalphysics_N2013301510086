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
    for i in range(1000000):
        c_x.append(c_x[i]+Constant_sigma*(c_y[i]-c_x[i])*dt)
        c_y.append(c_y[i]+(-c_x[i]*c_z[i]+r*c_x[i]-c_y[i])*dt)
        c_z.append(c_z[i]+(c_x[i]*c_y[i]-Constant_b*c_z[i])*dt)
        c_t.append((i+1)*0.0001)
    return 0

c_x = []
c_y = []
c_z = []
c_t = []
initial_x = 1.0
initial_y = 0.0
initial_z = 0.0
r = 163.8

c_t1=[]
c_z1=[]

Calculate()

print 't        z'
for i in range(1,len(c_t)-1):
    if c_z[i]>c_z[i-1] and c_z[i]>c_z[i+1]:
        c_z1.append(c_z[i])
        c_t1.append(c_t[i])
        print c_t[i],c_z[i]


plt.plot(c_t,c_z)
plt.xlabel('time')
plt.ylabel('z')
plt.title('Exercise 3.29 r=163.8')

print 'Time used',time.time()-start_time,'s'

plt.show()
```
