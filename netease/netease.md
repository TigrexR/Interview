### 1、Java基础、多线程、线程池、JVM
1. java数据类型
   - 基本数据类型: boolean，char，byte，short，int，long，float，double
   - 封装类类型：Boolean，Character，Byte，Short，Integer，Long，Float，Double
   - Object
      - == 比较的是变量(栈)内存中存放的对象的(堆)内存地址，用来判断两个对象的地址是否相同，即是否是指相同一个对象。比较的是真正意义上的指针操作。equals用来比较的是两个对象的内容是否相等，由于所有的类都是继承自java.lang.Object类的，所以适用于所有对象，如果没有对该方法进行覆盖的话，调用的仍然是Object类中的方法，而Object中的equals方法返回的却是==的判断。
      - hashCode()方法和equal()方法的作用其实一样，在Java里都是用来对比两个对象是否相等一致，那么equal()既然已经能实现对比的功能了，为什么还要hashCode()呢？因为重写的equal（）里一般比较的比较全面比较复杂，这样效率就比较低，而利用hashCode()进行对比，则只要生成一个hash值进行比较就可以了，效率很高，那么hashCode()既然效率这么高为什么还要equal()呢？因为hashCode()并不是完全可靠，有时候不同的对象他们生成的hashcode也会一样（生成hash值得公式可能存在的问题），所以hashCode()只能说是大部分时候可靠，并不是绝对可靠，所以我们可以得出：
      - equal()相等的两个对象他们的hashCode()肯定相等，也就是用equal()对比是绝对可靠的。
      - hashCode()相等的两个对象他们的equal()不一定相等，也就是hashCode()不是绝对可靠的。
      - 所有对于需要大量并且快速的对比的话如果都用equal()去做显然效率太低，所以解决方式是，每当需要对比的时候，首先用hashCode()去对比，如果hashCode()不一样，则表示这两个对象肯定不相等（也就是不必再用equal()去再对比了）,如果hashCode()相同，此时再对比他们的equal()，如果equal()也相同，则表示这两个对象是真的相同了，这样既能大大提高了效率也保证了对比的绝对正确性！
   - Integer
      - 答案： Integer类型的赋予int值时，会调用Integer的valueOf方法，然后valueOf方法在赋值的时候会判断int值是否在-128到127之间，如果是，那么会将这个Integer对象存到静态常量池中cache数组，重复利用，如果不是在这个范围内，那么会新建一个Integer对象并返回
      - int与Integer的基本使用对比
         - Integer是int的包装类；int是基本数据类型
         - Integer变量必须实例化后才能使用；int变量不需要
         - Integer实际是对象的引用，指向此new的Integer对象；int是直接存储数据值 
         - Integer的默认值是null；int的默认值是0
      - int与Integer的深入对比
         - 由于Integer变量实际上是对一个Integer对象的引用，所以两个通过new生成的Integer变量永远是不相等的（因为new生成的是两个对象，其内存地址不同）
         - Integer变量和int变量比较时，只要两个变量的值是向等的，则结果为true（因为包装类Integer和基本数据类型int比较时，java会自动拆包装为int，然后进行比较，实际上就变为两个int变量的比较）
         - 非new生成的Integer变量和new Integer()生成的变量比较时，结果为false。因为非new生成的Integer变量指向的是静态常量池中cache数组中存储的指向了堆中的Integer对象，而new Integer()生成的变量指向堆中新建的对象，两者在内存中的对象引用（地址）不同。
         - 对于两个非new生成的Integer对象，进行比较时，如果两个变量的值在区间-128到127之间，则比较结果为true，如果两个变量的值不在此区间，则比较结果为false；原因： java在编译Integer i = 100 ;时，会翻译成为Integer i = Integer.valueOf(100)。而java API中对Integer类型的valueOf的定义如下，对于-128到127之间的数，会进行缓存，Integer i = 127时，会将127这个Integer对象进行缓存，下次再写Integer j = 127时，就会直接从缓存中取，就不会new了
      - https://blog.csdn.net/chenliguan/article/details/53888018
   - String、StringBuilder、StringBuffer
      - String 存在两种创建方式，创建之后对象的内存地址不同
        ```
        String x = new String("123");//存储在堆中
        String y = new String("123");//存储在堆中
        String z = "123";//存储在常量池，常量池也存在堆中
        System.out.println(System.identityHashCode(x));
        System.out.println(System.identityHashCode(y));
        System.out.println(System.identityHashCode(z));
        System.out.println(System.identityHashCode(x.intern()));
        System.out.println(System.identityHashCode(y.intern()));
        System.out.println(System.identityHashCode(z.intern()));
        当通过new String() 创建的时候，还会去判断内容是否在常量池中，如果不存在，还会在常量池中创建一个常量字符串对象，然后这个新建的String()对象引用这个常量字符串对象的地址
        ```
      - 首先说运行速度，或者说是执行速度，在这方面运行速度快慢为：StringBuilder > StringBuffer > String
      - String为字符串常量，而StringBuilder和StringBuffer均为字符串变量，即String对象一旦创建之后该对象是不可更改的，但后两者的对象是变量，是可以更改的
      - 再来说线程安全：在线程安全上，StringBuilder是线程不安全的，而StringBuffer是线程安全的。如果一个StringBuffer对象在字符串缓冲区被多个线程使用时，StringBuffer中很多方法可以带有synchronized关键字，所以可以保证线程是安全的，但StringBuilder的方法则没有该关键字，所以不能保证线程安全，有可能会出现一些错误的操作。所以如果要进行的操作是多线程的，那么就要使用StringBuffer，但是在单线程的情况下，还是建议使用速度比较快的StringBuilder。
   - Collection、List、Set
      - 存储对象可以考虑：①数组 ②集合
      - 都继承于Collection；List接口：存储有序的，可以重复的元素；Set接口：存储无序的，不可重复的元素
      - List的实现：ArrayList（主要的实现类）、LinkedList（对于频繁的插入、删除操作）、Vector（古老的实现类、线程安全的）
      - Set的实现：HashSet、LinkedHashSet、TreeSet
        ```
        Set接口有两个子类：HashSet和TreeSet 。 
        |- HashSet 
        |- 特点：在不存在重复元素的基础上，还可以进行高速的存取元素。 
        |- 要求：需要为您的类重写hashCode()和equals()方法。 
        |- TreeSet 
        |- 特点：在不存在重复元素的基础上，还可以将元素自动排序。 
        |- 要求：需要为您的类实现Comparable接口，并重写compareTo方法。 
        |- 重写compareTo() 可以同时完成两份工作  排序和消除重复。
        ```
   - Map
      - HashMap、LinkedHashMap、TreeMap、Hashtable(子类：Properties)
      - 并发下有ConcurrentHashMap
