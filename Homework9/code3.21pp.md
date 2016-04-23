```python
import matplotlib.pylab as plt
import time,pp,sys
from math import *

start_time = time.time()

print 'Exercise 3.16 V1.0'
print 'Designed by roach'
Constant_g=9.8
Constant_l=9.8
Constant_q=0.5
Constant_Omegad=2.0/3.0
Initial_theta=0.2
Initial_omega=0.0

ppservers = ()
#ppservers = ("10.0.0.1",)
if len(sys.argv) > 1:
    ncpus = int(sys.argv[1])
    # Creates jobserver with ncpus workers
    job_server = pp.Server(ncpus, ppservers=ppservers)
else:
    # Creates jobserver with automatically detected number of workers
    job_server = pp.Server(ppservers=ppservers)
print "Starting pp with", job_server.get_ncpus(), "workers"


def Calculate2(F_d):
    dt = 0.01
    c_t = None
    c_theta = None
    c_omega = None
    result_theta = None
    result_theta2= None
    result_theta3= None
    resultall_theta_2=None
    F_dlist2_2=None
    c_t = []
    c_theta = []
    c_omega = []
    result_theta =[]
    result_theta2=[]
    result_theta3=[]
    resultall_theta_2=[]
    F_dlist2_2=[]
    c_theta.append(Initial_theta)
    c_omega.append(Initial_omega)
    c_t.append(0.0)
    print 'Initial_theta =',c_theta[0],'rad    ',
    print 'Initial_omega =',c_omega[0],'rad/s    ',
    print 'F_d =',F_d,'N    ',
    for i in range(30000):
        c_omega.append(c_omega[i]-(sin(c_theta[i])+Constant_q*c_omega[i]-F_d*sin(Constant_Omegad*c_t[i]))*dt)
        c_theta.append(c_theta[i] + c_omega[i+1]*dt)
        c_t.append(c_t[i]+dt)
        if c_theta[-1]>pi:
            c_theta[-1]=c_theta[-1]-2*pi
        if c_theta[-1]<-pi:
            c_theta[-1]=c_theta[-1]+2*pi
    for i in range(15000,29999):
        if c_theta[i]>c_theta[i-1] and c_theta[i]>c_theta[i+1] and c_theta[i] < 3.1:
            result_theta.append(c_theta[i])
            resultall_theta_2.append(c_theta[i])
    print 'Total steps =',i,'    ',
    print 'dt =',dt
    result_theta2=sorted(result_theta)
    result_theta3=sorted(result_theta)
#   print 'result thetas2',result_theta2   
    for n1 in range(len(result_theta2)-1):
        if abs(result_theta2[n1]-result_theta2[n1+1])<0.01:
            result_theta3[n1+1]=0
    print '        Result max thetas',sorted(result_theta3,reverse=True)
    return resultall_theta_2

F_dlist=[]
F_dlist2=[]
for i in range(900):
    F_dlist.append(1.4+0.0001*i)
result_theta=[]
resultall_theta=[]

#  for i1 in range(len(F_dlist)):
#      a = Calculate2(F_dlist[i1])
#      for i2 in range(len(a)):
#          F_dlist2.append(F_dlist[i1])
#          resultall_theta.append(a[i2])

jobs = [(input, job_server.submit(Calculate2,(input,), (sin,), ("math",))) for input in F_dlist]
for input, job in jobs:
    a = job()
    for i2 in range(len(a)):
        F_dlist2.append(input)
        resultall_theta.append(a[i2])


plt.scatter(F_dlist2,resultall_theta,label='Bifurcation diagram')
plt.xlabel('F_D (N)')
plt.ylabel('theta (rad)')
plt.title('Exercise 3.16 Bifurcation diagram')
plt.legend()

print 'Time used',time.time() - start_time,'s'

plt.show()
```
