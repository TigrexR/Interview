### 1、 final、finally、finalize的区别
- 1、final修饰符（关键字）。被final修饰的类，就意味着不能再派生出新的子类，不能作为父类而被子类继承。因此一个类不能既被abstract声明，又被final声明。将变量或方法声明为final，可以保证他们在使用的过程中不被修改。被声明为final的变量必须在声明时给出变量的初始值，而在以后的引用中只能读取。被final声明的方法也同样只能使用，即不能方法重写。
- 2、finally是在异常处理时提供finally块来执行任何清除操作。不管有没有异常被抛出、捕获，finally块都会被执行。try块中的内容是在无异常时执行到结束。catch块中的内容，是在try块内容发生catch所声明的异常时，跳转到catch块中执行。finally块则是无论异常是否发生，都会执行finally块的内容，所以在代码逻辑中有需要无论发生什么都必须执行的代码，就可以放在finally块中。
- 3、finalize是方法名。java技术允许使用finalize（）方法在垃圾收集器将对象从内存中清除出去之前做必要的清理工作。这个方法是由垃圾收集器在确定这个对象没有被引用时对这个对象调用的。它是在object类中定义的，因此所有的类都继承了它。子类覆盖finalize（）方法以整理系统资源或者被执行其他清理工作。finalize（）方法是在垃圾收集器删除对象之前对这个对象调用的。 

### 2、Exception、Error、运行时异常与一般异常有何异同
- Error层次结构描述了java运行时系统的内部错误和资源耗尽错误。大多数错误与代码编写者执行的操作无关，而表示代码运行时 JVM（Java 虚拟机）出现的问题。应用程序不应该抛出这种类型的对象。 
- Exception这个层次结构又分解为连个分支：一个分支派生于RuntimeException；另一个分支包含其他异常。划分两个分支的规则是：由程序错误导致的异常属于RuntimeException；而程序本身没有没有问题，但由于像I/O错误这类异常导致的异常属于其他异常。
- RuntimeException（运行时异常）： 
- - IndexOutOfBoundsException(下标越界异常) 
- - NullPointerException(空指针异常) 
- - NumberFormatException （String转换为指定的数字类型异常） 
- - ArithmeticException -（算术运算异常 如除数为0） 
- - ArrayStoreException - （向数组中存放与声明类型不兼容对象异常） 
- - SecurityException -（安全异常） 
- IOException（其他异常） 
- - FileNotFoundException（文件未找到异常。） 
- - IOException（操作输入流和输出流时可能出现的异常。） 
- - EOFException （文件已结束异常）

### 3、int 和 Integer 有什么区别，Integer的值缓存范围
- （1）Integer是int的包装类；int是基本数据类型； 
- （2）Integer变量必须实例化后才能使用；int变量不需要； 
- （3）Integer实际是对象的引用，指向此new的Integer对象；int是直接存储数据值 ； 
- （4）Integer的默认值是null；int的默认值是0。
- （5） 在-128~127 之内的数

### 4、包装类，装箱和拆箱


- 这八种包装类所继承的父类不全都相同。

    1）Integer ,Byte,Float,Double,Short,Long都属于Number类的子类，Number类本身提供了一系列的返回

    以上六种基本数据类型的操作。

    2）Character属于Object子类。

    3）Boolean属于Object子类。

    装箱：将基本数据类型变为包装类
    拆箱：将一个包装类变为基本数据类型
    在JDK1.5之前，对于程序本身来说，包装类不能直接进行“+，-,*,/，++，--”等操作，因为是一个类，

    所以不能这么操作。

    但是在JDK1.5之后，对程序的包装类功能进行了改变，增加了自动装箱和自动拆箱功能，而且，可以使用包装类直接进行数字运行。

    自动装箱和自动拆箱也就是，可以自动由int-->Integer类型转变，而自动拆箱就是自动由Integer-->int转变。


### 5、String、StringBuilder、StringBuffer
1. 首先说运行速度，或者说是执行速度，在这方面运行速度快慢为：StringBuilder >       StringBuffer > String
2. String为字符串常量，而StringBuilder和StringBuffer均为字符串变量，即String对     象一旦创建之后该对象是不可更改的，但后两者的对象是变量，是可以更改的。
3. 再来说线程安全：在线程安全上，StringBuilder是线程不安全的，而StringBuffer是线程安全的。如果一个StringBuffer对象在字符串缓冲区被多个线程使用时，StringBuffer中很多方法可以带有synchronized关键字，所以可以保证线程是安全的，但StringBuilder的方法则没有该关键字，所以不能保证线程安全，有可能会出现一些错误的操作。所以如果要进行的操作是多线程的，那么就要使用StringBuffer，但是在单线程的情况下，还是建议使用速度比较快的StringBuilder。
4.String：适用于少量的字符串操作的情况
StringBuilder：适用于单线程下在字符缓冲区进行大量操作的情况
StringBuffer：适用多线程下在字符缓冲区进行大量操作的情况

### 6、重载和重写的区别
- 方法重写(overriding)：
1. 也叫子类的方法覆盖父类的方法，要求返回值、方法名和参数都相同。
2. 子类抛出的异常不能超过父类相应方法抛出的异常。(子类异常不能超出父类异常)
3. 子类方法的的访问级别不能低于父类相应方法的访问级别(子类访问级别不能低于父类访问级别)
- 方法重载(overloading):重载是在同一个类中的两个或两个以上的方法，拥有相同的方法名，但是参数却不相同，方法体也不相同，最常见的重载的例子就是类的构造函数。

### 7、抽象类和接口有什么区别