2. 抽象类和接口
    |参数|抽象类|接口|
    |:----    |:---|:----- |
    |默认的方法实现 |它可以有默认的方法实现  |接口完全是抽象的。它根本不存在方法的实现 |
    |实现 |子类使用extends关键字来继承抽象类。如果子类不是抽象类的话，它需要提供抽象类中所有声明的方法的实现。  |子类使用关键字implements来实现接口。它需要提供接口中所有声明的方法的实现 | 
    |构造器  |抽象类可以有构造器  |接口不能有构造器
    |与正常Java类的区别   |除了你不能实例化抽象类之外，它和普通Java类没有任何区别   |接口是完全不同的类型|
    |访问修饰符   |抽象方法可以有public、protected和default这些修饰符  |接口方法默认修饰符是public。你不可以使用其它修饰符。|
    |main方法  |抽象方法可以有main方法并且我们可以运行它 |接口没有main方法，因此我们不能运行它。|
    |多继承  |抽象方法可以继承一个类和实现多个接口  |接口只可以继承一个或多个其它接口|
    |速度   |它比接口速度要快   |接口是稍微有点慢的，因为它需要时间去寻找在类中实现的方法。|
    |添加新方法   |如果你往抽象类中添加新的方法，你可以给它提供默认的实现。因此你不需要改变你现在的代码。 |如果你往接口中添加方法，那么你必须改变实现该接口的类。|
