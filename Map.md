##Map集合
Map<k,v>
特点：
1.Map集合是一个双列集合，一个元素包含两个值（一个key，一个value)
2.Map集合中的元素key和value的数据类型可以相同，也可以不同
3.Map集合中的元素,key是不允许重复的，value是可以重复的
4.Map集合中的元素，key和value是一一对应的

###HashMap集合
HashMap<K,V> implements Map<k,v>
1.HashMap集合底层是哈希表，查询的速度特别快
JDK1.8之前：数组+单向链表
JDK1.8之后：数组+单向链表/红黑树（链表长度超过8）
2.hashMap集合是一个无序的集合，存储元素和取出元素的顺序可能不一致

###LinkedHashMap集合
才有哈希表+链表结构
有序

###Map的方法
```java
public V put(K key,V value)//把指定的键与指定的值添加到Map集合中
///返回值V：若key不重复，返回的V是null，重复，使用新的value替换map中重复的value,返回被替换的值
public V remove(Object key);//把指定的键所对应的键值对元素在Map中删除，并返回被删除的值
boolean containsKey(Object key)//如果此映射包含指定键的映射，则返回true 。
Set<K> keySet();//返回此地图中包含的键的Set视图。
例：Set<String> set = map.keySet();
```

###Map.Entry<K,V>:在Map接口中有一个内部接口Entry
作用：当Map集合一创建，那么就会在Map集合中创建一个Entry对象，用来记录键和值的关系
```java
 Map<String,Integer> map = new HashMap<>();
     map.put("ab",158);
     map.put("zx",175);
     map.put("zh",178);
     System.out.println(map);


     Set<Map.Entry<String, Integer>> ent = map.entrySet();
     Iterator<Map.Entry<String, Integer>> it = ent.iterator();
     while (it.hasNext()){
         Map.Entry<String, Integer> entry = it.next();
         String key = entry.getKey();
         Integer value = entry.getValue();
         System.out.println(key+"+"+value);
     }
     for(Map.Entry<String,Integer> s :ent){
         String key = s.getKey();
         Integer value = s.getValue();
         System.out.println(key+value);
     }
```
###HashMap的方法
存储自定义类型的键值
key:Person类型
Person类就必须重写hashCode方法和equal方法以保证key唯一


###HashTable
哈希表，双链，同步，单线程 1.0之后
底层是一个哈希表，是一个线程安全的集合，是单线程集合

HashMap:底层是一个哈希表是一个线程不安全的集合，是多线程的集合，速度快

HashMap集合可以存储null值，null键
Hashtable集合，不能存储null值

Hashtable 和Vector集合一样，在jdk1.2版本之后被更先进的集合（HashMap,ArrayList)取代了
Hashtable的子类Properties依然活跃在历史舞台
Properties集合是一个唯一和IO流相结合的集合


###例子：
计算一个字符串中一个字符出现多少次：
```java
Scanner sc = new Scanner(System.in);//Scanner对象
    System.out.println("请输入一个字符");
    String sr = sc.next();

    Map<Character,Integer> map = new HashMap<>();
    //遍历字符串，获取每一个字符
    for(char c:sr.toCharArray()){
        if(map.containsKey(c)){//判断key是否存在
            Integer value = map.get(c);
            value++;
            map.put(c,value);

        }else {
            map.put(c,1);//存入map
        }
    }
    //遍历Map集合，输出结果
    for (Character c:map.keySet()){
        System.out.println(c+"="+map.get(c));

    }
```


###JDK9的新特性：
List接口，Set接口，Map接口：里边增加了一个静态的放大of可以给集合一次性添加多个元素


###自定义异常
java提供的一次行类不够使用，需要自己定义一些异常类
格式：
public class  XXException extends Exception | RuntimeException{
    添加一个空参数的构造方法
    添加一个带异常信息的构造方法
}
注意：
1.自定义异常类一般都是以Exception结尾，说明该类是一个异常类
2.自定义异常类必须继承Exception或者RuntimeException
继承Exception：那么自定义的异常类就是一个编译器异常，如果方法内部抛出了编译期异常，就必须处理这个异常，要么throw，要么try...catch
继承RuntimeException:那么自定义的异常类就是一个运行期异常，无需处理，交给虚拟机JVM处理（中断处理）
```java
public class RegisterException extends Exception{
    //一个无参构造方法
    public RegisterException() {
        super();
    }
    //带异常信息构造方法
    public RegisterException(String message){
        super(message);//错误信息返回父类
    }
    }

```

继承Exception

try...catch也可以用throws
```java
public class DemoRegisterException {
    static String[] usernames = {"张三","李四","王五"};

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.println("请输入姓名");
        String username =sc.next();

        checkName(username);
    }

    public static void checkName(String username) {
        for (String name: usernames){
            if(name.equals(username)){
                try {
                    throw  new RegisterException("该用户名已经被注册");
                } catch (RegisterException e) {
                    e.printStackTrace();
                    return;//结束方法
                }
            }
        }
        System.out.println("恭喜您注册成功");
    }
}
```

继承RuntimeException

交由虚拟机处理
```java
public static void checkName(String username) {
        for (String name: usernames){
            if(name.equals(username)){
               
                    throw  new RegisterException("该用户名已经被注册");
              
                 
            }
        }
        System.out.println("恭喜您注册成功");
    }
```