|参数|抽象类|接口|
|:----    |:---|:----- |
|默认的方法实现 |它可以有默认的方法实现  |接口完全是抽象的。它根本不存在方法的实现 |
|实现 |子类使用extends关键字来继承抽象类。如果子类不是抽象类的话，它需要提供抽象类中所有声明的方法的实现。  |子类使用关键字implements来实现接口。它需要提供接口中所有声明的方法的实现 |		
|构造器	|抽象类可以有构造器	|接口不能有构造器
|与正常Java类的区别	|除了你不能实例化抽象类之外，它和普通Java类没有任何区别	|接口是完全不同的类型|
|访问修饰符	|抽象方法可以有public、protected和default这些修饰符	|接口方法默认修饰符是public。你不可以使用其它修饰符。|
|main方法	|抽象方法可以有main方法并且我们可以运行它	|接口没有main方法，因此我们不能运行它。|
|多继承	|抽象方法可以继承一个类和实现多个接口	|接口只可以继承一个或多个其它接口|
|速度	|它比接口速度要快	|接口是稍微有点慢的，因为它需要时间去寻找在类中实现的方法。|
|添加新方法	|如果你往抽象类中添加新的方法，你可以给它提供默认的实现。因此你不需要改变你现在的代码。	|如果你往接口中添加方法，那么你必须改变实现该接口的类。|

### 8、说说反射的用途及实现
1. 在运行时判断任意一个对象所属的类
2. 在运行时构造任意一个类的对象
3. 在运行时判断任意一个类所具有的成员变量和方法（通过反射设置可以调用 private）
4. 在运行时调用人一个对象的方法
- Java反射机制是一个非常强大的功能，在很多的项目比如Spring，Mybatis都都可以看到反射的身影。通过反射机制，我们可以在运行期间获取对象的类型信息。利用这一点我们可以实现工厂模式和代理模式等设计模式，同时也可以解决java泛型擦除等令人苦恼的问题。

- 获取一个对象对应的反射类，在Java中有三种方法可以获取一个对象的反射类，通过getClass()方法,通过Class.forName()方法；使用类.class,通过类加载器实现，getClassLoader()

### 9、说说自定义注解的场景及实现
- 跟踪代码的依赖性，实现代替配置文件的功能。比较常见的是Spring等框架中的基于注解配置。还可以生成文档常见的@See@param@return等。如@override放在方法签名，如果这个方法 并不是覆盖了超类方法，则编译时就能检查出。使用@interface自定义注解时，自动继承了java.lang.annotation.Annotation接口，由编译程序自动完成其他细节，在定义注解时，不能继承其他注解或接口。
### 10、HTTP请求的GET与POST方式的区别
- 在客户机和服务器之间进行请求-响应时，两种最常被用到的方法是：GET 和 POST。

- GET - 从指定的资源请求数据。
- POST - 向指定的资源提交要被处理的数据
- GET方法
请注意，查询字符串（名称/值对）是在 GET 请求的 URL 中发送的：
/test/demo_form.asp?name1=value1&name2=value2
请求可被缓存
请求保留在浏览器历史记录中
请求可被收藏为书签
请求不应在处理敏感数据时使用
请求有长度限制
请求只应当用于取回数据
- POST方法
请注意，查询字符串（名称/值对）是在 POST 请求的 HTTP 消息主体中发送的：
POST /test/demo_form.asp HTTP/1.1
Host: w3schools.com
name1=value1&name2=value2
比较 GET 与 POST

|方法|GET|POST|
|:---- |:---- |:---- |
|缓存|能被缓存|不能缓存|
|编码类型|application/x-www-form-urlencoded|application/x-www-form-urlencoded 或 multipart/form-data。为二进制数据使用多重编码。|
|对数据长度的限制|是的。当发送数据时，GET|方法向 URL 添加数据；URL 的长度是受限制的（URL 的最大长度是 2048 个字符）	无限制。|
|对数据类型的限制|只允许 ASCII 字符|没有限制。也允许二进制数据|
|安全性	|与 POST 相比，GET 的安全性较差，因为所发送的数据是 URL 的一部分。在发送密码或其他敏感信息时绝不要使用 GET	|POST 比 GET 更安全，因为参数不会被保存在浏览器历史或 web 服务器日志中。|
|可见性	|数据在 URL 中对所有人都是可见的。	|数据不会显示在 URL 中。其他 HTTP 请求方法|

- HEAD 与 GET 相同，但只返回 HTTP 报头，不返回文档主体。
1. PUT 上传指定的 URI 表示。
2. DELETE 删除指定资源。
3. OPTIONS 返回服务器支持的 HTTP 方法
4. CONNECT 把请求连接转换到透明的 TCP/IP 通道。
### 11、Session与Cookie区别
1. cookie数据存放在客户的浏览器上，session数据放在服务器上。
2. cookie不是很安全，别人可以分析存放在本地的COOKIE并进行COOKIE欺骗考虑到安全应当使用session。
3. session会在一定时间内保存在服务器上。当访问增多，会比较占用你服务器的性能考虑到减轻服务器性能方面，应当使用COOKIE。
4. 单个cookie保存的数据不能超过4K，很多浏览器都限制一个站点最多保存20个cookie。
所以个人建议：
5. 将登陆信息等重要信息存放为SESSION，其他信息如果需要保留，可以放在COOKIE中
### 12、session 分布式处理
- 第一种：粘性session
粘性Session是指将用户锁定到某一个服务器上，比如上面说的例子，用户第一次请求时，负载均衡器将用户的请求转发到了A服务器上，如果负载均衡器设置了粘性Session的话，那么用户以后的每次请求都会转发到A服务器上，相当于把用户和A服务器粘到了一块，这就是粘性Session机制

- 第二种：服务器session复制
原理：任何一个服务器上的session发生改变（增删改），该节点会把这个 session的所有内容序列化，然后广播给所有其它节点，不管其他服务器需不需要session，以此来保证Session同步。

- 第三种：session共享机制
使用分布式缓存方案比如memcached、Redis，但是要求Memcached或Redis必须是集群。
原理：不同的 tomcat指定访问不同的主memcached。多个Memcached之间信息是同步的，能主从备份和高可用。用户访问时首先在tomcat中创建session，然后将session复制一份放到它对应的memcahed上

