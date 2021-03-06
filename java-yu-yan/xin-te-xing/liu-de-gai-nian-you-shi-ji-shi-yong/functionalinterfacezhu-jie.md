# @FunctionalInterface

---

FunctionalInterface的字面意思是函数式接口，而所谓的函数式接口，是指**只有一个抽象方法**的接口。函数式接口也叫做SAM接口，即Single Abstract Method interfaces。

所以，注解的@FunctionalInterface的作用就是：标识一个接口为函数式接口。

这里的“只能有一个抽象方法”，并不是说只能有一个方法，函数式接口还可以定义默认方法，静态方法，如下所示：

```java
// 正确的函数式接口
@FunctionalInterface
public interface EventListener {

    // 抽象方法
    void onEvent(String event);

    // java.lang.Object中的方法不是抽象方法
    boolean equals(Object var1);

    // default方法
    default void defaultMethod(){

    }

    // static 方法
    static void staticMethod(){

    }
}
```

函数式接口，主要是为lambda表达式服务的， 比如上面的接口可以用如下lambda表达式的形式来表示一个实现类：

```java
EventListener  eventListener = event ->{ System.out.print("i receive event :" + event)  };
```

以下常见的接口都被标识为了函数式接口：

java.lang.Runnable

java.awt.event.ActionListener

java.util.Comparator

java.util.concurrent.Callable

