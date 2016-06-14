#1
```python
import matplotlib.pyplot as plt
from math import *

print 'Final test V1.0'
print 'Designed by Roach'

Constant_g=9.8
Constant_l=9.8
Constant_q=0.5
Constant_Omegad=2.0/3.0

dt = 0.001
total_t=100
c_t = []
c_theta = []
c_omega = []
N=int(total_t/dt)

def Calculate():
    c_theta.append(Initial_theta)
    c_omega.append(Initial_omega)
    c_t.append(0.0)
    print 'Initial_theta =',c_theta[0],'rad    ',
    print 'Initial_omega =',c_omega[0],'rad/s    ',
    print 'F_d =',F_d,'N    ',
    for i in range(N):
        c_omega.append(c_omega[i]-(sin(c_theta[i])+Constant_q*c_omega[i]-F_d*sin(Constant_Omegad*c_t[i]))*dt)
        c_theta.append(c_theta[i]+c_omega[i+1]*dt)
        c_t.append(c_t[i]+dt)
        if c_theta[-1]>pi:
            c_theta[-1]=c_theta[-1]-2*pi
        if c_theta[-1]<-pi:
            c_theta[-1]=c_theta[-1]+2*pi
    print 'Total steps =',i,'    ',
    print 'dt =',dt
    return 0

Initial_theta=0.2
Initial_omega=0.0
F_dlist=[0,0.5,1.2]


F_dlist=[1.35,1.44,1.465]
    
plt.figure(figsize=(20,6))

for m in range(3):
    c_t = None
    c_theta = None
    c_omega = None
    c_t = []
    c_theta = []
    c_omega = []
    F_d=F_dlist[m]
    F_dstr=str(F_d)
    Calculate()
    plt.subplot(1,3,m+1)
 #   plt.title(r"$\omega$ versus time")
    plt.title(r"$\theta$ versus time")
    plt.plot(c_t,c_theta,label="$F_D$"+"="+F_dstr,color ='black')
    plt.ylim(-4,4)
    plt.xlim(0,100)
    plt.xlabel('t (s)')
  #  plt.ylabel(r"$\omega$ (radians/s)")
    plt.ylabel(r"$\theta$ (radians)")
    plt.legend()

plt.show()


```