- 第四种：session持久化到数据库
原理：就不用多说了吧，拿出一个数据库，专门用来存储session信息。保证session的持久化。 优点：服务器出现问题，session不会丢失 缺点：如果网站的访问量很大，把session存储到数据库中，会对数据库造成很大压力，还需要增加额外的开销维护数据库。

### 13、Spring的MVC设计思想
Spring MVC工作流程图



图一






图二 





Spring工作流程描述

      1. 用户向服务器发送请求，请求被Spring 前端控制Servelt DispatcherServlet捕获；

      2. DispatcherServlet对请求URL进行解析，得到请求资源标识符（URI）。然后根据该URI，调用HandlerMapping获得该Handler配置的所有相关的对象（包括Handler对象以及Handler对象对应的拦截器），最后以HandlerExecutionChain对象的形式返回；

      3. DispatcherServlet 根据获得的Handler，选择一个合适的HandlerAdapter。（附注：如果成功获得HandlerAdapter后，此时将开始执行拦截器的preHandler(...)方法）

       4.  提取Request中的模型数据，填充Handler入参，开始执行Handler（Controller)。 在填充Handler的入参过程中，根据你的配置，Spring将帮你做一些额外的工作：

      HttpMessageConveter： 将请求消息（如Json、xml等数据）转换成一个对象，将对象转换为指定的响应信息

      数据转换：对请求消息进行数据转换。如String转换成Integer、Double等

      数据根式化：对请求消息进行数据格式化。 如将字符串转换成格式化数字或格式化日期等

      数据验证： 验证数据的有效性（长度、格式等），验证结果存储到BindingResult或Error中

      5.  Handler执行完成后，向DispatcherServlet 返回一个ModelAndView对象；

      6.  根据返回的ModelAndView，选择一个适合的ViewResolver（必须是已经注册到Spring容器中的ViewResolver)返回给DispatcherServlet ；

      7. ViewResolver 结合Model和View，来渲染视图

      8. 将渲染结果返回给客户端。

Spring工作流程描述


为什么Spring只使用一个Servlet(DispatcherServlet)来处理所有请求？
详细见J2EE设计模式-前端控制模式
Spring为什么要结合使用HandlerMapping以及HandlerAdapter来处理Handler?
符合面向对象中的单一职责原则，代码架构清晰，便于维护，最重要的是代码可复用性高。如HandlerAdapter可能会被用于处理多种Handler。

1、请求旅程的第一站是Spring的DispatcherServlet。与大多数基于Java的Web框架一样，Spring MVC所有的请求都会通过一个前端控制器(front contrller)Servlet.前端控制器是常用Web应用程序模式。在这里一个单实例的Servlet将请求委托给应用的其他组件来执行实际的处理。在Spring MVC中，DisPatcherServlet就是前端控制器。


2、DisPactcher的任务是将请求发送Spring MVC控制器(controller).控制器是一个用于处理请求的Spring组件。在典型的应用中可能会有多个控制器，DispatcherServlet需要知道应该将请求发送给那个哪个控制器。所以Dispactcher以会查询一个或 多个处理器映射(Handler mapping),来确定请求的下一站在哪里。处理映射器根据请求携带的 URL信息来进行决策。


3、一旦选择了合适的控制器，DispatcherServlet会将请求发送给选中的控制器。到了控制器，请求会卸下其负载(用户提交的信息)并耐心等待控制器处理这些信息。(实际上，设计良好的控制器 本身只是处理很少，甚至不处理工作，而是将业务逻辑委托给一个或多个服务器对象进行处理)


4、控制器在完成处理逻辑后，通常会产生一些信息。这些 信息需要返回给 用户，并在浏览器上显示。这些信息被称为模型(Model),不过仅仅给用户返回原始的信息是不够的----这些信息需要以用户友好的方式进行格式化，一般会是HTML。所以，信息需要发送一个视图(View),通常会是JSP。


5、 控制器做的最后一件事就是将模型打包，并且表示出用于渲染输出的视图名。它接下来会将请求连同模型和视图发送回DispatcherServlet。


6、这样，控制器就不会与特定的视图相耦合*传递给控制器的视图名并不直接表示某个特定的jsp。实际上，它甚至并不能确定视图就是JSP。相反，它仅仅传递了一个逻辑名称，这个名字将会用来查找产生结果的真正视图。DispatcherServlet将会使用视图解析器(View resolver),来将逻辑视图名称匹配为一个特定的视图实现，他可能也可能不是JSP


7、虽然DispatcherServlet已经知道了哪个驶入渲染结果、那请求的任务基本上也就完成了，它的最后一站是试图的实现。在这里它交付给模型数据。请求的任务就结束了。视图将使用模型数据渲染输出。这个输出通过响应对象传递给客户端(不会像听上去那样硬编码)


可以看到，请求要经过很多步骤，最终才能形成返回给客户端的响应，大多数的 步骤都是在Spirng框架内部完成的。


14、MVC 设计思想

什么是设计思想？前人踩过无数的坑，总结出来的真理。一般用来解决特定问题。需要好好学习设计模式，框架中大量采用.


那MVC又是什么东东？


回答之前我们先看看设计的原则。单一职责，开闭原则，面向接口编程，对象最少知道。一句话总结：“高内聚，低耦合”。六个字一个逗号。


Model(模型层) ：一般存放处理逻辑，
View (视图层)：存放html，jsp，文件
Controller(控制层)：主要负责调度两者，实现解耦。

当我们像浏览器发送一个请求时，首先需要经过控制层(DispatcherServlet),其是它实际不做什么事情，委托给别人做。调用模型层(处理一些业务逻辑)，返回数据模型给控制器，接着在委托视图解析器解析视图。最后定位到视图的资源，返回给控制器，控制器在返回给客户端。(其实需要做的还有很多)


