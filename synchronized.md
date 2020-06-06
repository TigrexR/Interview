## 进程和线程

### 1.线程和进程的概念、并行和并发的概念
1. 进程（Process）是计算机中的程序关于某数据集合上的一次运行活动，是系统进行资源分配和调度的基本单位，是操作系统结构的基础。在早期面向进程设计的计算机结构中，进程是程序的基本执行实体；在当代面向线程设计的计算机结构中，进程是线程的容器。程序是指令、数据及其组织形式的描述，进程是程序的实体。

2. 线程，有时被称为轻量级进程（Lightweight Process,LWP），是程序执行流的最小单元。线程是程序中一个单一的顺序控制流程。进程内一个相对独立、可调度的执行单元，是系统独立调度和分派CPU的基本单位，也指运行中的程序的调度单位。在单个程序中同时运行多个线程完成不同的工作，称为多线程。

3. 并发（concurrency）：指在同一时刻只能有一条指令执行，但多个进程指令被快速的轮换执行，使得在宏观上具有多个进程同时执行的效果，但在微观上并不是同时执行的，只是把时间分成若干端，使多个进程快速交替的执行。 

4. 并行（parallellism）:指在同一时刻，有多条指令在多个处理器上同时执行 

5. 通过多线程实现并发，并行： 
- java中的Thread类定义了多线程，通过多线程可以实现并发或并行。 
- 在CPU比较繁忙，资源不足的时候（开启了很多进程），操作系统只为一个含有多线程的进程分配仅有的CPU资源，这些线程就会为自己尽量多抢时间片，这就是通过多线程实现并发，线程之间会竞争CPU资源争取执行机会。 
- 在CPU资源比较充足的时候，一个进程内的多线程，可以被分配到不同的CPU资源，这就是通过多线程实现并行。 
- 至于多线程实现的是并发还是并行？上面所说，所写多线程可能被分配到一个CPU内核中执行，也可能被分配到不同CPU执行，分配过程是操作系统所为，不可人为控制。所以，如果有人问我我所写的多线程是并发还是并行的？我会说，都有可能。 
- 不管并发还是并行，都提高了程序对CPU资源的利用率，最大限度地利用CPU资源

### 2创建线程的方式及实现
Java使用Thread类代表线程，所有的线程对象都必须是Thread类或其子类的实例。 
1. 继承Thread类创建线程类 
- 重写run方法。该run（）方法的方法体就代表了线程需要完成的任务。 
- 创建Thread子类的实例。 
- 调用线程对象的start（）方法来启动该线程。

        public class TestCode1 extends Thread
        {
                private int i;
                public void run()
                {
                        for(;i<100;i++)
                        {
                        System.out.println(getName()+" "+i);
                        }
                }


                public static void main(String[] args) 
                {
                        for(int i=0;i<100;i++)
                        {
                        System.out.println(Thread.currentThread().getName()+" "+i);
                        if(i==20){
                                new TestCode1().start();
                                new TestCode1().start();
                        }
                        }
                }
        }

2. 实现Runnable接口创建线程类 
- 定义Runnable的实现类，重写run（）方法。 
- 创建Runnable实现类的实例，并以此作为Thread的target来创建对象，该对象才是真正的线程对象。

        public class TestCode2 implements Runnable
                {
                private int i;
                public void run()
                {
                        for(;i<100;i++)
                        {
                        System.out.println(Thread.currentThread().getName()+" "+i);
                        }
                }


                public static void main(String[] args) 
                {
                        for(int i=0;i<100;i++)
                        {
                        System.out.println(Thread.currentThread().getName()+" "+i);
                        if(i==20){
                                TestCode2 test=new TestCode2();
                                new Thread(test,"新线程1").start();
                                new Thread(test,"新线程2").start();
                        }
                        }
                }
        }

