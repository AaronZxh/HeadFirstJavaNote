# JAVA 学习笔记

## Head First Java

### primitive主数据类型和引用

1.变量有两种，primitive主数据类型和引用。

​		*Dog myDog = new Dog()*；

​		`Dog myDog`声明了一个引用变量。

​		`myDog`并不是对象本身，而是指向通过`new Dog()`创建所的对象的引用。

​		引用变量如同遥控器，对引用变量使用圆点运算符可以存取对象的方法或者`实例变量`。

2.数组也是对象。

​		Dog myDogs = new Dog[3];

​		int[ ] a = {2,3,4};

​		int[ ] b;        

​		创建了一个数组。

​		数组中每一个元素都是一个引用变量，需要使用*myDogs[i]=new Dog()*来创建Dog对象赋值给数组元素，其他没有被赋值的数值元素为`NULL`。

-----

### 方法操作实例变量

1.实例变量是有默认值的：

int ——0

float ——0.0

booleans ——false

reference —— null

2.局部变量`没有`默认值。如果在变量被初始前就要使用，编译器会显示错误。=

**3.JAVA是通过按值传递的，即通过拷贝传递变量的。**

4.封装基本原则：将实例变量标记为私有的。

------

### 编写程序

1.前置与后置递增递减运算符

**++i**：先执行加减操作再来运用变量的值。

2.加强版for循环

for（String name:nameArray){ }              （C++:*for(auto a:b)*)

nameArry的每一个元素被赋给name

3.类型转换

* Interger.parseInt("3");      把代表数字的string转换成int

* int randomNum=(int)(Math.random()*5);

  (int)类型转换cast。

  Math.random()产生一个介于0到小于1之间的数double。

---

### 认识JAVA的API

1.ArrayList

**使用方法**：

1）导入包

import java.util.ArrayList；

2）打出全名

java.util.ArrayList<Dog>list=new java.util.ArrayList<Dog>();

**方法**

add()

remove()

indesOf()

isEmpty()

size()

**注意**

ArrayList只能携带对象而不是primitive主数据类型，编译器会自动的将主数据类型包装成Object存放于ArrayList中。

-----

### 继承与多态

**IS-A**测试：Animal-Canine-Wolf    Canine **IS-A** Animal  Wolf **IS-A**  Canine Wolf **IS-A** Animal 

**遵守合约：子类覆盖父类方法的规则。子类会继承父类所有的public类型的实例变量和方法，但是不会继承private类型的变量和方法**

1）参数必须一样，返回类型必须兼容。（自类必须保证返回类型为父类返回类型一样的类型或者子类）

2）不能降低方法的存取权限。（不能父类里是public的，子类里是private的）

`多态应用`

1)引用类型可以是实际对象类型的父亲

2)方法的参数

3)返回类型

---

### 接口与多态

**1.抽象类与方法**

在类声明前加上 abstract  ：

```java
abstract public class Canine extends Animal{
    public void roam(){}
}
```

抽象类不能被创造出实例。

将方法标记为abstract：

```java
public abstract void eat();//没有方法体，直接以分号结束
```

如果类中有一个抽象的方法，则这个类必须为`abstract类`。

具体的类，必须实现所有的抽象方法。

**2.Object类**

Java中所有类都继承自object类。

object类中的方法：

*equals（Object o)*   

*getClass()*

*hashCode()*  //列出次对象的hash代码

*toString()*    //列出类的名称。

```java
import java.util.ArrayList；
ArrayList<Object>myDogArrayList = new ArrayList<Object>();
Dog aDog =  new Dog();
myDogArrayList.add(aDog);
Dog d = myDogArrayList.get(0);//错误！任何从ArrayList<Object>取出的东西都是Object类型的引用把对象装进ArrayList<Object>，智能当做是Object。只能取得Object的遥控器
```

***编译器是根据引用类型来判断有哪些method可以用，而不是根据object确实的类型***。

**3.类型转换**

```java
Object o = myDogArrayList.get(0);
if (o isntanceof Dog){ //如果O确实为一个Dog。
Dog d =(Dog)o;
}//强制转换为Dog。
```

**4.接口**

```java
public interface Pet{   //interface 取代class
    public abstract void beFriendly(); //接口的方法一定是abstract的，没有类容
    public abstract void play();
}
public class Dog extends Canine implements Pet{
    public void beFriend(){...}; //必须在此实现pet的方法，是合约的规定
    public void play(){...};   //必须在此实现pet的方法，是合约的规定
    public void roam(){...};  //一般的覆盖方法
    public void eat(){...};
}
```

**5.调用父类的方法**

从子类调用父类的方法：super.runReport();

----