主要的目的是解耦，各司其职。做好你份内的事。对扩展性也好。增加需求不会影响到其他模块。


15、equals与==的区别
== 比较的是变量(栈)内存中存放的对象的(堆)内存地址，用来判断两个对象的地址是否相同，即是否是指相同一个对象。比较的是真正意义上的指针操作。
equals用来比较的是两个对象的内容是否相等，由于所有的类都是继承自java.lang.Object类的，所以适用于所有对象，如果没有对该方法进行覆盖的话，调用的仍然是Object类中的方法，而Object中的equals方法返回的却是==的判断。

16、hashCode和equals方法的区别与联系
 hashCode()方法和equal()方法的作用其实一样，在Java里都是用来对比两个对象是否相等一致，那么equal()既然已经能实现对比的功能了，为什么还要hashCode()呢？

 

     因为重写的equal（）里一般比较的比较全面比较复杂，这样效率就比较低，而利用hashCode()进行对比，则只要生成一个hash值进行比较就可以了，效率很高，那么hashCode()既然效率这么高为什么还要equal()呢？

 

           因为hashCode()并不是完全可靠，有时候不同的对象他们生成的hashcode也会一样（生成hash值得公式可能存在的问题），所以hashCode()只能说是大部分时候可靠，并不是绝对可靠，所以我们可以得出：

 

         1.equal()相等的两个对象他们的hashCode()肯定相等，也就是用equal()对比是绝对可靠的。

         2.hashCode()相等的两个对象他们的equal()不一定相等，也就是hashCode()不是绝对可靠的。

 

所有对于需要大量并且快速的对比的话如果都用equal()去做显然效率太低，所以解决方式是，每当需要对比的时候，首先用hashCode()去对比，如果hashCode()不一样，则表示这两个对象肯定不相等（也就是不必再用equal()去再对比了）,如果hashCode()相同，此时再对比他们的equal()，如果equal()也相同，则表示这两个对象是真的相同了，这样既能大大提高了效率也保证了对比的绝对正确性！


17、什么是Java序列化和反序列化，如何实现Java序列化？或者请解释Serializable 接口的作用
当两个进程在进行远程通信时，彼此可以发送各种类型的数据。无论是何种类型的数据，都会以二进制序列的形式在网络上传送。发送方需要把这个Java对象转换为字节序列，才能在网络上传送；接收方则需要把字节序列再恢复为Java对象。

　　只能将支持 java.io.Serializable 接口的对象写入流中。每个 serializable 对象的类都被编码，编码内容包括类名和类签名、对象的字段值和数组值，以及从初始对象中引用的其他所有对象的闭包。

1.概念

　　序列化：把Java对象转换为字节序列的过程。

　　反序列化：把字节序列恢复为Java对象的过程。

2.用途

　　对象的序列化主要有两种用途：

　　1） 把对象的字节序列永久地保存到硬盘上，通常存放在一个文件中；

　　2） 在网络上传送对象的字节序列。

 

3.对象序列化

序列化API

　　java.io.ObjectOutputStream代表对象输出流，它的writeObject(Object obj)方法可对参数指定的obj对象进行序列化，把得到的字节序列写到一个目标输出流中。只有实现了Serializable和Externalizable接口的类的对象才能被序列化。

　　java.io.ObjectInputStream代表对象输入流，它的readObject()方法从一个源输入流中读取字节序列，再把它们反序列化为一个对象，并将其返回。


18、Object类中常见的方法，为什么wait  notify会放在Object里边？
这些方法存在于同步中；
使用这些方法必须标识同步所属的锁；
锁可以是任意对象，所以任意对象调用方法一定定义在Object类中。
 

     Condition是在java 1.5中才出现的，它用来替代传统的Object的wait()、notify()实现线程间的协作，相比使用Object的wait()、notify()，使用Condition1的await()、signal()这种方式实现线程间协作更加安全和高效。因此通常来说比较推荐使用Condition，在阻塞队列那一篇博文中就讲述到了，阻塞队列实际上是使用了Condition来模拟线程间协作。

Condition是个接口，基本的方法就是await()和signal()方法；
Condition依赖于Lock接口，生成一个Condition的基本代码是lock.newCondition() 
 调用Condition的await()和signal()方法，都必须在lock保护之内，就是说必须在lock.lock()和lock.unlock之间才可以使用
     Conditon中的await()对应Object的wait()；

     Condition中的signal()对应Object的notify()；

     Condition中的signalAll()对应Object的notifyAll()；


19、List 和 Set 区别
/**
 * 1.存储对象可以考虑：①数组 ②集合
 * 2.数组存储对象的特点：Student[] stu = new Student[20]; stu[0] = new Student();....
 * >弊端：①一旦创建，其长度不可变。②真实的数组存放的对象的个数是不可知。
 * 集合其实底层也是通过数组实现的
 * 3.集合
 * Collection接口
 * |------List接口：存储有序的，可以重复的元素
 * |------ArrayList（主要的实现类）、LinkedList（对于频繁的插入、删除操作）、Vector（古老的实现类、线程安全的）
 * |------Set接口：存储无序的，不可重复的元素
 * |------HashSet、LinkedHashSet、TreeSet
 * Map接口：存储“键-值”对的数据
 * |-----HashMap、LinkedHashMap、TreeMap、Hashtable(子类：Properties)
 */

20、Set和hashCode以及equals方法的联系
Set接口有两个子类：HashSet和TreeSet 。 
|- HashSet 
|- 特点：在不存在重复元素的基础上，还可以进行高速的存取元素。 
|- 要求：需要为您的类重写hashCode()和equals()方法。 
|- TreeSet 
|- 特点：在不存在重复元素的基础上，还可以将元素自动排序。 
|- 要求：需要为您的类实现Comparable接口，并重写compareTo方法。 
|- 重写compareTo() 可以同时完成两份工作  排序和消除重复。

