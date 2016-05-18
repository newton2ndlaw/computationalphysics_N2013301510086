```python

def printCV(CV):
    print "------"
    for n1 in range(len(CV)):
        for n2 in range(len(CV[0])):
            print CV[n1][n2],
        print ""
    print "------"
    return 0


CV=[[0 for i in range(7)] for j in range(7)]
for n1 in range(7):
    for n2 in range(7):
        CV[n1][n2]=0.0

for n1 in range(7):
    CV[n1][0]=-1.0
    CV[n1][-1]=1.0
    CV[0][n1]=-1.0+1.0/3.0*n1
    CV[-1][n1]=-1.0+1.0/3.0*n1

printCV(CV)


CV2=[]

for i in range(20):
    CV2=None
    CV2=CV[:]
    for n1 in range(1,6):
        for n2 in range(1,6):
            CV2[n1][n2]=(CV[n1-1][n2]+CV[n1+1][n2]+CV[n1][n2-1]+CV[n1][n2+1])/4
    CV=CV2[:]
    printCV(CV2)

```