#2
```python
import matplotlib.pyplot as plt
from math import *
import time

starttime=time.time()
print 'Final test V1.0'
print 'Designed by Roach'

Constant_g=9.8
Constant_l=9.8
Constant_q=0.5
Constant_Omegad=2.0/3.0

dt = 0.01
total_t=300
c_t = []
c_theta = []
c_omega = []
N=int(total_t/dt)

def Calculate():
    c_theta.append(Initial_theta)
    c_omega.append(Initial_omega)
    c_t.append(0.0)
#   print 'Initial_theta =',c_theta[0],'rad    ',
#   print 'Initial_omega =',c_omega[0],'rad/s    ',
    print 'F_d =',F_d,'N    ',
    for i in range(N):
        c_omega.append(c_omega[i]-(sin(c_theta[i])+Constant_q*c_omega[i]-F_d*sin(Constant_Omegad*c_t[i]))*dt)
        c_theta.append(c_theta[i]+c_omega[i+1]*dt)
        c_t.append(c_t[i]+dt)
        if c_theta[-1]>pi:
            c_theta[-1]=c_theta[-1]-2*pi
        if c_theta[-1]<-pi:
            c_theta[-1]=c_theta[-1]+2*pi
    print 'Total steps =',i,'    ',
    print 'dt =',dt
    return 0

Initial_theta=0.2
Initial_omega=0.0

F_dlist=[]
F_dmin=1.4906
F_dmax=1.4907
F_dN=int((F_dmax-F_dmin)/0.000001)
for i in range(F_dN):
    F_dlist.append(F_dmin+0.000001*i)
print F_dlist
print len(F_dlist)

result_fd=[]
result_theta=[]


for m in range(len(F_dlist)):
    print m+1,".    ",
    c_t = None
    c_theta = None
    c_omega = None

    c_t = []
    c_theta = []
    c_omega = []
    F_d=F_dlist[m]
    F_dstr=str(F_d)
    Calculate()
    for i in range(int(250/dt),N-1):
        if c_theta[i]>c_theta[i-1] and c_theta[i]>c_theta[i+1] and c_theta[i] < 3.1:
            result_theta.append(c_theta[i])
            result_fd.append(F_d)

print ""
print "Time used",time.time()-starttime,"s"

plt.figure(figsize=(12,9))
plt.title("Bifurcation diagram (theta versus F_D)")
plt.scatter(result_fd,result_theta,s=1)
#plt.ylim(1,3)
#plt.xlim(1.4,1.5)
plt.xlabel('F_D')
plt.ylabel(r'$\theta$ (radians)')

plt.show()
```
#3
```python
import matplotlib.pyplot as plt
from math import *
import copy

print 'Final test V1.0'
print 'Designed by Roach'

Constant_g=9.8
Constant_l=9.8
Constant_q=0.5
Constant_Omegad=2.0/3.0

dt = 0.001
total_t=100
c_t = []
c_theta = []
c_omega = []
N=int(total_t/dt)

def Calculate():
    c_theta.append(Initial_theta)
    c_omega.append(Initial_omega)
    c_t.append(0.0)
    print 'Initial_theta =',c_theta[0],'rad    ',
    print 'Initial_omega =',c_omega[0],'rad/s    ',
    print 'F_d =',F_d,'N    ',
    for i in range(N):
        c_omega.append(c_omega[i]-(sin(c_theta[i])+Constant_q*c_omega[i]-F_d*sin(Constant_Omegad*c_t[i]))*dt)
        c_theta.append(c_theta[i]+c_omega[i+1]*dt)
        c_t.append(c_t[i]+dt)
        if c_theta[-1]>pi:
            c_theta[-1]=c_theta[-1]-2*pi
        if c_theta[-1]<-pi:
            c_theta[-1]=c_theta[-1]+2*pi
    print 'Total steps =',i,'    ',
    print 'dt =',dt
    return 0

Initial_theta=0.2
Initial_omega=0.0
F_dlist=[0,0.5,1.2]
#F_dlist=[1.35,1.44,1.465]


calculateresult1=[]
calculateresult2=[]
calculatedelta=[]
plt.figure(figsize=(20,6))

for m in range(3):
    c_t = None
    c_theta = None
    c_omega = None
    c_t = []
    c_theta = []
    c_omega = []
    calculateresult1=None
    calculateresult2=None
    calculatedelta=None
    calculateresult1=[]
    calculateresult2=[]
    calculatedelta=[]
    F_d=F_dlist[m]
    F_dstr=str(F_d)

    Initial_theta=0.2
    Calculate()
    calculateresult1=copy.deepcopy(c_theta)

    c_t = None
    c_theta = None
    c_omega = None
    c_t = []
    c_theta = []
    c_omega = []

    Initial_theta=0.2+0.001
    Calculate()
    calculateresult2=copy.deepcopy(c_theta)

    for i in range(len(calculateresult1)):
        calculatedelta.append(abs(calculateresult1[i]-calculateresult2[i]))

    plt.subplot(1,3,m+1)
#    plt.title(r"$\omega$ versus time")
    plt.title(r"$\Delta$"+r"$\theta$ versus time")
    plt.plot(c_t,calculatedelta,label="$F_D$"+"="+F_dstr)
#   plt.ylim(-4,4)
    plt.semilogy()
    plt.xlim(0,100)
    plt.xlabel('t (s)')
 #   plt.ylabel(r"$\omega$ (radians/s)")
    plt.ylabel(r"$\Delta$"+r"$\theta$ (radians)")
    plt.legend()

plt.show()
```
#4
```python
import matplotlib.pyplot as plt
from math import *

print 'Final test V1.0'
print 'Designed by Roach'

Constant_g=9.8
Constant_l=9.8
Constant_q=0.5
Constant_Omegad=2.0/3.0

dt = 0.01
total_t=500
c_t = []
c_theta = []
c_omega = []
N=int(total_t/dt)

def Calculate():
    c_theta.append(Initial_theta)
    c_omega.append(Initial_omega)
    c_t.append(0.0)
    print 'Initial_theta =',c_theta[0],'rad    ',
    print 'Initial_omega =',c_omega[0],'rad/s    ',
    print 'F_d =',F_d,'N    ',
    for i in range(N):
        c_omega.append(c_omega[i]-(sin(c_theta[i])+Constant_q*c_omega[i]-F_d*sin(Constant_Omegad*c_t[i]))*dt)
        c_theta.append(c_theta[i]+c_omega[i+1]*dt)
        c_t.append(c_t[i]+dt)
        if c_theta[-1]>pi:
            c_theta[-1]=c_theta[-1]-2*pi
        if c_theta[-1]<-pi:
            c_theta[-1]=c_theta[-1]+2*pi
    print 'Total steps =',i,'    ',
    print 'dt =',dt
    return 0


Initial_theta=0.2
Initial_omega=0.0
F_dlist=[0,1.4906,1.4907]
#F_dlist=[1.35,1.44,1.465]

plt.figure(figsize=(20,8))

for m in range(1,3):
    c_t = None
    c_theta = None
    c_omega = None
    c_t = []
    c_theta = []
    c_omega = []
    F_d=F_dlist[m]
    F_dstr=str(F_d)
    Calculate()
    plt.subplot(1,2,m)
    plt.title(r"$\omega$"+" versus "+r"$\theta$")
#   plt.title(r"$\theta$ versus time")
    plt.scatter(c_theta,c_omega,label="$F_D$"+"="+F_dstr,s=1)

    plt.xlabel(r"$\theta$ (radians)")
    plt.ylabel(r"$\omega$ (radians/s)")
#   plt.ylabel(r"$\theta$ (radians)")
    plt.legend()

plt.show()
```
#5
```python
import matplotlib.pyplot as plt
from math import *

print 'Final test V1.0'
print 'Designed by Roach'

Constant_g=9.8
Constant_l=9.8
Constant_q=0.5
Constant_Omegad=2.0/3.0

dt = pi/300
total_t=30000
c_t = []
c_theta = []
c_omega = []
N=int(total_t/dt)

def Calculate():
    c_theta.append(Initial_theta)
    c_omega.append(Initial_omega)
    c_t.append(0.0)
    print 'Initial_theta =',c_theta[0],'rad    ',
#   print 'Initial_omega =',c_omega[0],'rad/s    ',
    print 'F_d =',F_d,'N    ',
    for i in range(N):
        c_omega.append(c_omega[i]-(sin(c_theta[i])+Constant_q*c_omega[i]-F_d*sin(Constant_Omegad*c_t[i]))*dt)
        c_theta.append(c_theta[i]+c_omega[i+1]*dt)
        c_t.append(c_t[i]+dt)
        if c_theta[-1]>pi:
            c_theta[-1]=c_theta[-1]-2*pi
        if c_theta[-1]<-pi:
            c_theta[-1]=c_theta[-1]+2*pi

    print 'Total steps =',i,'    ',
#   print 'dt =',dt
    return 0

def Choose():
    i=0
    j=0
    while i<N:
        c_thetachoose.append(c_theta[j*900+225]) 
        c_omegachoose.append(c_omega[j*900+225])   
        j=j+1
        i=i+900+225
    print "j =",j
    return 0

Initial_theta=0.2
Initial_omega=0.0
F_dlist=[0,0.5,1.2]
#F_dlist=[1.35,1.44,1.465]
c_thetachoose=[]
c_omegachoose=[]


plt.figure(figsize=(20,8))

for m in range(1,3):
    c_t = None
    c_theta = None
    c_omega = None
    c_thetachoose=None
    c_omegachoose=None

    c_thetachoose=[]
    c_omegachoose=[]

    c_t = []
    c_theta = []
    c_omega = []
    F_d=F_dlist[m]
    F_dstr=str(F_d)
    Calculate()
    Choose()

    plt.subplot(1,2,m)
    plt.title(r"$\omega$"+" versus "+r"$\theta$")
#   plt.title(r"$\theta$ versus time")
    plt.scatter(c_thetachoose,c_omegachoose,label="$F_D$"+"="+F_dstr,s=1)
    plt.xlim(-4,4)
    plt.ylim(-2,1)
    plt.xlabel(r"$\theta$ (radians)")
    plt.ylabel(r"$\omega$ (radians/s)")
#   plt.ylabel(r"$\theta$ (radians)")
    plt.legend()

plt.show()
```
#6
```python
import matplotlib.pyplot as plt
from math import *
from mpl_toolkits.mplot3d import Axes3D

print 'Final test V1.0'
print 'Designed by Roach'

Constant_g=9.8
Constant_l=9.8
Constant_q=0.5
Constant_Omegad=2.0/3.0

dt = pi/300
total_t=100
c_t = []
c_theta = []
c_omega = []
c_phi =[]
N=int(total_t/dt)

def Calculate():
    c_theta.append(Initial_theta)
    c_omega.append(Initial_omega)
    c_phi.append(0.0)
    c_t.append(0.0)
    print 'Initial_theta =',c_theta[0],'rad    ',
#   print 'Initial_omega =',c_omega[0],'rad/s    ',
    print 'F_d =',F_d,'N    ',
    for i in range(N):
        c_omega.append(c_omega[i]-(sin(c_theta[i])+Constant_q*c_omega[i]-F_d*sin(Constant_Omegad*c_t[i]))*dt)
        c_theta.append(c_theta[i]+c_omega[i+1]*dt)
        c_phi.append(dt*i*Constant_Omegad)
        c_t.append(c_t[i]+dt)
        if c_theta[-1]>pi:
            c_theta[-1]=c_theta[-1]-2*pi
        if c_theta[-1]<-pi:
            c_theta[-1]=c_theta[-1]+2*pi

    print 'Total steps =',i,'    ',
#   print 'dt =',dt
    return 0

def Choose():
    i=0
    j=0
    while i<N:
        c_thetachoose.append(c_theta[j*900+225]) 
        c_omegachoose.append(c_omega[j*900+225])   
        j=j+1
        i=i+900+225
    print "j =",j
    return 0

Initial_theta=0.2
Initial_omega=0.0
F_dlist=[0,0.5,1.2]
#F_dlist=[1.35,1.44,1.465]
c_thetachoose=[]
c_omegachoose=[]




m=2
c_phi =None
c_t = None
c_theta = None
c_omega = None
c_thetachoose=None
c_omegachoose=None

c_thetachoose=[]
c_omegachoose=[]
c_phi = []
c_t = []
c_theta = []
c_omega = []
F_d=F_dlist[m]
F_dstr=str(F_d)
Calculate()

c3dx=[]
c3dy=[]
c3dz=[]

for i in range(N):
    c3dx.append((c_theta[i]+25)*cos(c_phi[i]))
    c3dy.append((c_theta[i]+25)*sin(c_phi[i]))
    c3dz.append(c_omega[i])

linex=[20,35,35,20,20]
liney=[0,0,0,0,0]
linez=[2,2,-1,-1,2]

fig=plt.figure(figsize=(16,12))
ax=fig.gca(projection='3d')
ax.set_title(r"$\omega$"+" versus "+r"$\theta$")
ax.scatter(c3dx,c3dy,c3dz,label="$F_D$"+"="+F_dstr,s=1)
ax.plot(linex,liney,linez)
ax.xaxis.set_major_locator(plt.NullLocator())
ax.yaxis.set_major_locator(plt.NullLocator())
ax.zaxis.set_major_locator(plt.NullLocator())
ax.set_zlim(-10,10)
plt.legend()

plt.show()
```
#7
```python
import matplotlib.pyplot as plt
from math import *

print 'Final test V1.0'
print 'Designed by Roach'

Constant_g=9.8
Constant_l=9.8
Constant_q=0.5
Constant_Omegad=2.0/3.0

dt = pi/300
total_t=30000
c_t = []
c_theta = []
c_omega = []
N=int(total_t/dt)

def Calculate():
    c_theta.append(Initial_theta)
    c_omega.append(Initial_omega)
    c_t.append(0.0)
    print 'Initial_theta =',c_theta[0],'rad    ',
#   print 'Initial_omega =',c_omega[0],'rad/s    ',
    print 'F_d =',F_d,'N    ',
    for i in range(N):
        c_omega.append(c_omega[i]-(sin(c_theta[i])+Constant_q*c_omega[i]-F_d*sin(Constant_Omegad*c_t[i]))*dt)
        c_theta.append(c_theta[i]+c_omega[i+1]*dt)
        c_t.append(c_t[i]+dt)
        if c_theta[-1]>pi:
            c_theta[-1]=c_theta[-1]-2*pi
        if c_theta[-1]<-pi:
            c_theta[-1]=c_theta[-1]+2*pi

    print 'Total steps =',i,'    ',
#   print 'dt =',dt
    return 0

psi=0
def Choose():
    i=0
    j=0
    while i<N:
        c_thetachoose.append(c_theta[j*900+psi]) 
        c_omegachoose.append(c_omega[j*900+psi])   
        j=j+1
        i=i+900+psi
    print "j =",j
    return 0

Initial_theta=0.2
Initial_omega=0.0
F_dlist=[0,0.5,1.2]
#F_dlist=[1.35,1.44,1.465]
c_thetachoose=[]
c_omegachoose=[]


plt.figure(figsize=(20,16))

for m in range(1,5):
    c_t = None
    c_theta = None
    c_omega = None
    c_thetachoose=None
    c_omegachoose=None

    c_thetachoose=[]
    c_omegachoose=[]

    c_t = []
    c_theta = []
    c_omega = []
    F_d=1.2
    F_dstr=str(F_d)
    Calculate()
    psi=m*113
    Choose()

    plt.subplot(2,2,m)
    plt.title(r"$\omega$"+" versus "+r"$\theta$")
#   plt.title(r"$\theta$ versus time")
    plt.scatter(c_thetachoose,c_omegachoose,label="$F_D$"+"="+F_dstr,s=1)
    plt.xlim(-4,4)
    plt.ylim(-2.5,2.5)
    plt.xlabel(r"$\theta$ (radians)")
    plt.ylabel(r"$\omega$ (radians/s)")
#   plt.ylabel(r"$\theta$ (radians)")
    plt.legend()

plt.show()
```
