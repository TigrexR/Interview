### 1、Java基础、多线程、线程池、
- 定义Integer x=20 Integer y=200 在内存里是个什么过程？
   - 答案： Integer类型的赋予int值时，会调用Integer的valueOf方法，然后valueOf方法在赋值的时候会判断int值是否在-128到127之间，如果是，那么会将这个Integer对象存到静态常量池中cache数组，重复利用，如果不是在这个范围内，那么会新建一个Integer对象并返回
   - 基本数据类型: boolean，char，byte，short，int，long，float，double
   - 封装类类型：Boolean，Character，Byte，Short，Integer，Long，Float，Double
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
- volite关键字的原理？它能保证原子性吗？AtomicInteger底层怎么实现的？

### 2、Spring全家桶、Mybtais

### 3、OpenFeign组件知识

### 4、Dubbo组件知识

### 5、Zookeeper、Eureka、Nacos

### 6、Mysql、Oracle

### 7、Redis、Elasticsearch、MongoDB

### 8、RabbitMq、Kafka

### 9、Nginx、Docker

### 10、Linux基本命令

### 11、八大排序算法