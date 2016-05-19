```python
import matplotlib
import numpy as np
import matplotlib.cm as cm
import matplotlib.mlab as mlab
import matplotlib.pyplot as plt
import time 
from math import *



print '''Exercise 5.7
Designed by roach
'''

def printCV(CV):
    print "------"
    for n1 in range(len(CV)):
        for n2 in range(len(CV[0])):
            print CV[n1][n2],
        print ""
    print "------"
    return 0

steps=2000
timebegin=time.time()
#initial CV
CV=[[0 for i in range(31)] for j in range(31)]
for n1 in range(31):
    for n2 in range(31):
        CV[n1][n2]=0.0

for n1 in range(10,21):
    CV[n1][10]=-1.0
    CV[n1][20]=1.0
for n1 in range(31):
    CV[n1][0]=0.0
    CV[n1][30]=0.0
    CV[0][n1]=0.0
    CV[30][n1]=0.0


#printCV(CV)


CV2=[]
n=0
maxdeltaV=[]



for itotal in range(steps):
    CV2=None
    CV2=[[0 for i in range(31)] for j in range(31)]

    CVbegin=None
    CVbegin=[[0 for i in range(31)] for j in range(31)]
    for n1 in range(31):
        for n2 in range(31):
            CVbegin[n1][n2]=CV[n1][n2]
            CV2[n1][n2]=CV[n1][n2]

#calculate CV2
    for n1 in range(1,len(CV)-1):
        for n2 in range(1,len(CV[0])-1):
            CV2[n1][n2]=(CV[n1-1][n2]+CV[n1+1][n2]+CV[n1][n2-1]+CV[n1][n2+1])/4.0

    for n3 in range(10,21):
        CV2[n3][10]=-1.0
        CV2[n3][20]=1.0

    CVdelta=None
    CVdelta=[]
    for n1 in range(31):
        for n2 in range(31):
            CVdelta.append(abs(CVbegin[n1][n2]-CV2[n1][n2]))

    CV=None
    CV=[[0 for i in range(31)] for j in range(31)]
    for n1 in range(31):
        for n2 in range(31):
            CV[n1][n2]=CV2[n1][n2]

    maxdeltaV.append(max(CVdelta))
    print "V",itotal,max(CVdelta)
    ntotal=itotal

strn=str(ntotal)
print "Total V",ntotal
print "Time used",time.time()-timebegin


CX=[]
CY=[]

for i in range(31):
    CX.append(-3.0+6*i/30.0)
    CY.append(-3.0+6*i/30.0)

plt.figure(figsize=(20,20))

CS = plt.contour(CX, CY, CV, 20,colors='brown')

plt.clabel(CS, fontsize=9, inline=1)
plt.title("Exercise5.7 V"+strn)
plt.xlabel("x")
plt.ylabel("y")
plt.xlim(-3.1,3.1)
plt.ylim(-3.1,3.1)
plt.plot([-1,-1],[-1,1],color = "blue",linewidth=3)
plt.plot([1,1],[1,-1],color = "red",linewidth=3)
plt.plot([3,-3,-3,3,3],[3,3,-3,-3,3],color = "black",linewidth=3)
plt.show()

xcv=[]
for i in range(steps):
    xcv.append(i)

plt.figure(figsize=(24,18))
plt.title("Exercise5.7 Max deltaV - Update times")
plt.xlabel("Update times")
plt.ylabel("Max deltaV")
plt.plot(xcv,maxdeltaV)
plt.show()

```