3. 使用Callable和Future创建线程 
- 创建Callable接口的实现类，并实现Call（）方法，该方法将作为线程执行体，且该方法有返回值，再创建Callable实现类的实例。从Java8开始，可以直接使用Lambda表达式创建Callable对象。 
- 使用FutureTask来包装Callable对象，该FutureTask对象封装了该Callable对象的call方法的返回值。 
- 使用FutureTask对象作为Thread对象的target创建并启动新线程。 
- 调用FutureTask对象的get（）方法来获取子线程执行结束后的返回值。

        public class TestCode3 {
                public static void main(String[] args) {
                        TestCode3 test = new TestCode3();
                        FutureTask<Integer> task = new FutureTask<Integer>((Callable<Integer>)()->{
                        int i=0;
                        for(;i<100;i++){
                                System.out.println(Thread.currentThread().getName()+"循环变量i的值："+i);
                        }
                        return i;
                        });
                        for(int i=0;i<100;i++){
                        System.out.println(Thread.currentThread().getName()+"循环变量i的值："+i);
                        if(i==20){
                                new Thread(task,"有返回值的线程").start();
                        }
                        try{
                                System.out.println("子线程的返回值："+task.get());
                        }
                        catch (Exception e) {
                                e.printStackTrace();
                        }
                        }
                }
        }

4. 浅谈三种方式优劣势 
通过继承Thread类或实现Runnable、Callable接口都可以实现多线程，不过实现Runnable接口与实现Callable接口的方式基本相同，只是Callable接口里定义的方法有返回值，可以声明抛出异常而已。因此可以将实现Runnable接口和实现Callable接口归为一种方式。这种方式与继承Thread方式之间的主要差别如下。 
1.采用实现Runnable、Callable接口的方式创建多线程的优缺点： 
优势：（1）线程类只是实现了Runnable接口与Callable接口，还可以继承其他类。 
（2）在这种方式下，多个线程可以共享一个target对象，所以非常适合多个相同线程来处理同一份资源的情况，从而可以将CPU、代码和数据分开，形成清晰的模型，较好地体现了面向对象的思想。 
劣势：编程稍稍复杂，如果需要访问当前线程，则必须使用Thread.currentThread（）方法。 
2.采用继承Thread类的方法创建多线程的优缺点： 
劣势：因为线程类已经继承了Thread类，所以不能再继承其他父类。 
优势：编写简单，如果需要访问当前线程，则无须使用Thread.currentThread（）方法，直接使用this即可获得当前线程。 
5. 总结 
鉴于上面分析，因此一般推荐采用实现Runnable接口、Callable接口的方式来创建多线程。

### 38.说说 CountDownLatch、CyclicBarrier 原理和区别
https://blog.csdn.net/tolcf/article/details/50925145
- 可以观看 https://github.com/TigrexR/JavaBase 中的CyclicBarrierTesth和CountDownTest类\

进程间通信的方式

说说 CountDownLatch、CyclicBarrier 原理和区别

说说 Semaphore 原理

说说 Exchanger 原理

ThreadLocal 原理分析，ThreadLocal为什么会出现OOM，出现的深层次原理

讲讲线程池的实现原理

线程池的几种实现方式

线程的生命周期，状态是如何转移的

可参考：《Java多线程编程核心技术》
## 锁机制

### 1.说说线程安全问题，什么是线程安全，如何保证线程安全
1. 

重入锁的概念，重入锁为什么可以防止死锁

产生死锁的四个条件（互斥、请求与保持、不剥夺、循环等待）

如何检查死锁（通过jConsole检查死锁）

volatile 实现原理（禁止指令重排、刷新内存）

synchronized 实现原理（对象监视器）

synchronized 与 lock 的区别

AQS同步队列

CAS无锁的概念、乐观锁和悲观锁

常见的原子操作类

什么是ABA问题，出现ABA问题JDK是如何解决的

乐观锁的业务场景及实现方式

Java 8并法包下常见的并发类

偏向锁、轻量级锁、重量级锁、自旋锁的概念

可参考：《Java多线程编程核心技术》