21、List 和 Map 区别
1.面试题：你说说collection里面有什么子类。 
（其实面试的时候听到这个问题的时候，你要知道，面试官是想考察List，Set） 
正如图一，list和set是实现了collection接口的。 
List：1.可以允许重复的对象。
　　 2.可以插入多个null元素。
        3.是一个有序容器，保持了每个元素的插入顺序，输出的顺序就是插入的顺序。
        4.常用的实现类有 ArrayList、LinkedList 和 Vector。ArrayList 最为流行，它提供了使用索引的随意访问，而 LinkedList 则对于经常需要从 List 中添加或删除元素的场合更为合适。
Set：1.不允许重复对象
　　 2. 无序容器，你无法保证每个元素的存储顺序，TreeSet通过 Comparator 或者 Comparable 维护了一个排序顺序。
        3. 只允许一个 null 元素
        4.Set 接口最流行的几个实现类是 HashSet、LinkedHashSet 以及 TreeSet。最流行的是基于 HashMap 实现的 HashSet；TreeSet 还实现了 SortedSet 接口，因此 TreeSet 是一个根据其 compare() 和 compareTo() 的定义进行排序的有序容器。
1.Map不是collection的子接口或者实现类。Map是一个接口。
2.Map 的 每个 Entry 都持有两个对象，也就是一个键一个值，Map 可能会持有相同的值对象但键对象必须是唯一的。
3. TreeMap 也通过 Comparator 或者 Comparable 维护了一个排序顺序。
4. Map 里你可以拥有随意个 null 值但最多只能有一个 null 键。
5.Map 接口最流行的几个实现类是 HashMap、LinkedHashMap、Hashtable 和 TreeMap。（HashMap、TreeMap最常用）
2.面试题：什么场景下使用list，set，map呢？
（或者会问为什么这里要用list、或者set、map，这里回答它们的优缺点就可以了）
如果你经常会使用索引来对容器中的元素进行访问，那么 List 是你的正确的选择。如果你已经知道索引了的话，那么 List 的实现类比如 ArrayList 可以提供更快速的访问,如果经常添加删除元素的，那么肯定要选择LinkedList。
如果你想容器中的元素能够按照它们插入的次序进行有序存储，那么还是 List，因为 List 是一个有序容器，它按照插入顺序进行存储。
如果你想保证插入元素的唯一性，也就是你不想有重复值的出现，那么可以选择一个 Set 的实现类，比如 HashSet、LinkedHashSet 或者 TreeSet。所有 Set 的实现类都遵循了统一约束比如唯一性，而且还提供了额外的特性比如 TreeSet 还是一个 SortedSet，所有存储于 TreeSet 中的元素可以使用 Java 里的 Comparator 或者 Comparable 进行排序。LinkedHashSet 也按照元素的插入顺序对它们进行存储。
如果你以键和值的形式进行数据存储那么 Map 是你正确的选择。你可以根据你的后续需要从 Hashtable、HashMap、TreeMap 中进行选择。

22、Arraylist 与 LinkedList 区别
1.ArrayList是实现了基于动态数组的数据结构，LinkedList基于链表的数据结构。 （LinkedList是双向链表，有next也有previous）
2.对于随机访问get和set，ArrayList觉得优于LinkedList，因为LinkedList要移动指针。
3.对于新增和删除操作add和remove，LinedList比较占优势，因为ArrayList要移动数据。 

23、ArrayList 与 Vector 区别
1）  Vector的方法都是同步的(Synchronized),是线程安全的(thread-safe)，而ArrayList的方法不是，由于线程的同步必然要影响性能，因此,ArrayList的性能比Vector好。 
2） 当Vector或ArrayList中的元素超过它的初始大小时,Vector会将它的容量翻倍,而ArrayList只增加50%的大小，这样,ArrayList就有利于节约内存空间。

24、HashMap 和 Hashtable 的区别
HashMap是Hashtable的轻量级实现（非线程安全的实现），他们都完成了Map接口。主要的区别有：线程安全性，同步(synchronization)，以及速度。

1.Hashtable继承自Dictionary类，而HashMap是Java1.2引进的Map interface的一个实现。

2.HashMap允许将null作为一个entry的key或者value，而Hashtable不允许。

3.HashMap是非synchronized，而Hashtable是synchronized，这意味着Hashtable是线程安全的，多个线程可以共享一个Hashtable；而如果没有正确的同步的话，多个线程是不能共享HashMap的。Java 5提供了ConcurrentHashMap，它是HashTable的替代，比HashTable的扩展性更好。（在多个线程访问Hashtable时，不需要自己为它的方法实现同步，而HashMap 就必须为之提供外同步(Collections.synchronizedMap)）

4.另一个区别是HashMap的迭代器(Iterator)是fail-fast迭代器，而Hashtable的enumerator迭代器不是fail-fast的。所以当有其它线程改变了HashMap的结构（增加或者移除元素），将会抛出ConcurrentModificationException，但迭代器本身的remove()方法移除元素则不会抛出ConcurrentModificationException异常。但这并不是一个一定发生的行为，要看JVM。这条同样也是Enumeration和Iterator的区别。fail-fast机制如果不理解原理，可以查看这篇文章：http://www.cnblogs.com/alexlo/archive/2013/03/14/2959233.html

5.由于HashMap非线程安全，在只有一个线程访问的情况下，效率要高于HashTable。

6.HashMap把Hashtable的contains方法去掉了，改成containsvalue和containsKey。因为contains方法容易让人引起误解。 

7.Hashtable中hash数组默认大小是11，增加的方式是 old*2+1。HashMap中hash数组的默认大小是16，而且一定是2的指数。

8..两者通过hash值散列到hash表的算法不一样：

