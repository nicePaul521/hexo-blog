---
title: Java提高
date: 2020-02-14
author: Paul Yu
toc: true
summary: 总结了Java面向对象编程的基本语法，以及常见的数据结构等。
categories: Java
tags: 提高
---

# 接口、继承和多态

## 类的继承

继承的基本思想是基于某个父类的扩展，制定出一个新的子类，子类可以继承父类原有的属性和方法，也可以增加父类所不具备的属性和方法。或者直接重写父类中的某些方法。Java中使用`extends`关键字来标识两个类的继承关系。

```java
class Test{
    public Test(){					//构造方法
        //someSentence
    }
    protected void doSomething(){		//成员方法
        //someSentence
    }
    protected Test dolt(){			//方法返回值为Test类型
        return new Test();
    }
}
class Test2 extends Test{			//继承父类
    public Test2(){					//构造方法
        super();					//调用父类构造方法
        super().doSomething();		//调用父类成员方法
    }
    public void doSomethingnew(){	//新增方法
        //someSentence
    }
    public void doSomething(){		//重写父类方法
        //someSentence
    }
    protected Test2 doit(){			//重写父类方法，方法返回值类型是Test2类型
        return new Test2();
    }     
}
```

在子类中可以使用`super()`来调用父类成员方法，但是子类没有权限调用父类被修饰为`private`的方法。重写就是在子类中将父类的成员方法的名称保留，重写成员方法的实现内容，更改成员方法的访问权限或修改成员方法的返回值类型。当重写父类方法时，修改方法的权限只能从**小的范围**到**大的范围**改变。

## Object类

在Java中所有的类都直接或间接继承了java.lang.Object类，Object是所有类的父类。Object类的主要方法有：

1.  getClass()

    返回对象执行时的Class实例，使用此实例调用getName()方法可以取得类的实例。即`getClass().getName()`.

2.  toString()

    将一个对象返回为字符串形式，返回一个String实例。实际中会重写该方法。

    ```java
    public class ObjectInstance{
        public String toString(){		//重写toString方法
            return "在"+getClass().getName()+"类中重写toString()方法";
        }
        public static void main(String args[]){
            //打印类对象时自动调用toString()
            System.out.println(new ObjectInstance());
        }
    }
    ```

3.  equals()

    >   比较运算符"=="，比较的是两个对象的引用是否相等。而equals()方法比较的是两个对象的引用是否相同。

## 对象类型转换

### 向上转型

从具体类向抽象父类转换，比如将平行四边形看作是四边形对象。

```java
class Quadrangle {						//四边形类
    public static void draw(Quadrangle q){
        //方法体
    }
}
public class Parallelogram extends Quadrangle{	//平行四边形
    public static void main(String args[]){
        Pallenlogram p = new Parallelogram();
        draw(p)
    }
}
```

相当于`Quadrangle obj = new Parallelogram()`，就是把子类对象赋值给父类类型的变量。称为向上转型。

### 向下转型

向下转型是将抽象的类转换为较具体的类。

```java
class Quadrangle{
    public static void draw(Quadrangle q){
        //方法体
    }
}
public class Parallelogram extends Quadrangle{
    public static void main(String args[]){
        draw(new Parallelogram());
        //将平行四边形对象看作四边形对象，称为向上转型操作
        Quadrangle q = new Parallelogram();
        //将父类对象赋予子类对象，并强制转换为子类型，这种方法是正确的。
        Parallelogram p = (Parallelogram)q;
    }
}
```

如果直接将父类对象赋予子类对象，会发生错误，因为父类对象不一定是子类的实例。如果父类对象不是子类对象的实例，会发生ClassCastException异常。所以在执行向下向下转之前先判断父类对象是否是子类对象的实例。`instanceof`操作符判断一个类是否实现了某个接口，或者判断一个实例对象是否属于一个类。

>   myobject instanceof ExampleClass
>
>   -   myobject：某个类的对象引用
>   -   ExampleClass：某个类
>   -   返回值类型：Boolean

