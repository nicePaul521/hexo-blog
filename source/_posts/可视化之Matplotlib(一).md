---
title: 可视化之Matplotlib(一)
author: paul yu
toc: true
categories:
- python库
- 可视化
tags: Matplotlib
---

Matplotlib是python中最基本的可视化工具，[官网](https://matplotlib.org/)提供了资料。使用时首先引用matplotlib库。

```python
import matplotlib as mpl
import matplotlib.pyplot as plt
%matplotlib inline
```

# Matplotlib

## 概述

Matplotlib总体来说包括两类元素：

-   **基础类**：线（line），点（marker），文字（text），图例（legend）,网格（grid）,标题（title），图片（image）等。
-   **容器类**：图（figure），坐标系（axes），坐标轴（axis）和刻度（tick）

基础类元素是想画出的标准对象，而容器类是基础类元素的寄居处。它们也有层级结构：`图->坐标系->坐标轴->刻度`

![](http://image-paul-blogs.test.upcdn.net/matplotlib/m01.jfif)

从上图可以看出：

-   图包含坐标系（多个）
-   坐标系由坐标轴构成（横轴xAxis和纵轴yAxis）
-   坐标轴上面有刻度（主刻度MajorTicks和副刻度MinorTicks）

python中万物皆对象，Matplotlib中这些元素也都是对象。下面代码打印出坐标系，坐标轴和刻度。

```python
fig = plt.figure()
ax = fig.add_subplot(1,1,1)
plt.show()

xax = ax.xaxis
yax = ax.yaxis

print( 'fig.axes:', fig.axes, '\n')
print( 'ax.xaxis:', xax )
print( 'ax.yaxis:', yax, '\n' )
print( 'ax.xaxis.majorTicks:', xax.majorTicks, '\n' )
print( 'ax.yaxis.majorTicks:', yax.majorTicks, '\n')
print( 'ax.xaxis.minorTicks:', xax.minorTicks )
print( 'ax.yaxis.minorTicks:', yax.minorTicks )
```

创建完以上四个容器元素后，可以在上面添加各种基础元素，比如：

-   在坐标轴和刻度上添加标签
-   在坐标系中添加线，点，网格，图例和文字
-   在图中添加图例

如下图所示：

![](http://image-paul-blogs.test.upcdn.net/matplotlib/m02.webp)

接下来介绍四大容器，先从图开始。

## 图

图是整个层级的顶部，在图中可以添加基本元素--`文字`。

```python
plt.figure()
plt.text(0.5,0.5,'Figure',ha='center',va='center',size=20,alpha=.5)
plt.xticks([]),plt.yticks([])
plt.show()
```

![](http://image-paul-blogs.test.upcdn.net/matplotlib/m03.webp)

用`plt.text()`函数，其参数解释如下：

-   第一，二个参数是指横轴和纵轴坐标
-   第三个参数字符是指要显示的内容
-   ha和va是横向和纵向位置
-   size设置字体大小
-   alpha设置透明度

在图中可以tu添加基本元素--`图片`

```python
from PIL import Image
plt.figure()
plt.xticks([]),plt.yticks([])
im = np.array(Image.open('...png'))
plt.imshow(im)
plt.show()
```

![](http://image-paul-blogs.test.upcdn.net/matplotlib/m04.webp)

用`Image.Open()`将图片转成像素存放在ndarry中，再用`plt.imshow()`来显示。

在图中可以添加基本元素--`折线`

```python
plt.figure()
plt.plot([0,1],[0,1])
plt.show()
```

![](http://image-paul-blogs.test.upcdn.net/matplotlib/m05.webp)

`plt.plot()`是用来画折线图的，前两个参数分别是x,y

每次在画东西，看起来实在图（Figure）中进行的，实际上是在坐标系（Axes）里面进行。一副图中可以有多个坐标系，因此在坐标系中画图更方便。

## 坐标系&子图

一幅图（Figure）可以有多个坐标系（Axes）,坐标系和子图有细微差异。

-   子图在母图的网格结构中一定是规则的
-   坐标系在母图中的网络结构中可以是不规则的

### 子图

把图想象成矩阵，那么子图就是矩阵中的元素，可以像定义矩阵那样定义子图-（行数，列数，第几个子图）。

>   subplot(rows,columns,i-th plots)

#### 1x2的子图

```python
plt.subplot(2,1,1)
plt.xticks([]),plt.yticks([])
plt.text(0.5,0.5,'subplot(2,1,1)',ha='center',va='center',size=20,alpha=.5)

plt.subplot(2,1,2)
plt.xticks([]),plt.yticks([])
plt.text(0.5,0.5,'subplot(2,1,2)',ha='center',va='center',size=20,alpha=.5)

plt.show()
```

![](http://image-paul-blogs.test.upcdn.net/matplotlib/m06.webp)

声明完子图后，下面所有的代码旨在这副子图中生效，直到声明下一个子图。

#### 2x1子图

```python
plt.subplot(1,2,1)
plt.xticks([]),plt.yticks([])
plt.text(0.5,0.5,'subplot(1,2,1)',ha='center',va='center',size=20,alpha=.5)

plt.subplot(1,2,2)
plt.xticks([]),plt.yticks([])
plt.text(0.5,0.5,'subplot(1,2,2)',ha='center',va='center',size=20,alpha=.5)
```

![](http://image-paul-blogs.test.upcdn.net/matplotlib/m07.webp)

#### 2x2子图

```python
fig,axes = plt.subplots(nrows=2,ncols=2)

for i,ax in enumerate(axes.flat):
    ax.set(xticks=[],yticks=[])
    s = 'subplot(2,2,'+str(i)+')'
    ax.text(0.5,0.5,s,ha='center',va='center',size=20,alpha=.5)
    
plt.show()
```

![](http://image-paul-blogs.test.upcdn.net/matplotlib/m11.png)

这次我们用坐标系来生成子图(子图是坐标系的特例)，`plt.subplots()`函数返回的axes是一个2*2的对象每个对象是一个坐标系对象，在for循环中用`ax.flat`将其打平，然后在每个ax上生成子图。

### 坐标系

坐标系比子图更加通用，有两种生成方式

-   用`gridspec`包加上`subplot()`
-   用`plt.axes()`

#### 不规则网络

```python
import matplotlib.gridspec as gridspec

G = gridspec.GridSpec(3,3)

ax1 = plt.subplot(G[0,:])
plt.xticks([]),plt.yticks([])
plt.text(0.5,0.5,'Axes 1',ha='center',va='center',size=20,alpha=.5)

ax1 = plt.subplot(G[1,:-1])
plt.xticks([]),plt.yticks([])
plt.text(0.5,0.5,'Axes 2',ha='center',va='center',size=20,alpha=.5)

ax1 = plt.subplot(G[1:,-1])
plt.xticks([]),plt.yticks([])
plt.text(0.5,0.5,'Axes 3',ha='center',va='center',size=20,alpha=.5)

ax1 = plt.subplot(G[-1,0])
plt.xticks([]),plt.yticks([])
plt.text(0.5,0.5,'Axes 4',ha='center',va='center',size=20,alpha=.5)

ax1 = plt.subplot(G[-1,1])
plt.xticks([]),plt.yticks([])
plt.text(0.5,0.5,'Axes 5',ha='center',va='center',size=20,alpha=.5)

plt.show()
```

![](http://image-paul-blogs.test.upcdn.net/matplotlib/m08.webp)

`GridSpec()`将整幅图分成3x3份赋值给G，利用`plt.subplot(G[])`生成了五个坐标系，G[]的用法和Numpy数组用法一样。

#### 大图套小图

```python
plt.axes([0.1,0.1,0.8,0.8])
plt.xticks([]),plt.yticks([])
plt.text(0.6,0.6,'axes[0.1,0.1,0.8,0.8]',ha='center',va='center',size=20,alpha=.5)

plt.axes([0.2,0.2,0.3,0.3])
plt.xticks([]),plt.yticks([])
plt.text(0.5,0.5,'axes[0.2,0.2,0.3,0.3]',ha='center',va='center',size=20,alpha=.5)

plt.show()
```

![](http://image-paul-blogs.test.upcdn.net/matplotlib/m09.webp)

`plt.axes([l,b,w,h])`其中`[l,b,w,h]`可以定义坐标系

-   l代表坐标系左边到Figure左边的水平距离
-   b代表坐标系底边到Figure底边的垂直距离
-   w代表坐标系的宽度
-   h代表坐标系的高度

如果l,b,w,h都小于1，则是标准化后的距离。比如Figure底边长度为10，坐标系底边到它的垂直距离为2，

#### 重叠图

```python
plt.axes([0.1,0.1,0.5,0.5])
plt.xticks([]),plt.yticks([])
plt.text(0.1,0.1,'axes([0.1,0.1,0.5,0.5])',ha='center',va='center',size=16,alpha=.5)

plt.axes([0.2,0.2,0.5,0.5])
plt.xticks([]),plt.yticks([])
plt.text(0.1,0.1,'axes([0.2,0.2,0.5,0.5])',ha='center',va='center',size=16,alpha=.5)

plt.axes([0.3,0.3,0.5,0.5])
plt.xticks([]),plt.yticks([])
plt.text(0.1,0.1,'axes([0.3,0.3,0.5,0.5])',ha='center',va='center',size=16,alpha=.5)

plt.axes([0.4,0.4,0.5,0.5])
plt.xticks([]),plt.yticks([])
plt.text(0.1,0.1,'axes([0.1,0.1,0.5,0.5])',ha='center',va='center',size=16,alpha=.5)

plt.show()
```

![](http://image-paul-blogs.test.upcdn.net/matplotlib/m10.webp)

### 两种生成坐标系的推荐代码

#### 代码1

同时生成图和坐标系

```python
fig,ax = plt.subplots()
ax.set(xticks = [],yticks=[])
s = 'Style 1\n\nfig,ax = plt.subplots()\nax.plot()'
ax.text(0.5,0.5,s,ha='center',va='center',size=16,alpha=.5)
```

![](http://image-paul-blogs.test.upcdn.net/matplotlib/m12.webp)

#### 代码2

先生成图再添加坐标系

```python
fig = plt.figure()
ax = fig.add_subplot(1,1,1)
ax.set(xticks=[],yticks=[])
s = 'Style 2\n\nfig,fig = plt.figure\nax = fig.add_subplot(1,1,1)\nax.plot()'
ax.text(0.5,0.5,s,ha='center',va='center',size=16,alpha=.5)
```

![](http://image-paul-blogs.test.upcdn.net/matplotlib/m13.webp)

## 坐标轴

一个坐标系（Axes），通常是二维，有两条坐标轴（Axis）：

-   横轴：XAxis
-   纵轴：YAxis

每个坐标轴包含两个元素

-   容器类元素[刻度]，该对象里还包含了`刻度本身`和`刻度标签`
-   基础类元素[标签]，该对象包含的是`坐标轴标签`

刻度和标签都是对象，下面代码通过改变他们的属性值进行可视化。

```python
fig,ax = plt.subplots()
ax.set_xlabel('Label on x-axis')
ax.set_ylabel('Label on y-axis')

for label in ax.xaxis.get_ticklabels():
    # label is a Text instance
    label.set_color(dt_hex)
    label.set_rotation(45)
    label.set_fontsize(20)
    
for line ax.yaxis.get_ticklines():
    # line is a line2D instance
    line.set_color(r_hex)
    line.set_markersize(500)
    line.set_markeredgewidth(30)
    
plt.show()
```

![](http://image-paul-blogs.test.upcdn.net/matplotlib/m14.webp)

第2和3行打印出x轴和y轴的标签，第5-9行处理[刻度]对象的刻度标签，将颜色设为深青色，字体大小设为20，旋转度为45度，第11-15行处理[刻度]对象的刻度本身（即一条短线）。将颜色设定为红色，标记长度和宽度分别为500和30.

## 刻度

刻度（tick）已经在坐标轴章节讲过，核心内容就是：

-   一条短线（刻度本身）
-   一串字符（刻度标签）

本节将深挖刻度，看看不同类型的刻度，需要用到各种各样的TickLocators。

### 前期工作

为了显示不同类型的刻度，首先定义一个`setup(ax)`函数，主要功能有：

-   去除左纵轴，右纵轴和上纵轴
-   去除y轴上的刻度
-   将x轴上的刻度位置定在轴底
-   设置主刻度和副刻度的长度和宽度
-   设置x轴和y轴的边界
-   将图中的patch设成完全透明

```python
import matplotlib.ticker as ticker

def setup(ax):
    ax.spines['right'].set_color('none')
    ax.spines['left'].set_color('none')
    ax.spines['top'].set_color('none')
    ax.yaxis.set_major_locator(ticker.NullLocator)
    ax.xaxis.set_ticks_position('bottom')
    
    ax.tick_parms(which='major',width=2.00)
    ax.tick_parms(which='major',length=10)
    ax.tick_parms(which='minor',width=0.75)
    ax.tick_parms(which='minor',width=2.5)
    
    ax.set_xlim(0,5)
    ax.set_ylim(0,1)
    
    ax.patch.set_alpha(0.0)
```

>   这些操作都是为了在下面显示刻度用

为了感受上面的每个操作对原图的影响，画出了6个子图，其中：

-   第一幅是原图
-   第二幅处理左，右，上轴
-   第三幅处理刻度标签
-   第四幅处理刻度尺寸
-   第五幅处理坐标轴边界
-   第六幅处理颜色和透明度

```python
fig,axes = plt.subplots(nrows=2,ncols=3,figsize=(8,4))

axes[0,0].set_title('Original')

axes[0,1].spines['right'].set_color('none')
axes[0,1].spines['left'].set_color('none')
axes[0,1].spines['top'].set_color('none')
axes[0,1].set_title('Handle Spines')

axes[0,2].yaxis.set_major_locator(ticker.NullLocator)
axes[0,2].xaxis.set_ticks_position('bottom')
axes[0,2].set_title('Handle Tick Labels')

axes[1,0].tick_parms(which='major',width=2.00)
axes[1,0].tick_parms(which='major',length=10)
axes[1,0].tick_parms(which='minor',width=0.75)
axes[1,0].tick_parms(which='minor',width=2.5)
axes[1,0].set_title('Handle Tick Width/Length')

axes[1,1].set_xlim(0,5)
axes[1,1].set_ylim(0,1)
axes[1,1].set_title('Handle Axis Limit')

axes[1,2].patch.set_color(black)
axes[1,2].patch.set_alpha(.3)
axes[1,2].set_title('Handle patch color')

plt.tight_layout()
plt.show()
```

![](http://image-paul-blogs.test.upcdn.net/matplotlib/m15.webp)

将上面效果全部合并，将坐标系中所有元素都去掉，只保留x轴来添加各种刻度。

### 刻度展示

不同的locator()可以生成不同的刻度对象，我们研究以下8种。

1.  `NullLocator()`:空刻度
2.  `MutipleLocator(a)`：刻度间隔=标量a
3.  `FixedLocator(a)`:刻度位置由数组a决定
4.  `LinearLocator(a)`:刻度数目=a
5.  `IndexLocator(b,o)`:刻度间隔=标量b，偏移量=标量o
6.  `AutoLocator()`:根据默认设置决定
7.  `MaxNLocator(a)`:最大刻度数目=标量a
8.  `LogLocator(b,n)`:基数=标量b，刻度数目=标量n

```python
plt.figure(figsize=(8,6))
n = 8

#Null Locator
ax = plt.subplot(n,1,1)
setup(ax)
ax.xaxis.set_major_locator(ticker.NullLocator())
ax.xaxis.set_minor_locator(ticker.NullLocator())
ax.text(0.0,0.1,'NullLocator',fontsize=14,transform=ax.transAxes)

# Multiple Locator
ax = plt.subplot(n,1,2)
setup(ax)
ax.xaxis.set_major_locator(ticker.MutipleLocator(0.5))
ax.xaxis.set_minor_locator(ticker.MutipleLocator(0.1))
ax.text(0.0,0.1,'MultipleLocator',fontsize=14,transform=ax.transAxes)

# Fixed Locator
ax = plt.subplot(n,1,3)
setup(ax)
majors = [0,1,5]
ax.xaxis.set_major_locator(ticker.FixedLocators(majors))
minors = np.linspace(0,1,11)[1:-1]
ax.xaxis.set_minor_locator(ticker.FixedLocators(minors))
ax.text(0.0,0.1,'FixedLocator',fontsize=14,transform=ax.transAxes)

#Linear Locator
ax = plt.subplot(n,1,4)
setup(ax)
ax.xaxis.set_major_locator(ticker.LinearLocator(3))
ax.xaxis.set_minor_locator(ticker.LinearLocator(11))
ax.text(0.0,0.1,'LinearLocator',fontsize=14,transform=ax.transAxes)

#Index Locator
ax = plt.subplot(n,1,5)
setup(ax)
ax.plot(range(0,5),[0*5],color='white')
ax.xaxis.set_major_locator(ticker.IndexLocator(base=.5,offset=.25))
ax.text(0.0,0.1,'IndexLocator',fontsize=14,transform=ax.transAxes)

# Auto Locator
ax = plt.subplot(n,1,6)
setup(ax)
ax.xaxis.set_major_locator(ticker.AutoLocator())
ax.xaxis.set_minor_locator(ticker.AutoMinorLocator())
ax.text(0.0,0.1,'AutoLocator',fontsize=14,transform=ax.transAxes)

#MaxN Locator
ax = plt.subplot(n,1,7)
setup(ax)
ax.xaxis.set_major_locator(ticker.MaxNLocator(4))
ax.xaxis.set_minor_locator(ticker.MaxNLocator(40))
ax.text(0.0,0.1,'MaxNlocator',fontsize=14,transform=ax.transAxes)

#Log Locator
ax = plt.subplot(n,1,8)
setup(ax)
ax.set_xlim(10**3,10**10)
ax.set_xscale('log')
ax.xaxis.set_major(ticket.LogLocator(base=10.0,numticks=15))
ax.text(0.0,0.1,'LogLocator',fontsize=14,transform=ax.transAxes)

plt.subplots_adjust(left=0.05,right=0.95,bottom=0.05,top=1.05)

plt.show()
```

![](http://image-paul-blogs.test.upcdn.net/matplotlib/m16.webp)

## 基础元素

目前已经介绍完四个重要容器以及它们的层级关系，但要画出一幅有内容的图，还需要在容器中添加基础元素如线（line），点（marker），文字（text），图例（legend），网格（grid），标题（title），图片（image）。具体来说：

-   画一条线：`plt.plot()、ax.plot()`
-   画个记号：`plt.scatter()、ax.scatter()`
-   添加文字：`plt.text()、ax.text()`
-   添加图例：`plt.legend()、ax.legend()`
-   添加图片：`plt.imshow()、ax.imshow()`

![](http://image-paul-blogs.test.upcdn.net/matplotlib/m17.webp)

# 画图

## 概述

在做图表设计时，经常面临者怎么选用合适的图表，图表展示的关系分为四大类：

1.  比较
2.  联系
3.  比较
4.  构成

![](http://image-paul-blogs.test.upcdn.net/matplotlib/m18.webp)

### 配置参数

-   `axex`: 设置坐标轴边界和表面的颜色、坐标刻度值大小和网格的显示
-   `figure`: 控制dpi、边界颜色、图形大小、和子区( subplot)设置
-   `font`: 字体集（font family）、字体大小和样式设置
-   `grid`: 设置网格颜色和线性
-   `legend`: 设置图例和其中的文本的显示
-   `line`: 设置线条（颜色、线型、宽度等）和标记
-   `patch`: 是填充2D空间的图形对象，如多边形和圆。控制线宽、颜色和抗锯齿设置等。
-   `savefig`: 可以对保存的图形进行单独设置。例如，设置渲染的文件的背景为白色。
-   `verbose`: 设置matplotlib在执行期间信息输出，如silent、helpful、debug和debug-annoying。
-   `xticks`和`yticks`: 为x,y轴的主刻度和次刻度设置颜色、大小、方向，以及标签大小。

### 线条相关属性标记设置

| 线条风格linestype或ls | 描述       |
| --------------------- | ---------- |
| '-'                   | 实线       |
| ':'                   | 虚线       |
| '_'                   | 破折线     |
| 'None',''             | 什么都不画 |
| '-.'                  | 点划线     |

### 线条标记

```python
标记maker            描述

‘o’                 圆圈  
‘.’                 点
‘D’                 菱形  
‘s’                 正方形
‘h’                 六边形1    
‘*’                 星号
‘H’                 六边形2    
‘d’                 小菱形
‘_’                 水平线 
‘v’                 一角朝下的三角形
‘8’                 八边形 
‘<’                 一角朝左的三角形
‘p’                 五边形 
‘>’                 一角朝右的三角形
‘,’                 像素  
‘^’                 一角朝上的三角形
‘+’                 加号  
‘\  ‘               竖线
‘None’,’’,’ ‘       无   
‘x’                 X
```

### 颜色

```python
别名             颜色   

b               蓝色  
g               绿色
r               红色  
y               黄色
c               青色
k               黑色   
m               洋红色 
w               白色
```

如果这些颜色不够用，可以通过其他两种方式定义颜色值:

-   HTML十六进制字符串：c = '#123456'
-   归一化到[0,1]的RGB元组：c = (0.3,0.3,0.4)

### plot属性

```python
属性                      值类型
alpha                   浮点值
animated                [True / False]
antialiased or aa       [True / False]
clip_box                matplotlib.transform.Bbox 实例
clip_on                 [True / False]
clip_path               Path 实例， Transform，以及Patch实例
color or c              任何 matplotlib 颜色
contains                命中测试函数
dash_capstyle           ['butt' / 'round' / 'projecting']
dash_joinstyle          ['miter' / 'round' / 'bevel']
dashes                  以点为单位的连接/断开墨水序列
data                    (np.array xdata, np.array ydata)
figure                  matplotlib.figure.Figure 实例
label                   任何字符串
linestyle or ls         [ '-' / '--' / '-.' / ':' / 'steps' / ...]
linewidth or lw         以点为单位的浮点值
lod                     [True / False]
marker                  [ '+' / ',' / '.' / '1' / '2' / '3' / '4' ]
markeredgecolor or mec  任何 matplotlib 颜色
markeredgewidth or mew  以点为单位的浮点值
markerfacecolor or mfc  任何 matplotlib 颜色
markersize or ms        浮点值
markevery               [ None / 整数值 / (startind, stride) ]
picker                  用于交互式线条选择
pickradius              线条的拾取选择半径
solid_capstyle          ['butt' / 'round' / 'projecting']
solid_joinstyle         ['miter' / 'round' / 'bevel']
transform               matplotlib.transforms.Transform 实例
visible                 [True / False]
xdata                   np.array
ydata                   np.array
zorder                  任何数值
```



## 直方图

直方图（histogram chart）,又称质量分布图，是一种统计报告图，用一系列高度不等的纵向条纹或线段表示数据分布情况，一般用横轴表示数据类型，纵轴表示分布情况。在Matplotlib里的语法是：

-   `plt.hist()`
-   `ax.hist()`

```python
fig,(ax0,ax1) = plt.subplots(nrows=2,figsize=(9,6))     #在窗口上添加2个子图
sigma = 1   #标准差
mean = 0    #均值
x=mean+sigma*np.random.randn(10000)   #正态分布随机数
ax0.hist(x,bins=40,normed=False,histtype='bar',facecolor='yellowgreen',alpha=0.75)   #normed是否归一化，histtype直方图类型，facecolor颜色，alpha透明度
ax1.hist(x,bins=20,normed=1,histtype='bar',facecolor='pink',alpha=0.75,cumulative=True,rwidth=0.8) #bins柱子的个数,cumulative是否计算累加分布，rwidth柱子宽度
plt.show()  #所有窗口运行
```

![](http://image-paul-blogs.test.upcdn.net/matplotlib/m20.webp)

>   x: 类型可以是series，list或者ndarry
>
>   bins: 分成多少堆
>
>   facecolor/color:前景色 

## 散点图

散点图用两组数据构成坐标点，考察坐标点的分布，判断两个变量是否存在某种联系的分布模式。在Matplotlib里的语法是：

-   `plt.scatter()`
-   `ax.scatter()`

```python
fig = plt.figure(4)          #添加一个窗口
ax =fig.add_subplot(1,1,1)   #在窗口上添加一个子图
x=np.random.random(100)      #产生随机数组
y=np.random.random(100)      #产生随机数组
ax.scatter(x,y,s=x*1000,c='y',marker=p,alpha=0.5,lw=2,facecolors='none')  #x横坐标，y纵坐标，s图像大小，c颜色，marker图片，lw图像边框宽度
plt.show()  #所有窗口运行
```

>   x,y: Series，list或者ndarray
>
>   s: 点的大小粗细
>
>   marker: 标记样式
>
>   c: 颜色

![](http://image-paul-blogs.test.upcdn.net/matplotlib/m21.webp)

## 柱状图

用来表示多种类型数据的分布情况，可以纵向或横向反映数据大小。在Matplotlib中的用法如下：

-   `plt.bar()`
-   `ax.bar()`

```python
plt.figure(3)
x_index = np.arange(5)   #柱的索引
x_data = ('A', 'B', 'C', 'D', 'E')
y1_data = (20, 35, 30, 35, 27)
y2_data = (25, 32, 34, 20, 25)
bar_width = 0.35   #定义一个数字代表每个独立柱的宽度

rects1 = plt.bar(x_index, y1_data, width=bar_width,alpha=0.4, color='b',label='legend1')            #参数：左偏移、高度、柱宽、透明度、颜色、图例
rects2 = plt.bar(x_index + bar_width, y2_data, width=bar_width,alpha=0.5,color='r',label='legend2') #参数：左偏移、高度、柱宽、透明度、颜色、图例
#关于左偏移，不用关心每根柱的中心不中心，因为只要把刻度线设置在柱的中间就可以了
plt.xticks(x_index + bar_width/2, x_data)   #x轴刻度线
plt.legend()    #显示图例
plt.tight_layout()  #自动控制图像外部边缘，此方法不能够很好的控制图像间的间隔
plt.show()
```

![](http://image-paul-blogs.test.upcdn.net/matplotlib/m19.webp)

## 折线图

折线图显示数据变化的趋势，在Matplotlib中的用法是：

-   `plt.plot()`
-   `ax.plot()`

```python
import matplotlib.pyplot as plt

## 提供输入值
input_value = [1, 2, 3, 4, 5]
## 提供输出值
squares = [1, 4, 9, 16, 25]

## 将输入值与输出值相对应
plt.plot(input_value, squares, linewidth=5)
plt.title('title', fontsize=24)
plt.xlabel('xvalue', fontsize=24)
plt.ylabel('yvalue', fontsize=24)
plt.tick_params(axis='both', labelsize=15)

plt.show()
```

![](http://image-paul-blogs.test.upcdn.net/matplotlib/m22.webp)

## 饼状图

饼状图（pie chart）是一个划分为几个扇形的圆形统计图表，用于描述量，频率或百分比之间的相对关系。每个扇区的面积大小为其所表示的数量的比例。在Matplotlib中的语法是

-   `plt.pie()`
-   `ax.pie()`

pie函数参数详解

```python
x       :(每一块)的比例，如果sum(x) > 1会使用sum(x)归一化；
labels  :(每一块)饼图外侧显示的说明文字；
explode :(每一块)离开中心距离；
startangle :起始绘制角度,默认图是从x轴正方向逆时针画起,如设定=90则从y轴正方向画起；
shadow  :在饼图下面画一个阴影。默认值：False，即不画阴影；
labeldistance :label标记的绘制位置,相对于半径的比例，默认值为1.1, 如<1则绘制在饼图内侧；
autopct :控制饼图内百分比设置,可以使用format字符串或者format function
        '%1.1f'指小数点前后位数(没有用空格补齐)；
pctdistance :类似于labeldistance,指定autopct的位置刻度,默认值为0.6；
radius  :控制饼图半径，默认值为1；
counterclock ：指定指针方向；布尔值，可选参数，默认为：True，即逆时针。将值改为False即可改为顺时针。
wedgeprops ：字典类型，可选参数，默认值：None。参数字典传递给wedge对象用来画一个饼图。例如：wedgeprops={'linewidth':3}设置wedge线宽为3。
textprops ：设置标签（labels）和比例文字的格式；字典类型，可选参数，默认值为：None。传递给text对象的字典参数。
center ：浮点类型的列表，可选参数，默认值：(0,0)。图标中心位置。
frame ：布尔类型，可选参数，默认值：False。如果是true，绘制带有表的轴框架。
rotatelabels ：布尔类型，可选参数，默认为：False。如果为True，旋转每个label到指定的角度。
```

```python
import matplotlib.pyplot as plt
plt.rcParams['font.sans-serif']=['SimHei'] #用来正常显示中文标签

labels = ['娱乐','育儿','饮食','房贷','交通','其它']
sizes = [2,5,12,70,2,9]
explode = (0,0,0,0.1,0,0)
plt.pie(sizes,explode=explode,labels=labels,autopct='%1.1f%%',shadow=False,startangle=150)
plt.title("饼图示例-8月份家庭支出")
plt.show()
```

![](http://image-paul-blogs.test.upcdn.net/matplotlib/m23.png)