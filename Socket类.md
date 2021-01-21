##Socket（客户端）
构造方法
Socket(InetAddress address, int port) 
创建流套接字并将其连接到指定IP地址的指定端口号。 

成员方法
OutputStream getOutputStream() 
返回此套接字的输出流。  
InputStream getInputStream() 
返回此套接字的输入流。  
void close() 
关闭此套接字 




##ServerSocket(服务器)
服务器端必须知道是那个客户端请求的服务器
构造方法
ServerSocket(int port) 
创建绑定到指定端口的服务器套接字。 

成员方法
Socket accept() 
侦听要连接到此套接字并接受它。 
客户端程序
```java
public class TCPClient {
    public static void main(String[] args) throws IOException {
        Socket socket = new Socket("127.0.0.1",8888);
        OutputStream opt = socket.getOutputStream();
        opt.write("你好服务器".getBytes());

        InputStream ipt = socket.getInputStream();

        byte[] bytes = new byte[1024];
        int len = ipt.read(bytes);
        System.out.println(new String(bytes,0,len));

        ipt.close();
        opt.close();
    }
}
```


服务器程序
```java
public class TCPServer {
    public static void main(String[] args) throws IOException {
        ServerSocket server = new ServerSocket(8888);

        Socket socket = server.accept();

        InputStream is = socket.getInputStream();

        byte[] bytes = new byte[1024];

        int len = is.read(bytes);

        System.out.println(new String(bytes,0,len));
        OutputStream opt = socket.getOutputStream();
        opt.write("收到谢谢".getBytes());

        socket.close();
        server.close();
    }
}
```