## 方法重载

方法重载允许在一个类中同时存在一个以上的同名方法，编译器可以根据方法名，方法`各参数类型`，`参数个数`以及`参数顺序`来确定类中的方法是否唯一。

不定长参数：

```java
public static int add(int...a){ 	//定义不定长参数
    int s=0;
    for(int i=0;i<a.length;i++){
        s += a[i];
    }
    return s;
}
```

不定长方法的语法如下：

>   返回值 方法名(参数数据类型...参数名称)

add()方法多种重载实例：

```java
public class OverLoad(){
    public static int add(int a,int b){
        return a+b;
    }
    public static double add(double a,double b){
        return a+b;
    }
    public static int add(int a){
        return ++a;
    }
    public static double add(int a,double b){
        return a+b;
    }
    public static int add(int...a){
        int s = 0;
        for(int i=0;i<a.length;i++)
            s+=a[i];
        return s;
    }
}
```

## 多态

利用多态可以使程序具有良好的扩展性，并且对所有的类进行通用处理。如果定义一个四边形，根据向上转使每个继承四边形类的对象作为draw()方法的参数，然后在draw方法中根据不同的类对象执行不同的动作。可以很好的解决代码冗余问题，同时易于维护。

```java
public class Quadrangle{
    //实例化保存四边形对象的数组
    private Quadrangle[] qtest = new Quadrangle[6];
    private int nextIndex = 0;
    public void draw(Quadrangle q){		//定义成员方法
        if(nextIndex<qtest.length){
            qtest[nextIndex] = q;
            System.out.println(nextIndex);
            nextIndex++;
        }
    }
    public static void main(String[] args){
        Quadrangle q = new Quadrangle();
        q.draw(new Square());		//正方形向上转为四方形
        q.draw(new Pallelogramgle());//平行四边形向上转为四方形
    }
}
//定义正方形类
class Square extends Quadrangle{
    public Square(){
        System.out.println("正方形")
    }
}
class Pallelogramgle extends Quadrangle{
    public Pallelogramgle(){
        System.out.println("平行四边形")
    }
}
```

以不同类对象为参数调用draw()方法，可以处理不同的图形问题，程序员无须在子类中定义执行相同功能的方法，避免了代码冗余。

## 抽象类

抽象类不能被实例化，只能被继承，常用作实际应用的父类。语法定义如下：

```java
public abstract class Test{
    abstract void testAbstract();//定义抽象方法
}
```

使用`abstract`关键字定义的类称为抽象类，使用这个主关键字定义的方法称为抽象方法。*抽象方法必须放置在抽象类中*。当抽象类被继承后需要实现其中所有的抽象方法，保证相同的方法名称，参数列表和相同返回值类型，创建出非抽象/抽象方法。

