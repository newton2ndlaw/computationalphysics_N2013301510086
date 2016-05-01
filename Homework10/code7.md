```python
from visual import *
from math import *
import time

c_x=[]
c_y=[]
c_vx=[]
c_vy=[]
c_t=[]
#Initial conditions
dt=0.001
initial_x=0.8
initial_y=0.0
initial_vx=1.0*cos(45*pi/180)
initial_vy=1.0*sin(45*pi/180)
circle_cx=-0.1
circle_cy=0.3
circle_r=0.0 #No use for circle r
#ellipse condition
circle_a=0.5
circle_b=0.3

print 'ball condition x =',initial_x,'        y =',initial_y
print '               vx =',initial_vx,'        vy =',initial_vy

c_x.append(initial_x)
c_y.append(initial_y)
c_vx.append(initial_vx)
c_vy.append(initial_vy)
c_t.append(0)

scene=display(
    width=800,height=800,
    x=0, y=0,
    title="Exercise 3.31 Vpython")

arrow(color=color.blue,pos=(-1.2,0,0),axis=(2.4,0,0),shaftwidth=0.01,dixedwidth=0.01)
arrow(color=color.blue,pos=(0,-1.2,0),axis=(0,2.4,0),shaftwidth=0.01,dixedwidth=0.01)
curve(x=arange(-1,2),y=1,color=color.white,radius=0.01)
curve(x=arange(-1,2),y=-1,color=color.white,radius=0.01)
curve(y=arange(-1,2),x=1,color=color.white,radius=0.01)
curve(y=arange(-1,2),x=-1,color=color.white,radius=0.01)

circle_x=[]
circle_y=[]
for i in range(510):
    circle_x.append(circle_a*cos(i*pi/250.0)+circle_cx)
    circle_y.append(circle_b*sin(i*pi/250.0)+circle_cy)
for i in range(509):
    curve(x=(circle_x[i],0.01),y=(circle_y[i],0.01))

ball=sphere(pos=(initial_x,initial_y),radius=0.03,color=color.red)
bv = arrow(pos=(c_x[-1],c_y[-1]),axis=(c_vx[-1]*0.2,c_vy[-1]*0.2),color=color.cyan,shaftwidth=0.01)



i=0
n0=0
while 1:
    rate(1000)
    c_x.append(c_x[i]+c_vx[i]*dt)
    c_y.append(c_y[i]+c_vy[i]*dt)
    c_vx.append(c_vx[i])
    c_vy.append(c_vy[i])
    c_t.append((i+1)*dt)
   #range square
    if c_x[-1]>1.0 or c_x[-1]<-1.0:
        c_vx[-1]=-c_vx[-1]
    if c_y[-1]>1.0 or c_y[-1]<-1.0:
        c_vy[-1]=-c_vy[-1]
    #range ellipse
    if ((c_x[-1]-circle_cx)/circle_a)**2+((c_y[-1]-circle_cy)/circle_b)**2<1.0 and n0>5:
        theta1=acos((c_x[-1]-circle_cx)/circle_a)
        theta2=asin((c_y[-1]-circle_cy)/circle_b)
        kx=circle_a*sin(theta1)
        ky=circle_b*cos(theta2)
        nx=abs(ky/(kx**2+ky**2)**0.5)
        ny=abs(kx/(kx**2+ky**2)**0.5)
        if c_x[-1]-circle_cx<0 and c_y[-1]-circle_cy<0:
            nx=-nx
            ny=-ny
        elif c_x[-1]-circle_cx>0 and c_y[-1]-circle_cy<0:
            ny=-ny
        elif c_x[-1]-circle_cx<0 and c_y[-1]-circle_cy>0:
            nx=-nx
        v_vertical=c_vx[-1]*nx+c_vy[-1]*ny
        v_verticalx=v_vertical*nx
        v_verticaly=v_vertical*ny
        v_parallelx=c_vx[-1]-v_verticalx
        v_parallely=c_vy[-1]-v_verticaly
        v_verticalx=-v_verticalx
        v_verticaly=-v_verticaly
        c_vx[-1]=v_verticalx+v_parallelx
        c_vy[-1]=v_verticaly+v_parallely
        n0=0
    ball.pos.x=c_x[-1]
    ball.pos.y=c_y[-1]
    bv.pos.x=c_x[-1]
    bv.pos.y=c_y[-1]
    bv.axis.x=c_vx[-1]*0.2
    bv.axis.y=c_vy[-1]*0.25
    n0=n0+1
    i=i+1


```
