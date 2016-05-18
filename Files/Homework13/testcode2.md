```python
import matplotlib
import numpy as np
import matplotlib.cm as cm
import matplotlib.mlab as mlab
import matplotlib.pyplot as plt


def printCV(CV):
    print "------"
    for n1 in range(len(CV)):
        for n2 in range(len(CV[0])):
            print CV[n1][n2],
        print ""
    print "------"
    return 0


CV=[[0 for i in range(50)] for j in range(50)]
for n1 in range(50):
    for n2 in range(50):
        CV[n1][n2]=0.0

for n1 in range(50):
    CV[n1][0]=-1.0
    CV[n1][-1]=1.0
    CV[0][n1]=-1.0+2.0/49.0*n1
    CV[-1][n1]=-1.0+2.0/49.0*n1

printCV(CV)


CV2=[]

for i in range(2000):
    CV2=None
    CV2=CV[:]
    for n1 in range(1,len(CV)-1):
        for n2 in range(1,len(CV[0])-1):
            CV2[n1][n2]=(CV[n1-1][n2]+CV[n1+1][n2]+CV[n1][n2-1]+CV[n1][n2+1])/4
    CV=CV2[:]
    n=i

print "V",n
printCV(CV)

CX=[]
CY=[]

for i in range(50):
    CX.append(-1.0+2*i/49.0)
    CY.append(-1.0+2*i/49.0)

plt.figure(figsize=(10,10))

CS = plt.contour(CX, CY, CV, 10,
                 colors='k',  # negative contours will be dashed by default
                 )
plt.clabel(CS, fontsize=9, inline=1)
plt.title('Single color - negative contours dashed')
plt.xlim(-2,2)
plt.ylim(-2,2)
plt.show()
```
