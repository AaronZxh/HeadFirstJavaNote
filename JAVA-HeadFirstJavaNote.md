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

java.util.ArrayList<Dog>=new java.util.ArrayList<Dog>();

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

**遵守合约：子类覆盖父类方法的规则**

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

### 数字与静态






















