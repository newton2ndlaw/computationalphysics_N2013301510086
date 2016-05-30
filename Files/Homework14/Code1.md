```python
import matplotlib.pyplot as plt
import numpy as np
import time
import math


starttime=time.time()

print '''Exercise 6.13
Designed by Roach
'''

constant_dx=0.005
constant_c=300.0
constant_dt=constant_dx/constant_c
constant_r=constant_c*constant_dt/constant_dx
total_L=1.0
total_t=0.1
total_M=int(total_L/constant_dx)
total_N=int(total_t/constant_dt)
print "Total t =",total_t
print "dt =",constant_dt
print "r =",constant_r
print "M(~x) =",total_M
print "N(~t) =",total_N
print "e =",math.e

#Initial Cy[t~N~n][x~M~i]
Cy=[[0.0 for i in range(total_M+1)] for n in range (total_N+1)]
for n in range(total_N+1):
    for i in range(total_M+1):
        Cy[n][i]=0.0

Cx0=0.3
constant_k=1000
for n in range(total_N+1):
    for i in range(total_M+1):
        Cy[n][i]=math.e**(-constant_k*((i*constant_dx-Cx0)**2))
    Cy[n][0]=0.0
    Cy[n][-1]=0.0

#Caculate
for n in range(2,total_N):
    for i in range(1,total_M): 
        Cy[n+1][i]=2*(1-constant_r**2)*Cy[n][i]-Cy[n-1][i]+(constant_r**2)*(Cy[n][i+1]+Cy[n][i-1])
    Cy[n][0]=0.0
    Cy[n][-1]=0.0

print "Time used", time.time()-starttime,"s"

plt.figure(figsize=(24,24))
plt.xlabel("x(m)")
plt.ylabel("y(m)")

plot_cx=[]
plot_cy=[]
for i in range(total_M+1):
    plot_cx.append(i*constant_dx)
    plot_cy.append(Cy[0][i])
plt.subplot(12, 1, 1)
plt.title("Waves on a string (Gaussian pluck)")
plt.xlabel("x(m)")
plt.ylabel("y(m)")
plt.xlim(0,1)
plt.ylim(-1,1)
plt.plot(plot_cx,plot_cy,label="0")

for nt in range(11):
    plot_cx=None
    plot_cy=None
    plot_cx=[]
    plot_cy=[]
    for i in range(total_M+1):
        plot_cx.append(i*constant_dx)
        plot_cy.append(Cy[(nt+1)*8][i])
    plt.subplot(12, 1, nt+2)
    plt.xlabel("x(m)")
    plt.ylabel("y(m)")
    plt.xlim(0,1)
    plt.ylim(-1,1)
    plt.plot(plot_cx,plot_cy,label=str(nt))

plt.show()

plot_ct=[]
plot_cyt=[]
Ctx=0.05
Nposition=int(Ctx/constant_dx)
for i in range(total_N+1):
    plot_ct.append(i*constant_dt)
    plot_cyt.append(Cy[i][Nposition])

plt.figure(figsize=(24,18))
plt.title("String signal versus time (at x=0.05m)")
plt.plot(plot_ct,plot_cyt)
plt.xlabel("Time(s)")
plt.ylabel("y(m)")
plt.show()


```
