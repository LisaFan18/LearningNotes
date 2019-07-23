# 1. JVM
## overview
Can you talk a little about Java?
1. 平台无关性：一次编译，到处运行
2. GC：Java有垃圾回收机制，不需要像C/C++ 那样手动释放堆内存
3. 语言特性: 泛型，反射，lamda
4. 面向对象：encapsulation, polymorphism, inheritance 
5. Build-in Libraries: collection, 并发，网络，IO，异常处理

## Java is Platform independent  
[How is Java is Platform independent](https://www.geeksforgeeks.org/java-platform-independent/)
1. The program is written in JAVA, the **javac** compiles it.  
2. The result of the JAVA compiler is the **.class file or the bytecode** and not the machine native code. Unlike C compiler, C compiler generates an .exe executable code which may be a sequence of machine instructions. And they can be executed by the CPU directly. Thus C/C++ are not platform independent 
3. The bytecode generated is a **non-executable code** and needs an interpreter to execute on a machine. 
4. This interpreter is the **JVM** and thus the Bytecode is executed by the JVM. So Java language is termed as **portability**
5. Java is platform independent but **JVM is platform dependent**. 因此[不同的OS对应不同的jdk](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) 
### how to implement JAVA "compile once, run anywhere"?
1. 为什么JVM不直接将source code解析成machine code去执行？
** 避免不必要的准备工作，如果jvm把 source code 解析成machine code去执行，每次都需要执行各种语法检查，冗余工作
** 兼容性考虑，其他语言也可以解析成byte code，在jvm上执行。例如Ruby, Groovy 等 其他[list of JVM languages](https://en.wikipedia.org/wiki/List_of_JVM_languages)
2. 如何实现
java首先利用命令**javac**把source code 转化为 byte code，再由不同平台的jvm进行解析成machine code。java语言在不同平台上的运行不需要进行重新编译，java 虚拟机通过命令**java**在执行字节码时，把字节码转化为具体平台上的机器指令。
### 如何查看字节码？
**javap** -c class文件

## JVM class loader
1. JVM 是如何加载.class 文件的？ 利用JVM的 class loader模块
### JVM 的 4 大components:  
* class loader：根据特定格式把.class文件加载到内存 . 
* execution enginee：对命令进行解析 .  
* native interface：融合不同语言的原生库为java所用。例如方法 static Class.forName(String className) Returns the Class object associated with the class or interface with the given string name. 就调用了native 方法 . 
* Runtime data area: JVM 内存空间结构模型 .   
### classLoader
1. 类从编译到执行的过程  
* javac 编译器将People.java source code编译为People.class字节码文件；
* classloader 将字节码转换为jvm中的Class<People> 对象；
* JVM 利用Class<People>对象实例化为People对象
2. class loader definition  
它是java的核心组件， 所有的class都是由classloader进行加载的。classloader 负责通过将class文件的二进制数据load进系统，然后交给java 虚拟机进行链接，初始化等操作。
3. types  
 * BoostrapClassLoader: C++编写，加载核心课java.*
 *  ExtClassLoader: java编写，加载扩展库javax.*
 *  AppClassLoader: java编写，加载程序所在目录
 *  自定义ClassLoader:java 编写，定制化加载。通过extends ClassLoader, 自定义findClass(name)和loadClassData(name)两个函数即可
4. practise
```java
  public class MyClassLoader extends ClassLoader {
    private String path;
    private String classLoaderName;

    public MyClassLoader(String path, String classLoaderName) {
        this.path = path;
        this.classLoaderName = classLoaderName;
    }

    //用于寻找类文件
    @Override
    public Class findClass(String name) {
        byte[] b = loadClassData(name);
        return defineClass(name, b, 0, b.length);
    }

    //用于加载类文件: 找到class文件，并输出为byte[]
    private byte[] loadClassData(String name) {
        name = path + name + ".class";
        InputStream in = null;
        ByteArrayOutputStream out = null;
        try {
            in = new FileInputStream(new File(name));
            out = new ByteArrayOutputStream();
            int i = 0;
            while ((i = in.read()) != -1) {
                out.write(i);
            }
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            try {
                out.close();
                in.close();
            } catch (Exception e) {
                e.printStackTrace();
            }
        }
        return out.toByteArray();
    }
```

## Reflection
1. Defintion: 反射机制是在运行时状态中，对于任意一个类，都能够知道这个类的所有属性和方法；对于任意个对象，都能够call它的任意方法和属性。这种动态获取
信息以及动态调用对象方法的功能称为java 语言的反射机制。
2. Practise: 
```java
Class pc = Class.forName("com.java.reflection.People");
People p = (People)pc.newInstance();
System.out.println(p.getName);
// Method sayHi = pc.getDeclaredMethod("sayHi");
Method sayHi = pc.getMethod("sayHi");
sayHi.invoke(p);
Field name = pc.getDeclaredField("name");
name.setAccessible(true);
name.set(p, "John");
```
