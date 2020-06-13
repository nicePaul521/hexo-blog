---
title: Java基础
date: 2020-02-12
author: Paul Yu
toc: true
summary: 总结了Java面向对象编程的基本语法，以及常见的数据结构等。
categories: Java
tags: 基础
---

# 成员变量与局部变量

通常将类的属性称为全局变量（成员变量），将方法中的属性称为局部变量。全局变量声明在类体中。

## 基本数据类型

![基本数据结构](http://image-paul-blogs.test.upcdn.net/java/001.png)

整型数据在Java程序中可分为十进制，八进制和十六进制。八进制必须以0开头，如**0123**，十六进制必须以<em>0x</em>或<em>0X</em>开头，如**0x25**。

整型根据它所占内存大小的不同可分为byte，short,int 和long四种类型，他们具有不同的取值范围。

![17zxYt.png](http://image-paul-blogs.test.upcdn.net/java/002.png)

浮点类型标识有小数部分的数字，浮点类型可分为单精度浮点类型（float）和双精度浮点类型（double），默认情况下小数都被看成double型数据，若使用float型数据，则需要在小数后面加上F或f。声明float类变量时如果不加f，系统会认为变量是double类型而出错。

![浮点数据类型](http://image-paul-blogs.test.upcdn.net/java/003.png)

字符类型用于存储单个字符，占用16位内存空间。Java也可以把字符当作证书对待。若想得到一个0~65536之间的数所代表的unicode表相应位置上的字符，须使用char显式转换。

```java
public class Gess{
	public static void main(String[] args){
        char word='d',word2='@';
        int p=23045,p2=45213;
        System.out.println("d在unicode表中顺序位置是："+(int)word);
        System.out.println("@在unicode表中顺序位置是："+(int)word2);
        System.out.println("unicode表中第23045位是："+(int)p);
    }
}
```

![](http://image-paul-blogs.test.upcdn.net/java/004.png)

布尔类型又称逻辑类型，通过关键字boolean来定义布尔类型变量，只有true和false两个值，且不能与整数类型转换。

## 常量与变量

标识符用来标识类名、变量名、方法名、数组名、文件名的有效字符序列。

> Java规定标识符由任意顺序的字母、下划线(_)、美元符号($)和数字组成。并且第一个字符不能是数字

声明变量就是要告诉编译器这个变量的数据类型，在程序运行过程中，空间内的值是变化的，这个内存空间就称为变量。这个空间的名字就是变量名。

在程序运行过程一直不会改变的量称为常量，常量在整个程序运行期间只能被赋值一次。

> final 数据类型 常量名称[=值]

### 成员变量

在类体中所定义的变量称为成员变量，成员变量在整个类中都有效。可分为静态变量和实例变量。`static 数据类型 变量名称[=值]`，`数据类型 变量名称[=值]`。前者为静态变量，后者为实例变量。静态变量的有效范围可以跨类。对于静态变量除了能在定义它的类内存取，也可以直接以`类名.静态变量`的方法在其他类中使用。

### 局部变量

在类的方法体中定义的变量称为局部变量。局部变量只在当前定义的方法中有效。当方法调用结束后，则会释放内存空间。局部变量名与成员变量相同时，成员变量将被隐藏。

## 运算符

### 赋值运算符

以符号`=`表示。将右方的操作数所含的值赋给左方的操作数。赋值运算符处理时会先取得右方表达式处理的结果，因此一个表达式含有两个以上的`=`运算符，会从最右方的`=`开始处理。如`c=b=a+4`，将a与4的值赋给变量b，然后再赋给c。

### 算术运算符

![](http://image-paul-blogs.test.upcdn.net/java/005.png)

### 逻辑运算符

![](http://image-paul-blogs.test.upcdn.net/java/006.png)

> &&与&的区别：
>
> 逻辑运算符`&&`针对boolean类型的表达式进行判断，当第一个表达式为false时则不会判断第二个表达式。而`&`则会两个表达式都会判断。前者称为`短路`运算符，后者称为`非短路`运算。

### 位运算符

位运算是完全针对位方面的操作，整型数据在内存中以二进制形式表示。左边最高位是符号位，最高位0表示正数，若为1则表示负数。负数以补码存储。

- `按位与(&)`:两个整型数对应位都是1，则结果为1，反之为0。
- `按位或(|)`:两个操作数对应位都是0，则结果为0，反之为1。
- `按位取反(~)`:单目运算符，将操作数二进制中的1改为0，0改为1。
- `按位异或(^)`:两个操作数对应位相同，则结果为0，反之为1。
- 移位操作
  - `<<`:左移，右边移空的部分补0。
  - `>>`:右移，如果最高位为0，左边移空位置填0，否则填1。
  - `>>>`:无符号右移，无论高位是0还是1，左侧移空位置均填0。

### 三元运算符

> 条件式？值1:值2

若条件表达式为true，则整个表达式取值1，否则取值2。

##### 运算符优先级

`自增自减运算符>算数运算>比较运算>逻辑运算>赋值运算`

![](http://image-paul-blogs.test.upcdn.net/java/007.png)

## 数据类型转换

### 隐式转换

从低类型到高类型的转换，自动由精度低向精度高转换。精度类型从低到高排列顺序为：`byte<short<int<long<float<double`

### 显式类型转换

当把高精度变量的值赋给低精度的变量时，必须使用显式类型（强制类型）转换。

> (类型名)要转换的值

```java
int a = (int)45.23;		//45
long y = (long)456.6f;	//456
int b = (int)'d';  		//100
```

# 流程控制

## 条件语句

if[...else if[...else]]多分支语句用于针对某一事件的多种情况进行处理。

语法如下：

```java
if (条件表达式1){
	语句序列1
}
else if (条件表达式2){
	语句序列2
}
...
else if(条件表达式n){
	语句序列n
}
else{
 	语句序列n+1
}
```

>   - 条件表达式1~条件表达式n；可以由多个表达式组成，但最后返回结果一定为boolean类型。
>   - 语句序列：可以是一条或多条语句，当某个语句表达式为true时，则执行该表达式对应语句序列，并省略其他语句序列。

![多分支执行流程](http://image-paul-blogs.test.upcdn.net/java/008.png)

在Java中使用switch多分支语句，将动作组织起来，实现`多选一`操作。

语法如下：

```
switch(表达式):
{
	case 常量值1:语句块1 [break;]
	...
	case 常量值n:语句块n [break;]
	[default:语句块n+1 [break;]]
}
```

>   * 表达式的值必须是整型，字符型或字符串类型，常量值1~n也必须是整型、字符型或字符串类型。
>   * 如果某个表达式的值和某个case后面的常量值相同，则执行case后面的语句块，直到遇到break语句跳出switch语句。
>   * 如果该case语句中没有break语句，则继续执行后面case语句，直到遇到break语句为止。
>   * 如果和所有case常量值不匹配，则执行default中的语句块。

## 循环语句

while和do...while语句的执行流程如下：



<img src="http://image-paul-blogs.test.upcdn.net/java/009.png" alt="while语句" style="zoom:80%;" />

![do while](http://image-paul-blogs.test.upcdn.net/java/010.png)

>   while循环与do...while类似，它们之间的区别是，while语句先判断条件是否成立再执行循环体，而do...while则是先执行一次循环在判断条件是否成立。此外do...while在结尾处多了一个分号。

for语句，语法如下：

```java
for(表达式1;表达式2;表达式3)
{
	语句序列
}
```

* 表达式1：初始化表达式，负责完成变量初始化。
* 表达式2：循环条件表达式，值为boolean型的表达式，指定循环条件。
* 表达式3：循环后操作表达式，修整变量，改变循环条件。

foreach语句是for语句的简化版本。语法如下：

```java
for(数据类型 元素变量x:遍历对象obj){
	引用x的语句序列
}
```

实例如下：

```java
public class Repetition{
	public static void main(String args[]){
		int arr[] = {7,10,1};
		System.out.println("一维数组中的元素分别为：");
		for(int x:arr){
			System.out.println(x);
		}
	}
}
```

使用break跳出循环嵌套时，只会跳出包含它的最内层循环，只跳出一层循环。continue语句不立即跳出当前循环，而是停止执行本轮循环，跳到下一轮循环。

# String类

## 初始化字符串

1.  使用字符数组创建String对象。

    ```java
    char a[] = {'g','o','o','d'};
    String s = new String(a);
    ```

2.  通过字符串形参构造String对象。

    ```java
    String s = new String("good");
    ```

3.  通过字符串常量引用赋值。

    ```java
    String s = "good";
    ```

可以通过`+`运算符连接多个运算符产生一个String对象。将字符串与其他数据类型连接时会将这些数据直接转成字符串。

## 获取字符串信息

`str.length()`：获取字符串长度。

`str.indexOf(String s)`：返回字符串s在指定字符串str中首次出现的索引位置。索引是从0开始的，如果未检索到字符串则返回-1.

`str.lastIndexOf(String s)`：从当前字符串的开始位置检索字符串s，并将最后一次出现s的索引位置返回。未检索到则返回-1.

`str.charAt(int index)`：将字符串str指定索引位置的字符返回。

## 字符串操作

`str.trim()`：去除空格，返回字符串副本，去除前导空格和尾部空格。str.

`str.substring(int beginIndex[,int endIndex])`：指定从某一索引处开始截取字符串。

`str.replace(char oldChar,char newChar)`：将str中旧字符或字符串oldChar替换成新的字符或字符串newChar。

`str.startsWith(String prefix)`：判断当前字符串对象的前缀是否为prefix指定的前缀的字符串，返回值类型位boolean。

`str.endsWith(String suffix)`：判断当前字符串是否以指定后缀结尾。

`==`不能用于比较两个字符串内容是否相等，两个对象的内存地址不同，使用的比较运算仍会返回false。

`str.equals(String otherstr)`: 比较两个字符串对象是否相等。

`str.equalsIgnoreCase(String otherstr)`：忽略大小写情况下比较两个字符串是否相等。

`str.compareTo(String otherstr)`：按字典顺序比较两个字符串。若str的字典顺序大于otherstr,返回正整数，否则返回负整数，相等则返回0.

`str.toLowerCase()`：将原字符串的每个大写字母转换成小写字母。

`str.toUpperCase()`：将原字符串的每个小写字母转换成大写字母。

`str.split(String sign[,int limit])`：将字符串按指定的分割符sign分割limit次，返回字符串数组。

## 格式化字符串

String类的静态`format()`方法用于创建格式化的字符串。

![常规类型格式化](http://image-paul-blogs.test.upcdn.net/java/011.png)

```java
public class General{
	public static void main(String args[]){
		String str = String.format("%d",400/2);
		String str2 = String.format("%b",3>5);
		String str3 = String.format("%x",200);
         System.out.println("400的一半是："+str);
         System.out.println("3>5正确么？"+str2);
         System.out.println("200的十六进制是："+str3);
	}
}
```

## 字符串生成器

可变字符序列类String-Builder类，可动态执行添加，删除和插入字符串的编辑操作。

`append()`方法用于向字符串生成器中追加内容，通过该方法的多个重载形式，可以实现任何类型的数据，如int，boolean，char,String,double或者另一个字符串生成器。

>   append(content)
>
>   - content是要追加到字符串生成器中的内容，可以是任何类型数据或其他对象。

`insert(int offsert arg)`方法用于向字符串指定位置插入数据内容。

>   insert(int offset arg)
>
>   - offset：字符串生成器的位置（待插入位置），必须大于等于0，且小于序列长度。
>   - arg: 将插入到字符串生成器位置。该参数可以说任何数据类型或对象。

`delete(int start,int end)`方法用于移除此序列子字符串中的字符。

>   delete(int start,int end)
>
>   -   start：将要删除的字符串的起始位置。
>   -   end：将要删除的字符串终点位置。(不包括end索引位置)

实例如下：

```java
StringBuilder bf = new StringBuilder("StringBuilder");
bf.insert(5,"word");
System.out.println(bf.toString());
bf.delete(5,10);
System.out.println(bf.toString());
```

# 数组

## 一维数组初始化

声明一维数组的两种方式：

-   数组元素类型 数组名字[]
-   数字元素类型[] 数组名字

数组元素类型可以是Java`任意的`数据类型。

声明的同时为数组分配内存：

`数组元素类型 数组名 = new 数组元素类型[数组元素个数]`

初始化一维数组的两种方式：

-   int arr[] = new int[]{1,2,3,5,25}
-   int arr[] = {1,2,3,5,25}

## 二维数组初始化

声明二维数组的两种方法：

-   数组元素类型 数组名字\[][]
-   数组元素类型\[][] 数组名字 

声明数组的同时分配内存

1.  int a\[][] = new int\[2][4] 

2.  int a\[][] = new int\[2][];a[0] = new int[2];a[1] = new int[3];

二维数组初始化

>   type arrayname[][] = {value1,value2,....,valuen}
>
>   type: 数组类型。
>
>   arrayname：数组名称。
>
>   value：数组中各个元素值。

二维数组的遍历

```java
public class Matrix{
    public static void main(String args[]){
        int a[][] = new int[3][4];
        for(int i=0;i<a.length;i++){
            for(int j=0;j<a[i].length;j++){
                System.out.println(a[i][j]);
            }
        }
    }
}
```

```java
public class Matrix{
    public static void main(String args[]){
        int arr[][] = new int[3][4];
        int i = 0;
        for(int x[]:arr){
            i++;
            int j = 0;
            for(int e:x){
                j++;
                if(i==arr.length && j==x.length){//判断是否是最后一个元素
                    System.out.println(e)
                }else{
                    System.out.println(e+'、')
                }
            }
        }
    }
}
```

## 填充替换数组元素

>   fill(int[] a[,int fromIndex,int toIndex],int value)
>
>   -   a:要进行填充的数组
>   -   fromIndex: 要使用指定值填充的第一个元素的索引
>   -   endIndex: 要使用指定值填充的最后一个元素的索引（不包括）
>   -   value：要填充的数值

## 数组排序

通过`Arrays`类的静态方法`sort()`方法可以实现对数组排序。语法如下：

>   Arrays.sort(object)
>
>   object是待排序数组名称

## 复制数组

通过`Arrays`类的`copyOf()`方法复制数组到指定长度。

>   Arrays.copyOf(arr,int newLength)
>
>   -   arr: 要进行复制的数组
>   -   newLength: 指复制后新数组的长度，一般是arr的元素个数

## 数组查询

`Arrays`类的`binarySearch()`方法，可使用二分搜索法来搜索指定数组，返回搜索元素的索引值。

>   Arrays.binarySearch(Object[] a[,int fromIndex,int toIndex],Object key)
>
>   -   a：要进行检索的数组
>   -   fromIndex: 指定范围开始处索引
>   -   toIndex: 指定范围结束处索引(不包含)
>   -   key: 要查找元素

# 类和对象

类是封装对象属性和行为的载体。对象的属性以成员变量变量的形式存在，对象的方法以成员方法的形式存在。

## 成员方法

定义成员方法的格式如下：
```java
权限修饰符 返回值类型 方法名(参数类型 参数名...){
	...//方法体
	return 返回值；
}
```

若无返回值可用关键字void表示。成员方法的返回值可以是计算结果，也可以是其他想要的数值和对象。

## 权限修饰符

Java中的权限修饰符主要包括`private`,`public`,`protected`,这些修饰符控制着对`类`和`类成员变量`以及`成员方法`的访问。

![修饰符权限](http://image-paul-blogs.test.upcdn.net/java/012.png)

## this关键字

this关键字代表本类对象的引用如`this.成员变量/成员方法`，this关键字被隐式的用于引用对象的成员变量和方法。当然也可以通过`对象.成员变量/成员方法`。this还可以作为方法返回值。

```java
public Book getBook(){
    return this;
}
```

## 类的构造方法

每实例化一个对象时，类都会自动调用构造方法。

```java
public book(){
    ...//方法体
}
```

>   1.  构造方法没有返回值
>   2.  构造方法的名称要与本类名称相同
>   3.  一个类中可以有多个构造方法，根据参数个数，类型以及参数顺序进行区分和匹配。

this关键字也可调用类的构造方法

```java
public class AnyThting{
    public AnyThting(){
        this("this调用有参构造方法");
        System.out.println("无参数构造方法");
    }
    public AnyThting(String name){
        System.out.println(name)
    }
}
```

## 静态变量、常量和方法

由关键字`static`修饰的变量，常量和方法称为静态变量、常量和方法，称为静态成员。对静态成员的调用通过：`类名.静态类成员`

静态数据与静态方法的作用是为了提供共享数据或方法。静态成员的使用同样受权限修饰符的约束。

```java
public class StaticTest{
    final static double PI=3.1415926;
    static int id;
    
    public static void method1(){
        //do something
    }
    public static void method2(){
        method1();//直接调用
        System.out.println(StaticTest.PI);//类名.静态类成员
}
```



>   静态方法的两点约束：
>
>   1.  在静态方法中不可以使用this关键字
>   2.  静态方法中不可以直接调用非静态方法（直接通过方法名调用），但在主函数（静态）中可以通过实例化类对象调用非静态方法

**Java中规定不能将方法体中的局部变量声明为static.**

## 类的主方法

主方法提供对程序流向的控制。语法如下：

```java
public static void main(String[] args){
    //方法体
}
```

>   -   主方法是静态的，如果需要直接在主方法中调用其他方法，该方法必须是静态的。
>
>   -   主方法无返回值
>
>   -   主方法的形参为数组，其中args[0]~args[n]表示程序第1到n个参数。

## 对象

### 对象创建

通过关键字`new`创建对象,对象被创建后就是一个对象的引用，这个引用在内存中为对象分配了内存空间。在构造方法中初始化成员变量，当创建对象自动调用构造方法。创建语法如下：

```java
Test test = new Test();
Test test = new Test('a');
```

同一个类的不同对象对非静态成员变量的操作是独立的，操作互不影响。但对于静态成员，由于共享同一内存，不同对象对同一内存的操作都会影响静态成员的值。实例如下：

```java
public class AccessProperty{
    static int i=47;
    public void call(){
        System.out.println("调用call()方法");
        for(i=0;i<3;i++){
            System.out.print(i+' ');
            if(i==2){
                System.out.println('\n');
            }
        }
    }
}
```

结果如下：

![result](http://image-paul-blogs.test.upcdn.net/java/013.png)

# 包装类

## Integer

Integer类，Long类和Short类，分别将基本类型int，long和short封装成一个类。这些类都是`Number`的子类,所含的方法基本相同。

Integer类的两种构造方法：

>   1.  Integer(int number)
>
>       该方法以一个int类型变量作为参数来获取Integer对象

>   2.  Integer(String str)
>
>       该方法以一个数值型字符串变量（如"123"）作为参数获取Integer对象。

Integer类的常用方法：

|               方法                | 返回值  |                          功能描述                           |
| :-------------------------------: | :-----: | :---------------------------------------------------------: |
|            byteValue()            |  byte   |                 以byte类型返回该Integer的值                 |
| compareTo(Integer anotherInteger) |   int   | 比较两个Integer对象的值大小。返回sign(integer-anotherInger) |
|      equals(Object integer)       | boolean |                    比较两个对象是否相等                     |
|            intValue()             |   int   |                 以int形式返回此Integer对象                  |
|           shortValue()            |  short  |                以short形式返回此Integer对象                 |
|            toString()             | String  |             返回一个表示该Integer值的String对象             |
|        valueOf(String str)        | Integer |              返回保存指定String值的Integer对象              |
|       parseInt(String str)        |   int   |        返回包含在由str指定的字符串中数字的等价整数值        |

```java
public class Summation{
    public static void main(String[] args){
        String str[] = {"89","12","10","18","36"};
        int sum = 0;
        for(int i=0;i<str.length;i++){
            int myInt = Integer.parseInt(str[i]);
            sum += myInt;
        }
        System.out.println("数组中各元素之和为："+sum);
    }
}
```

`toBinaryString()`、`toHexString()`、`toOctalString()`方法分别将值转换成二进制，十六进制和八进制的字符串。

## Character

Character类在对象中包装类一个基本类型为char的值。

构造方法：`Charater(char value)`

常用方法：

| 方法                                  | 返回值  | 功能描述                                |
| :------------------------------------ | ------- | --------------------------------------- |
| charvalue()                           | char    | 返回此Character对象的值                 |
| compareTo(Character anocherCharacter) | int     | 根据数字比较两个character，若相等则返回 |
| equals(Object obj)                    | Boolean | 判断是否相等                            |
| toUpperCase(char ch)                  | char    | 将字符参数转换为大写                    |
| toLowerCase(char ch)                  | char    | 将字符参数转换为小写                    |
| toString()                            | String  | 返回一个表示指定char值的String对象      |
| charValue()                           | char    | 返回一个Character对象的值               |
| isUpperCase(char ch)                  | boolean | 判断指定字符是否为大写字母              |
| isLowerCase(char ch)                  | boolean | 判断指定字符是否为小写字母              |

