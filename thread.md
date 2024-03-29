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
**1. thread的start和run方法的区别**
* run()方法只是thread的普通方法的调用，不会创建一个新的进程. Thread.currentThread().getName() return "main"
* start()方法会创建一个新的子线程并启动。 Thread.currentThread().getName() return "Thread - 0"
```java

```
**2. how does start() method work?**
* java.lang.Thread.start() -> native start0() -> JVM_StartThread -> thread_entry -> run()
* native方法是外部非java的源码，在[openjdk可以查看对应source code](https://hg.openjdk.java.net/jdk8u/jdk8u/jdk/file/3ef3348195ff/src/share/native/java/lang/Thread.c)
```java
// Thread.c
static JNINativeMethod methods[] = {
    {"start0",           "()V",        (void *)&JVM_StartThread},
    ...
};
// jvm.cpp
JVM_ENTRY(void, JVM_StartThread(JNIEnv* env, jobject jthread)){
...
native_thread = new JavaThread(&thread_entry, sz);
...}
// thread_entry: 会new一个thread，用这个thread去call run方法
static void thread_entry(JavaThread* thread, TRAPS) {
  ...
  JavaCalls::call_virtual(...
                          vmSymbols::run_method_name(),
                         ..);
}
```
**3. Runnable 和 Thread是什么关系**
* Thread是实现了Runnable接口的类，使得run支持多线程
* java 类的单一继承原则，推荐多使用Runnable接口

**4. run()方法如何传参？**    
跟thread相关的业务逻辑需要放在run方法里。public void run(){...} 通过下面的方法给run方法传参：
* 构造函数传参
* 成员变量传参(set/get method)
* 回调函数传参

**5. run()方法如何得到返回值？**
有的程序的执行依赖于子任务的返回值。如何实现处理线程的返回值？实现子线程返回值的方法有：
* 主线程循环等待法，直到子线程结束. 优点：实现简单，缺点：如果等待的成员变量很多，代码就会臃肿。
* use Thread.join()方法，堵塞当前thread直到子thread处理完毕。优点：实现起来更简单，可以比主线程等待法更精准的控制；缺点：无法实现更精准的依赖关系，例如当无法实现：thread1执行到一半时，执行thread2.
* 通过[Callable接口](https://docs.oracle.com/javase/8/docs/api/index.html?java/util/concurrent/Callable.html)实现：
   * future task: 实现了Callable接口的任务，执行结束后可以得到一个future的对象。在该对象上调用get方法就可以得到该任务返回的object。

```java
   public class MyCallable implements Callable<String>{

	@Override
	public String call() throws Exception {
		String value = "test Callable";
		System.out.println("ready to work: ");
		Thread.currentThread().sleep(5000);
		System.out.println("work is done ");
		return value;
	}

  }
   public class FutureTaskDemo {
	public static void main(String[] args) throws InterruptedException, ExecutionException {
		MyCallable myCallable = new MyCallable();
		FutureTask<String> futureTask = new FutureTask<>(myCallable);
		new Thread(futureTask).start();
		if(!futureTask.isDone()) {
			System.out.println("Please wait: tasks haven't finished");
		}
		
		System.out.println("by futureTask.get(), value = " + futureTask.get());
	}
    }
```
   * thread pool: 优点：可以提交多个实现Callable的类，让threadpool同时执行多个任务。方便对实现Callable的类做统一的管理
   
   ```java
   public class ThreadPoolDemo {
	public static void main(String[] args) {
		ExecutorService threadPool = Executors.newCachedThreadPool();
		Future<String> futureTask = threadPool.submit(new MyCallable());
		
		if(!futureTask.isDone()) {
			System.out.println("Please wait: tasks haven't finished");
		}
		
		try {
			System.out.println("by futureTask.get(), value = " + futureTask.get());
		} catch (InterruptedException e) {
			e.printStackTrace();
		} catch (ExecutionException e) {
			e.printStackTrace();
		} finally {
			threadPool.shutdown();
		}
	}
  }
 ```

## Q3 sleep 和 wait的区别
**1. Life cycle of a Thread (states)**  
A thread can be in one of [five states](https://www.javatpoint.com/life-cycle-of-a-thread): [new](http://www.tutorialspoint.com/java/java_multithreading.htm), runnable, running, waiting, dead. 

**2. sleep 和 wait的区别**
* sleep()是[Thread类的方法](https://docs.oracle.com/javase/7/docs/api/java/lang/Thread.html)   
**public static native void sleep(long timeout)** Causes the currently executing thread to sleep (temporarily cease execution) for the specified number of milliseconds
* wait() 是[Object类的方法](https://docs.oracle.com/javase/7/docs/api/java/lang/Object.html).   
**public final native void wait(long timeout)** Causes the current thread to wait until another thread invokes the notify() method or the notifyAll() method for this object.
* sleep 可以在任何地方使用。wait只能在sychronized方法或块里使用
* Thread.sleep() 只会让出CPU，不会改变lock的行为；object.wait()不仅让出CPU，还会释放已经占有的资源同步锁。




