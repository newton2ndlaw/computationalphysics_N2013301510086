# Homework3
## 摘要

用字符表示字母，目标：
 
- [x] 作业L1 在屏幕上用字符拼出自己姓名的英文
- [x] 作业L2 在屏幕上用字符拼出任意次序的姓名
- [x] 作业L3 在80*80点阵上用字符拼出你想画的东西，希望脑洞大开！（比如字符，火柴人，实现移动、旋转等等）

## 背景介绍
  显卡的工作原理。
  
## 正文
### 作业L1 在屏幕上用字符拼出自己姓名的英文
效果如图
![3-2](https://raw.githubusercontent.com/newton2ndlaw/computationalphysics_N2013301510086/master/Homework3/Homework3-1.png)
代码如下
```python
print "##### #   #   #   #   #  ####        ###  ##### "
print "   #  #   #  # #  ##  # #           #   #   #   "
print "  #   ##### ##### # # # #  ##       # # #   #   "
print " #    #   # #   # #  ## #   #       #  ##   #   "
print "##### #   # #   # #   #  ####        #### ##### "
```


### 作业L2 在屏幕上用字符拼出任意次序的姓名

**以下内容纯属原创，如果引用，请注明本文档链接。**

程序采用Microsoft Visual Studio 2015编写。


#### 第一版（一共有三个版本。暂时完成的第二版提供了换行的功能。）

**这是第一版，更加丰富的功能请看第二版。**

先正序和反序显示自己的名字，接下来可以输入任意的字母（包括空格），然后用字符显示出来。

使用了一个二维数组，并没有使用字典。为了简便，每个字母用5*5的字符表示出来。表示数组的每一行代表一个字母，每一列代表每个字母的每一行。后面为了简洁，因此使用了一个数表和循环进行识别输入的字符。以下这个是不支持换行的，后面对代码进行了升级，可以实现换行。

效果如图：
![3-2](https://raw.githubusercontent.com/newton2ndlaw/computationalphysics_N2013301510086/master/Homework3/Homework3-2.png)

代码如下：
```python
#letter list designed by Zhang Qi
letter=[['     ','     ','     ','     ','     ']] #space 0
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

name = raw_input('Please write down your name (small letter): ') #可以输入任意的小写字母,包括空格

#可以识别相应的字母,然后用点阵的方式显示出来
for i in range(5):
    for i0 in range(len(name)):
        for i1 in range(27):
            if name[i0] == all_letter[i1]:
                print letter[i1][i],
                break
    print ''

raw_input()
```
#### 第二版

更改了最后输循环出之后，可以实现换行功能了。（20个字母一排） 为了实现换行功能，多添加了一个循环，每当变量循环到20就换行。但是由于最后一行可能不满20个字幕，因此最后一行进行了单独的处理。

实现换行功能的程序效果图：
![3-2](https://raw.githubusercontent.com/newton2ndlaw/computationalphysics_N2013301510086/master/Homework3/Homework3-2-2.png)

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

#字母识别列表
all_letter=(' ','a','b','c','d','e','f','g','h','i','j','k','l','m','n','o','p','q','r','s','t','u','v','w','x','y','z')

name = raw_input('Please write down your name (small letter): ') #输入名字,支持换行20个一行
lenname = len(name) #获取文字长度
column = lenname / 20 #获取行数
#除了最后一行的输出
for i3 in range(column):
    for i in range(5):
        for i0 in range(20):
           for i1 in range(27):
                if name[i0 + 20 * i3] == all_letter[i1]:
                    print letter[i1][i],
                    break
        print ''
    print ''
#最后一行进行单独处理
for i in range(5):
    for i0 in range(lenname - 20 * column):
       for i1 in range(27):
            if name[i0 + 20 * column] == all_letter[i1]:
                print letter[i1][i],
                break
    print ''

raw_input()
```
#### 第三版
将会扩充到所有的字符。

### 作业L3 在80*80点阵上用字符拼出你想画的东西，希望脑洞大开！（比如字符，火柴人，实现移动、旋转等等）

#### 第一版
画了一个斜眼图（静态的）。
代码如下：
```python
print '                     .;;hShhhhhh5s;;.                      '
print '                  ,:;rr:;,       .:irrr:                   '
print '             .i1hi:,                 .:s1hh:               '
print '          ,59hi:.  ..                    .rs1r             '
print '        rS9hs;;iiiii1s1i:                   ;35,           '
print '      ,9B@MS         .:iS5,                   18i          '
print '      39B@#H,  . .       r9;                   :8r         '
print '    ,3sh33hrrrrrrrsh1:    :G;                   ,8s        '
print '   ;As  . .        ,r35    i8:     ,:riiii::,    ,8r       '
print '  .8r                 59    hS   1ss      ^rh51i  :8,      '
print '  5h                   59.  5S  58sr.        .;S3; 13      '
print ' .8.                    h9s59; 18h@@h           ;S1 9i     '    
print ' s1 .r                   ;5r   ;Gs9G1rhsrsshr:   .81i9     '    
print ' sr i9                          ::888;     :s8S   ,G,9.    '    
print ' 1r 91                                        85   9G9.    '    
print ' 1r r9                          .h1:iSi       ;9, ;MH&     '    
print ' 1r ,9                          iS   iXr       s55H5S1     '    
print ' ,S,.8s                         ;3    ;95ss:        &:     '    
print '  19 ,9i                         r8s,   ,:sS1111h5i9A;.    '    
print '   8h iXh                         :1ShSsir...   .::is133i  '    
print '   :8S .99i                           ,;:ss1SSs        iX5 '    
print '     39. i9S:.                          ,i:  GAX5        HG'   
print '      ;8h  :;hhs.                   .;158r  58.8@1      :#8'   
print '       ,1Ss.  ,is5s1;;.      .,;rh1Ssir,  r9S. r@8     .AB.'   
print '         .11hs:   .iihsssssssshhri,     r9S:  ;HB.    rAX. '   
print '            .iisS1:,               ,:55rr:   rH3.    3@5   '   
print '               rXhshrhsiirririis515rr.      i:      X@G    '  
print '                 i&.  .:::::,::::.                    h@X. '   
print '                  13                                   5@S '   
print '                   h1                                   &#.'   
print '                   55                                   5#.'   
print '                   ;X,                                  5@,'   
print '                    G&                                 .&B.'   
print '                   :H9                                .&#; '   
print '                   1#                                .MM.  '   
```

#### 第二版
下面让这幅图可以横向移动30格

效果如图

![3-3](https://raw.githubusercontent.com/newton2ndlaw/computationalphysics_N2013301510086/master/Homework3/Homework3-3.jpg)

代码如下：
```python
import os
#              123456789 123456789 123456789 123456789 123456789 123456789 123456789 123456789
picture=['                     .;;hShhhhhh5s;;.                      '] #0
picture.append('                  ,:;rr:;,       .:irrr:                   ') #1
picture.append('             .i1hi:,                 .:s1hh:               ') #2
picture.append('          ,59hi:.  ..                    .rs1r             ') #3
picture.append('        rS9hs;;iiiii1s1i:                   ;35,           ') #4
picture.append('      ,9B@MS         .:iS5,                   18i          ') #5
picture.append('      39B@#H,  . .       r9;                   :8r         ') #6
picture.append('    ,3sh33hrrrrrrrsh1:    :G;                   ,8s        ') #7
picture.append('   ;As  . .        ,r35    i8:     ,:riiii::,    ,8r       ') #8
picture.append('  .8r                 59    hS   1ss      ^rh51i  :8,      ') #9
picture.append('  5h                   59.  5S  58sr.        .;S3; 13      ') #10
picture.append(' .8.                    h9s59; 18h@@h           ;S1 9i     ') #11
picture.append(' s1 .r                   ;5r   ;Gs9G1rhsrsshr:   .81i9     ') #12
picture.append(' sr i9                          ::888;     :s8S   ,G,9.    ') #13  
picture.append(' 1r 91                                        85   9G9.    ') #14 
picture.append(' 1r r9                          .h1:iSi       ;9, ;MH&     ') #15  
picture.append(' 1r ,9                          iS   iXr       s55H5S1     ') #16   
picture.append(' ,S,.8s                         ;3    ;95ss:        &:     ') #17   
picture.append('  19 ,9i                         r8s,   ,:sS1111h5i9A;.    ') #18
picture.append('   8h iXh                         :1ShSsir...   .::is133i  ') #19
picture.append('   :8S .99i                           ,;:ss1SSs        iX5 ') #20
picture.append('     39. i9S:.                          ,i:  GAX5        HG') #21
picture.append('      ;8h  :;hhs.                   .;158r  58.8@1      :#8') #22
picture.append('       ,1Ss.  ,is5s1;;.      .,;rh1Ssir,  r9S. r@8     .AB.') #23
picture.append('         .11hs:   .iihsssssssshhri,     r9S:  ;HB.    rAX. ') #24
picture.append('            .iisS1:,               ,:55rr:   rH3.    3@5   ') #25
picture.append('               rXhshrhsiirririis515rr.      i:      X@G    ') #26 
picture.append('                 i&.  .:::::,::::.                    h@X. ') #27
picture.append('                  13                                   5@S ') #28
picture.append('                   h1                                   &#.') #29
picture.append('                   55                                   5#.') #30
picture.append('                   ;X,                                  5@,') #31
picture.append('                    G&                                 .&B.') #32
picture.append('                   :H9                                .&#; ') #33
picture.append('                   1#                                .MM.  ') #34

import os

for i0 in range(30):
    i = os.system('cls')
    for i1 in range(35):
        for i2 in range(i0):
            print '',
        print picture[i1]

raw_input()
```

#### 第三版
接下来还会继续制作其他移动方式。

## 结论

待会弄个图片上去。

## 致谢

* 这次作业没有参考别人的结果。