25、HashSet 和 HashMap 区别
面试中经常被问到HashMap与HashSet的区别。于是本渣静下心来总结了一下HashSet与HashMap的区别。

　　先了解一下HashMap跟HashSet

 HashSet：

　　HashSet实现了Set接口，它不允许集合中出现重复元素。当我们提到HashSet时，第一件事就是在将对象存储在

HashSet之前，要确保重写hashCode（）方法和equals（）方法，这样才能比较对象的值是否相等，确保集合中没有

储存相同的对象。如果不重写上述两个方法，那么将使用下面方法默认实现：

　public boolean add(Object obj)方法用在Set添加元素时，如果元素值重复时返回 "false"，如果添加成功则返回"true"

HashMap：

　　HashMap实现了Map接口，Map接口对键值对进行映射。Map中不允许出现重复的键（Key）。Map接口有两个基本的实现

TreeMap和HashMap。TreeMap保存了对象的排列次序，而HashMap不能。HashMap可以有空的键值对（Key（null）-Value（null））

HashMap是非线程安全的（非Synchronize），要想实现线程安全，那么需要调用collections类的静态方法synchronizeMap（）实现。

public Object put(Object Key,Object value)方法用来将元素添加到map中。

HashSet与HashMap的区别：

HashMap	HashSet
实现了Map接口	实现Set接口
存储键值对	仅存储对象
调用put（）向map中添加元素	调用add（）方法向Set中添加元素
HashMap使用键（Key）计算Hashcode	
HashSet使用成员对象来计算hashcode值，

对于两个对象来说hashcode可能相同，

所以equals()方法用来判断对象的相等性，

如果两个对象不同的话，那么返回false

HashMap相对于HashSet较快，因为它是使用唯一的键获取对象	HashSet较HashMap来说比较慢

26、HashMap 和 ConcurrentHashMap 的区别

27、HashMap 的工作原理及代码实现，什么时候用到红黑树
https://blog.csdn.net/u011240877/article/details/53358305
这里有hashmap的原理和红黑树的代码解析

28、多线程情况下HashMap死循环的问题
https://www.cnblogs.com/dongguacai/p/5599100.html
这里有hashmap在多线程下死循环的代码实现和原理解析

29、ConcurrentHashMap 的工作原理及代码实现，如何统计所有的元素个数
https://blog.csdn.net/yan_wenliang/article/details/51029372
这里有currentHashMap的具体实现，size方法就是元素个数的实现

30、BIO、NIO、AIO的概念
https://blog.csdn.net/u013068377/article/details/70312551

31、什么是长连接和短连接
https://www.cnblogs.com/gotodsp/p/6366163.html

32、三次握手和四次挥手、为什么挥手需要四次
https://blog.csdn.net/baixiaoshi/article/details/67712853

33、MySQL 索引使用的注意事项
https://www.cnblogs.com/heyonggang/p/6610526.html
索引虽然好处很多，但过多的使用索引可能带来相反的问题，索引也是有缺点的：

虽然索引大大提高了查询速度，同时却会降低更新表的速度，如对表进行INSERT,UPDATE和DELETE。因为更新表时，mysql不仅要保存数据，还要保存一下索引文件
建立索引会占用磁盘空间的索引文件。一般情况这个问题不太严重，但如果你在要给大表上建了多种组合索引，索引文件会膨胀很宽
      索引只是提高效率的一个方式，如果mysql有大数据量的表，就要花时间研究建立最优的索引，或优化查询语句。

     使用索引时，有一些技巧：

    1.索引不会包含有NULL的列

       只要列中包含有NULL值，都将不会被包含在索引中，复合索引中只要有一列含有NULL值，那么这一列对于此符合索引就是无效的。

    2.使用短索引

       对串列进行索引，如果可以就应该指定一个前缀长度。例如，如果有一个char（255）的列，如果在前10个或20个字符内，多数值是唯一的，那么就不要对整个列进行索引。短索引不仅可以提高查询速度而且可以节省磁盘空间和I/O操作。

    3.索引列排序

       mysql查询只使用一个索引，因此如果where子句中已经使用了索引的话，那么order by中的列是不会使用索引的。因此数据库默认排序可以符合要求的情况下不要使用排序操作，尽量不要包含多个列的排序，如果需要最好给这些列建复合索引。

    4.like语句操作

      一般情况下不鼓励使用like操作，如果非使用不可，注意正确的使用方式。like ‘%aaa%’不会使用索引，而like ‘aaa%’可以使用索引。

    5.不要在列上进行运算

    6.不使用NOT IN 、<>、！=操作，但<,<=，=，>,>=,BETWEEN,IN是可以用到索引的

    7.索引要建立在经常进行select操作的字段上。

       这是因为，如果这些列很少用到，那么有无索引并不能明显改变查询速度。相反，由于增加了索引，反而降低了系统的维护速度和增大了空间需求。

    8.索引要建立在值比较唯一的字段上。

    9.对于那些定义为text、image和bit数据类型的列不应该增加索引。因为这些列的数据量要么相当大，要么取值很少。

    10.在where和join中出现的列需要建立索引。

    11.where的查询条件里有不等号(where column != …),mysql将无法使用索引。

    12.如果where字句的查询条件里使用了函数(如：where DAY(column)=…),mysql将无法使用索引。

    13.在join操作中(需要从多个数据表提取数据时)，mysql只有在主键和外键的数据类型相同时才能使用索引，否则及时建立了索引也不会使用。

34、DDL、DML、DCL分别指什么
DML（data manipulation language）： 
它们是SELECT、UPDATE、INSERT、DELETE，就象它的名字一样，这4条命令是用来对数据库里的数据进行操作的语言 
DDL（data definition language）： 
DDL比DML要多，主要的命令有CREATE、ALTER、DROP等，DDL主要是用在定义或改变表（TABLE）的结构，数据类型，表之间的链接和约束等初始化工作上，他们大多在建立表时使用 
DCL（Data Control Language）： 
是数据库控制功能。是用来设置或更改数据库用户或角色权限的语句，包括（grant,deny,revoke等）语句。在默认状态下，只有sysadmin,dbcreator,db_owner或db_securityadmin等人员才有权力执行DCL 