3. 关键字
   - final、finally、finalize的区别
      - final修饰符（关键字）。被final修饰的类，就意味着不能再派生出新的子类，不能作为父类而被子类继承。因此一个类不能既被abstract声明，又被final声明。将变量或方法声明为final，可以保证他们在使用的过程中不被修改。被声明为final的变量必须在声明时给出变量的初始值，而在以后的引用中只能读取。被final声明的方法也同样只能使用，即不能方法重写。
      - finally是在异常处理时提供finally块来执行任何清除操作。不管有没有异常被抛出、捕获，finally块都会被执行。try块中的内容是在无异常时执行到结束。catch块中的内容，是在try块内容发生catch所声明的异常时，跳转到catch块中执行。finally块则是无论异常是否发生，都会执行finally块的内容，所以在代码逻辑中有需要无论发生什么都必须执行的代码，就可以放在finally块中。
      - finalize是方法名。java技术允许使用finalize（）方法在垃圾收集器将对象从内存中清除出去之前做必要的清理工作。这个方法是由垃圾收集器在确定这个对象没有被引用时对这个对象调用的。它是在object类中定义的，因此所有的类都继承了它。子类覆盖finalize（）方法以整理系统资源或者被执行其他清理工作。finalize（）方法是在垃圾收集器删除对象之前对这个对象调用的。 
   - 重载和重写的区别
     - 方法重写(overriding)：
        1. 也叫子类的方法覆盖父类的方法，要求返回值、方法名和参数都相同。
        2. 子类抛出的异常不能超过父类相应方法抛出的异常。(子类异常不能超出父类异常)
        3. 子类方法的的访问级别不能低于父类相应方法的访问级别(子类访问级别不能低于父类访问级别)
     - 方法重载(overloading):重载是在同一个类中的两个或两个以上的方法，拥有相同的方法名，但是参数却不相同，方法体也不相同，最常见的重载的例子就是类的构造函数。
4. 反射、动态代理
   - 反射
      - 用途
        ```
        1. 在运行时判断任意一个对象所属的类
        2. 在运行时构造任意一个类的对象
        3. 在运行时判断任意一个类所具有的成员变量和方法（通过反射设置可以调用 private）
        4. 在运行时调用人一个对象的方法
        ```
   - 静态代理：静态代理就是在程序运行之前，代理类字节码.class就已编译好，通常一个静态代理类也只代理一个目标类，代理类和目标类都实现相同的接口。
   - jdk动态代理
   - cglib动态代理
5. 多线程、线程池
   - 多线程基础知识
      - 线程概念：是一个正在运行的函数
      - 线程实现：继承Thread、实现Runnable接口、实现Callable接口
      - 线程状态
        - NEW：初始状态，线程被构建，但是还没有调用 start()方法
        - RUNNABLE：可运行状态，可运行状态可以包括：运行中状态和就绪状态
        - BLOCKED：阻塞状态，处于这个状态的线程需要等待其他线程释放锁或者等待进入synchronized
        - WAITING：表示等待状态，处于该状态的线程需要等待其他线程对其进行通知或中断等操作，进而进入下一个状态
        - TIME_WAITING：超时等待状态。可以在一定的时间自行返回
        - TERMINATED：终止状态，当前线程执行完毕
      - 线程对象都存在wait、notify、synchronized同步方法，并且每个对象都存在monitor，用于监控对象，wait、notify必须存在于synchronized代码块中
      - volatile
        - 被volatile修饰的变量，每一次处理的时候，都会将main memory（主存）中的值load到working memory（线程栈）中，然后修改，然后将自身线程栈的变量再同步会主存中，每次变量操作都激发一次load and save
        - volatile可以保证线程可见性，并能防止指令重排，但是不能保证变量操作原子性
      - 多线程相关类
        - 原子操作类：AtomicBoolean、AtomicInteger、AtomicLong、AtomicDouble、AtomicIntegerArray、AtomicLongArray、AtomicReferenceArray、AtomicReference、AtomicReferenceFieldUpdater、AtomicMarkableReference、AtomicIntegerFieldUpdater、AtomicLongFileUpdater、AtomicStampedReference，这些原子操作类都基于Unsafe类中的CAS保证数据变更的原子性
        - 容器类
          - ConcurrentHashMap
          - Collections的并发包装方法
          - Queue
   - 线程池种类
     - jdk基本线程池相关接口和类
       - 接口：Executor、ExecutorService、ScheduledExecutorService
       - 抽象类：AbstractExecutorService，实现类：ForkJoinPool、ThreadPoolExecutor、ScheduledThreadPoolExecutor，工具类：Executors
     - spring线程池相关接口类
       - 接口：TaskExecutor、AsyncTaskExecutor、AsyncListenableTaskExecutor、SchedulingTaskExecutor
       - 实现类：ThreadPoolTaskExecutor
        ```
        corePoolSize：线程池维护线程最小的数量，默认为1
        maxPoolSize：线程池维护线程最大数量，默认为Integer.MAX_VALUE
        keepAliveSeconds：(maxPoolSize-corePoolSize)部分线程空闲最大存活时间，默认存活时间是60s
        queueCapacity：阻塞任务队列的大小，默认为Integer.MAX_VALUE，默认使用LinkedBlockingQueue
        allowCoreThreadTimeOut：设置为true的话，keepAliveSeconds参数设置的有效时间对corePoolSize线程也有效，默认是flase
        threadFactory：：用于设置创建线程的工厂，可以通过线程工厂给每个创建出来的线程设置更有意义的名字。使用开源框架guava提供的ThreadFactoryBuilder可以快速给线程池里的线程设置有意义的名字
        rejectedExecutionHandler：拒绝策略，当队列workQueue和线程池maxPoolSize都满了，说明线程池处于饱和状态，那么必须采取一种策略处理提交的新任务。这个策略默认情况下是AbortPolicy，表示无法处理新任务时抛出异常，有以下四种策略，当然也可以根据实际业务需求类实现RejectedExecutionHandler接口实现自己的处理策略
          ①AbortPolicy：丢弃任务，并且抛出RejectedExecutionException异常
          ②DiscardPolicy：丢弃任务，不处理，不抛出异常
          ③CallerRunsPolicy：只用调用者所在线程来运行任务
          ③DiscardOldestPolicy：丢弃队列里最近的一个任务，并执行当前任务，并且重复该操作
        ```
