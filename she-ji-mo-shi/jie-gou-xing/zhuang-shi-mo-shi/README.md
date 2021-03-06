# 装饰模式

装饰器模式：创建一个装饰类来包装原来的类，在不改变原来类结构不变的情况下，扩展其功能。                              装饰模式是继承的一个替代模式，这里有一个合成复用原则：尽量使用对象组合，而不是继承来达到复用的目的（优先has-a而非is-a）。装饰类和被装饰类可以独立发展，不会相互耦合，不会受到继承的约束。

**装饰器模式的本质：动态组合。**

**装饰模式中的角色**

* Component（抽象构件）：ConcreteComponent和Decorator的共同父类，声明在具体构件中需要的业务方法，可以使客户端以一致的方式处理未被装饰的对象以及装饰之后的对象，实现客户端的透明操作。
* ConcreteComponent（具体构件）：Component的子类，定义具体的构件对象，实现Component中声明的方法，装饰器就是给该角色增加额外的方法。
* Decorator（抽象装饰类）：Component的子类，用于给ConcreteComponent增加方法（仅声明），维护一个指向Component引用。
* ConcreteDecorator（具体装饰类）：Decorator的子类，负责向构件添加新的职责。每一个具体装饰类都定义了一些新的行为，它可以调用在抽象装饰类中定义的方法，并可以增加新的方法用以扩充对象的行为。                                                                                                   

**                                                                                    装饰模式结构代码**

Component：根据实际情况，Component可以是接口，也可以是抽象类

```java
public interface Component{

    public void operation();
}                                                                                                                      
```

ConcreteComponent

```java
pubilc class ConcreteComponent implements Component{

    public void operation(){
        System.out.print("origin operation implements");
    }
}                                                                                                            
```

Decorator

```java
public class Decorator implements Component{

       //维持一个对抽象构件对象的引用
       private Component component;

       public Decorator(Component component){
              this.component=component;
       }

       public void operation(){
              //调用原来的业务方法
              component.operation();
       }
}
```

ConcreteDecorator：两种不同类型的具体装饰器类

```java
class XXXConcreteDecoratorA extends Decorator{

       public ConcreteDecorator(Component  component){
              super(component);
       }

       public void operation(){
              super.operation();//调用原有业务方法
              addedBehavior();  //调用新增业务方法
       }

       //新增业务方法
       public  void addedBehavior(){    
              System.out.print("add func in origin operation");
       }
}

class ConcreteDecoratorB extends Decorator{

       public ConcreteDecorator(Component  component){
              super(component);
       }

       public void operation(){
              super.operation();//调用原有业务方法
       }

       //新增业务方法
       public  void newOperation(){    
              System.out.print("new operation...");
       }
}
```

注意：被装饰器装饰的原始类，可能也是一个装饰类。

现在来看一个例子：假如现在要开发一套图形界面构件库VisualComponent，该构件库提供基本构件，如窗体、文本框、列表框等。同时，还要满足用户定制的一些特效显示效果，如带滚动条的窗体、带黑色边框的文本框、既带滚动条又带黑色边框的列表框等等。

Component：只有一个方法`display()`，显示本基本构建

```java
public interface Component{
       void display();
}
```

ConcreteComponent：包含三种，分别是窗体Window，文本框TextBox，列表框ListBox

```java
//窗体类：具体构件类
public class Window implements Component{
       public  void display(){
              System.out.println("显示窗体！");
       }
}

//文本框类
public class TextBox implements Component{
       public  void display(){
              System.out.println("显示文本框！");
       }
}

//列表框类
public class ListBox implements Component{
       public  void display(){
              System.out.println("显示列表框！");
       }
}
```

Decorator：

```java
public class ComponentDecorator implements Component{

       //维持对抽象构件类型对象的引用
       private Component component;  

       public ComponentDecorator(Component  component){
              this.component = component;
       }

       public void display(){
              component.display();
       }
}
```

ConcreteDecorator：具体装饰器，有两个，一个是提供滚动条功能，另一个是提供黑色边框功能；

```java
//滚动条装饰类
class ScrollBarDecorator extends  ComponentDecorator{

       public ScrollBarDecorator(Component  component){
              super(component);
       }

       public void display(){
              this.setScrollBar();
              super.display();
       }

       public void setScrollBar(){
              System.out.println("为构件增加滚动条！");
       }
}

//黑色边框装饰类
public class BlackBorderDecorator extends  ComponentDecorator{

       public BlackBorderDecorator(Component  component){
              super(component);
       }

       public void display(){
              this.setBlackBorder();
              super.display();
       }

       public void setBlackBorder(){
              System.out.println("为构件增加黑色边框！");
       }
}
```

客户端

```java
public class Client{
       public  static void main(String args[]){
              Component window = new Window();
              window.display();

              Component scroll = new ScrollBarDecorator(window);
              scroll.display();

              Component border = new BlackBorderDecorator(window);
              border.display();

              Component scrollAndBorder = new ScrollBarDecorator(new BlackBorderDecorator(new TextBox()));
              scrollAndBorder.display();
       }
}
//输出如下
显示窗体

为构建添加滚动条！
显示窗体

为构建添加黑色边框！
显示窗体

为构建添加滚动条
为构建添加黑色边框
显示文本框
```

假如现在需要再为基础构建添加悬浮功能，只需要再增加一个悬浮装饰类即可，原有代码无需改动，只需要客户端在使用时使用这个悬浮装饰类装饰一下原始构件，即可为构件增加悬浮功能。