35、
ACID一般是指数据库事务正确执行的几个基本要求。需要undo和redo的底层支持。

1.原子性(Atomicity):事务要么成功(可见)，要么失败(不可见)。不存在事务部分成功的情况。

        当我们修改一条数据，我们同时生成一条undo记录描述如何撤销这个修改。这就意味着当我们处在事务处理中时，如果另外一个用户试图查看正在被我们修改的数据，会被告知需要使用undo记录，构造数据被修改之前的状态。这就使得修改只有在提交之后才可见。保证了其他用户要么看到事务的全部或者啥也看不到。


2.一致性(Consistency)：数据库在事务开始前和结束后都应该是一致的。
        一致性要求数据库在任何时候都是处于一个一致、合法的状态。我们可能会说undo数据的存在意味着其他用户会被阻止看到事务中间过程的数据，因此，看不到数据库从一个合法的状态到另外一个暂时的不合法状态，他们看到的要么是事务之前的状态要么是事务之后的状态。(数据库内部当然能看到中间过程的状态数据，而且有些时候很有用，但是终端用户看不到不一致的数据)。假入银行有A、B两个用户，账户余额都是100元。现在A用户向B用户转账50元。过程如下：
        事务开始
        1.A用户账户减去50元
        2.B用户账户加上50元
        3.记录一条转账日志
        事务结束        
        在事务的第1步之后的这个中间状态，A用户账户余额为50元，B用户账户余额还没有增加，还是100元，这就是一个事务中间的非一致状态。但是我们知道，事务要么成功，要么失败，不存在部分成功，所以，用户看到的数据，永远是一致的。

3.隔离性(Isolation):一个事务不会看到另外一个还未完成的事务产生的结果。每个事务就像在单独、隔离的环境下运行一样。
        我们已经知道undo数据使得用户看不到事务的中间数据直到我们提交了修改。实际上，我们走的更远：undo数据使得其他事务在整个事务过程中，不必受到我们事务的影响(这个不是Oracle默认的隔离级别，但是支持)。当然，当2个用户同时去修改同样的数据时，还是会发生问题。完美的隔离是不可能的，因为事实上一个事务必须在有限的时间内完成。

4.持久性(Durability)：成功提交的事务，数据是持久保留，不会因为系统失败而丢失。
        持久性是redo日志提供的一大好处。你怎么保证提交的事务数据在系统失败的情况下也不会丢失？很明显的策略就是不停地把redo日志写到磁盘。如果你没有redo日志，当你修改数据的时候，这就可能意味着你要做很多数据块的随机写。想象一下你往表order_lines中插入10条数据，表上面有3个索引。这个可能需要31个随机的分散的磁盘写操作，让1个表数据块和31个索引块数据持久保存下来。但是Oracle有redo机制。你只要保留少量的关于修改的日志，而不是整个你修改的数据块。31条修改日志最后可能只是1个顺序写操作。







未实现区域
1.3、进程和线程

线程和进程的概念、并行和并发的概念

创建线程的方式及实现

进程间通信的方式

说说 CountDownLatch、CyclicBarrier 原理和区别

说说 Semaphore 原理

说说 Exchanger 原理

ThreadLocal 原理分析，ThreadLocal为什么会出现OOM，出现的深层次原理

讲讲线程池的实现原理

线程池的几种实现方式

线程的生命周期，状态是如何转移的

可参考：《Java多线程编程核心技术》
1.4、锁机制

说说线程安全问题，什么是线程安全，如何保证线程安全

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

1.5、JVM

JVM运行时内存区域划分

内存溢出OOM和堆栈溢出SOE的示例及原因、如何排查与解决

如何判断对象是否可以回收或存活

常见的GC回收算法及其含义

常见的JVM性能监控和故障处理工具类：jps、jstat、jmap、jinfo、jconsole等

JVM如何设置参数

JVM性能调优

类加载器、双亲委派模型、一个类的生命周期、类是如何加载到JVM中的

类加载的过程：加载、验证、准备、解析、初始化

强引用、软引用、弱引用、虚引用

Java内存模型JMM

1.6、设计模式

常见的设计模式

设计模式的的六大原则及其含义

常见的单例模式以及各种实现方式的优缺点，哪一种最好，手写常见的单利模式

设计模式在实际场景中的应用

Spring中用到了哪些设计模式

MyBatis中用到了哪些设计模式

你项目中有使用哪些设计模式

说说常用开源框架中设计模式使用分析

动态代理很重要！！！

1.7、数据结构

树（二叉查找树、平衡二叉树、红黑树、B树、B+树）

深度有限算法、广度优先算法

克鲁斯卡尔算法、普林母算法、迪克拉斯算法

什么是一致性Hash及其原理、Hash环问题

常见的排序算法和查找算法：快排、折半查找、堆排序等

2.1、数据库

MySQL 索引使用的注意事项

DDL、DML、DCL分别指什么

explain命令

left join，right join，inner join

数据库事物ACID（原子性、一致性、隔离性、持久性）

事物的隔离级别（读未提交、读以提交、可重复读、可序列化读）

脏读、幻读、不可重复读

数据库的几大范式

数据库常见的命令

说说分库与分表设计

分库与分表带来的分布式困境与应对之策（如何解决分布式下的分库分表，全局表？）

说说 SQL 优化之道

MySQL遇到的死锁问题、如何排查与解决

存储引擎的 InnoDB与MyISAM区别，优缺点，使用场景

索引类别（B+树索引、全文索引、哈希索引）、索引的原理

什么是自适应哈希索引（AHI）

为什么要用 B+tree作为MySQL索引的数据结构

