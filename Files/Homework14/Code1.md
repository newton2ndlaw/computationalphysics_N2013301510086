#Code

##Code1
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

##Code2
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
# print "e =",math.e

#Initial Cy[t~N~n][x~M~i]
Cy=[[0.0 for i in range(total_M+1)] for n in range (total_N+1)]
for n in range(total_N+1):
    for i in range(total_M+1):
        Cy[n][i]=0.0

Cx0=0.3
constant_k=1000
intCx0=int(Cx0/constant_dx)
for n in range(total_N+1):
    for i in range(0,intCx0):
        Cy[n][i]=1.0/0.3*i*constant_dx
    for i in range(intCx0,total_M+1):
        Cy[n][i]=-1.0/0.7*(i*constant_dx-Cx0)+1
    Cy[n][0]=0.0
    Cy[n][-1]=0.0

#Caculate
for n in range(2,total_N):
    for i in range(1,total_M): 
        Cy[n+1][i]=2*(1-constant_r**2)*Cy[n][i]-Cy[n-1][i]+(constant_r**2)*(Cy[n][i+1]+Cy[n][i-1])
    Cy[n][0]=0.0
    Cy[n][-1]=0.0


print "Time used", time.time()-starttime,"s"

# plt.figure(figsize=(24,24))
# plt.xlabel("x(m)")
# plt.ylabel("y(m)")

plot_cx=[]
plot_cy=[]
for i in range(total_M+1):
    plot_cx.append(i*constant_dx)
    plot_cy.append(Cy[0][i])


#2
plt.figure(figsize=(24,18))

for rangectx in range(5):
    plot_ct=[]
    plot_cyt=[]
    plot_ct=None
    plot_cyt=None
    plot_ct=[]
    plot_cyt=[]
    Ctx=0.1*rangectx+0.1
    strCtx=str(Ctx)
    Nposition=int(Ctx/constant_dx)
    for i in range(total_N+1):
        plot_ct.append(i*constant_dt)
        plot_cyt.append(Cy[i][Nposition])
    plot_yreal=[]
    plot_yimag=[]
    plot_fourier=[]
    plot_freq=[]
    plot_freq0=[]
    plot_yreal=None
    plot_yimag=None
    plot_fourier=None
    plot_freq=None
    plot_freq0=None
    plot_yreal=[]
    plot_yimag=[]
    plot_fourier=[]
    plot_freq=[]
    plot_freq0=[]
    plot_yreal=np.fft.fft(plot_cyt).real
    plot_yimag=np.fft.fft(plot_cyt).imag
    plot_fourier=[]
    for i in range(len(plot_cyt)):
        plot_fourier.append(plot_yreal[i]**2+plot_yimag[i]**2)
    
    plot_freq0=np.fft.fftfreq(len(plot_cyt))
    plot_freq=[]
    for i in range(len(plot_freq0)):
        plot_freq.append(plot_freq0[i]/constant_dt)
    plt.plot(plot_freq,plot_fourier,label="x="+strCtx+"m")

plt.xlim(0,3000)
plt.title("Power spectrum (Line)")
plt.xlabel("Frequency (Hz)")
plt.ylabel("Power (arbitary units)")
plt.legend()

print "Time used", time.time()-starttime,"s"

plt.show()import matplotlib.pyplot as plt
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
# print "e =",math.e

#Initial Cy[t~N~n][x~M~i]
Cy=[[0.0 for i in range(total_M+1)] for n in range (total_N+1)]
for n in range(total_N+1):
    for i in range(total_M+1):
        Cy[n][i]=0.0

Cx0=0.3
constant_k=1000
intCx0=int(Cx0/constant_dx)
for n in range(total_N+1):
    for i in range(0,intCx0):
        Cy[n][i]=1.0/0.3*i*constant_dx
    for i in range(intCx0,total_M+1):
        Cy[n][i]=-1.0/0.7*(i*constant_dx-Cx0)+1
    Cy[n][0]=0.0
    Cy[n][-1]=0.0

#Caculate
for n in range(2,total_N):
    for i in range(1,total_M): 
        Cy[n+1][i]=2*(1-constant_r**2)*Cy[n][i]-Cy[n-1][i]+(constant_r**2)*(Cy[n][i+1]+Cy[n][i-1])
    Cy[n][0]=0.0
    Cy[n][-1]=0.0


print "Time used", time.time()-starttime,"s"

# plt.figure(figsize=(24,24))
# plt.xlabel("x(m)")
# plt.ylabel("y(m)")

plot_cx=[]
plot_cy=[]
for i in range(total_M+1):
    plot_cx.append(i*constant_dx)
    plot_cy.append(Cy[0][i])


#2
plt.figure(figsize=(24,18))

