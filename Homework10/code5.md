```python
import matplotlib.pylab as plt
import time
from math import *

start_time = time.time()

print 'Exercise 3.31 V1.0'
print 'Designed by roach'


dt=0.001


def calculate():
    c_x.append(initial_x)
    c_y.append(initial_y)
    c_vx.append(initial_vx)
    c_vy.append(initial_vy)
    c_t.append(0)
    n=0
    for i in range(1000000):
        c_x.append(c_x[i]+c_vx[i]*dt)
        c_y.append(c_y[i]+c_vy[i]*dt)
        c_vx.append(c_vx[i])
        c_vy.append(c_vy[i])
        c_t.append(c_t[i]+dt)
        if c_x[-1]>1.0 or c_x[-1]<-1.0:
            c_vx[-1]=-c_vx[-1]
        if c_y[-1]>1.0 or c_y[-1]<-1.0:
            c_vy[-1]=-c_vy[-1]
        if c_x[-1]**2+c_y[-1]**2<0.5**2 and n>10:
            v_vertical=c_vx[-1]*c_x[-1]/0.5+c_vy[-1]*c_y[-1]/0.5
            v_verticalx=v_vertical*c_x[-1]/0.5
            v_verticaly=v_vertical*c_y[-1]/0.5
            v_parallelx=c_vx[-1]-v_verticalx
            v_parallely=c_vy[-1]-v_verticaly
            v_verticalx=-v_verticalx
            v_verticaly=-v_verticaly
            c_vx[-1]=v_verticalx+v_parallelx
            c_vy[-1]=v_verticaly+v_parallely
            n=0
        n=n+1
    return 0



c_x=[]
c_y=[]
c_vx=[]
c_vy=[]
c_t=[]
initial_x=0.6
initial_y=0.0
initial_vx=1.0
initial_vy=1.2
calculate()

print 'Total time',c_t[-1]
print 'Time used',time.time() - start_time,'s'

plt.figure(figsize=(20,20))
plt.scatter(c_x,c_y,s=1)
plt.title('Exercise 3.31')
plt.xlabel('x')
plt.ylabel('y')
plt.xlim(-1.2,1.2)
plt.ylim(-1.2,1.2)
plt.legend()
plt.show()
```