6. IO、BIO、NIO、AIO、Netty使用
7. JVM
   - 分区
     - 程序计数器：用于记录下一条要执行的指令，每个线程都有自己的程序计数器，配合线程栈用于在线程调度时的线程上下文切换。执行本地方法时程序计数器中没有值或为undefined
     - 虚拟机方法栈：Java的栈，每个线程有一个线程调用栈，栈的元素是栈帧。栈帧包括：局部变量表、操作数栈、指向堆中对象的引用、返回地址、附加信息。每个方法调用时，回向当前指向的线程栈顶部压入一个栈帧，栈帧的大小是固定的，虚拟机通过解析.class文件可以得知
     - 本地方法栈：native方法调用时的方法调用栈，存储本地栈帧
     - 堆：堆是所有Java线程共享的一个内存区域，用于分配对象
        - jdk8之前HotSpot分为新生代、老年代、永久代, 永久代的一部分就是方法区的实现，占用一部分堆内存，永久代不参与垃圾回收
        - jdk8之后HotSpot分为新生代（Eden+From Survivor+To Survivor）、老年代（OldGen），堆中会存字符串常量池、静态变量
     - 方法区：存储类的信息（类名、方法信息、字段信息）、静态变量、常量池
        - jdk8之后方法区由元空间(Metaspace)代替，存储在本地内存，不在虚拟机中，存储类的信息（类名、方法信息、字段信息）、常量池（包括常量和运行时常量池）

