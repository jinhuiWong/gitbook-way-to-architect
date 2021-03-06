# Java: for\(;;\) vs. while\(true\)

Semantically, they're completely equivalent. It's a matter of taste, but I think `while(true)` looks cleaner, and is easier to read and understand at first glance. In Java neither of them causes compiler warnings.

At the bytecode level, it might depend on the compiler and the level of optimizations, but in principle the code emitted should be the same.

**EDIT:**

On my compiler, using the [Bytecode Outline](http://andrei.gmxhome.de/bytecode/) plugin,the bytecode for `for(;;){}` looks like this:

```text
   L0
    LINENUMBER 6 L0
   FRAME SAME
    GOTO L0
```

And the bytecode for `while(true){}` looks like this:

```text
   L0
    LINENUMBER 6 L0
   FRAME SAME
    GOTO L0
```

So yes, at least for me, they're identical.

所以，代码中使用while\(true\)还是for\(;;\)，只是个人喜好问题，编译后的字节码是相同的，无所谓哪个性能更好。

**验证**

Java代码

```java
public class ForAndWhile {
    public void forTest(){
        for(;;){
            System.out.println("");
        }
    }
    public void forWhile(){
        while (true){
            System.out.println("");
        }
    }
}
```

 编译后的字节码：

```java
// class version 52.0 (52)
// access flags 0x21
public class com/maxwell/learning/common/ForAndWhile {

  // compiled from: ForAndWhile.java

  // access flags 0x1
  public <init>()V
   L0
    LINENUMBER 7 L0
    ALOAD 0
    INVOKESPECIAL java/lang/Object.<init> ()V
    RETURN
   L1
    LOCALVARIABLE this Lcom/maxwell/learning/common/ForAndWhile; L0 L1 0
    MAXSTACK = 1
    MAXLOCALS = 1

  // access flags 0x1
  public forTest()V
   L0
    LINENUMBER 11 L0
   FRAME SAME
    GETSTATIC java/lang/System.out : Ljava/io/PrintStream;
    LDC ""
    INVOKEVIRTUAL java/io/PrintStream.println (Ljava/lang/String;)V
    GOTO L0
   L1
    LOCALVARIABLE this Lcom/maxwell/learning/common/ForAndWhile; L0 L1 0
    MAXSTACK = 2
    MAXLOCALS = 1

  // access flags 0x1
  public forWhile()V
   L0
    LINENUMBER 17 L0
   FRAME SAME
    GETSTATIC java/lang/System.out : Ljava/io/PrintStream;
    LDC ""
    INVOKEVIRTUAL java/io/PrintStream.println (Ljava/lang/String;)V
    GOTO L0
   L1
    LOCALVARIABLE this Lcom/maxwell/learning/common/ForAndWhile; L0 L1 0
    MAXSTACK = 2
    MAXLOCALS = 1
}
```



问答来源：Stack Oveflow——[Java: for\(;;\) vs. while\(true\)](https://stackoverflow.com/questions/8880870/java-for-vs-whiletrue)

