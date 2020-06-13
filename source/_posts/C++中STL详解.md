---
title: C++中STL详解
toc: true
author: Paul Yu
categories: c++
tags: STL
---

# 什么是STL

STL即标准模板库，是一个具有工业强度的，高效C++程序库，包含了计算科学领域常用的基本数据结构和算法。

STL的一个重要特点就是数据结构和算法的分离，使得STL变得非常通用。另一个重要特性是它S

STL中主要的三个组件

-   容器：是一种数据结构，如list,vector和deques。以模板类的方法提供。为了访问容器中的数据，可以使用由容器输出的迭代器。
-   迭代器：提供了访问容器对象的方法。可以使用一对迭代器指定list或vector中一定范围的对象。迭代器就如同一个指针。
-   算法：用来操纵容器中对象的方法。函数本身与他们操作的数据结构和类型无关，因此可以在从简单数组到高度复杂容器的任何数据结构上使用。

# vector

使用它时需要包含头文件：`#include<vector>`

## 初始化

```c++
(1) vector<int> a(10); //定义了10个整型元素的向量（尖括号中为元素类型名，它可以是任何合法的数据类型），但没有给出初值，其值是不确定的。
(2) vector<int> a(10,1); //定义了10个整型元素的向量,且给出每个元素的初值为1
(3) vector<int> a(b); //用b向量来创建a向量，整体复制性赋值
(4) vector<int> a(b.begin(),b.begin+3); //定义了a值为b中第0个到第2个（共3个）元素
(5) int b[7]={1,2,3,4,5,9,8};
    vector<int> a(b,b+7); //从数组中获得初值
```

## vector重要操作

```c++
（1）a.assign(b.begin(), b.begin()+3); //b为向量，将b的0~2个元素构成的向量赋给a
（2）a.assign(4,2); //是a只含4个元素，且每个元素为2
（3）a.back(); //返回a的最后一个元素
（4）a.front(); //返回a的第一个元素
（5）a[i]; //返回a的第i个元素，当且仅当a[i]存在2013-12-07
（6）a.clear(); //清空a中的元素
（7）a.empty(); //判断a是否为空，空则返回ture,不空则返回false
（8）a.pop_back(); //删除a向量的最后一个元素
（9）a.erase(a.begin()+1,a.begin()+3); //删除a中第1个（从第0个算起）到第2个元素，也就是说删除的元素从a.begin()+1算起（包括它）一直到a.begin()+         3（不包括它）
（10）a.push_back(5); //在a的最后一个向量后插入一个元素，其值为5
（11）a.insert(a.begin()+1,5); //在a的第1个元素（从第0个算起）的位置插入数值5，如a为1,2,3,4，插入元素后为1,5,2,3,4
（12）a.insert(a.begin()+1,3,5); //在a的第1个元素（从第0个算起）的位置插入3个数，其值都为5
（13）a.insert(a.begin()+1,b+3,b+6); //b为数组，在a的第1个元素（从第0个算起）的位置插入b的第3个元素到第5个元素（不包括b+6），如b为1,2,3,4,5,9,8         ，插入元素后为1,4,5,9,2,3,4,5,9,8
（14）a.size(); //返回a中元素的个数；
（15）a.capacity(); //返回a在内存中总共可以容纳的元素个数
（16）a.resize(10); //将a的现有元素个数调至10个，多则删，少则补，其值随机
（17）a.resize(10,2); //将a的现有元素个数调至10个，多则删，少则补，其值为2
（18）a.reserve(100); //将a的容量（capacity）扩充至100，也就是说现在测试a.capacity();的时候返回值是100.这种操作只有在需要给a添加大量数据的时候才         显得有意义，因为这将避免内存多次容量扩充操作（当a的容量不足时电脑会自动扩容，当然这必然降低性能） 
（19）a.swap(b); //b为向量，将a中的元素和b中的元素进行整体性交换
（20）a==b; //b为向量，向量的比较操作还有!=,>=,<=,>,<
```

## 元素遍历

1.  向向量中添加元素

    1.  ```c++
        vector<int> a;
        for(int i=0;i<10;i++)
            a.push_back(i);
        ```

    2.  也可以从现有向量中选择元素向向量中添加

        ```c++
        int a[6]={1,2,3,4,5,6};
        vector<int> b;
        vector<int> c(a,a+4);
        for(vector<int>::iterator it=c.begin();it<c.end();it++)
        b.push_back(*it);
        ```