### 2、Tomcat、Spring全家桶、Mybtais
1. tomcat
2. spring
   - DI：依赖注入，通过反射将属性和依赖对象注入到一个对象中
   - IOC：控制反转，将对象的加载、连接（验证、准备、解析）、初始化、卸载托管给spring的ioc容器管理（bean工厂），通过di完成类的加载、连接、初始化，通过动态代理对类的方法进行增强
   - BeanFactory和ApplicationContex：BeanFactory 可以理解为含有 bean 集合的工厂类，BeanFactory 包含了种 bean 的定义，以便在接收到客户端请求时将对应的 bean 实例化。BeanFactory 还能在实例化对象的时生成协作类之间的关系。此举将 bean 自身与 bean 客户端的配置中解放出来。BeanFactory 还包含 了 bean 生命周期的控制，调用客户端的初始化方法（initialization methods）和销毁方法（destruction methods）。而ApplicationContex是对BeanFactory的增强。
      ```
      增强点
      提供了支持国际化的文本消息
      统一的资源文件读取方式
      已在监听器中注册的 bean 的事件
      ```
   - Bean的生命周期
     1. Spring对Bean进行实例化
     2. Spring将值和Bean的引用注入进Bean对应的属性中
        - 如果Bean实现了BeanNameAware接口，Spring将Bean的ID传递给setBeanName()方法（实现BeanNameAware清主要是为了通过Bean的引用来获得Bean的ID，一般业务中是很少有用到Bean的ID的）
        - .如果Bean实现了BeanFactoryAware接口，Spring将调用setBeanFactory(BeanFactory bf)方法并把BeanFactory容器实例作为参数传入。（实现BeanFactoryAware 主要目的是为了获取Spring容器，如Bean通过Spring容器发布事件等）
        - 如果Bean实现了ApplicationContextAware接口，Spring容器将调用setApplicationContext(ApplicationContext ctx)方法，把y应用上下文作为参数传入。(作用与BeanFactory类似都是为了获取Spring容器，不同的是Spring容器在调用setApplicationContext方法时会把它自己作为setApplicationContext 的参数传入，而Spring容器在调用setBeanDactory前需要程序员自己指定（注入）setBeanDactory里的参数BeanFactory )
     3. 如果Bean实现了BeanPostProcessor接口，Spring将调用它们的postProcessBeforeInitialization（预初始化）方法。（作用是在Bean实例创建成功后对进行增强处理，如对Bean进行修改，增加某个功能）
     4. 如果Bean实现了InitializingBean接口，Spring将调用它们的afterPropertiesSet方法，作用与在配置文件中对Bean使用init-method声明初始化的作用一样，都是在Bean的全部属性设置成功后执行的初始化方法
     5. 如果Bean实现了BeanPostProcessor接口，Spring将调用它们的postProcessAfterInitialization（后初始化）方法（作用与3的一样，只不过3是在Bean初始化前执行的，而这个是在Bean初始化后执行的，时机不同 )
     6. 经过以上的工作后，Bean将一直驻留在应用上下文中给应用使用，直到应用上下文被销毁
     7. 如果Bean实现了DisposableBean接口，Spring将调用它的destory方法，作用与在配置文件中对Bean使用destory-method属性的作用一样，都是在Bean实例销毁前执行的方法
   - Bean的作用域
     - singleton：这种 bean 范围是默认的，这种范围确保不管接受到多少个请求，每个容器中只有一个bean 的实例，单例的模式由 bean factory 自身来维护
     - prototype：原形范围与单例范围相反，为每一个 bean 请求提供一个实例
     - request：在请求 bean 范围内会每一个来自客户端的网络请求创建一个实例，在请求完成以后，bean 会失效并被垃圾回收器回收
     - session：与请求范围类似，确保每个 session 中有一个 bean 的实例，在 session 过期后，bean会随之失效
     - global- session：global-session 和 Portlet 应用相关。当你的应用部署在 Portlet 容器中工作时，它包含很多 portlet。如果 你想要声明让所有的 portlet 共用全局的存储变量的话，那么这全局变量需要存储在 global-session 中。全局作用域与 Servlet 中的 session 作用域效果相同
3. springmvc
4. springboot
5. mybatis

### 3、OpenFeign组件知识
1. hystrix
2. ribbon
3. feign

### 4、Dubbo组件知识
1. sentinel
2. dubbo
3. seata

### 5、Zookeeper、Eureka、Nacos

### 6、Mysql、Oracle
1. 索引数据结构
   - B+TREE mysql索引，当然也和数据库引擎有关
   - B*TREE oracle索引
