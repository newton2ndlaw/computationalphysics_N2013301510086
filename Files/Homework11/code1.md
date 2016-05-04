```python
import matplotlib.pylab as plt
import time
from math import *

start_time = time.time()

print """Exercise 4.9 V1.0
Designed by Roach
"""

c_vx=[]
c_vy=[]
c_x=[]
c_y=[]
c_r=[]
c_t=[]

def Calculate():
# initialize
    c_x.append(Initial_x)
    c_y.append(Initial_y)
    c_vx.append(Initial_vx)
    c_vy.append(Initial_vy)
    c_t.append(0.0)
    range_i=int(total_t/dt)
    for i in range(range_i):
        c_r.append((c_x[i]**2+c_y[i]**2)**0.5)
        c_vx.append(c_vx[i]-(4*(pi**2)*c_x[i])*dt/(c_r[i]**(beta+1)))
        c_vy.append(c_vy[i]-(4*(pi**2)*c_y[i])*dt/(c_r[i]**(beta+1)))
        c_x.append(c_x[i]+c_vx[i+1]*dt)
        c_y.append(c_y[i]+c_vy[i+1]*dt)
        c_t.append(i*dt)
    print "Total steps",range_i
    return 0

# initial conditions
Initial_vx=0.0
Initial_vy=2.0*pi
Initial_x=1.0
Initial_y=0.0
beta=2.1
total_t=5.0
dt=0.0001

Calculate()
plt.figure(figsize=(20,20))
plt.xlim(-1.5,1.5)
plt.ylim(-1.5,1.5)
plt.title("Exercise 4.9")
plt.plot(c_x,c_y,color = "blue",label = "trajectory")
plt.scatter(0,0,color = "red",label = "sun")
plt.legend()

total_time = time.time()-start_time
print "Time used",total_time,"s"

plt.show()
```
