## Reference
1. [Quora: the best of tutorial of java multithreading](https://www.quora.com/Where-can-I-find-the-best-tutorial-of-Java-multithreading)
  * https://www.javatpoint.com/multithreading-in-java 
  * http://www.tutorialspoint.com/java/java_multithreading.htm 
  * https://docs.oracle.com/javase/tutorial/essential/concurrency/procthread.html

## Q1_进程和线程的区别
1. 背景知识点  
Linux的用户态和内核态是如何进行转换的，系统中断，内核态的多进程是如何通过轻量级线程实现的。把这些概念融入到java 线程相关的题目里
2. 进程和线程的由来
* 串行： 初期的计算机串行执行任务，需要长时间等待用户输入
* 批处理： 预先将用户的指令集中成清单，批量串行处理用户指令， 仍然无法并发执行。
* 并行——进程：
  * 由于cpu的执行速度比IO更快。当CPU执行任务A一半时，需要停下来等待读取数据，此时CPU是闲置的，能否在等待的这段时间让CPU去执行任务B呢？
   为了充分的利用CPU，能否在任务A等待IO读取时，先去执行任务B，当IO读取结束时再回去执行任务A。然而内存里只有一个程序的运行数据？ 
  * 进程： 如何在内存里辨别多个程序的运行数据呢？于是进程就出现了。进程独占内存空间，保存各自运行状态，相互间不干扰且可以互相切换，为并发处理任务提供了可能。
  * 当只有一个CPU时，为什么用户感觉多个任务在同时执行呢？因为CPU分给每个进程的时间片很短，CPU不断的在多个任务间切换，给用户一种多个任务同时执行的“假象”
* 并行 -- 线程
  * 进程解决了OS的并发问题。但用户对实时性提出了更高的要求。把进程再划分让一个线程去执行一个子任务，线程让进程的内部并发成为可能。
  * 进程解决了OS的并发问题。但用户对实时性提出了更高的要求。进程细分为多个子任务，让一个线程去执行一个子任务，线程让进程的内部并发成为可能。
  * 线程： 共享进程的内存资源，相互间切换更快速，支持更细粒度的任务控制，使进程内的子任务得以并发执行
2. 进程和线程的区别
* 进程： 是资源分配的最小单位，是抢占CPU调度的单位。所有进程相关的资源，都被记录在PCB中。
  * a process is an instance of a program in execution 
  * a process is an independent entity to which system resources(CPU and memory) are allowed.
  * each process is excuted in a separate address space. one process cannot access the variables and data structures of another process
* 线程： 是cpu调度的最小单位。线程属于某个进程，共享其资源。被记录在TCB
  * a thread exists within a process and shares the process's resources(heap space)
  * multiple threads within the same process will share the same heap sapce
  * each thread has its own registers and stack,
* 区别
  * 进程可以看成独立应用，而线程不能
  * 进程有独立的地址空间，相互不影响；线程只是进程的不同执行路径
  * 进程的切换比线程的切换开销大，多进程的程序比多线程的程序健壮
3. Java 进程和线程的关系
* java对OS提供的功能进行封装，包括进程和线程
* 运行一个程序会产生一个进程，进程包含一个或多个线程
* 每个进程对应一个jvm实例，多个线程共享jvm里的heap
* 主线程可以创建子线程，原则上要后于子线程完成执行。因此，耗费资源的任务要放在子线程中去完成，以免堵塞main线程的执行。
* java采用单线程编程模型，程序会自动创建主线程
```java
public class CurrentThread {
	public static void main(String[] args) {
    //output: Current Thread:main
		System.out.println("Current Thread:" + Thread.currentThread().getName()); 
	}
}
```

## Q2_ thread的start和run方法的区别
1. run()方法只是只是thread的普通方法的调用，不会创建一个新的进程
2. start()方法会创建一个新的子线程并启动。
