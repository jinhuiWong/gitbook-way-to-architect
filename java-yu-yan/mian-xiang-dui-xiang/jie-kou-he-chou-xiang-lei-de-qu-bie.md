# 接口和抽象类的区别

## 抽象类和接口有什么区别

概念：

* **抽象类是用来捕捉子类的通用特性的** 。它不能被实例化，只能被用作子类的超类。抽象类是被用来创建继承层级里子类的模板。
* **接口是抽象方法的集合**。如果一个类实现了某个接口，那么它就继承了这个接口的抽象方法。这就像契约模式，如果实现了这个接口，那么就必须确保使用这些方法。接口只是一种形式，接口自身不能做任何事情。

比较：

| 比较项 | **抽象类** | **接口** |
| :--- | :--- | :--- |
| 默认的方法实现 | 它可以有默认的方法实现 | 接口完全是抽象的。它根本不存在方法的实现 |
| 实现 | 子类使用**extends**关键字来继承抽象类。如果子类不是抽象类的话，它需要提供抽象类中所有声明的方法的实现。 | 子类使用关键字**implements**来实现接口。它需要提供接口中所有声明的方法的实现 |
| 构造器 | 抽象类可以有构造器 | 接口不能有构造器 |
| 与正常Java类的区别 | 除了你不能实例化抽象类之外，它和普通Java类没有任何区别 | 接口是完全不同的类型 |
| 访问修饰符 | 抽象方法可以有**public**、**protected**和**default**这些修饰符 | 接口方法默认修饰符是**public**。你不可以使用其它修饰符。 |
| main方法 | 抽象方法可以有main方法并且我们可以运行它 | 接口没有main方法，因此我们不能运行它。 |
| 多继承 | 抽象方法可以继承一个类和实现多个接口 | 接口只可以继承一个或多个其它接口 |
| 速度 | 它比接口速度要快 | 接口是稍微有点慢的，因为它需要时间去寻找在类中实现的方法。 |
| 添加新方法 | 如果你往抽象类中添加新的方法，你可以给它提供默认的实现。因此你不需要改变你现在的代码。 | 如果你往接口中添加方法，那么你必须改变实现该接口的类。 |
| 成员变量 | 成员变量可以是**public**、**protected、private**和**default** | 成员变量必须是**public static final**的 |

## 什么时候使用抽象类和接口

* 如果你拥有一些方法并且想让它们中的一些有默认实现，那么使用抽象类吧。
* 如果你想实现多重继承，那么你必须使用接口。由于**Java不支持多继承**，子类不能够继承多个类，但可以实现多个接口。因此你就可以使用接口来解决它。
* 如果基本功能在不断改变，那么就需要使用抽象类。如果不断改变基本功能并且使用接口，那么就需要改变所有实现了该接口的类。

## Java8中的默认方法和静态方法

JDK1.8中向接口中引入默认方法和静态方法，以此来减少抽象类和接口之间的差异。

### 默认方法

意义：可以为接口添加新的默认方法，而不会破坏接口的实现

示例：

```text
public interface vehicle {
   default void print(){
      System.out.println("我是一辆车!");
   }
}
```

假如一个类实现了多个接口，且这些接口有相同的默认方法，那这个类该怎么选择，有两种方案：

①**创建自己的默认方法，来覆盖重写接口的默认方法**

②**使用 super 来调用指定接口的默认方法**

比如，有两个接口：

```text
public interface vehicle {
   default void print(){
      System.out.println("我是一辆车!");
   }
}

public interface fourWheeler {
   default void print(){
      System.out.println("我是一辆四轮车!");
   }
}
```

使用第一种方案：

```text
public class car implements vehicle, fourWheeler {
   default void print(){
      System.out.println("我是一辆四轮汽车!");
   }
}
```

使用第二种方案：

```text
public class car implements vehicle, fourWheeler {
   default void print(){
      vehicle.super.print();
   }
}
```

### 静态方法

意义：可以从接口直接调用和它相关的辅助方法（Helper method），而不是从其它的类中调用（之前这样的类往往以对应接口的复数命名，例如Collections）。

示例：

```text
public interface MyInterf {

    String m1();

    static String m2() {
        return "Hello，I am an static method in Interface!";
    }
}
```

内容来源：

[Java抽象类与接口的区别](http://www.importnew.com/12399.html)  
[Java8的默认方法和静态接口方法](http://blog.csdn.net/l_sail/article/details/70951419)

