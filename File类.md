static String pathSeparator 与系统有关的路径分隔符，表示为一个字符串
static char pathSeparatorChar与系统有关的路径分隔符

static String separator 与系统有关的默认名称分隔符，被表示为一个字符串
static char separatorChar 与系统有关的默认名称分隔符

```java
 //路径分隔符 windows:分号 linux:冒号
        String pathSeparator = File.pathSeparator;
        System.out.println(pathSeparator);
        
        //文件名称分隔符 windows:反斜杠\ linux:正斜杠/
        String separator = File.separator;
        System.out.println(separator);
```
File类方法
**获取功能方法**
* public String getAbsolutePath() :返回此File的绝对路径名字符串
* public String getPath():将此File转换为路径名字符串
* public String getName() :返回此File表示的文件或目录的名称
* public long length() :返回此File表示的文件的长度(文件大小)

**构造方法***
Constructor and Description 
File(File parent, String child) 
从父抽象路径名和子路径名字符串创建新的 File实例。  
File(String pathname) 
通过将给定的路径名字符串转换为抽象路径名来创建新的 File实例。  
File(String parent, String child) 
从父路径名字符串和子路径名字符串创建新的 File实例。  
File(URI uri) 
通过将给定的 file: URI转换为抽象路径名来创建新的 File实例。  

**判断功能方法**
 
boolean isDirectory() 
测试此抽象路径名表示的文件是否为目录。  
boolean isFile() 
测试此抽象路径名表示的文件是否为普通文件。  
boolean exists() 
测试此抽象路径名表示的文件或目录是否存在。  

**删除功能方法**
boolean createNewFile() 
当且仅当具有该名称的文件尚不存在时，原子地创建一个由该抽象路径名命名的新的空文件。
文件存在返回false  
boolean delete() 
删除由此抽象路径名表示的文件或目录。 
boolean mkdir() 
创建由此抽象路径名命名的目录。  
boolean mkdirs() 
创建由此抽象路径名命名的目录，包括任何必需但不存在的父目录。  

**目录的遍历功能**
String[] list() 
返回一个字符串数组，命名由此抽象路径名表示的目录中的文件和目录。  
String[] list(FilenameFilter filter) 
返回一个字符串数组，命名由此抽象路径名表示的目录中满足指定过滤器的文件和目录。  
File[] listFiles() 
返回一个抽象路径名数组，表示由该抽象路径名表示的目录中的文件。  
File[] listFiles(FileFilter filter) 
返回一个抽象路径名数组，表示由此抽象路径名表示的满足指定过滤器的目录中的文件和目录。  
File[] listFiles(FilenameFilter filter) 
返回一个抽象路径名数组，表示由此抽象路径名表示的满足指定过滤器的目录中的文件和目录。  
