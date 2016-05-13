```python
import matplotlib.pylab as plt
import time,sys
from math import *

start_time = time.time()

print """Exercise 4.16
Designed by Roach
"""

#Constants
constantme=6.0*(10**24)
constantmj=1.9*(10**27)*100
constantms=2.0*(10**30)
dt=0.0001
t=100


#Initial
initial_cvex=0.0
initial_cvey=2.0*pi
initial_cex=1.0
initial_cey=0.0

initial_cvjx=0.0
initial_cvjy=2.0*pi*5.2/11.86
initial_cjx=5.2
initial_cjy=0.0

#Total momentum zero
initial_cvsx=0.0
initial_cvsy= -(constantme*initial_cvey+constantmj*initial_cvjy)/constantms
initial_csx=0.0
initial_csy=0.0

cvex=[]
cvey=[]
cex=[]
cey=[]

cvjx=[]
cvjy=[]
cjx=[]
cjy=[]

cvsx=[]
cvsy=[]
csx=[]
csy=[]

def Calculate():
    cvex.append(initial_cvex)
    cvey.append(initial_cvey)
    cex.append(initial_cex)
    cey.append(initial_cey)
    cvjx.append(initial_cvjx)
    cvjy.append(initial_cvjy)
    cjx.append(initial_cjx)
    cjy.append(initial_cjy)
    cvsx.append(initial_cvsx)
    cvsy.append(initial_cvsy)
    csx.append(initial_csx)
    csy.append(initial_csy)
    rangei=int(t/dt)
    n=0
    for i in range(rangei):
        rse=((csx[i]-cex[i])**2+(csy[i]-cey[i])**2)**0.5
        res=rse
        rje=((cjx[i]-cex[i])**2+(cjy[i]-cey[i])**2)**0.5
        rej=rje
        rsj=((csx[i]-cjx[i])**2+(csy[i]-cjy[i])**2)**0.5
        rjs=rsj
        #Earth
        cvex.append(cvex[i]+(4*pi*pi*(csx[i]-cex[i])/(rse**3)+4*pi*pi*(constantmj/constantms)*(cjx[i]-cex[i])/(rje**3))*dt)
        cvey.append(cvey[i]+(4*pi*pi*(csy[i]-cey[i])/(rse**3)+4*pi*pi*(constantmj/constantms)*(cjy[i]-cey[i])/(rje**3))*dt)
        #Jupiter
        cvjx.append(cvjx[i]+(4*pi*pi*(constantme/constantms)*(cex[i]-cjx[i])/(rej**3)+4*pi*pi*(csx[i]-cjx[i])/(rsj**3))*dt)
        cvjy.append(cvjy[i]+(4*pi*pi*(constantme/constantms)*(cey[i]-cjy[i])/(rej**3)+4*pi*pi*(csy[i]-cjy[i])/(rsj**3))*dt)
        #Sun
        cvsx.append(cvsx[i]+(4*pi*pi*(constantmj/constantms)*(cjx[i]-csx[i])/(rjs**3)+4*pi*pi*(constantme/constantms)*(cex[i]-csx[i])/(res**3))*dt)
        cvsy.append(cvsy[i]+(4*pi*pi*(constantmj/constantms)*(cjy[i]-csy[i])/(rjs**3)+4*pi*pi*(constantme/constantms)*(cey[i]-csy[i])/(res**3))*dt)
        #Position
        cex.append(cex[i]+cvex[i+1]*dt)
        cey.append(cey[i]+cvey[i+1]*dt)
        cjx.append(cjx[i]+cvjx[i+1]*dt)
        cjy.append(cjy[i]+cvjy[i+1]*dt)
        csx.append(csx[i]+cvsx[i+1]*dt)
        csy.append(csy[i]+cvsy[i+1]*dt)
        if i == n*int(rangei/100):
            sys.stdout.write("\rPercent:%d%%" %(n))
            n=n+1

Calculate()
plt.figure(figsize=(20,20))
plt.xlim(-7,7)
plt.ylim(-7,7)
plt.xlabel("x(AU)")
plt.ylabel("y(AU)")
plt.title("Exercise 4.16")

plt.plot(csx,csy,label="Sun",color= "red")
plt.plot(cex,cey,label="Earth",color ="blue")
plt.plot(cjx,cjy,label="Jupiter",color ="brown")

plt.legend()

total_time=time.time()-start_time
print ""
print "Time used",total_time,"s"

plt.show()
```
