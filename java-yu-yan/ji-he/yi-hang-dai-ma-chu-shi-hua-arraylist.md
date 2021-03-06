# 一行代码初始化ArrayList

很多时候，我们需要初始化一个集合，元素可能就是String或者Integer这种简单数据类型，最常规的方法如下：

```java
List<String> colors = new ArrayList<String>();
colors.add("red");
colors.add("white");
colors.add("black");
```

但如上写法，显得繁琐，可考虑使用如下方式：

```java
①匿名内部类的形式
List<String> list = new ArrayList<String>() {{
    add("red");
    add("white");
    add("black");
}};

②借助Arrays.asList()方法
List<String> list = new ArrayList<String>(Arrays.asList("red", "white", "black"));

③如果只是list，不要求ArrayList，可直接使用Arrays.asList()方法，但要注意此时集合不可变
List<String> list = Arrays.asList("red", "white", "black");

④如果只是想创建不可变集合，可借助guava提供的ImmutableList
List<String> list = ImmutableList.of("red", "white", "black");
⑤如果只是想创建不可变集合，且只有一个元素，除了借助guava提供的ImmutableList，还可以使用JDK自带的Collections
List<String> list = Collections.singletonList("color");

⑥如果只是想创建某个对象的n副本集合
List<String> list = Collections.nCopies(1000, "red");

⑦自己写工具类
public static <T> ArrayList<T> createArrayList(T ... elements) {
        ArrayList<T> list = new ArrayList<T>();
        for (T element : elements) {
            list.add(element);
        }
        return list;
}
```

 

