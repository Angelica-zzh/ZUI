###Junit单元测试

Junit属于白盒测试
*步骤：
1.定义一个测试类
建议：测试类名：被测试的类名Test
报名：xxxx.xxx.xx.test
2.定义测试方法：可以独立运行
3.给方法加@Test
4.导入Junit依赖


判定结果：
* 红色：失败
* 绿色：成功
* 易班我们会使用断言操作来处理结果
    *Assert.assertEquals(期望的结果，运算的结果) 

```java
//初始化方法,用于资源的申请，所有测试方法在执行之前都会执行该方法
    @Before
    public void init(){
        System.out.println("init...");
    }

    //释放资源的方法，在所有测试方法执行完之后都会自动执行该方法
    @After
    public void close(){
        System.out.println("close"
        );
    }

    //进行测试
    @Test
    public void testSub(){
        Calculate c =new Calculate();
        int result = c.sub(2,3);
        //断言，断言结果为多少
        Assert.assertEquals(-1,result);

    }

    @Test
    public  void testAdd(){
        Calculate c = new Calculate();
        int result = c.add(2,3);
        Assert.assertEquals(5,result);
    }


}
```
##反射：框架设计的灵魂
JAVA反射机制是在运行状态中，对于任意一个类，都能够知道这个类的所有属性和方法；对于任意一个对象，都能够调用它的任意方法和属性；这种动态获取信息以及动态调用对象方法的功能称为java语言的反射机制。


##反射——获取字节码Class对象的三种方法
    getFields
    public Field[] getFields()
                    throws SecurityException返回包含一个数组Field对象反射由此表示的类或接口的所有可访问的公共字段类对象。 
    如果此类对象表示没有无法访问的公共字段的类或接口，则此方法返回长度为0的数组。 

    如果这个类对象表示一个类，那么这个方法返回该类及其所有超类的公共字段。 

    如果此类对象表示一个接口，则该方法返回接口及其所有超级接口的字段。 

    如果这个类对象表示一个数组类型，一个基本类型或者void，那么这个方法返回一个长度为0的数组。 

    返回的数组中的元素不会被排序，并且不是以任何特定的顺序。 

    结果 
    表示公共字段的 Field对象的数组 
    异常 


    ```java
    public class ReflectDemo01 {
    public static void main(String[] args) throws NoSuchFieldException, IllegalAccessException {
        //获取Person的Class对象
        Class personClass = Person.class;
        //Field[]  getFields
        Field[] fields = personClass.getFields();
        for (Field field : fields) {
            System.out.println(field);
        }

        Field a = personClass.getField("a");
        //获取成员变量a的值,此时的a必须为public
        Person p =new Person();
        Object value = a.get(p);
        System.out.println(value);

        //设置a的值
        a.set(p,"张三");
        System.out.println(p);
         Field[] declare= personClass.getDeclaredFields();
        for (Field field : declare) {
            System.out.println(field);
        }


        Field b = personClass.getDeclaredField("b");
        //忽略访问权限修饰符的安全检查
        b.setAccessible(true);//暴力反射
        Object value2 = b.get(p);
        System.out.println(value2);

        //设置b的值
        b.set(p,"李四");
        System.out.println(p);


    }
}
```

##Constructor提供了一个类的单个构造函数的信息和访问。
* 方法
Constructor<T> getConstructor(类<?>... parameterTypes) 
返回一个 Constructor对象，该对象反映 Constructor对象表示的类的指定的公共 类函数。  



T newInstance(Object... initargs) 
使用此 Constructor对象表示的构造函数，使用指定的初始化参数来创建和初始化构造函数的声明类的新实例。  

```java
public class ReflectDemo03 {
    public static void main(String[] args) throws Exception {
        //获取Person的Class对象
        Class personClass = Person.class;
        //Constructor<T> getConstructor(类<?>... parameterTypes)
        //返回一个 Constructor对象，该对象反映 Constructor对象表示的类的指定的公共 类函数。
        Constructor constructor = personClass.getConstructor(String.class,int.class);
        System.out.println(constructor);
        //创建对象
        Object person = constructor.newInstance("李四",22);//newInstance方法
        System.out.println(person);
    }
}
```

##方法 getMethod(String name, 类<?>... parameterTypes) 
返回一个 方法对象，它反映此表示的类或接口的指定公共成员方法 类对象。  
方法[] getMethods() 
返回包含一个数组 方法对象反射由此表示的类或接口的所有公共方法 类对象，包括那些由类或接口和那些从超类和超接口继承的声明。  


Object invoke(Object obj, Object... args) 
在具有指定参数的 方法对象上调用此 方法对象表示的底层方法。 

##写一个框架
1.配置文件 properties
2.反射






##注解
Java中常见的基本注解
* @Override：用于标识方法，标识该方法属于重写父类的方法
* @Deprecated：用于标识方法或类，标识该类或方法已过时，建议不要使用
* @SuppressWarnnings:用于有选择的关闭编译器对类、方法、成员变量、变量初始化的警告
一般传递参数（“all”)


*自定义注解
*格式：
   元注解
   public @interface 注解名称{}
*本质：注解本质上就是一个接口，该接口默认继承Annotation接口

*属性：接口中可以定义的成员方法
* 要求：
1.属性的返回值类型
* 基本数据类型
* String
* 枚举
* 注解
* 以上类型的数据
2.定义了属性在使用时需要给属性赋值
1.在使用属性的时候可以使用default关键字给属性默认初始化值
2.如果只有一个属性需要赋值，并且属性的名称是value，则value可以省略，直接定义值即可

* 元注解：用于描述注解的注解
* @Target:描述注解能够作用的位置
* ElementType取值：
    * TYPE：可以作用在类上
    * METHOD:可以作用于方法上
    * FIELD:可以作用于成员变量上
@Retention:描述注解被保留的阶段
 * @Retention(RetentionPolicy.RUNTIME):当前背描述的注解，会保留到class字节码文件中，并被JVM读到
 * @Document:描述注解是否被抽取到api文档中
 * @Inherited: 描述注解是否被子类继承


 * 解析注解
 ```java
 //解析注解
        //1.1获取该类字节码文件对象
        Class<ReflectTest> reflectTestClass = ReflectTest.class;
        //获取上边的注解对象
        RenotationTest annotation = reflectTestClass.getAnnotation(RenotationTest.class);

        //2.获取配置文件中定义的数据
        String className = annotation.className();
        String method = annotation.methodName();

        //加载该类进内存
        Class<?> cls = Class.forName(className);
        //创建方法
        Object o = cls.newInstance();
        //获取方法对象
        Method method1 = cls.getMethod(method,String.class);
        //执行方法
        method1.invoke(o,"hello,gonna eat");

    }


}
```





