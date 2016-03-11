# Homework3
## 摘要

用字符表示字母，目标：
 
- [x] 1.把自己的名字用字符表示。
- [x] 2.倒着打一遍。
- [x] 3.实现任意输出。

## 背景介绍
  显卡的工作原理。
  
## 正文
### 1.把自己的名字用字符表示。
代码如下
```python
print "##### #   #   #   #   #  ####        ###  ##### "
print "   #  #   #  # #  ##  # #           #   #   #   "
print "  #   ##### ##### # # # #  ##       # # #   #   "
print " #    #   # #   # #  ## #   #       #  ##   #   "
print "##### #   # #   # #   #  ####        #### ##### "
```

### 2.反着打一遍。
代码和第三个写在了一起。

### 3.实现任意输出。
使用的是二维数组，并没有用字典。
代码如下
```python
#letter list designed by Zhang Qi
letter=[['     ','     ','     ','     ','     ']] #space
letter.append(['  #  ',' # # ','#####','#   #','#   #']) #A 1
letter.append(['#### ','#   #','#### ','#   #','#### ']) #B 2
letter.append([' ### ','#   #','#    ','#   #',' ### ']) #C 3
letter.append(['#### ','#   #','#   #','#   #','#### ']) #D 4
letter.append(['#####','#    ','#####','#    ','#####']) #E 5
letter.append(['#####','#    ','#####','#    ','#    ']) #F 6
letter.append([' ####','#    ','#  ##','#   #',' ####']) #G 7
letter.append(['#   #','#   #','#####','#   #','#   #']) #H 8
letter.append(['#####','  #  ','  #  ','  #  ','#####']) #I 9
letter.append(['#####','  #  ','  #  ','# #  ',' ##  ']) #J 10
letter.append(['#   #','#  # ','###  ','#  # ','#   #']) #K 11
letter.append(['#    ','#    ','#    ','#    ','#####']) #L 12
letter.append(['#   #','## ##','# # #','#   #','#   #']) #M 13
letter.append(['#   #','##  #','# # #','#  ##','#   #']) #N 14
letter.append([' ### ','#   #','#   #','#   #',' ### ']) #O 15
letter.append(['#### ','#   #','#### ','#    ','#    ']) #P 16
letter.append([' ### ','#   #','# # #','#  ##',' ## #']) #Q 17
letter.append(['#### ','#   #','#### ','#  # ','#   #']) #R 18
letter.append([' ### ','#    ','  #  ','    #',' ### ']) #S 19
letter.append(['#####','  #  ','  #  ','  #  ','  #  ']) #T 20
letter.append(['#   #','#   #','#   #','#   #',' ### ']) #U 21
letter.append(['#   #','#   #','#   #',' # # ','  #  ']) #V 22
letter.append(['#   #','#   #','# # #','## ##','#   #']) #W 23
letter.append(['#   #',' # # ','  #  ',' # # ','#   #']) #X 24
letter.append(['#   #','#   #',' ### ','  #  ','  #  ']) #Y 25
letter.append(['#####','   # ','  #  ',' #   ','#####']) #Z 26

#测试所有的字母,一排显示15个
print 'Test all the letters, 15 letters in a line:'
for i0 in range(5):
    for i1 in range(15):
        print letter[i1][i0],
    print ''
print ''
for i0 in range(5):
    for i1 in range(15,27):
        print letter[i1][i0],
    print ''
print ''

#正向输出名字
print 'My name in order:'
for i in range(5):
    print letter[26][i],letter[8][i],letter[1][i],letter[14][i],letter[7][i],letter[0][i],letter[17][i],letter[9][i]
    
print ''
print 'My name in reverse order:'
#反向输出名字
for i in range(5):
    print letter[9][i],letter[17][i],letter[0][i],letter[7][i],letter[14][i],letter[1][i],letter[8][i],letter[26][i]
print ''

#字母识别列表
all_letter=(' ','a','b','c','d','e','f','g','h','i','j','k','l','m','n','o','p','q','r','s','t','u','v','w','x','y','z')

name = raw_input('Please write down your name (small letter): ') #输入名字,暂时不支持换行

for i in range(5):
    for i0 in range(len(name)):
        for i1 in range(27):
            if name[i0] == all_letter[i1]:
                print letter[i1][i],
                break
    print ''

raw_input()
```

## 结论

## 致谢
