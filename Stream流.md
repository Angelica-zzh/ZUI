##Stream流
JDK1.8之后出现
关注做什么而不是怎么做

Stream<T> filter(Predicate<? super T> predicate) 
返回由与此给定谓词匹配的此流的元素组成的流。  


```java
public class StreamTest {
    public static void main(String[] args) {
        //把集合转换成Stream流
        List<String> list = new ArrayList<>();
        Stream<String> stream1 = list.stream();

        Set<String> set = new HashSet<>();
        Stream<String> stream2 = set.stream();

        //获取键存储到一个Set集合中
        Map<String,String> map = new HashMap<>();
        Set<String> keyset = map.keySet();
        Stream<String> stream3 = keyset.stream();

        //获取值，存储到一个Collection集合中
        Collection<String> values = map.values();
        Stream<String> stream4 = values.stream();

        //获取键值的对应关系
        Set<Map.Entry<String,String>> set1 = map.entrySet();
        Stream<Map.Entry<String, String>> stream5 = set1.stream();

        //把数组转换为Stream流
        Stream<Integer> integerStream = Stream.of(1, 2, 3, 4, 5);

        //Stream的of方法可以获取数据对应的流
        Integer[] arr = {1,2,3,4,5};
        Stream<Integer> arr1 = Stream.of(arr);
        String[] arr2 ={"害","离谱"};
        Stream<String> arr21 = Stream.of(arr2);


    }
}
```


####方法一
forEach
void forEach(Consumer<? super T> action)对此流的每个元素执行操作。 
这是一个terminal operation 。 

这个操作的行为显然是不确定的。 对于并行流管道，此操作不保证遵守流的遇到顺序，因为这样做将牺牲并行性的好处。 对于任何给定的元素，动作可以在图书馆选择的任何时间和任何线索中执行。 如果操作访问共享状态，则负责提供所需的同步。 

```java
   Stream<String> stringStream = Stream.of("张三", "李四", "王五");
        stringStream.forEach(name-> System.out.println(name));
```



Stream流只能使用一次



####方法二
map
<R> Stream<R> map(Function<? super T,? extends R> mapper)返回由给定函数应用于此流的元素的结果组成的流。 
这是一个intermediate operation 。 

```java
  Stream<String> number = Stream.of("1", "2", "3", "4");
        Stream<Integer> Int = number.map((String num)-> Integer.parseInt(num));
        Int.forEach(num-> System.out.println(num));
```


####方法三
count
long count()返回此流中的元素数。 这是一个reduction的特殊情况，相当于： 
   return mapToLong(e -> 1L).sum();  这是一个terminal operation 。 

