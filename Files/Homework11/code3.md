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
    for i in range(range_i):
        c_r.append((c_x[i]**2+c_y[i]**2)**0.5)
        c_vx.append(c_vx[i]-(4*(pi**2)*c_x[i])*dt/(c_r[i]**(beta+1)))
        c_vy.append(c_vy[i]-(4*(pi**2)*c_y[i])*dt/(c_r[i]**(beta+1)))
        c_x.append(c_x[i]+c_vx[i+1]*dt)
        c_y.append(c_y[i]+c_vy[i+1]*dt)
        c_t.append(i*dt)
    print "Beta =",beta,"    ",
    return 0

# initial conditions
Initial_vx=0.0
Initial_vy=1.9*pi
Initial_x=1.0
Initial_y=0.0
beta=3.0
total_t=4.0
dt=0.0001

range_i=int(total_t/dt)
print "Total steps =",range_i

# list of beta
betalist=[]
for i in range(1000):
    betalist.append(2.0+i*0.001)

betalist2=[]
anglelist=[]
# find max r
for i in range(len(betalist)):
    c_vx=None
    c_vy=None
    c_x=None
    c_y=None
    c_r=None
    c_t=None 
    c_vx=[]
    c_vy=[]
    c_x=[]
    c_y=[]
    c_r=[]
    c_t=[]
    beta=betalist[i]
    Calculate()
    max_r=None
    max_rx=None
    max_ry=None
    max_r=[]
    max_rx=[]
    max_ry=[]
    for i in range(1,range_i-1):
        if c_r[i]>c_r[i-1] and c_r[i]>c_r[i+1]:
            max_r.append(c_r[i])
            max_rx.append(c_x[i])
            max_ry.append(c_y[i])
    # print "max r",max_r,"AU"
    # print "max rx",max_rx,"AU"
    # print "max ry",max_ry,"AU"
    
    # calculate angle
    if len(max_r)<=1:
        print "None"
    else:
        max_angle=None
        max_angle=[]
        for i in range(len(max_r)):
            max_angle.append(atan(max_ry[i]/max_rx[i]))
   #    print "max angle",max_angle,"rad"
        delta_angle=abs(max_angle[1]-max_angle[0])
        if delta_angle>pi/2:
            delta_angle=pi-delta_angle
        anglelist.append(delta_angle)
        betalist2.append(beta)
        print "Theta =",delta_angle,"rad"

# strbeta=str(beta)

# plt.figure(figsize=(20,20))
# plt.xlim(-2.0,2.0)
# plt.ylim(-2.0,2.0)
# plt.xlabel("x(AU)")
# plt.ylabel("y(AU)")
# plt.title("Simulation of elliptical orbit")
# plt.text(-1.8,1.8,"beta="+strbeta)
# 
# plt.scatter(max_rx,max_ry,color = "green")
# plt.scatter(c_x,c_y,color = "blue",label = "trajectory",s=1)
# plt.scatter(0,0,color = "red",label = "sun")
# 
# plt.legend()

plt.figure(figsize=(24,18))
plt.plot(betalist2,anglelist)
plt.xlabel("beta")
plt.ylabel("theta(rad)")
plt.title("Exercise 4.9")


total_time = time.time()-start_time
print "Time used",total_time,"s"

plt.show()
```
