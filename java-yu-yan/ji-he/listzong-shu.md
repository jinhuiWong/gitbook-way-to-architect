List：元素有序，元素可重复，添加的元素放在最后（按照插入顺序保存元素）

## **java.util**

**ArrayList：数据结构为数组，访问快（可以直接通过下标访问），增删慢，未实现线程同步**

> ArrayList实现了可变大小的数组。它允许所有元素，包括null。ArrayList没有同步。size，isEmpty，get，set方法运行时间为常数。但是add方法开销为分摊的常数，添加n个元素需要O\(n\)的时间。其他的方法运行时间为线性。&lt;/br&gt;  
> 每个ArrayList实例都有一个容量（Capacity），即用于存储元素的数组的大小。这个容量可随着不断添加新元素而自动增加，但是增长算法 并没有定义。当需要插入大量元素时，在插入前可以调用ensureCapacity方法来增加ArrayList的容量以提高插入效率。和LinkedList一样，ArrayList也是非同步的（unsynchronized）。

**LinkedList：数据结构为链表，增删速度快，查询慢，未实现线程同步**

> LinkedList实现了List接口，允许null元素。此外LinkedList提供额外的get，remove，insert方法在 LinkedList的首部或尾部。这些操作使LinkedList可被用作堆栈（stack），队列（queue）或双向队列（deque）。

**Vector：数据结构为数组，访问快（可以直接通过下标访问），增删慢，实现线程同步**

> Vector非常类似ArrayList，但是Vector是同步的。由Vector创建的Iterator，虽然和 ArrayList创建的Iterator是同一接口，但是，因为Vector是同步的，当一个Iterator被创建而且正在被使用，另一个线程改变了 Vector的状态（例如，添加或删除了一些元素），这时调用Iterator的方法时将抛出 ConcurrentModificationException。

** Stack：**

Vector的一个子类，它实现了一个标准的后进先出的栈。

## java.util.concurrent

**CopyOnWriteArrayList**

通过写时复制来支持并发的List，可看做ArrayList的线程安全版本，但要注意是数据最终一致，而非实时一致。

## 总结

| List | 说明 |
| :--- | :--- |
| ArrayList | 最常用的集合类，底层为数组 |
| LinkedList | 不仅是List，也是Deque，底层为双向链表 |
| Vector | 不推荐使用（使用synchronized进行方法同步，效率低） |
| Stack | 不推荐使用 |
| CopyOnWriteArrayList | 写时复制List，支持并发 |



