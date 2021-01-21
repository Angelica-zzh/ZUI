###Lambda表达式
使用lambda表达式简化匿名内部类
```java
public class Demo06InvokeCook {
    public static void main(String[] args) {
        invokeCooke(new Cook() {
            @Override
            public void makeFood() {
                System.out.println("starting eat");
            }
        });
        invokeCooke(() ->{
                System.out.println("starting eat");
        });
    }
    public static void invokeCooke(Cook cook){
        cook.makeFood();
    }
}
```


```java
 public static void main(String[] args) {
        Person[] arr = {
                new Person("刘艳",19),
                new Person("迪丽热",39),
                new Person("古力娜扎",34)
        };

        Arrays.sort(arr, new Comparator<Person>() {
            @Override
            public int compare(Person o1, Person o2) {
                return o1.getAge()-o2.getAge();
            }
        });
        //用lambda格式来简化匿名内部类
        Arrays.sort(arr,(Person a,Person b)->{
            return a.getAge()-b.getAge();
        });

        for (Person p : arr) {
            System.out.println(p);

        }

    }

}
```
###省略规则
在Lambda标准格式的基础上，使用省略写法的规则为：
1.小括号内参数的类型可以省略
2.如果小括号内有且仅有一个参数，则小括号可以省略；
3.如果大括号内有且仅有一个语句，则无论是否有返回值，都可以省略大括号，return关键字及语句分号。
注意：要省略{}，return,分号必须一起省略

```java
//使用匿名内部类的方式实现多线程
        new Thread(new Runnable() {
            @Override
            public void run() {
                System.out.println("新线程创建");
            }
        }).start();
        //使用Lambda表达式，实现多线程
        new Thread(()->{
            System.out.println("新线程创建");
        });

        //简化省略Lambda表达式，实现多线程
        new Thread(()-> System.out.println("新线程创建")).start();

    }
```

###Lambda使用前提
1.使用Lambda必须具有接口，且要求接口中有且仅有一个抽象方法。
2.使用Lambda必须具有上下文推断
也就是方法的参数或者局部变量类型必须为Lambda对应的接口类型
备注：有且仅有一个抽象方法的接口，称为“函数式接口”



####lambda的引用
1.通过对象名引用
2.通过类引用静态成员方法
3.通过super引用父类的成员方法
4.通过this引用本类成员方法