2.  从向量中读取元素

    1.  通过下标方式读取

        ```c++
        int a[6]={1,2,3,4,5,6};
        vector<int> b(a,a+4);
        for(int i=0;i<=b.size()-1;i++)
            cout<<b[i]<<" ";
        ```

    2.  通过遍历器方式读取

        ```c++
        int a[6]={1,2,3,4,5,6};
        vector<int> b(a,a+4);
        for(vector<int>::iterator it=b.begin();it!=b.end();it++)
            cout<<*it<<" ";
        ```

        

## 几种重要算法

引入头文件`#include<algorithm>`.

```c++
（1）sort(a.begin(),a.end()); //对a中的从a.begin()（包括它）到a.end()（不包括它）的元素进行从小到大排列
（2）reverse(a.begin(),a.end()); //对a中的从a.begin()（包括它）到a.end()（不包括它）的元素倒置，但不排列，如a中元素为1,3,2,4,倒置后为4,2,3,1
（3）copy(a.begin(),a.end(),b.begin()+1); //把a中的从a.begin()（包括它）到a.end()（不包括它）的元素复制到b中，从b.begin()+1的位置（包括它）开        始复制，覆盖掉原有元素
（4）find(a.begin(),a.end(),10); //在a中的从a.begin()（包括它）到a.end()（不包括它）的元素中查找10，若存在返回其在向量中的位置
```

# List

list是一种序列式容器，功能和双向链表极其相似。list中数据元素通过链表指针串联成逻辑意义上的线性表。

## 构造函数

`list()` 声明一个空列表

`list(n)` 声明一个有n个元素的列表

`list(n,val)` 声明一个有n个元素的列表，每个元素的值都是val

`list(first,last)` 声明一个列表，其元素初始值来源于区间所指定的序列中的元素

## 常见方法

`begin()和end()`: 通过调用list容器成员函数begin()得到一个指向容器起始位置的iterator，可以调用list容器的end()函数得到list末端的下一个位置。相当于：int a[n]中的第n+1个位置a[n]，实际上是不存在的。

`push_back(E)`和`push_front(E)`: 将元素E插入到list中，前者是从list末端插入，而后者是从list的头部插入。

`empty()`: 判断list是否为空。

`resize(int n[,val])`: 如果调用该函数将list的长度改为只能容纳n个元素，超出的元素将被删除，也可以将元素都赋予同一个值val

`clear()`: 清空list中所有的元素

`front()`和`back()`：通过front()获取list容器的头部元素通过back()获取list最后一个元素。使用之前最好先判断list是否为空。

`pop_back()`和`pop_front()`：分别返回并删除最后一个元素和第一个元素。如果list为空则会出错

`assign()`: 两种用法：

		1. `l1.assign(n,val)`: 将l1中n个元素赋值为val。
  		2. `l1.assign(l2.begin(),l2.end())`: 将l2.begin()到l2.end()之间的数值赋给l1。

`swap():` 交换两个链表。l1.swap(l2);swap(l1,l2).

`reverse()`: 完成list的逆置。

`merge()`: 合并两个链表并使之默认升序。l1.merge(l2),l2变为空，l1中包含原来l1和l2中的元素，并且排好序。

```c++
#include <iostream>
#include <list>
 
using namespace std;

int main()
{
 list<int> l1;
 list<int> l2(2,0);
 list<int>::iterator iter;
 l1.push_back(1);
 l1.push_back(2);
 l2.push_back(3);
 l1.merge(l2,greater<int>());//合并后升序排列，实际上默认就是升序
 for(iter = l1.begin() ; iter != l1.end() ; iter++)
  {
   cout<<*iter<<" ";
   }
   cout<<endl<<endl;
   if(l2.empty())
   {
   cout<<"l2 变为空 ！！";
    }
   cout<<endl<<endl;
    return 0;
    }
```

`insert()`: 向指定位置插入一个或多个元素(三个重载)

-   l1.insert(l1.begin(),100): 在l1开始位置插入100
-   l1.insert(l1.begin(),2,100): 在l1开始位置插入两个100
-   l1.insert(l1.begin(),l2.begin(),l2.end()): 在l1的位置开始插入l2的所有元素。

`erase()`: 删除一个元素或一个区域的元素(两个重载)

-   l1.erase(l1.begin()): 将l1第一个元素删除
-   l1.erase(l1.begin(),l1.end()): 将l1中所有元素删除

