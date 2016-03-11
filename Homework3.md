# Homework3
## 摘要

用字符表示字母，目标：
 
- [x] 作业L1 在屏幕上用字符拼出自己姓名的英文
- [x] 作业L2 在屏幕上用字符拼出任意次序的姓名
- [ ] 作业L3 在80*80点阵上用字符拼出你想画的东西，希望脑洞大开！（比如字符，火柴人，实现移动、旋转等等）

## 背景介绍
  显卡的工作原理。
  
## 正文
### 作业L1 在屏幕上用字符拼出自己姓名的英文
代码如下
```python
print "##### #   #   #   #   #  ####        ###  ##### "
print "   #  #   #  # #  ##  # #           #   #   #   "
print "  #   ##### ##### # # # #  ##       # # #   #   "
print " #    #   # #   # #  ## #   #       #  ##   #   "
print "##### #   # #   # #   #  ####        #### ##### "
```

### 作业L2 在屏幕上用字符拼出任意次序的姓名
**以下内容纯属原创，如果引用，请注明本文档位置。**

程序采用Microsoft Visual Studio 2015编写。

先正序和反序显示自己的名字，接下来可以输入任意的字母（包括空格），然后用字符显示出来。

弄了一个二维数组，并没有使用字典。为了简便，每个字母用5*5的字符表示出来。表示数组的每一行代表一个字母，每一列代表每个字母的每一行。后面为了简洁，因此使用了一个数表和循环进行识别输入的字符。暂时没有加入换行的功能，明天再弄。
代码如下：
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

### 作业L3 在80*80点阵上用字符拼出你想画的东西，希望脑洞大开！（比如字符，火柴人，实现移动、旋转等等）

随便画？

## 结论

待会弄个图片上去。

## 致谢
