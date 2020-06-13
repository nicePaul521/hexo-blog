---
title: K-均值聚类
author: Paul Yu
toc: false
categories: 
- 机器学习
- 无监督学习
tags: 聚类
---

聚类是一种无监督学习，将相似对象归为一个簇中，簇内的对象越相似，聚类的效果越好。k-均值聚类是因为它可以发现k个不同的簇，且每个簇的中心采用所含值的均值计算而成。

聚类与分类最大的不同：分类的目标事先已知，而聚类的类别没有预先定义。聚类将相似对象归为一类，不相似对象归为不同簇。`相似`概念取决于选择的相似的计算方法。

>   优点：容易实现
>
>   缺点：容易收敛到**局部最小值**，在大规模数据上收敛较慢

k-均值聚类算法伪代码：

```python
创建k个质点作为质心(随机选择)
当任意一个点的簇分配结果发生改变时
	对数据集中的每个数据点
    	对每个质心
        	计算质心与数据点之间的距离
        将数据点分配到距其最近的簇
    对每个簇，计算簇中所有点的均值并将均值作为质心
```

k均值算法的性能受所选距离计算方法的影响。

```python
from numpy import *
#加载文本
def loadDataSet(fileName):      #general function to parse tab -delimited floats
    dataMat = []                #assume last column is target value
    fr = open(fileName)#打开文件
    for line in fr.readlines():#逐行读取文本
        curLine = line.strip().split('\t')#去除多余空格并按制表符切割该字符串返回字符串列表
        fltLine = map(float,curLine) #map all elements to float()
        dataMat.append(fltLine)#封装成列表的列表，容易转换成矩阵
    return dataMat
#计算两个向量之间的欧式距离，度量两个向量之间的相似性
def distEclud(vecA, vecB):
    return sqrt(sum(power(vecA - vecB, 2))) #la.norm(vecA-vecB)
#初始化k个质心
def randCent(dataSet, k):
    n = shape(dataSet)[1]#获取数据集的特征数
    centroids = mat(zeros((k,n)))#create centroid mat
    for j in range(n):#create random cluster centers, within bounds of each dimension
        minJ = min(dataSet[:,j]) #压缩行，得到j列最小值
        rangeJ = float(max(dataSet[:,j]) - minJ)#j列最大值与最小值之差
        centroids[:,j] = mat(minJ + rangeJ * random.rand(k,1))#得到介于范围的随机取值，注意广播机制，返回k*1的矩阵
    return centroids#返回包含k个质点的矩阵
```

>   random.rand(d1,d2,d3...)生成多维的矩阵，矩阵每个取值是介于0-1的正态分布随机数

`loadDataSet()`函数将文本文件导入到一个列表中，将每一行为tab分割的浮点数。每个列表会被添加到dataMat中，该返回值是一个包含列表的列表。这种格式容易被封装到矩阵中。

`distEclud()`计算两个向量的**欧式距离**。

`randCent()`函数为给定的数据集构建一个包含k个质心的集合。随机质心必须要在整个数据集的边界之内。这可以通过找到每一维的最小最大值来完成，然后生成0-1.0之间的随机数并通过取值范围和最小值，确保随机点在数据的边界之中。

准备完成后，就可以实现K-均值算法。该算法会创建k个质心，然后将每个点分配到最近的质心，再重新计算质心。重复数次直到簇分配结果不再改变为止。

```python
def kMeans(dataSet, k, distMeas=distEclud, createCent=randCent):
    m = shape(dataSet)[0]
    clusterAssment = mat(zeros((m,2)))#create mat to assign data points 
                                      #to a centroid, also holds SE of each point
    centroids = createCent(dataSet, k)#随机K个质点
    clusterChanged = True
    while clusterChanged:
        clusterChanged = False
        for i in range(m):#for each data point assign it to the closest centroid
            minDist = inf; minIndex = -1
            for j in range(k):
                distJI = distMeas(centroids[j,:],dataSet[i,:])#对数据集中每个点与每个质点的距离进行比较
                if distJI < minDist:
                    minDist = distJI; minIndex = j#得到距离每个样本点最近的质点
            if clusterAssment[i,0] != minIndex: clusterChanged = True#对质点比较结束后判断该样本点的簇索引是否发生改变
            clusterAssment[i,:] = minIndex,minDist**2#更新数据点的簇索引及误差
        print centroids
        for cent in range(k):#recalculate centroids
            ptsInClust = dataSet[nonzero(clusterAssment[:,0].A==cent)[0]]#get all the point in this cluster
            centroids[cent,:] = mean(ptsInClust, axis=0) #assign centroid to mean 
    return centroids, clusterAssment
```

>   `clusterAssment[:,0].A`返回所有数据点的簇索引数组，然后找到簇索引为cent的布尔索引。
>
>   `nonzero()[0]`：返回布尔索引中不为0，即为true的索引的行索引。利用行索引得到数据集中簇索引为cent的所有数据点。

`kmeans()`函数接受4个参数。数据集及簇的数目时必选参数，而计算距离和创建初始质心的函数都是可选的。该函数先确定数据集中数据点的个数，然后创建一个矩阵存储每个点的簇分配结果，簇分配结果矩阵`clusterAssment`包含两列：**一列记录簇索引值**，**第二列存储误差**。误差指当前点到簇质心的距离。可以用该误差评价聚类效果。

