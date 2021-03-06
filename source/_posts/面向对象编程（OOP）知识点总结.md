---
title: Java面向对象的一些总结
tags: [Interview,java,面向对象]
categories: Java Basic
copyright: true
---
#### 一.面向对象的基本概念
##### 1.解释下多态性（polymorphism），封装性（encapsulation），内聚（cohesion）以及耦合（coupling）
**抽象**：抽象是将一类对象的共同特征总结出来构造类的过程，包括**数据抽象**和**行为抽象**两方面。抽象**只关注对象有哪些属性和行为**，并不关注这些行为的细节是什么。

**封装**：通常认为**封装是把数据和操作数据的方法绑定起来，对数据的访问只能通过已定义的接口**。面向对象的本质就是将现实世界描绘成一系列完全自治、封闭的对象。我们在类中编写的方法就是对实现细节的一种封装；我们编写一个类就是对数据和数据操作的封装。可以说，封装就是隐藏一切可隐藏的东西，只向外界提供最简单的编程接口（可以想想普通洗衣机和全自动洗衣机的差别，明显全自动洗衣机封装更好因此操作起来更简单；我们现在使用的智能手机也是封装得足够好的，因为几个按键就搞定了所有的事情）。
<!--more-->
**内聚**：进行架构设计时的内聚高低是指，**设计某个模块或者关注点时，模块或关注点内部的一系列相关功能的相关程度的高低**。高内聚提供了更好的可维护性和可复用性。而低内聚的模块则表名模块直接的依赖程度高，那么一旦修改了该模块依赖的对象则无法使用该模块，必须也进行相应的修改才可以继续使用。

**耦合**：简单地说，软件工程中对象之间的**耦合度就是对象之间的依赖性**。指导使用和维护对象的主要问题是对象之间的多重依赖性。对象之间的耦合越高，维护成本越高。因此对象的设计应使类和构件之间的耦合最小。**耦合性是程序结构中各个模块之间相互关联的度量**。它取决于各个模块之间的接口的复杂程度、调用模块的方式以及哪些信息通过接口。

