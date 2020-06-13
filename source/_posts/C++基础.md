---
title: C++基础
author: Paul Yu
categories: c++
tag: 基础
---



# C++基本语法

```c++
#include<iostream>
using namespace std;

int main()
{
    cout<<"hello world";
    return 0;
}
```

-   C++语言定义了一些头文件，头文件中包含了程序中必需或有用的信息
-   std是命名空间
-   int main()是主函数，程序从这里开始执行
-   return 0;终止main()函数。

## 标识符

标识符是用来标识变量，函数，类，模块或任何其他用户自定义项目的名称，标识符用车以字母或`_`开头，后跟零或多个字母、下划线和数字。C++严格区分大小写。

## 注释

C++支持单行和多行注释。

单行：`//语句`

多行：`/*语句   ...*/`

# 数据类型

## 基本类型

| 布尔型   | bool   |
| -------- | ------ |
| 字符型   | char   |
| 整型     | int    |
| 浮点型   | float  |
| 双浮点型 | double |
| 无类型   | void   |

一个基本类型可以使用一个或多个类型修饰符进行修饰：

-   signed
-   unsigned
-   short
-   long

不同变量类型的存储空间大小不同。

![](http://image-paul-blogs.test.upcdn.net/C%2B%2B/c01.png)

## typedef声明

可以使用`typedef`关键字为已有类型取一个新的名字。

>   typedef type newname
>
>   ```C++
>   typedef int feet;
>   feet distance
>   ```
>
>   

## 枚举类型

枚举类型是若干枚举常量的集合，需要使用关键字`enum`。如果一个变量有几种可能的值，枚举是将变量的值一一列举出来，枚举变量的值只能取列举出来的值的范围。一般形式为：

>   enum 枚举名{
>
>   ​	标识符[=整型常量],
>
>   ​	....
>
>   ​	标识符[=整型常量]
>
>   }枚举变量；



实例如下：

```c++
enum color {red,green,blue} c;
c = blue;
```

# 变量

## 变量初始化

>   typedef variable_name = name

```c++
extern int d=3,f=5;
char x = 'x';
byte z = 22;
```

## 变量作用域

-   在函数或一个人代码块内部声明的变量称为局部变量
-   在函数参数定义声明的变量，称为形式参数
-   在函数外部声明的变量，称为全局变量

局部变量只能被函数内部的语句调用，全局变量可以在任何函数中被访问。

# 常量

## 整数常量

整数常量可以是十进制，八进制或十六进制的常量。整数可以添加U(无符号整数)，L(长整数)。不区分大小写。

```C++
85		//十进制
0213	//八进制
0x4b	//十六进制
30u		//无符号整数
23ul	//无符号长整型
```

## 浮点常量

浮点常量通常以小数形式或指数形式表示。当使用小数形式，必须同时包含整数部分，小数部分。当使用指数形式，必须同时包含指数，以及小数(/整数)。

```c++
3.14159
314159E-5L
```

## 布尔常量

-   true(!=1)
-   false(!=0)

## 字符常量

字符常量是扩在单引号中，字符常量可以是一个普通的字符`x`，一个转义字符`\t`，或一个通用的字符`\u02C0`。

## 字符串常量

字符串常量扩在双引号`""`中，可以使用空格做分隔符把一个很长的字符串常量进行分行。

```c++
"hello, \
dear"
```

## 定义常量

### 使用#define关键字

>   #define identifier value

```C++
#include <iostream>
using namespace std;
 
#define LENGTH 10   
#define WIDTH  5
#define NEWLINE '\n'
 
int main()
{
 
   int area;  
   
   area = LENGTH * WIDTH;
   cout << area;
   cout << NEWLINE;
   return 0;
}
```

### const关键字

>   const type variable = value

```c++
#include <iostream>
using namespace std;
 
int main()
{
   const int  LENGTH = 10;
   const int  WIDTH  = 5;
   const char NEWLINE = '\n';
   int area;  
   
   area = LENGTH * WIDTH;
   cout << area;
   cout << NEWLINE;
   return 0;
}
```

## 修饰符类型

数据类型修饰符：

-   signed
-   unsigned
-   long
-   short

修饰符signed,unsigned,long和short可应用于整型，signed和signed可应用于字符型，long可应用于双精度型。

```c++
#include <iostream>
using namespace std;
 
/* 
 * 这个程序演示了有符号整数和无符号整数之间的差别
*/
int main()
{
   short int i;           // 有符号短整数
   short unsigned int j;  // 无符号短整数
 
   j = 50000;
 
   i = j;
   cout << i << " " << j;
 
   return 0;
}
```

运行结果为：`-15536` `50000`

# 运算符

## 算术运算符

![](http://image-paul-blogs.test.upcdn.net/C%2B%2B/c02.png)

## 关系运算符

假设变量A=10，变量B=20，则：

![](http://image-paul-blogs.test.upcdn.net/C%2B%2B/c03.png)

## 逻辑运算符

假设A的值为1，B的值为2

![](http://image-paul-blogs.test.upcdn.net/C%2B%2B/c04.png)

## 位运算符

假如此处A=60，且B=13。现已二进制格式表示，如下所示：

A = 0011 1100

B = 0000 1101

![](http://image-paul-blogs.test.upcdn.net/C%2B%2B/c05.png)

## 杂项运算符

![](http://image-paul-blogs.test.upcdn.net/C%2B%2B/c06.png)

## C++运算符优先级

![](http://image-paul-blogs.test.upcdn.net/C%2B%2B/c07.png)

# 循环语句

C++提供了while，for，do...while多种循环类型，而循环控制语句可以更改执行的正常序列。

>   -   break: 终止loop语句或switch语句，程序跳出最近的一层循环
>   -   continue：结束本轮循环，不再执行循环体剩余部分，执行下一轮循环

# 函数

C++中函数定义形式如下：

```c++
return_type function_name (parameter list)
{
    //
}
```

## 函数声明

函数声明告诉编译器如何调用函数，函数的定义在调用函数之后，在调用函数之前需要提前声明。函数声明如下：

>   return_type function_name(paramter list)

在声明中，参数名称并不重要，只有参数类型是必须的。

如：int max(int,int)

```c++
#include <iostream>
using namespace std;
 
// 函数声明
int max(int num1, int num2);
 
int main ()
{
   // 局部变量声明
   int a = 100;
   int b = 200;
   int ret;
 
   // 调用函数来获取最大值
   ret = max(a, b);
 
   cout << "Max value is : " << ret << endl;
 
   return 0;
}
 
// 函数返回两个数中较大的那个数
int max(int num1, int num2) 
{
   // 局部变量声明
   int result;
 
   if (num1 > num2)
      result = num1;
   else
      result = num2;
 
   return result; 
}
```

如果函数要使用参数，必须声明接受参数值的变量，这些变量称为`形式参数`。

## 调用函数

当调用函数时，有三种向函数传递参数的方式：

| 调用类型 | 描述                                                         |
| -------- | ------------------------------------------------------------ |
| 传值调用 | 该参数把参数实际的值赋值给函数的形参                         |
| 指针调用 | 把参数的地址赋给形式参数，修改形式参数会影响实际参数         |
| 引用调用 | 把参数的引用赋值给形式参数，该引用用于访问调用中需要用到的实际参数，修改形式参数会影响实际参数 |

## 参数的默认值

当定义函数时，可以在参数列表后每一个参数指定默认值，用于参数未赋值时使用。

```c++
#include <iostream>
using namespace std;
 
int sum(int a, int b=20)
{
  int result;
 
  result = a + b;
  
  return (result);
}
 
int main ()
{
   // 局部变量声明
   int a = 100;
   int b = 200;
   int result;
 
   // 调用函数来添加值
   result = sum(a, b);
   cout << "Total value is :" << result << endl;
 
   // 再次调用函数
   result = sum(a);
   cout << "Total value is :" << result << endl;
 
   return 0;
}
```

结果如下：

```c++
Total value is :300
Total value is :120
```

## Lambda函数与表达式

Lambda表达式把函数当作对象，lambda表达式可以像对象一样被使用。可以将他们赋给变量和作为参数传递。

表达形式如下：

>   \[capture](parameters)->return_type{body}

如：[]\(int x,int y) ->int {int z = x+y;return z+x;}

如果lambda表达式没有返回值，其返回类型可完全忽略。

在lambda表达式中可以访问当前作用域的变量，c++变量传递有传值和传引用的区别。可以通过[]来指定：

```
[]      // 沒有定义任何变量。使用未定义变量会引发错误。
[x, &y] // x以传值方式传入（默认），y以引用方式传入。
[&]     // 任何被使用到的外部变量都隐式地以引用方式加以引用。
[=]     // 任何被使用到的外部变量都隐式地以传值方式加以引用。
[&, x]  // x显式地以传值方式加以引用。其余变量以引用方式加以引用。
[=, &z] // z显式地以引用方式加以引用。其余变量以传值方式加以引用。
```

# 数组

## 数组初始化

c++中声明一个数组，需要指定元素类型和元素数量。

>   type arrayName [size]

在初始化时，如下：

```c++
double bal[3] = {1000.0,2.0,3.4};
double bal2[] = {100.0,2.0,3.4};
double bal3[3] = 50.0;
```

# 字符串

使用字符串中的方法时，需要引入类`string`.即`#include <string>`.具有下列特性：

-   string直接支持字符串连接
-   string直接支持字符串类型大小比较
-   string直接支持子串查找和提取
-   string直接支持字符串的插入和替换
-   string具有字符数组的灵活性，可以通过[]来访问每个元素

## string类常用的构造函数

```c++
string str;			//生成一个空字符串
string str("ABC") ;   //等价于str="ABC"
string str ("ABC", strlen)  // 将"ABC"存到str里,最多存储前strlen个字节

string s("ABC",stridx,strlen)   //将"ABC"的stridx位置,做为字符串开头,存到str里.且最多存储strlen个字节.
   
string s(strlen, 'A')  //存储strlen个'A'到str里
```

## string类常用成员函数

```c++
str1.assign("ABC");　　　　　　　　//清空string串,然后设置string串为"ABC"

str1.length()；                 //获取字符串长度

str1.size();　　　　　　　　　　　 //获取字符串数量,等价于length()

str1.capacity();　　　　　　　　  //获取容量,容量包含了当前string里不必增加内存就能使用的字符数

str1.resize(10);　　　　　　     //表示设置当前string里的串大小,若设置大小大于当前串长度,则用字符\0来填充多余的.
str1.resize(10,char c);　　　　 //设置串大小，若设置大小大于当前串长度,则用字符c来填充多余的

str1.reserve(10);　　　　　　　　　//设置string里的串容量,不会填充数据.
str1.swap(str2);        　　    //替换str1 和 str2 的字符串

str1.puch_back ('A');    　　//在str1末尾添加一个'A'字符,参数必须是字符形式
 
str1.append ("ABC");     　　//在str1末尾添加一个"ABC"字符串,参数必须是字符串形式

str1.insert (2,"ABC");       //在str1的下标为2的位置,插入"ABC"

str1.erase(2);         　　　　//删除下标为2的位置,比如: "ABCD" --> "AB"

str1.erase(2,1);              //从下标为2的位置删除1个,比如: "ABCD"  --> "ABD"

str1.clear();           　　 //删除所有

str1.replace(2,4, "ABCD"); //从下标为2的位置,替换4个字节,为"ABCD"

str1.empty();         　　 //判断为空, 为空返回true
 

　　

/*assign() :赋值函数 ,里面会重新释放分配字符串内存 */
str1.assign("HELLO");                   //str1="HELLO"
str1.assign("HELLO", 4);                //str1="HELL" ,只保留4个字符
str1.assign("HELLO", 2, 3);             //str1="LLO"    ,从位置2开始,只保留3个字符
str1.assign(5, 'c');                    //str1="CCCCC"             //按字符赋值
 
```

## 反转相关

位于头文件`<algorithm>`中。

```c++
string str("hello");
reserve(str.begin(),str.end());
cout<<str<<endl;
```

## 查找相关 

```c++
string str("ABCDEFGABCD");                      //11个字符
int n;
/*查找成功返回位置,查找失败,则n等于-1*/
/*find():从头查找某个字符串*/
n= str.find('A');              //查找"A",n=0;
n= str.find("AB");             //查找"AB",n=0;
n= str.find("BC",1);           //从位置1处,查找"BC",n=1;
n= str.find("CDEfg",1,3);      //从位置1处,查找"CDEfg"的前3个字符,等价于str.find("CDE",1),n=2;

/*rfind():反向(reverse)查找,从末尾处开始,向前查找*/
n= str.rfind("CD");           //从位置10开始向前查找,n=9
n= str.rfind("CD",5);         //从位置5开始向前查找,n=2
n= str.rfind("CDEfg",5,3);    //等价于str.rfind("CDE",5);       ,所以n=2


/* find_first_of ():查找str里是否包含有子串中任何一个字符*/
n= str.find_first_of("abcDefg");     //由于str位置3是'D',等于"abcDefg"的'D',所以n=3
n= str.find_first_of("abcDefg",1,4); //等价于str. find_first_of ("abcD",1); 所以n=3


/* find_last_of ():末尾查找, 从末尾处开始,向前查找是否包含有子串中任何一个字符*/
n= str.find_last_of("abcDefg");      //由于str末尾位置10是'D',所以n=10
n= str.find_last_of("abcDefg",5,4);  //等价于str. find_last_of ("abcD",5); 所以n=3

 
/* find_first_not_of ():匹配子串任何一个字符,若某个字符不相等则返回str处的位置,全相等返回-1*/
n= str.find_last_not_of("ABC");    //由于str位置3'D',在子串里没有,所以 n=3
n= str.find_last_not_of("aABDC");  //由于str位置4 'F',在子串里没有,所以 n=4
n= str.find_last_not_of("aBDC");   //由于str位置0 'A',在子串里没有,所以 n=0

/* find_last_not_of ():反向匹配子串任何一个字符,若某个字符不相等则返回str处的位置,全相等返回-1*/
n= str.find_last_not_of("aBDC");  //由于str位置7'A',在子串里没有,所以 n=7
```

## 拷贝相关

```c++
str2=str1.substr(2);        //提取子串,提取出str1的下标为2到末尾,给str2

str2=str1.substr(2,3);     //提取子串,从 str1的下标为2开始,提取3个字节给str2

const char *s1= str.data();   //将string类转为字符串数组,返回给s1


char *s=new char[10];
str.copy(s,count,pos);    //将str里的pos位置开始,拷贝count个字符,存到s里.
```

## 通过string类实现字符串循环右移功能

```c++
#include <iostream>
#include <string>
#include <sstream>

using namespace std;

string operator >>(const string& str,int n)
{
       string ret;
       n %= str.length();

       ret=str.substr(str.length()-n);              //找到右移的字符串
       ret+=str.substr(0,str.length()-n);  

       return ret;
}

int main()
{     
       string str="abcdefg";
       string ret= str>>3 ;
       cout<<ret<<endl;

       return 0;
}
```

## 字符串与数字的转换

在C++标准库中，提供了字符串与数字的转换，位于`<sstream>`头文件。同时需要两个类：

-   istringstream		//字符串输入流
-   ostringstream	//字符串输入流

### 将string字符串->数字

```c++
istringstream iss ("123.5");    //定义对象iss,初始化为"123.5" ,  
//等价于:
//istringstream iss;
//iss.str("123.5");                 //设置对象iss为"123.5" ,

double num;

 if(iss>>num)                 //通过调用iss.operator >>(num), 将"123.5"转为数字,并返回bool类型变量
{
    cout<<num << endl;
}

/*临时对象转换*/
string str="123.5";

double num;

if(istringstream(str)>>num)        //通过临时对象,来将str转为数字
  cout<<num<<endl;
```

### 数字->string字符串

```c++
ostringstream oss;
oss <<123.5;                   //相当于调用: oss.str("123.5");
string str= oss.str() ;
cout<<str << endl;
```

# 指针

指针时一个变量，其值为另一个变量的地址，即内存位置的直接地址。必须在使用指针存储其他变量地址前对其进行声明。

>   type *var_name

使用实例如下：

```c++
#include <iostream>
 
using namespace std;
 
int main ()
{
   int  var = 20;   // 实际变量的声明
   int  *ip;        // 指针变量的声明
 
   ip = &var;       // 在指针变量中存储 var 的地址
 
   cout << "Value of var variable: ";
   cout << var << endl;
 
   // 输出在指针变量中存储的地址
   cout << "Address stored in ip variable: ";
   cout << ip << endl;
 
   // 访问指针中地址的值
   cout << "Value of *ip variable: ";
   cout << *ip << endl;
 
   return 0;
}
```

## 指针的算数运算

可以对指针执行四种算数运算`+`,`-`,`++`,`--`。

我们可以在程序中使用指针代替数组，因为指针变量可以递增，而数组时一个常量指针不能递增。

```c++
#include <iostream>
 
using namespace std;
const int MAX = 3;
 
int main ()
{
   int  var[MAX] = {10, 100, 200};
   int  *ptr;
 
   // 指针中的数组地址
   ptr = var;//指向数组的首地址
   for (int i = 0; i < MAX; i++)
   {
      cout << "Address of var[" << i << "] = ";
      cout << ptr << endl;
 
      cout << "Value of var[" << i << "] = ";
      cout << *ptr << endl;
 
      // 移动到下一个位置
      ptr++;
   }
   return 0;
}
```

结果如下：

```c++
Address of var[0] = 0xbfa088b0
Value of var[0] = 10
Address of var[1] = 0xbfa088b4
Value of var[1] = 100
Address of var[2] = 0xbfa088b8
Value of var[2] = 200
```

也可以对指针执行递减操作。

```c++
#include <iostream>
 
using namespace std;
const int MAX = 3;
 
int main ()
{
   int  var[MAX] = {10, 100, 200};
   int  *ptr;
 
   // 指针中最后一个元素的地址
   ptr = &var[MAX-1];
   for (int i = MAX; i > 0; i--)
   {
      cout << "Address of var[" << i << "] = ";
      cout << ptr << endl;
 
      cout << "Value of var[" << i << "] = ";
      cout << *ptr << endl;
 
      // 移动到下一个位置
      ptr--;
   }
   return 0;
}
```

可以对指针指向的地址通过关系运算符比较地址的大小，修改上面的实例，只要变量指针指向的地址小于或等于数组最后一个元素的地址`&var[MAX-1]`则把指针变量进行递增。

```c++
#include <iostream>
 
using namespace std;
const int MAX = 3;
 
int main ()
{
   int  var[MAX] = {10, 100, 200};
   int  *ptr;
 
   // 指针中第一个元素的地址
   ptr = var;
   int i = 0;
   while ( ptr <= &var[MAX - 1] )
   {
      cout << "Address of var[" << i << "] = ";
      cout << ptr << endl;
 
      cout << "Value of var[" << i << "] = ";
      cout << *ptr << endl;
 
      // 指向上一个位置
      ptr++;
      i++;
   }
   return 0;
}
```

## 指针和数组

指针和数组很多情况下可以互换。比如指向数组开头的指针，可以使用指针的算数运算或数组索引来访问数组。

```c++
#include <iostream>
 
using namespace std;
const int MAX = 3;
 
int main ()
{
   int  var[MAX] = {10, 100, 200};
   int  *ptr;
 
   // 指针中的数组地址
   ptr = var;
   for (int i = 0; i < MAX; i++)
   {
      cout << "var[" << i << "]的内存地址为 ";
      cout << ptr << endl;
 
      cout << "var[" << i << "] 的值为 ";
      cout << *ptr << endl;
      cout << *(ptr+i) << endl;
      cout << *(var+i) << endl;
 
      // 移动到下一个位置
      ptr++;
   }
   return 0;
}
```

## 传递指针给函数

允许将指针传递给函数，只需声明函数参数为指针类型即可。

```c++
#include <iostream>
#include <ctime>
 
using namespace std;
void getSeconds(unsigned long *par);
 
int main ()
{
   unsigned long sec;
   getSeconds( &sec );
   // 输出实际值
   cout << "Number of seconds :" << sec << endl;
   return 0;
}
void getSeconds(unsigned long *par)
{
   // 获取当前的秒数
   *par = time( NULL );
   return;
}
```

也可以接受数组作为参数

```c++
#include <iostream>
using namespace std; 
// 函数声明
double getAverage(int *arr, int size);
 
int main ()
{
   // 带有 5 个元素的整型数组
   int balance[5] = {1000, 2, 3, 17, 50};
   double avg;
   // 传递一个指向数组的指针作为参数
   avg = getAverage( balance, 5 ) ;
 
   // 输出返回值
   cout << "Average value is: " << avg << endl; 
   return 0;
}
 
double getAverage(int *arr, int size)
{
  int    i, sum = 0;       
  double avg;          
  for (i = 0; i < size; ++i)
  {
    sum += arr[i];
    //sum += *(arr+i);
   }
  avg = double(sum) / size;
  return avg;
}
```

## 从函数返回指针

c++不支持从函数外部返回局部变量的地址，除非定义局部变量为`static`类型。

```c++
#include <iostream>
#include <ctime>
#include <cstdlib>
 
using namespace std;
 
// 要生成和返回随机数的函数
int * getRandom( )
{
  static int  r[10];
 
  // 设置种子
  srand( (unsigned)time( NULL ) );
  for (int i = 0; i < 10; ++i)
  {
    r[i] = rand();
    cout << r[i] << endl;
  }
 
  return r;
}
 
// 要调用上面定义函数的主函数
int main ()
{
   // 一个指向整数的指针
   int *p;
 
   p = getRandom();
   for ( int i = 0; i < 10; i++ )
   {
       cout << "*(p + " << i << ") : ";
       cout << *(p + i) << endl;
   }
 
   return 0;
}
```

# 引用

引用变量是一个别名，是某个已存在变量的另一个名字。

## 引用与指针区别

-   不存在空引用，引用必须连接到一块合法的内存
-   一旦引用被初始化为一个对象，就不能被指向另一个对象。指针可以在任何时候指向另一个对象。
-   引用必须在创建时被初始化。指针可以在任何时间被初始化

## 创建引用

变量名称是变量附属在内存位置中的标签，可以把引用当成变量附属在内存位置的第二个标签，因此可以通过原始变量名称或引用来访问变量名称。

>   变量类型& 引用名称 = 变量名

```c++
#include <iostream>
 
using namespace std;
 
int main ()
{
   // 声明简单的变量
   int    i;
   double d;
 
   // 声明引用变量
   int&    r = i;
   double& s = d;
   
   i = 5;
   cout << "Value of i : " << i << endl;
   cout << "Value of i reference : " << r  << endl;
 
   d = 11.7;
   cout << "Value of d : " << d << endl;
   cout << "Value of d reference : " << s  << endl;
   
   return 0;
}
```

```c++
Value of i : 5
Value of i reference : 5
Value of d : 11.7
Value of d reference : 11.7
```

## 将引用作为参数

使用引用实现引用调用函数

```c++
#include <iostream>
using namespace std;
 
// 函数声明
void swap(int& x, int& y);
 
int main ()
{
   // 局部变量声明
   int a = 100;
   int b = 200;
 
   cout << "交换前，a 的值：" << a << endl;
   cout << "交换前，b 的值：" << b << endl;
 
   /* 调用函数来交换值 */
   swap(a, b);
 
   cout << "交换后，a 的值：" << a << endl;
   cout << "交换后，b 的值：" << b << endl;
 
   return 0;
}
 
// 函数定义
void swap(int& x, int& y)
{
   int temp;
   temp = x; /* 保存地址 x 的值 */
   x = y;    /* 把 y 赋值给 x */
   y = temp; /* 把 x 赋值给 y  */
  
   return;
}
```

```c++
交换前，a 的值： 100
交换前，b 的值： 200
交换后，a 的值： 200
交换后，b 的值： 100
```

## 把引用作为返回值

当函数返回一个引用时，则返回一个指向返回值的隐式指针，函数可以放在赋值语句的左边。

```c++
#include <iostream>
 
using namespace std;
 
double vals[] = {10.1, 12.6, 33.1, 24.1, 50.0};
 
double& setValues( int i )
{
  return vals[i];   // 返回第 i 个元素的引用
}
 
// 要调用上面定义函数的主函数
int main ()
{
 
   cout << "改变前的值" << endl;
   for ( int i = 0; i < 5; i++ )
   {
       cout << "vals[" << i << "] = ";
       cout << vals[i] << endl;
   }
 
   setValues(1) = 20.23; // 改变第 2 个元素
   setValues(3) = 70.8;  // 改变第 4 个元素
 
   cout << "改变后的值" << endl;
   for ( int i = 0; i < 5; i++ )
   {
       cout << "vals[" << i << "] = ";
       cout << vals[i] << endl;
   }
   return 0;
}
```

```c++
改变前的值
vals[0] = 10.1
vals[1] = 12.6
vals[2] = 33.1
vals[3] = 24.1
vals[4] = 50
改变后的值
vals[0] = 10.1
vals[1] = 20.23
vals[2] = 33.1
vals[3] = 70.8
vals[4] = 50
```

# 数据结构

数组存储相同类型的变量，而结构体可以存储不同类型的数据项。定义结构体时必须使用`struct`关键字。格式如下：

```c++
struct type_name {
member_type1 member_name1;
member_type2 member_name2;
member_type3 member_name3;
.
.
} object_names;
```

type_name是结构体名称，结构体中可以声明基本类型及数组或其他结构体。object_names是结构体变量，可以声明多个，并用`,`隔开。

访问结构体成员可通过`object_names.member_name`来访问。其中`.`是**成员运算符**。

```c++
#include <iostream>
#include <cstring>
 
using namespace std;
 
// 声明一个结构体类型 Books 
struct Books
{
   char  title[50];
   char  author[50];
   char  subject[100];
   int   book_id;
};
 
int main( )
{
   Books Book1;        // 定义结构体类型 Books 的变量 Book1
   Books Book2;        // 定义结构体类型 Books 的变量 Book2
 
   // Book1 详述
   strcpy( Book1.title, "C++ 教程");
   strcpy( Book1.author, "Runoob"); 
   strcpy( Book1.subject, "编程语言");
   Book1.book_id = 12345;
 
   // Book2 详述
   strcpy( Book2.title, "CSS 教程");
   strcpy( Book2.author, "Runoob");
   strcpy( Book2.subject, "前端技术");
   Book2.book_id = 12346;
 
   // 输出 Book1 信息
   cout << "第一本书标题 : " << Book1.title <<endl;
   cout << "第一本书作者 : " << Book1.author <<endl;
   cout << "第一本书类目 : " << Book1.subject <<endl;
   cout << "第一本书 ID : " << Book1.book_id <<endl;
 
   // 输出 Book2 信息
   cout << "第二本书标题 : " << Book2.title <<endl;
   cout << "第二本书作者 : " << Book2.author <<endl;
   cout << "第二本书类目 : " << Book2.subject <<endl;
   cout << "第二本书 ID : " << Book2.book_id <<endl;
 
   return 0;
}
```

## 把结构体作为函数参数

```c++
#include <iostream>
#include <cstring>
 
using namespace std;
void printBook( struct Books book );
 
// 声明一个结构体类型 Books 
struct Books
{
   char  title[50];
   char  author[50];
   char  subject[100];
   int   book_id;
};
 
int main( )
{
   Books Book1;        // 定义结构体类型 Books 的变量 Book1
   Books Book2;        // 定义结构体类型 Books 的变量 Book2
 
    // Book1 详述
   strcpy( Book1.title, "C++ 教程");
   strcpy( Book1.author, "Runoob"); 
   strcpy( Book1.subject, "编程语言");
   Book1.book_id = 12345;
 
   // Book2 详述
   strcpy( Book2.title, "CSS 教程");
   strcpy( Book2.author, "Runoob");
   strcpy( Book2.subject, "前端技术");
   Book2.book_id = 12346;
 
   // 输出 Book1 信息
   printBook( Book1 );
 
   // 输出 Book2 信息
   printBook( Book2 );
 
   return 0;
}
void printBook( struct Books book )
{
   cout << "书标题 : " << book.title <<endl;
   cout << "书作者 : " << book.author <<endl;
   cout << "书类目 : " << book.subject <<endl;
   cout << "书 ID : " << book.book_id <<endl;
}
```

```c++
书标题 : C++ 教程
书作者 : Runoob
书类目 : 编程语言
书 ID : 12345
书标题 : CSS 教程
书作者 : Runoob
书类目 : 前端技术
书 ID : 12346
```

## 指向结构体的指针

定义指向结构体的指针

>   struct struct_type *struct_pointer

为了使用指向该结构体的指针访问结构的成员，必须使用`->`运算符。

```c++
#include <iostream>
#include <cstring>
 
using namespace std;
void printBook( struct Books *book );
 
struct Books
{
   char  title[50];
   char  author[50];
   char  subject[100];
   int   book_id;
};
 
int main( )
{
   Books Book1;        // 定义结构体类型 Books 的变量 Book1
   Books Book2;        // 定义结构体类型 Books 的变量 Book2
 
    // Book1 详述
   strcpy( Book1.title, "C++ 教程");
   strcpy( Book1.author, "Runoob"); 
   strcpy( Book1.subject, "编程语言");
   Book1.book_id = 12345;
 
   // Book2 详述
   strcpy( Book2.title, "CSS 教程");
   strcpy( Book2.author, "Runoob");
   strcpy( Book2.subject, "前端技术");
   Book2.book_id = 12346;
 
   // 通过传 Book1 的地址来输出 Book1 信息
   printBook( &Book1 );
 
   // 通过传 Book2 的地址来输出 Book2 信息
   printBook( &Book2 );
 
   return 0;
}
// 该函数以结构指针作为参数
void printBook( struct Books *book )
{
   cout << "书标题  : " << book->title <<endl;
   cout << "书作者 : " << book->author <<endl;
   cout << "书类目 : " << book->subject <<endl;
   cout << "书 ID : " << book->book_id <<endl;
}
```

## typedef关键字

可以给创建的结构体取一个别名。

```c++
typedef struct Books
{
   char  title[50];
   char  author[50];
   char  subject[100];
   int   book_id;
}Books;
Books Book1, Book2;
```

