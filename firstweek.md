##System
```java
static long currentTimeMillis() //获取当前时间
public static void arraycopy(Object src,int srcPos,Object dest,int destPos, int length)//复制某个数组的一段到另一个数组的一段
```
##StringBuilder

```java
append()//在末尾添加
insert(number,x)//在指定位置添加
```
* 链式编程：方法返回值是一个对象，可以继续调用方法

##包装类
* Integer
* Character
  
**装箱：把基本类型的数据，包装到包装类中**
**拆箱： 在包装类中取出基本类型的数据**

* ***Interger***
  ```java
  static String toString(int i)//返回一个指定整数的String对象
  static String valueOf(int i)//返回int参数的字符串表现形式,**这是一个String类方法**
  static int parseInt(String s)//把数值S转为int类型
  ```

##Collection集合
>集合是java中的一种容器
数组的长度是固定的而集合的长度是可变的
集合存储的都是对象而且对象的类型可以不一样
数组存储的对象都是同一类型的元素

* Vector
* ArrayList
* LinkedList
* TreeSet
* HashSet
* LinkedHashSet

**List接口**
* 有序的集合（存取元素顺序相同）
* 允许存储重复的元素
* 有素引，可以使用普通的for循环遍历
* Vector ArrayList LinkedList

**Set接口**
* 不允许有重复的元素
* 没有索引（不能使用普通的for循环遍历）
* TreeSet HashSet(无序的集合) LinkedHashSet(有序)

**Collection 接口没有带索引的方法**

##Collection常用功能
集合层次结构中的根界面 。 集合表示一组被称为其元素的对象。 一些集合允许重复元素，而其他集合不允许。定义所有单列集合共性的方法
共性的方法：
* public boolean add(E e): 把给定的对象添加到当前集合中
* public void clear():     清空集合中所有的元素
* public boolean remove(E e): 把给定对象在当前的集合中删除
* public boolean contains(E e): 判断当前集合中是否包含给定的对象
* public int size(): 返回集合中元素的个数
* public Object[] toArray(): 把集合中的元素存储到数组中

##Iterator接口
迭代：Collection集合元素的通用获取方式
* boolean hasNext() 判断是否含有下一个元素 有就返回true
* E next() 返回迭代的下一个元素

Iterator迭代器是一个接口，我们无法直接使用，需要使用Iterator接口的实现类对象，获取实现类的方式比较特殊

Collection接口中有一个方法叫iterator(),这个方法返回的就是迭代器的实现类对象

Iterator<E> iterator() 返回再次collection的元素上进行迭代的迭代器
迭代器的使用步骤(重点)：
1.使用集合中的帆帆发iterator()获取迭代器的实现类对象，使用Iterator接口接收(多态)
2.使用Iterator接口中的方法hasNext()来判断是否含有下一个元素
3.使用next()取出下一个元素

##增强for循环
>底层使用的也是迭代器，使用for循环的格式，简化了迭代器的书写
* 用来遍历集合和数组

Collection<E>extends Iterable<E>:所有单列集合都可以使用增强for

##泛型
ArrayList集合再定义的时候不知道集合中都会存储什么类型的数据
**定义一个含有泛型的方法**
```java
public <M> void method(M m){
    System.out.println(m)
}
```

##泛型通配符
**?：代表任意的数据类型**
>泛型的上线限定：?extends E 代表使用的泛型只能是E类型的子类
泛型的下限限定： ? super E代表使用的泛型只能是E类型的父类