![抽象类继承关系](http://image-paul-blogs.test.upcdn.net/java/014.png)

## 接口

接口是抽象类的延申，接口中所有的方法都没有方法体。Java中不允许多重继承，但可实现多个接口。接口使用`interface`关键字进行定义，语法如下：

```java
public interface drawTest{
    void draw();//接口中的方法使用abstract关键字
}
```

*   public: 接口是可以像类一样被权限修饰符修饰。
*   interface：定义接口关键字
*   drawTest: 接口名称

一个类实现一个接口可以使用`implements`关键字。如下：

```java
public class Parallelogram extends Quadrangle implements drawTest{
    ..//
}
```

>   在接口中定义的方法必须是为public或abstract权限

多态与接口结合的实例如下：

```java
interface drawTest{ 		//定义接口
    public void draw();		//定义方法
}
//定义平行四边形类，该类继承了四边形类，并实现了drawTest接口
class Parallelogramgle extends Quadrangle implements drawTest{
    public void draw(){//覆盖接口的draw方法
        System.out.println("平行四边形.draw()")
    }
    void doAnyThing(){	//覆盖父类方法
        //方法体
    }
}
class Square extends Quadrangle implements drawTest{
    public void draw(){
        System.out.println("正方形.draw()")
    }
    void doAnyThing(){
        //方法体
    }
}
class AnyThing extends Quadrangle{     //只继承四边形类
    void doAnyThing(){
        //方法体
    }
}
public class Quadrangle{			//定义四边形类
    public void doAnyThing(){
        //方法体
    }
    public static void main(String[] args){
        drawTest[] d = {new Square(),new Parallelogramgle()};
        for(int i=0;i<d.length;i++){
            d[i].draw();
        }
    }
}
```

# 类的高级特性

## Java 类包

![完整类名](http://image-paul-blogs.test.upcdn.net/java/015.png)

一个完整的类名是需要包名与类名的组合，只要保证同一包中的类不同名，就不会发生类名冲突。

1.  使用`import`关键字导入包

    import的关键语法如下：

    >   import com.lzw.*
    >
    >   指定在从com.lzw包中的所有类都可以使用

2.  使用`import`导入静态成员

    ```java
    import static java.lang.Math.max;//导入静态成员方法
    import static java.lang.System.out;//导入静态成员变量
    
    public class ImportTest(){
        public static void main(String[] args){
            //在主方法中可以直接使用这些静态成员
            out.println("1和4的较大值为："+max(1,4));
        }
    }
    ```

## final变量

final变量用于变量声明，由final定义的变量为常量。final声明的变量必须在声明时就对其进行赋值操作。

在Java中定义全局常量，通常使用public static final 修饰，这样的常量只能在被定义时赋值。

```java
public static final double PI_VALUE = 3.14
```

常量示例：

```java
import java.util.Random;
 
class Test
{
	int i = 0;
}
 
/**
 * 常量示例
 * 
 * @author pan_junbiao
 *
 */
public class FinalData
{
	static Random rand = new Random();
	private final int VALUE_1 = 9; // 声明一个final常量
	private static final int VALUE_2 = 10; // 声明一个final、static常量
	private final Test test = new Test(); // 声明一个final引用
	private Test test2 = new Test(); // 声明一个不是final的引用
	private final int[] a = { 1, 2, 3, 4, 5, 6 }; // 声明一个定义为final的数组
	private final int i4 = rand.nextInt(20);
	private static final int i5 = rand.nextInt(20);
 
	public String toString()
	{
		return "i4值：" + i4 + " i5值：" + i5 + " ";
	}
 
	public static void main(String[] args)
	{
		FinalData data = new FinalData();
 
		// 报错：不能改变定义为final的常量值
		// data.VALUE_1 = 8;
 
		// 报错：不能改变定义为final的常量值
		// data.VALUE_2 = 9;
 
		// 报错：不能将定义为final的引用指向其他引用
		// data.test = new Test();
 
		// 正确： 可以对指定为final的引用中的成员变量赋值
		data.test.i = 1;
 
		// 正确： 可以将没有定义为final的引用指向其他引用
		data.test2 = new Test();
 
		// 报错：不能对定义为final的数组赋值
		// int b[] = { 7, 8, 9 };
		// data.a = b;
 
		// 但是final的数组中的每一项内容是可以改变的
		for (int i = 0; i < data.a.length; i++)
		{
			data.a[i] = 9;
		}
 
		System.out.println(data);
		System.out.println("data2");
		System.out.println(new FinalData());
	}
}
```

运行结果如下：

<img src='http://image-paul-blogs.test.upcdn.net/java/016.png' />

我们知道一个被定义为final的对象引用只能指向唯一一个对象，不可以将它再指向其它对象，但是一个对象的值却是可以改变的，那么为了使一个常量真正做到不可更改，可以将常量声明为static final。

```java
import static java.lang.System.out;
 
import java.util.Random;
 
/**
 * FinalStaticData类
 * 
 * @author pan_junbiao
 *
 */
public class FinalStaticData
{
	private static Random rand = new Random(); // 实例化一个Random类对象
	// 随机产生0~10之间的随机数赋予定义为final的a1
	private final int a1 = rand.nextInt(10);
	// 随机产生0~10之间的随机数赋予定义为static final的a2
	private static final int a2 = rand.nextInt(10);
 
	public static void main(String[] args)
	{
		FinalStaticData fdata = new FinalStaticData(); // 实例化一个对象
		// 调用定义为final的a1
		out.println("重新实例化对象调用a1的值：" + fdata.a1);
		// 调用定义为static final的a2
		out.println("重新实例化对象调用a2的值：" + fdata.a2);
		// 实例化另外一个对象
		FinalStaticData fdata2 = new FinalStaticData();
		out.println("重新实例化对象调用a1的值：" + fdata2.a1);
		out.println("重新实例化对象调用a2的值：" + fdata2.a2);
	}
}
```

运行结果如下：

![result](http://image-paul-blogs.test.upcdn.net/java/017.png)

从本示例运行结果中可以看出，定义为final的常量不是恒定不变的，将随机数赋予定义为final的常量，可以做到每次运行程序时改变a1的值。但是a2与a1不同，由于它被声明为static final形式，所以在内存中为a2开辟了一个恒定不变的区域，当再次实例化一个FinalStaticData对象时，仍然指向a2这块内存区域，所以a2的值保存不变。a2是在装载时被初始化，而不是每次创建新对象时被初始化；而a1会重新实例化对象时被更改。
最后总结一下在程序中final数据可以出现的位置。

```java
/**
 * 总结一下在程序中final数据可以出现的位置
 * 
 * @author pan_junbiao
 *
 */
public class FinalDataTest
{
	// final成员变量不可更改
	final int VALUE_ONE = 6;
 
	// 在声明final成员变量时没有赋值，称为空白final
	final int BLANK_FINALVAULE;
 
	// 在构造方法中为空白final赋值
	public FinalDataTest()
	{
		BLANK_FINALVAULE = 8;
	}
 
	// 设置final参数，不可以改变参数x的值
	int doIt(final int x)
	{
		return x + 1;
	}
 
	// 局部变量定义为final，不可以改变i的值
	void doSomething()
	{
		final int i = 7;
	}
}
```

## final方法

定义为final的方法不能被重写，将方法定义为final类型可以防止子类修改该类的定义与实现方式。被定义为private的方法隐式的指定为final类型，无须将一个定义为private的方法再定义为final类型。语法如下：

```java
private final void test(){
    ..//
}
```

## final类

如果希望一个类不允许任何类继承，并且不允许其它类对该类做任何改动，可以将这个类设置为final形式。语法如下：

>   final 类名{}

final关键字总结

| 修饰对象 | 解释说明                             | 备注                                                         |
| -------- | ------------------------------------ | ------------------------------------------------------------ |
| 类       | 无子类，不可以被继承，更不可能被重写 | final类中的方法默认是final的                                 |
| 方法     | 方法不能在子类中被覆盖               | final方法不能被子类覆盖，但可以被继承                        |
| 对象     | 称为常量，初始化后不能更改值         | 用final修饰的成员变量表示常量，值一旦给定就无法改变！final修饰的变量有：静态变量，实例变量和局部变量 |

## 内部类

如果在类中再定义一个类，则在类中在定义的那个类称为内部类。内部类分为成员内部类、局部内部类以及匿名类。

### 成员内部类

```java
public class OuterClass{		//外部类
    private class innerClass{	//内部类
        //...
    }
}
```

在内部类中可以直接使用外部类的私有成员变量和方法。内部类的实例一定绑定在外部类的实例上，内部类的初始化方式，使用`new`关键字。如：`OuterClass out=new OuterClass();OuterClass.innerClass in=out.new innerClass()`.不能在`new`操作符前使用外部类名称实例化内部类对象，而应该使用外部类对象来创建内部类对象。

如果外部类定义的成员变量与内部类的成员变量名称相同，可以使用`this`关键字。

```java
public class TheSameName{
    private int x;
    private class inner{
        private int x=9;
        public void doit(int x){
            x++;				//调用形参x
            this.x++;			//调用内部类变量x
            TheSameName.this.x++;//调用外部类的变量x
        }
    }
}
```

### 局部内部类

可以在类的方法或任意作用域中均可以定义内部类。

```java
interface OutInterface{}              	//定义一个接口
class OuterClass{
    public OutInterface doit(final String x){
        //在doit方法中定义内部类
        class InnerClass implements OutInterface{
            InnerClass(String s){			//内部类构造方法
                s=x;
                System.out.println(s);
            }
        }
        return new InnerClass("doit"); //向上转为接口
    }
}
```

内部类InnerClass是方法doit()的一部分，并非是outerClass类的一部分，所以在doit()方法外部无法访问该内部类。

### 匿名内部类

将上述源码修改：

```java
class OuterClass{
    public OutInterface doit(){			//定义外部类成员方法
        return new OutInterface(){		//声明匿名内部类
            private int i=0;
            public int getValue(){		//内部类方法
                return i
            }
        };
    }
}
```

这里再doit()中返回一个接口引用，然后在return中插入定义内部类的代码，实际上就是创建一个实现接口的匿名类对象。

语法如下：

```java
return new A(){
    ..//内部类体
}
```

# 异常处理

异常产生后如果不做任何处理，程序就会被终止。Java的异常捕捉结构由`try`、`catch`和`finally` 3部分组成。其中try语句存放可能发生异常的Java语句；catch程序在try语句块之后，用于激发捕捉的异常；finally语句块是无论try语句块如何推出，都将执行finally语句块。语法如下：

```java
try{
    //程序代码块
}
catch(Exception1 e){
    //对Exception1的处理
}
catch(Exception2 e){
    //对Exception2的处理
}
...
finally{
    //总是被执行的程序块
}
```

>   Exception是程序块传递给catch代码块的变量类型，e是变量名。catch代码块中语句可以对e来进行异常处理。可通过e的3个函数来获取异常的相关信息。
>
>   -   getMessage():输出错误性质
>   -   toString():给出异常的类型与性质
>   -   printStackTrance():指出异常的类型，性质，栈层次，以及出现在程序中的位置

# 集合类

Java.util包中提供了一些集合类，又称为`容器`.容器的长度是可变的，并且存放的是对对象的引用。常见的集合有`List`、`Set`、`Map`集合类。继承关系如下：

![](http://image-paul-blogs.test.upcdn.net/java/018.png)

## Collection接口

Collection接口提供了添加元素，删除元素，管理数据的方法，由于List与Set接口都继承了Collection接口，因此这些方法对List与Set集合也是通用的。

| 方法             | 功能描述                               |
| ---------------- | -------------------------------------- |
| add(E,e)         | 将指定对象加到该集合中                 |
| remove(Object o) | 将指定对象从该集合中删除               |
| isEmpty()        | 返回Boolean值，判断当前集合是否为空    |
| iterator()       | 返回该集合的迭代器，用于遍历集合中元素 |
| size()           | 返回int值，获取集合中元素个数          |

```java
import java.util.*;
public class Muster{
    public static void main(String[] args){
        Collection<String> list = new ArrayList<>();//实例化集合类对象
        list.add("a");
        list.add("b");
        list.add("c");
        Iterator<String> it = list.iterator();//创建迭代器
        while(it.hasNext()){
            String str = (String)it.next();//获取集合中元素
            System.out.printIn(str);
        }
    }
}
```

## List集合

List接口中的两个重要方法：

>   1.  get(int index): 获得指定索引位置的元素
>   2.  set(int index,Object obj): 将集合中指定索引位置的对象修改为指定的对象。

List接口实现类：

-   ArrayList类实现了长度可变数组，允许保存所有元素，包括null，并可根据索引位置对集合进行快速随机访问；缺点是向指定索引位置插入和删除对象速度较慢。
-   LinkedList采用链表结构保存对象，这种结构的优点是便于向集合中插入和删除元素，但随即访问元素的效率较低。

```java
List<> list1 = new ArrayList<>();
List<> list2 = new LinkedList<>();
```

## Set集合

Set集合不能包含重复元素。Set接口的实现类主要有HashSet类和TreeSet:

1.  HashSet: 由哈希表支持，不保证迭代的顺序，不保证集合元素排列顺序恒定。允许使用null值。

2.  TreeSet类不仅实现了Set接口，还实现了java.util.SortedSet接口。TreeSet集合在遍历时按照递增顺序递增排列，TreeSet中新增方法如下：

    | first()                            | 返回集合中第一个(最小)元素                      |
    | ---------------------------------- | ----------------------------------------------- |
    | last()                             | 返回集合中最后一个(最大)元素                    |
    | comparator()                       | 返回对此Set进行排序的比较器                     |
    | headSet(E toElement)               | 返回toElement(不包括)之前的元素集合             |
    | subSet(E fromElement,E endElement) | 返回[fromElemment,endElement)对象之间的所有对象 |
    | tailSet(E fromElement)             | 返回一个新的包含fromElement之后元素的集合       |

## Map集合

Map接口提供了将key映射到值的方法，一个映射不能包含重复的key，每个key只能映射一个值。

| 方法                   | 功能描述                                                  |
| ---------------------- | --------------------------------------------------------- |
| put(K key,V value)     | 向指定集合中添加key与value的映射关系                      |
| containsKey(K key)     | 如果此映射包含指定key的映射关系，则返回true               |
| containsValue(V,value) | 如果此映射将一个或多个key映射到指定值，则返回true         |
| get(K key)             | 如果存在指定的key对象，则返回该对象对应的值，否则返回null |
| keySet()               | 返回该集合中所有key对象形成的Set集合                      |
| values()               | 返回集合中所有值对象形成的Collection集合                  |

```java
public class UpdateStu{
    public static void main(String[] args){
        Map<String,String> map = new HashMap<>();//构建map集合
        map.put("01","张三");
        map.put("01","李四");
        Set<String> set = map.keySet();
        Iterator <String> it = set.iterator();//创建集合迭代器
        System.out.printIn("key集合中的元素");
        while(it.hasNext()){
            System.out.printIn(it.next());
        }
        Collection<String> coll = map.values();
        it = coll.iterator();
        System.out.printIn("value集合中的元素：");
        while(it.hasNext()){
            System.out.printIn(it.next());
        }
    }
}
```

Map接口常用的实现类由HashMap和TreeMap。HashMap类实现Map添加，删除映射关系效率更高。

-   HashMap类是基于哈希表的Map接口的实现，允许使用null值和null键，但必须保证键的唯一性。HashMap通过Hash表对其内部的映射关系进行快速查找。此类不保证映射顺序。
-   TreeMap集合中的映射关系存在一定的顺序。

```java
public class Emp{
    private String e_id;
    private String e_name;
    public Emp(String e_id,String e_name){
        this.e_id = e_id;
        this.e_name = e_name;
    }
    /*******省略了属性的setXXX(),getXXX()方法*********/
}
public class MapText{
    public static void main(String[] args){
        Map<String,String> map = new HashMap<>();
        Emp emp = new Emp("351","张三");
        Emp emp2 = new Emp("512","李四");
        Emp emp3 = new Emp("125","王一");
        Emp emp4 = new Emp("341","黄七");
        
        map.put(emp3.getE_id(),emp3.getE_name());
        map.put(emp2.getE_id(),emp3.getE_name());
        map.put(emp1.getE_id(),emp3.getE_name());
        map.put(emp4.getE_id(),emp3.getE_name());
        
        Set<String> set = map.keySet();
        Iterator<String> it = set.iterator();
        System.out.printIn("HashMap类实现Map集合，无序");
        while(it.hasNext()){
            String str = (String)it.next();
            String name = (String)map.get(str);
            System.out.printIn(str+" :"+name);
        }
    }
}
```

