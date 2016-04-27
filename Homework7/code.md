from visual import *
from math import *
import time
print 'Exercise 2.19 The effect of backspin on the range of a batted ball V2.0'
print 'Designed by Roach'
t = 0
c_x = []
c_y = []
c_z = []
c_vx = []
c_vy = []
c_vz = []
c_v = []
Constant_vd = 35.0
Constant_delta= 5.0
Constant_g = 9.794
Constant_S0m = 4.1*(10**(-4))
dt = 0.0001
omega = 2000.0
Initial_vx = 0.0
Initial_vy = 0.0
Initial_vz = 0.0
Initial_z = 2.0
def initialize(Initial_vx,Initial_vy,Initial_vz):
    global c_vx,c_vy,c_vz,c_x,c_y,c_z
    Initial_vx = Initial_vxs[m1]
    Initial_vy = Initial_vys[m2]
    Initial_vz = Initial_vzs[m3]
    c_vx.append(Initial_vx)
    c_vy.append(Initial_vy)
    c_vz.append(Initial_vz)
    c_v.append((Initial_vx**2+Initial_vy**2+Initial_vz**2)**0.5)
    c_x.append(0.0)
    c_y.append(0.0)
    c_z.append(Initial_z)
    print 'Initial position x =',c_x[0],'m    '
    print 'Initial position y =',c_y[0],'m    '
    print 'Initial position z =',c_z[0],'m    '
    print 'Initial velocity x =',c_vx[0],'m/s    '
    print 'Initial velocity y =',c_vy[0],'m/s    '
    print 'Initial velocity z =',c_vz[0],'m/s    '
    return 0
def calculate(c_vx,c_vy,c_vz,c_x,c_y,c_z,c_v,dt,Constant_vd,Constant_delta,Constant_g,omega):
    i = 0
    while c_z[i]>=0:
        B_ratio = 0.0039 + 0.0058/( 1 + exp( (c_v[i]-Constant_vd) /Constant_delta) )
        c_vx.append( c_vx[i] - B_ratio * c_v[i] * c_vx[i] * dt )
        c_vy.append( c_vy[i] - Constant_g * dt)
        c_vz.append( c_vz[i] - Constant_S0m * c_vx[i] * omega * dt)        
        c_v.append((c_vx[i+1]**2 + c_vy[i+1]**2 + c_vz[i+1]**2)**0.5)
        c_x.append( c_x[i] + c_vx[i+1] * dt)
        c_y.append( c_y[i] + c_vy[i+1] * dt)
        c_z.append( c_z[i] + c_vz[i+1] * dt)
        i=i+1
    print 'Landing point x =',c_x[-1],'m    ',
    print 'y =',c_y[-1],'m    ',
    print 'z =',c_z[-1],'m    ',
    print 'Total steps =',i,'    ',
    print 'dt =',dt,'s'
    return 0

Initial_vxs=[20]
Initial_vys=[0]
Initial_vzs=[0]
m1=0
m2=0
m3=0
c_x = None
c_y = None
c_z = None
c_vx = None
c_vy = None
c_vz = None
c_v = None
c_x = []
c_y = []
c_z = []
c_vx = []
c_vy = []
c_vz = []
c_v = []
initialize(Initial_vx,Initial_vy,Initial_vz)


arrow(color=color.red,axis=(30,0,0), shaftwidth=0.1, fixedwidth=10)
arrow(color=color.green,axis=(0,30,0), shaftwidth=0.1 , fixedwidth=10)
arrow(color=color.blue,axis=(0,0,30), shaftwidth=0.1, fixedwidth=10)
ball = sphere(pos=(0,0,1), radius=1, color=color.red)
bv = arrow(pos = (c_x[-1],c_y[-1],c_z[-1]), axis=(c_vx[-1]*0.1,c_vy[-1]*0.1,c_vz[-1]*0.1), color=color.cyan)

i=0
while 1:
    rate(10000)
    B_ratio = 0.0039 + 0.0058/( 1 + exp( (c_v[i]-Constant_vd) /Constant_delta) )
    c_vx.append( c_vx[i] - B_ratio * c_v[i] * c_vx[i] * dt )
    c_vy.append( c_vy[i] - Constant_g * dt)
    c_vz.append( c_vz[i] - Constant_S0m * c_vx[i] * omega * dt)        
    c_v.append((c_vx[i+1]**2 + c_vy[i+1]**2 + c_vz[i+1]**2)**0.5)
    c_x.append( c_x[i] + c_vx[i+1] * dt)
    c_y.append( c_y[i] + c_vy[i+1] * dt)
    c_z.append( c_z[i] + c_vz[i+1] * dt)
    ball.pos.x = c_x[-1]
    ball.pos.y = c_y[-1]
    ball.pos.z = c_z[-1]
    bv.pos.x = c_x[-1]
    bv.pos.y = c_y[-1]
    bv.pos.z = c_z[-1]
    bv.axis.x = c_vx[-1]*0.1
    bv.axis.y = c_vy[-1]*0.1
    bv.axis.z = c_vz[-1]*0.1
    i=i+1