2. sql优化工具
   - explain mysql
      - explain 参数
        - id:是一组数字，代表多个表之间的查询顺序，或者包含子句查询语句中的顺序，id 总共分为三种情况，依次详解
          ```
          id 相同，执行顺序由上至下
          id 不同，如果是子查询，id 号会递增，id 值越大优先级越高，越先被执行
          id 相同和不同的情况同时存在
          ```
        - select_type：查询类型
          - simple:简单的 select 查询，查询中不包含子查询或者 union 查询
          - primary:如果 SQL 语句中包含任何子查询，那么子查询的最外层会被标记为 primary
          - subquery:在 select 或者 where 里包含了子查询，那么子查询就会被标记为 subQquery，同三.二同时出现
          - derived:在 from 中包含的子查询，会被标记为衍生查询，会把查询结果放到一个临时表中
          - union / union result:如果有两个 select 查询语句，他们之间用 union 连起来查询，那么第二个 select 会被标记为 union，union 的结果被标记为 union result。它的 id 是为 null 的
          - table:表示这一行的数据是哪张表的数据
        - type：type 是代表 MySQL 使用了哪种索引类型，不同的索引类型的查询效率也是不一样的
          - system：表中只有一行记录，system 是 const 的特例，几乎不会出现这种情况，可以忽略不计
          - const：将主键索引或者唯一索引放到 where 条件中查询，MySQL 可以将查询条件转变成一个常量，只匹配一行数据，索引一次就找到数据了
          - eq_ref：在多表查询中，如 T1 和 T2，T1 中的一行记录，在 T2 中也只能找到唯一的一行，说白了就是 T1 和 T2 关联查询的条件都是主键索引或者唯一索引，这样才能保证 T1 每一行记录只对应 T2 的一行记录
          - ref：不是主键索引，也不是唯一索引，就是普通的索引，可能会返回多个符合条件的行
          - range：体现在对某个索引进行区间范围检索，一般出现在 where 条件中的 between、and、<、>、in 等范围查找中
          - index：将所有的索引树都遍历一遍，查找到符合条件的行。索引文件比数据文件还是要小很多，所以比不用索引全表扫描还是要快很多
          - all：没用到索引，单纯的将表数据全部都遍历一遍，查找到符合条件的数据
        - possible_keys：此次查询中涉及字段上若存在索引，则会被列出来，表示可能会用到的索引，但并不是实际上一定会用到的索引
        - key：此次查询中实际上用到的索引
        - key_len：表示索引中使用的字节数，通过该属性可以知道在查询中使用的索引长度，注意：这个长度是最大可能长度，并非实际使用长度，在不损失精确性的情况下，长度越短查询效率越高
        - ref：显示关联的字段。如果使用常数等值查询，则显示 const，如果是连接查询，则会显示关联的字段
          - tb_emp：表为非唯一性索引扫描，实际使用的索引列为 idx_name，由于 tb_emp.name='rose'为一个常量，所以 ref=const
          - tb_dept：为唯一索引扫描
        - rows：根据表信息统计以及索引的使用情况，大致估算说要找到所需记录需要读取的行数，rows 越小越好
        - extra：不适合在其他列显示出来，但在优化时十分重要的信息
          - using fileSort（重点优化）：俗称 " 文件排序 " ，在数据量大的时候几乎是“九死一生”，在 order by 或者在 group by 排序的过程中，order by 的字段不是索引字段，或者 select 查询字段存在不是索引字段，或者 select 查询字段都是索引字段，但是 order by 字段和 select 索引字段的顺序不一致，都会导致 fileSort
          - using temporary（重点优化）：使用了临时表保存中间结果，常见于 order by 和 group by 中
          - USING index（重点）：表示相应的 select 操作中使用了覆盖索引（Coveing Index）,避免访问了表的数据行，效率不错！ 如果同时出现 using where，表明索引被用来执行索引键值的查找；如果没有同时出现 using where，表面索引用来读取数据而非执行查找动作
          - Using wher：表明使用了 where 过滤
          - using join buffer：使用了连接缓存
          - impossible where：where 子句的值总是 false，不能用来获取任何元组
          - select tables optimized away：在没有 GROUPBY 子句的情况下，基于索引优化 MIN/MAX 操作或者 对于 MyISAM 存储引擎优化 COUNT(*)操作，不必等到执行阶段再进行计算， 查询执行计划生成的阶段即完成优化
          - distinct：优化 distinct，在找到第一匹配的元组后即停止找同样值的工作
   - plsql f5 oracle
3. 数据库索引创建，使用，失效问题
4. 基础的sql优化常识

