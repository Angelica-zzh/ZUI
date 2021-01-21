###Properties
方法
store 把集合中的临时数据持久化写入到硬盘中春初
可以使用Properties中的方法load把硬盘中保存的文件，读取到集合中使用
Properties集合是一个双列集合，key和value默认都是字符串
Object setProperty(String key, String value) 
致电 Hashtable方法 put 。  

String getProperty(String key) 
使用此属性列表中指定的键搜索属性。  

Set<String> stringPropertyNames() 
返回此属性列表中的一组键，其中键及其对应的值为字符串，包括默认属性列表中的不同键，如果尚未从主属性列表中找到相同名称的键 


```java
 public static void main(String[] args) {
        Properties prop = new Properties();
        prop.setProperty("赵丽颖", "168");
        prop.setProperty("古力娜扎", "168");
        prop.setProperty("迪丽热巴", "168");

        Set<String> set = prop.stringPropertyNames();

        for (String s : set) {
            String value = prop.getProperty(s);
            System.out.println(s + "=" + value);

        }

    }
```
void store(OutputStream out, String comments) 
将此属性列表（键和元素对）写入此 Properties表中，以适合于使用 load(InputStream)方法加载到 Properties表中的格式输出流。  
void store(Writer writer, String comments) 
将此属性列表（键和元素对）写入此 Properties表中，以适合使用 load(Reader)方法的格式输出到输出字符流。  
```java
 Properties prop = new Properties();
        prop.setProperty("赵丽颖", "168");
        prop.setProperty("古力娜扎", "168");
        prop.setProperty("迪丽热巴", "168");

        FileWriter fw = new FileWriter("Boon//b.txt");

        prop.store(fw,"save data");

        fw.close();

```



void load(InputStream inStream) 
从输入字节流读取属性列表（键和元素对）。  
void load(Reader reader) 
以简单的线性格式从输入字符流读取属性列表（关键字和元素对）。 

```java
 Properties prop = new Properties();


        FileReader fd = new FileReader("Boon//b.txt");

        prop.load(fd);


        Set<String> set = prop.stringPropertyNames();

        for (String s : set) {
            String value = prop.getProperty(s);
            System.out.println(s + "=" + value);

        }


        fd.close();

```