for rangectx in range(5):
    plot_ct=[]
    plot_cyt=[]
    plot_ct=None
    plot_cyt=None
    plot_ct=[]
    plot_cyt=[]
    Ctx=0.1*rangectx+0.1
    strCtx=str(Ctx)
    Nposition=int(Ctx/constant_dx)
    for i in range(total_N+1):
        plot_ct.append(i*constant_dt)
        plot_cyt.append(Cy[i][Nposition])
    plot_yreal=[]
    plot_yimag=[]
    plot_fourier=[]
    plot_freq=[]
    plot_freq0=[]
    plot_yreal=None
    plot_yimag=None
    plot_fourier=None
    plot_freq=None
    plot_freq0=None
    plot_yreal=[]
    plot_yimag=[]
    plot_fourier=[]
    plot_freq=[]
    plot_freq0=[]
    plot_yreal=np.fft.fft(plot_cyt).real
    plot_yimag=np.fft.fft(plot_cyt).imag
    plot_fourier=[]
    for i in range(len(plot_cyt)):
        plot_fourier.append(plot_yreal[i]**2+plot_yimag[i]**2)
    
    plot_freq0=np.fft.fftfreq(len(plot_cyt))
    plot_freq=[]
    for i in range(len(plot_freq0)):
        plot_freq.append(plot_freq0[i]/constant_dt)
    plt.plot(plot_freq,plot_fourier,label="x="+strCtx+"m")

plt.xlim(0,3000)
plt.title("Power spectrum (Line)")
plt.xlabel("Frequency (Hz)")
plt.ylabel("Power (arbitary units)")
plt.legend()

print "Time used", time.time()-starttime,"s"

plt.show()
```

##Code3
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
total_t=0.05
total_M=int(total_L/constant_dx)
total_N=int(total_t/constant_dt)
print "Total t =",total_t
print "dt =",constant_dt
print "r =",constant_r
print "M(~x) =",total_M
print "N(~t) =",total_N
# print "e =",math.e

#Initial Cy[t~N~n][x~M~i]
Cy=[[0.0 for i in range(total_M+1)] for n in range (total_N+1)]
for n in range(total_N+1):
    for i in range(total_M+1):
        Cy[n][i]=0.0

Cx0=0.3
constant_k=1000
intCx0=int(Cx0/constant_dx)
for n in range(total_N+1):
    for i in range(0,intCx0):
        Cy[n][i]=1.0/0.3*i*constant_dx
    for i in range(intCx0,total_M+1):
        Cy[n][i]=-1.0/0.7*(i*constant_dx-Cx0)+1
    Cy[n][0]=0.0
    Cy[n][-1]=0.0


#Caculate
for n in range(2,total_N):
    for i in range(1,total_M): 
        Cy[n+1][i]=2*(1-constant_r**2)*Cy[n][i]-Cy[n-1][i]+(constant_r**2)*(Cy[n][i+1]+Cy[n][i-1])
    Cy[n][0]=0.0
    Cy[n][-1]=0.0


print "Time used", time.time()-starttime,"s"

# plt.figure(figsize=(24,24))
# plt.xlabel("x(m)")
# plt.ylabel("y(m)")

plot_cx=[]
plot_cy=[]
for i in range(total_M+1):
    plot_cx.append(i*constant_dx)
    plot_cy.append(Cy[0][i])


#2
plt.figure(figsize=(24,24))

plt.title("Power spectrum (Line)")

for rangectx in range(5):
    plot_ct=[]
    plot_cyt=[]
    plot_ct=None
    plot_cyt=None
    plot_ct=[]
    plot_cyt=[]
    Ctx=0.1*rangectx+0.1
    strCtx=str(Ctx)
    Nposition=int(Ctx/constant_dx)
    for i in range(total_N+1):
        plot_ct.append(i*constant_dt)
        plot_cyt.append(Cy[i][Nposition])
    plot_yreal=[]
    plot_yimag=[]
    plot_fourier=[]
    plot_freq=[]
    plot_freq0=[]
    plot_yreal=None
    plot_yimag=None
    plot_fourier=None
    plot_freq=None
    plot_freq0=None
    plot_yreal=[]
    plot_yimag=[]
    plot_fourier=[]
    plot_freq=[]
    plot_freq0=[]
    plot_yreal=np.fft.fft(plot_cyt).real
    plot_yimag=np.fft.fft(plot_cyt).imag
    
    for i in range(len(plot_cyt)):
        plot_fourier.append(plot_yreal[i]**2+plot_yimag[i]**2)
    
    plot_freq0=np.fft.fftfreq(len(plot_cyt))
    plot_freq=[]
    for i in range(len(plot_freq0)):
        plot_freq.append(plot_freq0[i]/constant_dt)
    plt.subplot(5, 1, rangectx+1)
    plt.title("Power spectrum (Line)")
    plt.plot(plot_freq,plot_fourier,label="x="+strCtx+"m")

    plt.xlim(0,1000)
    plt.ylabel("Power (arbitary units)")
    plt.legend()
plt.xlabel("Frequency (Hz)")

print "Time used", time.time()-starttime,"s"

plt.show()
```
