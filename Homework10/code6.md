```python
import matplotlib.pylab as plt
import time
from math import *

start_time = time.time()

##circle not in the middle

print 'Exercise 3.31 V2.0'
print 'Designed by roach'

#calculate circle condition
def calculate():
    c_x.append(initial_x)
    c_y.append(initial_y)
    c_vx.append(initial_vx)
    c_vy.append(initial_vy)
    c_t.append(0)
    n=0
    for i in range(100000):
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
#range circle
        if (c_x[-1]-circle_cx)**2+(c_y[-1]-circle_cy)**2<circle_r**2 and n>5:
            v_vertical=c_vx[-1]*(c_x[-1]-circle_cx)/circle_r+c_vy[-1]*(c_y[-1]-circle_cy)/circle_r
            v_verticalx=v_vertical*(c_x[-1]-circle_cx)/circle_r
            v_verticaly=v_vertical*(c_y[-1]-circle_cy)/circle_r
            v_parallelx=c_vx[-1]-v_verticalx
            v_parallely=c_vy[-1]-v_verticaly
            v_verticalx=-v_verticalx
            v_verticaly=-v_verticaly
            c_vx[-1]=v_verticalx+v_parallelx
            c_vy[-1]=v_verticaly+v_parallely
            n=0
        n=n+1
    return 0

#calculate ellipse condition
def calculate2():
    c_x.append(initial_x)
    c_y.append(initial_y)
    c_vx.append(initial_vx)
    c_vy.append(initial_vy)
    c_t.append(0)
    n0=0
    for i in range(100000):
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
#           plt.plot([c_x[-1]-nx*0.1,c_x[-1]+nx*0.1],[c_y[-1]-ny*0.1,c_y[-1]+ny*0.1])
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
#           plt.plot([c_x[-1]-nx*0.1,c_x[-1]+nx*0.1],[c_y[-1]-ny*0.1,c_y[-1]+ny*0.1])
        n0=n0+1
    return 0


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


#if it is a circle
if circle_a == circle_b:
    circle_r = circle_a
    print 'circle condition x =',circle_cx,'        y =',circle_cy
    print '                 r =',circle_r
    calculate()
    plt.figure(figsize=(20,20))
    plt.scatter(initial_x,initial_y,color='blue',label='initial position')
    plt.scatter(c_x,c_y,s=1,label='trajectory',color ='red')
    plt.title('Exercise 3.31 circle x='+str(circle_cx)+'  y='+str(circle_cy)+'  r='+str(circle_r))
    plt.xlabel('x(length unit)')
    plt.ylabel('y(length unit)')
    plt.xlim(-1.2,1.2)
    plt.ylim(-1.2,1.2)
#draw a square
    plt.plot([1,-1,-1,1,1],[1,1,-1,-1,1],color='black',label='range')
#draw a circle
    circle_x=[]
    circle_y=[]
    for i in range(510):
        circle_x.append(circle_r*cos(i*pi/250.0)+circle_cx)
        circle_y.append(circle_r*sin(i*pi/250.0)+circle_cy)
    plt.plot(circle_x,circle_y,color='black',label=None)
    plt.legend()
#total time used
    print 'Total time',c_t[-1],'time unit'
    print 'Time used',time.time() - start_time,'s'
    plt.show()
#if it is a ellipse
else:
#swap a and b    
    if circle_a<circle_b:
        conditionb = circle_a
        conditiona = circle_b
        conditione = (1-(conditionb/conditiona)**2)**0.5
        print 'ellipse condition x =',circle_cx,'        y =',circle_cy
        print '                  a =',conditiona,'        b =',conditionb
        print '                  e =',conditione
        print '    a parallel y axis'
        
    else:
        conditiona = circle_a
        conditionb = circle_b
        conditione = (1-(conditionb/conditiona)**2)**0.5
        print 'ellipse condition x =',circle_cx,'        y =',circle_cy
        print '                  a =',circle_a,'        b =',circle_b
        print '                  e =',(conditiona**2-conditionb**2)**0.5/conditiona
        print '    a parallel x axis'
    

    calculate2()
    plt.figure(figsize=(20,20))
    plt.scatter(initial_x,initial_y,color='blue',label='initial position')
    plt.scatter(c_x,c_y,s=1,label='trajectory',color ='red')
    plt.title('Exercise 3.31 ellipse x='+str(circle_cx)+'  y='+str(circle_cy)+'  x_='+str(circle_a)+'  y_='+str(circle_b)+'  e='+str(conditione))
    plt.xlabel('x(length unit)')
    plt.ylabel('y(length unit)')
    plt.xlim(-1.2,1.2)
    plt.ylim(-1.2,1.2)
#draw a square
    plt.plot([1,-1,-1,1,1],[1,1,-1,-1,1],color='black',label='range')
#draw a circle
    ellipse_x=[]
    ellipse_y=[]
    for i in range(510):
        ellipse_x.append(circle_a*cos(i*pi/250.0)+circle_cx)
        ellipse_y.append(circle_b*sin(i*pi/250.0)+circle_cy)
    plt.plot(ellipse_x,ellipse_y,color='black',label=None)
    plt.legend()
#total time used
    print 'Total time',c_t[-1],'time unit'
    print 'Time used',time.time() - start_time,'s'
    plt.show()


```
