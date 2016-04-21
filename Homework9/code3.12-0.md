import matplotlib.pyplot as plt
from math import *

print 'Exercise 3.12 V1.0'
print 'Designed by roach'

Constant_g=9.8
Constant_l=9.8
Constant_q=0.5
Constant_Omegad=2.0/3.0

dt = 0.01

c_t = []
c_theta = []
c_omega = []

def Calculate(Initial_theta,Initial_omega,c_t,c_theta,c_omega):
    c_theta.append(Initial_theta)
    c_omega.append(Initial_omega)
    c_t.append(0.0)
    print 'Initial_theta =',c_theta[0],'rad    ',
    print 'Initial_omega =',c_omega[0],'rad/s    ',
    print 'F_d =',F_d,'Force unit    ',
    for i in range(10000):
        c_omega.append(c_omega[i]-(sin(c_theta[i])+Constant_q*c_omega[i]+F_d*sin(Constant_Omegad*c_t[i]))*dt)
        c_theta.append(c_theta[i] + c_omega[i+1]*dt)
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

for m in range(3):
    c_t = None
    c_theta = None
    c_omega = None
    c_t = []
    c_theta = []
    c_omega = []
    F_d=F_dlist[m]
    F_dstr=str(F_d)
    Calculate(Initial_theta,Initial_omega,c_t,c_theta,c_omega)

    plt.plot(c_t,c_theta,label='F_D = '+F_dstr+' (Force unit)')


plt.xlabel('t (s)')
plt.ylabel('theta (rad)')
plt.legend()
plt.show()