### 构造器与垃圾收集器

**1.局部变量与实例变量**

实例变量：声明在类之中的变量。实例变量储存在所属的对象之中。

局部变量：声明在方法中。包括`方法的参数`，和方法内声明的变量。

**2.栈与堆**

**栈**：方法调用+局部变量

**堆**：所有的对象

对于对象来说，对象本身是在堆上的；然而如果指向对象的引用是个局部变量，它在栈上。

如果实例变量是耨个对象的引用，则引用与对象都在堆上。

**3.构造函数**

* 构造函数没有返回类型。
* 如果已经写了一个有参数的构造函数，则编译器不会再帮忙写出另一个没有参数的构造函数。

**4.父类继承与构造函数(子类会继承父类所有的public类型的实例变量和方法，但是不会继承private类型的变量和方法)**

在创建新对象时，所有继承下来的构造函数都会执行。即使是抽象的类也有构造函数，其构造函数也会在具体子类创建出实例时执行。

**调用父类的构造函数**

1.无参数的super()

```java
public class Duck extend Animal{
    int size;
    public Duck(int newSize){
        super();     //如果没有加上super，编译器会帮忙加上。
        size=newSize;
    }
```

2.有参数的父类构造函数

```java
public abstract class Animal{  //创建一个抽象类Animal
    private String name;  
    piblic String getName(){
        return name;
    }
    public Animal(String theName){ //抽象类也有构造函数，但是不能使用new()操作
        name=theName;
    }
}
public class Hippo extend Animal{  //河马类继承了Animal的getName(),但是没有继承私有的name。
    public Hippo(String name){
        super(name);
    }
}
public class MakeHippo{
    public static void main(String[] args){
        Hippo h=new Hippo("Buffy");
        System.out.println(h.getName()); //河马类继承了Animal的getName()
    }
}
```

**注意**：父类的部分必须在子类创建完成之前就完整的成型。`子类可以通过从父类继承下来的方法访问父类的私有成员`。

**5.this()**

```java
class Mini extend Car{
    Color color;
    public Mini(){
        this(Color.Red);  //无参数的构造函数以默认的颜色值调用真正的构造函数
    }
    public Mini(Color C){   //真正的构造函数
        super("Mini");
        color =c;
    }
}
```

`this()必须在构造函数第一行，与super只能二选一！`

**6.对象的生命周期**

:jack_o_lantern:局部变量：

`Life`:局部变量活到方法执行完毕为止

`Scope`:局部变量的范围只限于声明他的方法之内

:jack_o_lantern:引用变量与对象：

只要有活着的引用，对象也就会活着。

---

### 数字与静态

Math这个类中所有的方法都不需要实例变量值。因为所有的方法都是静态的。所以无需Math的实例，只会用到他的类本身。

static标记出不需要类实例的方法，直接以：`类名.方法名()`调用

可以用私有的构造函数来限制非抽象类被初始化，但是并不是有静态方法的类就不能被初始化。

**1.静态的方法不能使用非静态的变量与非静态的方法**

因为静态的方法是通过类名称来调用，所以静态的方法无法引用到该类的任何实例变量。

**2.静态变量**

静态变量也是通过类的名称来存取。

静态变量的值对所有实例来说都相同。所有的实例共享一个静态变量。

静态变量是在类被加载时初始化的，会在执行任何静态方法前就初始化。如没有给静态变量赋值，执行默认初始化。

**3.final**

1）用于静态变量

被标记为final的变量：一旦被初始化之后就不会再改动。

**初始化**：

```java
public static final double PT = 3.1415926   //第一种初始化方法
```

```java
public class Bar{
    public static final BAR_SIGN;
    static{
        BAR_SIGN=(double)Math.random();   //第二种初始化方法
}
```

2）用于普通变量、method、类

```java
final int size =3;//表示size将无法改变
final void calcEhuffie(){} //不能被覆盖
final class MyMostPerfectClass{}//不能被继承
```

**4.primitive主数据类型的包装**

无法将primitive主数据类型直接放在ArrayList或者HashMap中，需要进行包装成类。

* Boolean
* Character
* Byte
* Short
* Interger
* Long
* Float
* Double

autoboxing功能：自动包装

```java
puiblic void doNumsNewWay(){
    ArrayList<Interger>listOfNumbers = new ArrayList<Interger>();
    listOfNumbers.add(3);
    int num = listOfNumbers.get(0);    //自动解开Interger的包装。
}
```

**5.数字的格式化**

```java
String.format("%[argument number][flag][width][.precison]type")
```

[flag]：特定类型的选项，如加逗号或正负号

[width]：最小字符数

[.persion]：精确度

[type]：类型标识








