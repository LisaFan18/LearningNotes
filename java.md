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