聚集索引与非聚集索引的区别

遇到过索引失效的情况没，什么时候可能会出现，如何解决

limit 20000 加载很慢怎么解决

如何选择合适的分布式主键方案

选择合适的数据存储方案

常见的几种分布式ID的设计方案

常见的数据库优化方案，在你的项目中数据库如何进行优化的

2.2、Redis

Redis 有哪些数据类型，可参考《Redis常见的5种不同的数据类型详解》

Redis 内部结构

Redis 使用场景

Redis 持久化机制，可参考《使用快照和AOF将Redis数据持久化到硬盘中》

Redis 集群方案与实现

Redis 为什么是单线程的？

缓存雪崩、缓存穿透、缓存预热、缓存更新、缓存降级

使用缓存的合理性问题

Redis常见的回收策略

2.3、消息队列

消息队列的使用场景

消息的重发补偿解决思路

消息的幂等性解决思路

消息的堆积解决思路

自己如何实现消息队列

如何保证消息的有序性

三、开源框架和容器

3.1、SSM/Servlet

Servlet的生命周期

转发与重定向的区别

BeanFactory 和 ApplicationContext 有什么区别

Spring Bean 的生命周期

Spring IOC 如何实现

Spring中Bean的作用域，默认的是哪一个

说说 Spring AOP、Spring AOP 实现原理

动态代理（CGLib 与 JDK）、优缺点、性能对比、如何选择

Spring 事务实现方式、事务的传播机制、默认的事务类别

Spring 事务底层原理

Spring事务失效（事务嵌套），JDK动态代理给Spring事务埋下的坑，可参考《JDK动态代理给Spring事务埋下的坑！》

如何自定义注解实现功能

Spring MVC 运行流程

Spring MVC 启动流程

Spring 的单例实现原理

Spring 框架中用到了哪些设计模式

Spring 其他产品（Srping Boot、Spring Cloud、Spring Secuirity、Spring Data、Spring AMQP 等）

有没有用到Spring Boot，Spring Boot的认识、原理

MyBatis的原理

可参考《为什么会有Spring》

可参考《为什么会有Spring AOP》

3.2、Netty

为什么选择 Netty

说说业务中，Netty 的使用场景

原生的 NIO 在 JDK 1.7 版本存在 epoll bug

什么是TCP 粘包/拆包

TCP粘包/拆包的解决办法

Netty 线程模型

说说 Netty 的零拷贝

Netty 内部执行流程

Netty 重连实现

3.3、Tomcat

Tomcat的基础架构（Server、Service、Connector、Container）

Tomcat如何加载Servlet的

Pipeline-Valve机制

可参考：《四张图带你了解Tomcat系统架构！》

四、分布式4.1、Nginx

请解释什么是C10K问题或者知道什么是C10K问题吗？

Nginx简介，可参考《Nginx简介》

正向代理和反向代理.

Nginx几种常见的负载均衡策略

Nginx服务器上的Master和Worker进程分别是什么

使用“反向代理服务器”的优点是什么?

4.2、分布式其他

谈谈业务中使用分布式的场景

Session 分布式方案

Session 分布式处理

分布式锁的应用场景、分布式锁的产生原因、基本概念

分布是锁的常见解决方案

分布式事务的常见解决方案

集群与负载均衡的算法与实现

说说分库与分表设计，可参考《数据库分库分表策略的具体实现方案》

分库与分表带来的分布式困境与应对之策

4.3、Dubbo

什么是Dubbo，可参考《Dubbo入门》

什么是RPC、如何实现RPC、RPC 的实现原理，可参考《基于HTTP的RPC实现》

Dubbo中的SPI是什么概念

Dubbo的基本原理、执行流程

五、微服务

5.1、微服务

前后端分离是如何做的？

微服务哪些框架

Spring Could的常见组件有哪些？可参考《Spring Cloud概述》

领域驱动有了解吗？什么是领域驱动模型？充血模型、贫血模型

JWT有了解吗，什么是JWT，可参考《前后端分离利器之JWT》

你怎么理解 RESTful

说说如何设计一个良好的 API

如何理解 RESTful API 的幂等性

如何保证接口的幂等性

说说 CAP 定理、BASE 理论

怎么考虑数据一致性问题

说说最终一致性的实现方案

微服务的优缺点，可参考《微服务批判》

微服务与 SOA 的区别

如何拆分服务、水平分割、垂直分割

如何应对微服务的链式调用异常

如何快速追踪与定位问题

如何保证微服务的安全、认证

5.2、安全问题

如何防范常见的Web攻击、如何方式SQL注入

服务端通信安全攻防

HTTPS原理剖析、降级攻击、HTTP与HTTPS的对比

5.3、性能优化

性能指标有哪些

如何发现性能瓶颈

性能调优的常见手段

说说你在项目中如何进行性能调优

六、其他

6.1、设计能力

说说你在项目中使用过的UML图

你如何考虑组件化、服务化、系统拆分

秒杀场景如何设计

可参考：《秒杀系统的技术挑战、应对策略以及架构设计总结一二！》
6.2、业务工程

说说你的开发流程、如何进行自动化部署的

你和团队是如何沟通的

你如何进行代码评审

说说你对技术与业务的理解

说说你在项目中遇到感觉最难Bug，是如何解决的

介绍一下工作中的一个你认为最有价值的项目，以及在这个过程中的角色、解决的问题、你觉得你们项目还有哪些不足的地方

6.3、软实力

说说你的优缺点、亮点

说说你最近在看什么书、什么博客、在研究什么新技术、再看那些开源项目的源代码

说说你觉得最有意义的技术书籍

工作之余做什么事情、平时是如何学习的，怎样提升自己的能力

说说个人发展方向方面的思考    

说说你认为的服务端开发工程师应该具备哪些能力

说说你认为的架构师是什么样的，架构师主要做什么

如何看待加班的问题