按上述方式(`计算质心-分配-重新计算`)，反复迭代，直到所有数据点的簇分配结果不再改变为止。标志向量**clusterChanged**，如果该值为true。则继续迭代。接下来遍历所有数据找到距离每个点最近的质心，这可以对每个点遍历所有质心并计算点到每个质心的距离来完成。

最后，遍历所有质心并更新它们的取值。实现步骤如下：首先通过数组过滤来获得给定簇的所有点；然后计算所有点的均值，`axis=0`表示沿矩阵**列方向**进行均值计算；最后程序返回所有类质心与点分配结果。

k均值聚类算法收敛但聚类效果较差的原因是，k均值聚类算法收敛到了局部最小值，而非全局最小值。一种用于度量聚类效果的指标是SSE，即平方误差和。SSE越小，说明数据点越接近它们的质心，聚类效果也越好。一种降低SSE值的方法是增加簇数目，但违背了聚类的目标，聚类的目标是在保持簇数目不变的情况下提高簇的质量。

为了克服k-均值聚类算法收敛于局部最小值的问题，有人提出了另一种被称为二分K-均值的算法，该算法首先将所有点作为一个簇，然后将该簇一分为二。之后选择其中一个簇继续划分，选择哪一个簇进行划分取决于对其划分是否可以最大降低SSE的值。上述基于SSE的划分过程不断重复，直到得到用户指定的簇数目为止。

二分K-均值伪代码如下：

```python
将所有点看成一个簇
当簇数目小于k时
对于每一个簇
	计算总误差
    在给定的簇上面进行k-均值聚类(k=2)
    计算将该簇一分为二之后的总误差
选择使得误差最小的那个簇进行划分操作
```

```python
def biKmeans(dataSet, k, distMeas=distEclud):
    m = shape(dataSet)[0]
    clusterAssment = mat(zeros((m,2)))#生成m*2大小的零矩阵
    centroid0 = mean(dataSet, axis=0).tolist()[0]#对数据集按列求均值，并转换成列表
    centList =[centroid0] #初始化质心列表，只含有一个质心
    for j in range(m):#计算数据集样本点的初始误差
        clusterAssment[j,1] = distMeas(mat(centroid0), dataSet[j,:])**2
    while (len(centList) < k):
        lowestSSE = inf
        for i in range(len(centList)):#遍历每个簇，对每个簇进行分裂
            ptsInCurrCluster = dataSet[nonzero(clusterAssment[:,0].A==i)[0],:]#get the data points currently in cluster i
            centroidMat, splitClustAss = kMeans(ptsInCurrCluster, 2, distMeas)#返回质心矩阵与数据集簇索引矩阵
            sseSplit = sum(splitClustAss[:,1])#compare the SSE to the currrent minimum
            sseNotSplit = sum(clusterAssment[nonzero(clusterAssment[:,0].A!=i)[0],1])#
            print "sseSplit, and notSplit: ",sseSplit,sseNotSplit
            if (sseSplit + sseNotSplit) < lowestSSE:#分裂后与分裂前的误差进行比较
                bestCentToSplit = i#得到这一轮分裂效果最好的簇索引
                bestNewCents = centroidMat#得到分裂效果最好的质心矩阵
                bestClustAss = splitClustAss.copy()#得到数据集簇索引矩阵的副本
                lowestSSE = sseSplit + sseNotSplit#更新当前误差
        bestClustAss[nonzero(bestClustAss[:,0].A == 1)[0],0] = len(centList) #更新分裂后数据集的簇索引
        bestClustAss[nonzero(bestClustAss[:,0].A == 0)[0],0] = bestCentToSplit
        print 'the bestCentToSplit is: ',bestCentToSplit
        print 'the len of bestClustAss is: ', len(bestClustAss)
        centList[bestCentToSplit] = bestNewCents[0,:].tolist()[0]#更新质点矩阵 
        centList.append(bestNewCents[1,:].tolist()[0])
        clusterAssment[nonzero(clusterAssment[:,0].A == bestCentToSplit)[0],:]= bestClustAss#重新计算误差
    return mat(centList), clusterAssment#返回质点集合与数据集簇索引矩阵
```

>   `mean(dataSet,axis=0)`,对每列求均值，压缩行，返回一个**1*n**的矩阵，`tolist()`将其转换为列表的形式，即[[]]，取第一个元素[0],则得到[]列表。

该函数首先创建一个矩阵来存储数据集中每个点的簇分配结果及平方误差，然后计算整个数据集的质心，并使用一个列表保留所有质心。得到质心后，就可以遍历数据集中所有点来计算每个点到质心的误差值。

在while循环中，不停的对簇进行划分，直到得到想要的簇数目为止。然后遍历所有簇来决定最佳的簇进行划分。为此需要比较划分前后的SSE值。对每个簇，将该簇中的所有点看成一个小的数据集**ptsInCurrCluster**。将**ptsIncurrCluster**输入函数`kMeans()`中进行处理**(k=2)**.k-均值算法会生成两个质心(簇)，同时给出每个簇的误差值。这些误差与剩余数据集的误差作为本次划分的误差。如果该划分的SSE值最小，则本次划分被保存。一旦决定了要划分的簇，接下来要实际执行划分操作，即将要划分的簇中所有点的簇分配结果进行修改即可。当使用`kMeans()`函数并且指定簇数位2时，会得到两个编号分别为0和1的结果簇。需要将这些簇编号修改为划分簇及新加簇的编号，该过程通过两个数组过滤器来完成。最后新的簇分配结果被更新，新的质心会被添加到`centList`中。