### 7、Redis、Elasticsearch、MongoDB
1. redis
   - String、Hash、List、Set、Sorted-Set，最大存储为512MB一个字符串
   - Redis 有哪几种数据淘汰策略
      - noeviction:返回错误当内存限制达到，并且客户端尝试执行会让更多内存被使用的命令。
      - allkeys-lru: 尝试回收最少使用的键（LRU），使得新添加的数据有空间存放。
      - volatile-lru: 尝试回收最少使用的键（LRU），但仅限于在过期集合的键,使得新添加的数据有空间存放。
      - allkeys-random: 回收随机的键使得新添加的数据有空间存放。
      - volatile-random: 回收随机的键使得新添加的数据有空间存放，但仅限于在过期集合的键。
      - volatile-ttl: 回收在过期集合的键，并且优先回收存活时间（TTL）较短的键,使得新添加的数据有空间存放。
   - redis 持久化
      - RDB(Redis DataBase:在不同的时间点将 redis 的数据生成的快照同步到磁盘等介质上):内存到硬盘的快照，定期更新。缺点：耗时，耗性能(fork+io 操作)，易丢失数据。
      - AOF(Append Only File：将 redis 所执行过的所有指令都记录下来，在下次 redis 重启时，只需要执行指令就可以了):写日志。缺点：体积大，恢复速度慢。
      - bgsave 做镜像全量持久化，aof 做增量持久化。因为 bgsave 会消耗比较长的时间，不够实时，在停机的时候会导致大量的数据丢失，需要 aof 来配合，在 redis 实例重启时，优先使用 aof 来恢复内存的状态，如果没有 aof 日志，就会使用 rdb 文件来恢复。Redis 会定期做aof 重写，压缩 aof 文件日志大小。Redis4.0 之后有了混合持久化的功能，将 bgsave 的全量和 aof 的增量做了融合处理，这样既保证了恢复的效率又兼顾了数据的安全性。bgsave 的原理，fork 和 cow, fork 是指 redis 通过创建子进程来进行 bgsave 操作，cow 指的是 copy on write，子进程创建后，父子进程共享数据段，父进程继续提供读写服务，写脏的页面数据会逐渐和子进程分离开来。
   - redis lua实现分布式锁、redission实现分布式锁
2. ElasticSearch
   - 分词器
      - 内置分词器
        ```
        Standard Analyzer - 默认分词器，按词切分，小写处理
        Simple Analyzer - 按照非字母切分（符号被过滤），小写处理
        Stop Analyzer - 小写处理，停用词过滤（the ，a，is）
        Whitespace Analyzer - 按照空格切分，不转小写
        Keyword Analyzer - 不分词，直接将输入当做输出
        Pattern Analyzer - 正则表达式，默认 \W+
        Language - 提供了 30 多种常见语言的分词器
        Customer Analyzer - 自定义分词器
        ```
      - 中文分词器
        ```
        ICU Analyzer - 它提供了 Unicode 的支持，更好的支持亚洲语言
        IK Analyzer - 支持自定义词库，支持热更新分词字典
        jieba Analyzer - Python 中最流行的分词系统，支持分词和词性标注，支持繁体分词、自定义词典、并行分词等
        THULAC - THU Lexucal Analyzer for Chinese, 清华大学自然语言处理和社会人文计算实验室的一套中文分词器
        ```
   - 数据结构
      - Cluster：集群，一个ES集群由一个或多个节点（Node）组成，每个集群都有一个cluster name作为标识。
      - node：节点，一个ES实例就是一个node，一个机器可以有多个实例，所以并不能说一台机器就是一个node，大多数情况下每个node运行在一个独立的环境或虚拟机上。
      - index： 索引，即一系列documents的集合。
      - shard：
         - 分片，ES是分布式搜索引擎，每个索引有一个或多个分片，索引的数据被分配到各个分片上，相当于一桶水用了N个杯子装。
         - 分片有助于横向扩展，N个分片会被尽可能平均地（rebalance）分配在不同的节点上（例如你有2个节点，4个主分片(不考虑备份)，那么每个节点会分到2个分片，后来你增加了2个节点，那么你这4个节点上都会有1个分片，这个过程叫relocation，ES感知后自动完成)。
         - 分片是独立的，对于一个Search Request的行为，每个分片都会执行这个Request。
         - 每个分片都是一个Lucene Index，所以一个分片只能存放 Integer.MAX_VALUE - 128 = 2,147,483,519 个docs。
      - replica
         - 复制，可以理解为备份分片，相应地有primary shard（主分片）。
         - 主分片和备分片不会出现在同一个节点上（防止单点故障），默认情况下一个索引创建5个分片一个备份（即5primary+5replica=10个分片）
         - 如果你只有一个节点，那么5个replica都无法分配（unassigned），此时cluster status会变成Yellow。
         - 对于一个索引，除非重建索引否则不能调整分片的数目（主分片数, number_of_shards），但可以随时调整replica数(number_of_replicas)。
         - replica主要作用
            ```
            a.容灾：primary分片丢失，replica分片就会被顶上去成为新的主分片，同时根据这个新的主分片创建新的replica，集群数据安然无恙
            b. 提高查询性能：replica和primary分片的数据是相同的，所以对于一个query既可以查主分片也可以查备分片，在合适的范围内多个replica性能会更优（但要考虑资源占用也会提升[cpu/disk/heap]），另外index request只能发生在主分片上，replica不能执行index request。
            ```
      - ES集群状态
         - Green：所有主分片和备份分片都准备就绪（分配成功），即使有一台机器挂了（假设一台机器一个实例），数据都不会丢失，但会变成Yellow状态。
         - Yellow：所有主分片准备就绪，但存在至少一个主分片（假设是A）对应的备份分片没有就绪，此时集群属于警告状态，意味着集群高可用和容灾能力下降，如果刚好A所在的机器挂了，并且你只设置了一个备份（已处于未就绪状态），那么A的数据就会丢失（查询结果不完整），此时集群进入Red状态。
         - Red：至少有一个主分片没有就绪（直接原因是找不到对应的备份分片成为新的主分片）,此时查询的结果会出现数据丢失（不完整）。