耦合可以分为以下几种，它们之间的耦合度由高到低排列如下：
- **内容耦合**。当一个模块直接修改或操作另一个模块的数据时，或一个模块不通过正常入口而转入另一个模块时，这样的耦合被称为内容耦合。内容耦合是最高程度的耦合，应该避免使用之。
- **公共耦合**。两个或两个以上的模块共同引用一个全局数据项，这种耦合被称为公共耦合。在具有大量公共耦合的结构中，确定究竟是哪个模块给全局变量赋了一个特定的值是十分困难的。
- **外部耦合** 。一组模块都访问同一全局简单变量而不是同一全局数据结构，而且不是通过参数表传递该全局变量的信息，则称之为外部耦合。
控制耦合 。一个模块通过接口向另一个模块传递一个控制信号，接受信号的模块根据信号值而进行适当的动作，这种耦合被称为控制耦合。
标记耦合 。若一个模块A通过接口向两个模块B和C传递一个公共参数，那么称模块B和C之间存在一个标记耦合。
- **数据耦合**。模块之间通过参数来传递数据，那么被称为数据耦合。数据耦合是最低的一种耦合形式，系统中一般都存在这种类型的耦合，因为为了完成一些有意义的功能，往往需要将某些模块的输出数据作为另一些模块的输入数据。
- **非直接耦合** 。两个模块之间没有直接关系，它们之间的联系完全是通过主模块的控制和调用来实现的。
![高内聚&低耦合](http://upload-images.jianshu.io/upload_images/8926909-d63352e73d06a55c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
>[参考：《面向对象三大特性五大原则 + 低耦合高内聚》](http://www.cnblogs.com/corvoh/p/5747856.html)

##### 2.多态的用途和实现原理
>**1、编译时多态（又称静态多态）
2、运行时多态（又称动态多态）**

**重载（overload）**就是**编译时多态**的一个例子，编译时多态在编译时就已经确定，运行时运行的时候调用的是确定的方法。
我们通常所说的**多态指的都是运行时多态**，也就是编译时不确定究竟调用哪个具体方法，一直延迟到运行时才能确定。这也是为什么有时候多态方法又被称为**延迟方法**的原因。
- 多态通常有两种实现方法：
1、子类继承父类（extends）
2、子类实现接口（implements）
- **多态最大的用途**
个人认为在于**对设计和架构的复用**，更进一步来说，《[设计模式](http://book.douban.com/subject/1052241/)》中提倡的针对接口编程而不是针对实现编程就是充分利用多态的典型例子。**定义功能和组件时定义接口，实现可以留到之后的流程中。**同时一个接口可以有多个实现，甚至于完全可以在一个设计中同时使用一个接口的多种实现。
- **多态实现原理**
多态允许具体访问时实现方法的动态绑定。Java对于动态绑定的实现主要**依赖于方法表**，通过继承和接口的多态实现有所不同。
**继承**：在执行某个方法时，在方法区中找到该类的方法表，再确认该方法在方法表中的偏移量，找到该方法后如果被重写则直接调用，否则认为没有重写父类该方法，这时会按照继承关系搜索父类的方法表中该偏移量对应的方法。
**接口**：Java 允许一个类实现多个接口，从某种意义上来说相当于多继承，这样同一个接口的的方法在不同类方法表中的位置就可能不一样了。所以不能通过偏移量的方法，而是通过搜索完整的方法表。
*tips：因为每次接口调用都要搜索方法表，所以从效率上来说，接口方法的调用总是慢于类方法的调用的。*

> [《Java 多态的实现机制》](http://www.cnblogs.com/crane-practice/p/3671074.html)
[《Java技术——多态的实现原理》](http://blog.csdn.net/seu_calvin/article/details/52191321)

##### 3.对象封装的原则是什么?
在面向对象程式设计方法中，封装（英语：Encapsulation）是指一种将抽象性函式接口的实现细节部份包装、隐藏起来的方法。封装可以被认为是一个保护屏障，防止该类的代码和数据被外部类定义的代码随机访问。要访问该类的代码和数据，必须通过严格的接口控制。封装最主要的功能在于我们能修改自己的实现代码，而不用修改那些调用我们代码的程序片段。适当的封装可以让程式码更容易理解与维护，也加强了程式码的安全性。
- 修改属性的可见性来限制对属性的访问（一般限制为private）；
- 对每个值属性提供对外的公共方法访问，也就是创建一对赋取值方法，用于对私有属性的访问；

##### 4.获得一个类的类对象有哪些方式？
- 1.通过对象的getClass方法进行获取。这种方式需要具体的类和该类的对象，以及调用getClass方法。
- 2.任何数据类型(包括基本数据类型)都具备着一个静态的属性class，通过它可直接获取到该类型对应的Class对象。这种方式要使用具体的类，然后调用类中的静态属性class完成，无需调用方法，性能更好。
- 3.通过Class.forName()方法获取。这种方式仅需使用类名，就可以获取该类的Class对象，更有利于扩展。
```java
import org.junit.Test;
/**
 * 演示获取Class c对象的三种方法
 *@fileName ReflectGetClass.java
 */
public class ReflectGetClass {

    /**
     * 法1：通过对象---对象.getClass()来获取c(一个Class对象)
     */
    @Test
    public void get1(){
        Person p=new Person("Jack", 23);
        Class c=p.getClass();//来自Object方法
    }

    /**
     * 法2：通过类(类型)---任何数据类型包括(基本数据类型)
     * 都有一个静态的属性class ，他就是c 一个Class对象
     */
    @Test
    public void get2(){
        Class c=Person.class;
        Class c2=int.class;
    }

    /**
     * 法3：通过字符串(类全名 )---能够实现解耦：Class.forName(str)
     */
    @Test
    public void get3(){
        try {
            Class c=Class.forName("cn.hncu.reflect.test.Person");
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        }
    }
}
```

##### 5.重载（Overload）和重写（Override）的区别。重载的方法能否根据返回类型进行区分？
**一、重写（override）**
override是重写（覆盖）了一个方法，以实现不同的功能。一般是用于子类在继承父类时，重写（重新实现）父类中的方法。重写（覆盖）的规则：
- 1、重写方法的参数列表必须完全与被重写的方法的相同,否则不能称其为重写而是重载.
- 2、重写方法的访问修饰符一定要大于被重写方法的访问修饰符（public>protected>default>private）。
- 3、重写的方法的返回值必须和被重写的方法的返回一致；
- 4、重写的方法所抛出的异常必须和被重写方法的所抛出的异常一致，或者是其子类；
- 5、被重写的方法不能为private，否则在其子类中只是新定义了一个方法，并没s有对其进行重写。
- 6、静态方法不能被重写为非静态的方法（会编译出错）。
**二、overload是重载**
一般是用于在一个类内实现若干重载的方法，这些方法的名称相同而参数形式不同。
重载的规则：
- 1、在使用重载时只能通过相同的方法名、不同的参数形式实现。不同的参数类型可以是不同的参数类型，不同的参数个数，不同的参数顺序（参数类型必须不一样）；
- 2、不能通过访问权限、返回类型、抛出的异常进行重载；
- 3、方法的异常类型和数目不会对重载造成影响；
多态的概念比较复杂，有多种意义的多态，一个有趣但不严谨的说法是：继承是子类使用父类的方法，而多态则是父类使用子类的方法。一般，我们使用多态是为了避免在父类里大量重载引起代码臃肿且难于维护。
《java编程思想》中很好的回答了**不能以返回值来区分重载方法：**
```java
void f(){ }
void f(){ return 1; }
```
假如有`int x=f()`,这里是可以区分重载方法，但有时候并不需要返回值，只是调用方法，那么像这样的`f()`就让人无法理解了。

##### 6.说出几条 Java 中方法重载的最佳实践？**
- a）不要重载这样的方法：一个方法接收 int 参数，而另个方法接收 Integer 参数。
- b）不要重载参数数量一致，而只是参数顺序不同的方法。
- c）如果重载的方法参数个数多于 5 个，采用**可变参数**。

#### 二、抽象类和接口
##### 1.抽象类和接口的区别
- **一、相似性**
- 接口和抽象类都不能被实例化，它们都位于继承树的顶端，用于被其他类实现和继承。
- 接口和抽象类都可以包含抽象方法，实现接口或继承抽象类的普通子类都必须实现这些抽象方法。
**二、接口和抽象类的区别**
- 接口里只能包含抽象方法，静态方法和默认方法，不能为普通方法提供方法实现，抽象类则完全可以包含普通方法。
- 接口里只能定义静态常量，不能定义普通成员变量，抽象类里则既可以定义普通成员变量，也可以定义静态常量。
- 接口不能包含构造器，抽象类可以包含构造器，抽象类里的构造器并不是用于创建对象，而是让其子类调用这些构造器来完成属于抽象类的初始化操作。
- 接口里不能包含初始化块，但抽象类里完全可以包含初始化块。
- 一个类最多只能有一个直接父类，包括抽象类，但一个类可以直接实现多个接口，通过实现多个接口可以弥补Java单继承不足。
>接口可以继承接口。
抽象类可以实现(implements)接口
抽象类可继承具体类。
抽象类中可以有静态的main方法。

备注：只要明白了接口和抽象类的本质和作用，这些问题都很好回答，你想想，如果你是java语言的设计者，你是否会提供这样的支持，如果不提供的话，有什么理由吗？如果你没有道理不提供，那答案就是肯定的了。只有记住抽象类与普通类的唯一区别就是不能创建实例对象和允许有abstract方法。

##### 2.java接口的基本概念，是否可继承，以及优点？
**接口（Interface）**，在JAVA编程语言中是一个抽象类型，是抽象方法的集合。接口通常以interface来声明。一个类通过继承接口的方式，从而来继承接口的抽象方法。如果一个类只由抽象方法和全局常量组成，那么这种情况下不会将其定义为一个抽象类。只会定义为一个接口，所以接口严格的来讲属于一个特殊的类，而这个类里面只有抽象方法和全局常量，就连构造方法也没有。

- 一个接口可以继承多个接口.
`interface C extends A, B {}`是可以的.
- 一个类可以实现多个接口:
`class D implements A,B,C{}`
- 但是一个类只能继承一个类,不能继承多个类
`class B extends A{}`
- 在继承类的同时,也可以继承接口:
`class E extends D implements A,B,C{}`
这也正是选择用接口而不是抽象类的原因


##### 3、接口的优点或者说面向接口编程的思想是什么（这里要结合运行时多态更好理解）
在系统分析和架构中，分清层次和依赖关系，每个层次不是直接向其上层提供服务（即不是直接实例化在上层中），而是**通过定义一组接口，仅向上层暴露其接口功能，上层对于下层仅仅是接口依赖，而不依赖具体类**。
好处：首先对系统灵活性大有好处。当下层需要改变时，只要接口及接口功能不变，则上层不用做任何修改。甚至可以在不改动上层代码时将下层整个替换掉。接口体现的是一种规范和实现分离的设计哲学，充分利用接口可以极好地降低程序各模块之间的耦合，从而提高系统的可扩展性和可维护性。基于这种原则，通常推荐“面向接口”编程，而不是面向实现类编程，希望通过面向接口编程来降低程序的耦合。
总的来说就是：**降低程序耦合度，提高系统的可扩展性和维护性。**
#### 三、继承
**1、继承（Inheritance）与聚合（Aggregation）的区别在哪里**
**2、继承和组合之间有什么不同**
- 如果存在一种IS-A的关系（比如Bee“是一个”Insect），并且一个类需要向另一个类暴露所有的方法接口，那么更应该用继承的机制。
- 如果存在一种HAS-A的关系（比如Bee“有一个”attack功能），那么更应该运用组合。

**3、为什么类只能单继承，接口可以多继承**
首先，类的多继承有缺点：
第一，如果一个类继承多个父类，如果父类中的方法名如果相同，那么就会产生歧义。
第二，如果父类中的方法同名，子类中没有覆盖，同样会产生上面的错误。
但是接口就设计成多继承，是因为接口可以避免上述问题：
首先，接口中的只有抽象方法和静态常量。对于一个类实现多个接口的情况和一个接口继承多个接口的情况，因为接口只有抽象方法，具体方法只能由实现接口的类实现（也是因为实现类一定会覆盖接口中的方法），在调用的时候始终只会调用实现类（也就是子类覆盖的方法）的方法（不存在歧义），因此不存在 多继承的第二个缺点；而又因为接口只有静态的常量，但是由于静态变量是在编译期决定调用关系的，即使存在一定的冲突也会在编译时提示出错；而引用静态变量一般直接使用类名或接口名，从而避免产生歧义，因此也不存在多继承的第一个缺点。
**4、存在两个类，C 继承 B，B 继承 A，能将 B 转换为 C 么？如 C = (C) B**
不能转换，测试代码报错：
`Exception in thread "main" java.lang.ClassCastException: interfaceDemo.B cannot be cast to interfaceDemo.C`

**5、如果类 a 继承类 b，实现接口c，而类 b 和接口 c 中定义了同名变量，请问会出现什么问题**

#### 四、泛型
##### 1、泛型的存在是用来解决什么问题？
首先需要明确泛型的概念，**泛型（Generics ）**是把类型参数化，运用于类、接口、方法中，可以通过执行泛型类型调用 分配一个类型，将用分配的具体类型替换泛型类型。然后，所分配的类型将用于限制容器内使用的值，这样就无需进行类型转换，还可以在编译时提供更强的类型检查。
总结来说就是：
（1）消除显示的强制类型转换，提高代码复用
（2）提供更强的类型检查，避免运行时的`ClassCastException`。
这个问题产生的背景是针对容器中，基于继承的泛型实现会带来两个问题，请看代码：
```java
public class ArrayList {
    public Object get(int i) { ... }
    public void add(Object o) { ... }
    ...
    private Object[] elementData;
}
```
基于继承的泛型实现会带来两个问题：第一个问题是有关`get()`方法的，我们每次调用`get()`方法都会返回一个`Object`对象，每一次都要强制类型转换为我们需要的类型，这样会显得很麻烦；第二个问题是有关add方法的，假如我们往聚合了`String`对象的`ArrayList`中加入一个`File`对象，编译器不会产生任何错误提示，而这不是我们想要的。所以，从Java 5开始，ArrayList在使用时可以加上一个类型参数（type parameter），这个类型参数用来指明ArrayList中的元素类型。类型参数的引入解决了以上提到的两个问题，如以下代码所示：
```java
ArrayList<String> s = new ArrayList<String>();
s.add("abc");
String s = s.get(0); //无需进行强制转换
s.add(123);  //编译错误，只能向其中添加String对象
```
##### 2、泛型的常用特点？
这里其实问的就是泛型在使用过程中遵循的相关规范。类型参数（又称类型变量）用作占位符，指示在运行时为类分配类型。根据需要，可能有一个或多个类型参数，并且可以用于整个类。根据惯例，类型参数是单个大写字母，该字母用于指示所定义的参数类型。下面列出每个用例的标准类型参数：
```java
E：元素
K：键
N：数字
T：类型
V：值
S、U、V 等：多参数情况中的第 2、3、4 个类型
? 表示不确定的java类型（无限制通配符类型）
```
>[《Java 泛型一览笔录》](http://www.importnew.com/27037.html)
[《深入理解Java之泛型》](http://www.importnew.com/19740.html)
#### 五、匿名内部类
**内部类（nested classes）**，面向对象程序设计中，可以在一个类的内部定义另一个类。嵌套类分为两种，即静态嵌套类和非静态嵌套类。静态嵌套类使用很少，最重要的是非静态嵌套类，也即是被称作为内部类(inner)。内部类是JAVA语言的主要附加部分。内部类几乎可以处于一个类内部任何位置，可以与实例变量处于同一级，或处于方法之内，甚至是一个[表达式](http://baike.baidu.com/view/420676.htm)的一部分。
##### 1、匿名内部类是否可以继承其它类？是否可以实现接口？
使用匿名内部类我们必须要继承一个父类或者实现一个接口，当然也仅能只继承一个父类或者实现一个接口。同时它也是没有class关键字，这是因为匿名内部类是直接使用new来生成一个对象的引用，当然这个引用是隐式的。不可以继承其它类和实现接口。

##### 2、内部类分为几种？
>- 成员内部类，在一个类（外部类）中直接定义的内部类；
>- 局部内部类，在一个方法（外部类的方法）中定义的内部类;
>- 匿名内部类，

**1.成员内部类**
可以访问它的外部类的所有成员变量和方法，不管是静态的还是非静态的都可以。
在外部类里面创建成员内部类的实例：`this.new B()；`
在外部类之外创建内部类的实例：`(new Test1()).new B().go();`
**2.局部内部类**
定义在方法中，比方法的范围还小。是内部类中最少用到的一种类型。像局部变量一样，不能被`public`,`protected`, `private`和`static`修饰。只能访问方法中定义的final类型的局部变量。
方法内部类在方法中定义，所以只能在方法中使用，即只能在方法当中生成方法内部类的实例并且调用其方法。
**3.匿名内部类**
没有名字的局部内部类，不使用关键字class, extends, implements, 没有构造方法。什么情况下需要使用匿名内部类？如果满足下面的一些条件，使用匿名内部类是比较合适的：
- 只用到类的一个实例。
- 类在定义后马上用到。
- 类非常小（SUN推荐是在4行代码以下）
- 给类命名并不会导致你的代码更容易被理解。

**在使用匿名内部类时，要记住以下几个原则：**
- 匿名内部类不能有构造方法。
- 匿名内部类不能定义任何静态成员、方法和类。
- 匿名内部类不能是public,protected,private,static。
- 只能创建匿名内部类的一个实例。
- 一个匿名内部类一定是在new的后面，用其隐含实现一个接口或实现一个类。
- 因匿名内部类为局部内部类，所以局部内部类的所有限制都对其生效。
```java
//实例代码
interface innerclass{
    public void print();
}

public class Main {
    public static void main(String[] args) {
        innerclass i = new innerclass() {
            @Override
            public void print() {
                System.out.println("匿名内部类");
                // TODO Auto-generated method stub

            }
        };
        i.print();
    }
}
```
匿名内部类的高频使用场景是在多线程下(灵活使用箭头函数语法糖)：
```java
// Java 8之前：
new Thread(new Runnable() {
    @Override
    public void run() {
        System.out.println("Before Java8, too much code for too little to do");
    }
}).start();

//Java 8方式：
new Thread(() -> System.out.println("In Java8, Lambda expression!!") ).start();
```
##### 3、内部类可以引用它的包含类（外部类）的成员吗？
内部类可以直接访问外部类的成员属性

##### 4、请说一下 Java 中为什么要引入内部类？还有匿名内部类？
-  内部类对象可以访问创建它的对象的实现，包括私有数据；
- 内部类不为同一包的其他类所见，具有很好的封装性；
- 使用内部类可以很方便的编写事件驱动程序；
- 匿名内部类可以方便的定义运行时回调；
- 内部类可以方便的定义



