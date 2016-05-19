```python
import matplotlib
import numpy as np
import matplotlib.cm as cm
import matplotlib.mlab as mlab
import matplotlib.pyplot as plt
import time 
from math import *

timebegin=time.time()

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

#initial CV
CV=[[0 for i in range(30)] for j in range(30)]
for n1 in range(30):
    for n2 in range(30):
        CV[n1][n2]=0.0

for n1 in range(10,20):
    CV[n1][9]=-1.0
    CV[n1][19]=1.0
for n1 in range(30):
    CV[n1][0]=0.0
    CV[n1][29]=0.0
    CV[0][n1]=0.0
    CV[29][n1]=0.0


#printCV(CV)


CV2=[]
n=0

for i in range(10):
    CV2=None
    CV2=CV[:]

#calculate CV2
    for n1 in range(1,len(CV)-1):
        for n2 in range(1,len(CV[0])-1):
            CV2[n1][n2]=(CV[n1-1][n2]+CV[n1+1][n2]+CV[n1][n2-1]+CV[n1][n2+1])/4.0
   
    for n3 in range(10,20):
        CV2[n3][9]=-1.0
        CV2[n3][19]=1.0

    CV=None
    CV=CV2[:]

    print "V",i
    n=i

strn=str(n)
print "Total V",n
print "Time used",time.time()-timebegin
#printCV(CV)

CX=[]
CY=[]

for i in range(30):
    CX.append(-3.0+6*i/29.0)
    CY.append(-3.0+6*i/29.0)

plt.figure(figsize=(20,20))

CS = plt.contour(CX, CY, CV, 10,colors='brown')
plt.clabel(CS, fontsize=9, inline=1)
plt.title("Exercise5.7 V"+strn)
plt.xlabel("x")
plt.ylabel("y")
plt.xlim(-3.1,3.1)
plt.ylim(-3.1,3.1)
plt.plot([-1,-1],[-1,1],color = "blue",linewidth=5)
plt.plot([1,1],[1,-1],color = "red",linewidth=5)
plt.plot([3,-3,-3,3,3],[3,3,-3,-3,3],color = "black",linewidth=5)
plt.show()
```