3. MongoDB
   - 基础特性
      - 面向文档存储，基于JSON/BSON 可表示灵活的数据结构
      - 动态 DDL能力，没有强Schema约束，支持快速迭代
      - 高性能计算，提供基于内存的快速数据查询
      - 容易扩展，利用数据分片可以支持海量数据存储
      - 丰富的功能集，支持二级索引、强大的聚合管道功能，为开发者量身定做的功能，如数据自动老化、固定集合等等
      - 跨平台版本、支持多语言SDK
   - 数据结构
      - database 数据库，与SQL的数据库(database)概念相同，一个数据库包含多个集合(表)
      - collection 集合，相当于SQL中的表(table)，一个集合可以存放多个文档(行)。 不同之处就在于集合的结构(schema)是动态的，不需要预先声明一个严格的表结构。更重要的是，默认情况下 MongoDB 并不会对写入的数据做任何schema的校验。
      - document 文档，相当于SQL中的行(row)，一个文档由多个字段(列)组成，并采用bson(json)格式表示。
      - field 字段，相当于SQL中的列(column)，相比普通column的差别在于field的类型可以更加灵活，比如支持嵌套的文档、数组。此外，MongoDB中字段的类型是固定的、区分大小写、并且文档中的字段也是有序的。
      - _id 主键，MongoDB 默认使用一个_id 字段来保证文档的唯一性。
      - reference 引用，勉强可以对应于 外键(foreign key) 的概念，之所以是勉强是因为 reference 并没有实现任何外键的约束，而只是由客户端(driver)自动进行关联查询、转换的一个特殊类型。
      - view 视图，MongoDB 3.4 开始支持视图，和 SQL 的视图没有什么差异，视图是基于表/集合之上进行动态查询的一层对象，可以是虚拟的，也可以是物理的(物化视图)。
      - index 索引，与SQL 的索引相同。
      - $lookup 这是一个聚合操作符，可以用于实现类似 SQL-join 连接的功能
      - transaction 事务，从 MongoDB 4.0 版本开始，提供了对于事务的支持
      - aggregation 聚合，MongoDB 提供了强大的聚合计算框架，group by 是其中的一类聚合操作。

### 8、RabbitMQ、Kafka
1. RabbitMQ
   - 交换器
    - direct交换器：如果路由键匹配的话，消息就被投递到对应的队列。
    - fanout交换器：当你发送一条消息到fanout交换器时，他会把消息投递给所有附加在此交换器上的队列。
    - topic交换器：通配符匹配Key，#匹配全量，*匹配单个
      ```
      例如
      1.2.log、1.log、hello.log
      #.log 匹配 1.2.log、1.log、hello.log
      *.log 匹配 1.log、hello.log
      ```
   - 队列
   - 服务提供者推送队列
   - 消费者消费队列
   - 绑定 routing key 绑定关系和交换器类型也有关系
   - 重复推送、重复消费、消费确认机制
2. Kafka
3. RocketMQ

### 9、Nginx、Docker

### 10、Linux基本命令

### 11、八大排序算法