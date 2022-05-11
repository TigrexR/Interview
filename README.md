# 吾生也有涯，而知也无涯。以有涯随无涯，殆已！学如不及，犹恐失之。
- 网络
   - TCP、UDP
   - HTTP
   - session、cookie
- JAVA
   - jdk8、jdk11、jdk17
   - synchronized、thread pool、localthread、cas、aqs、unsafe
   - bio、nio、aio、netty
   - jvm、GI、ZGC、hotspot
   - 代码：https://github.com/TigrexR/netty-springboot-demo
- data structure
   - set、list、map、tree
    - 红黑树
    - b+tree
    - b*tree
   - 八大排序算法
   - 插入排序-直接插入排序
   - 插入排序-希尔排序
   - 选择排序-简单选择排序、二元选择排序
   - 选择排序—堆排序
   - 交换排序—冒泡排序
   - 交换排序—快速排序
   - 归并排序
   - 基数排序
   - 代码：https://github.com/TigrexR/DataStruct
- 设计模式
   - 单一职责原则、里氏替换原则、依赖倒置原则、接口隔离原则、迪米特法则、开闭原则
   - 创建型
      - 简单工厂模式（Simple Factory Pattern）
      - 工厂方法模式（Factory Method Pattern）
      - 抽象工厂模式（Abstract Factory Pattern）
      - 单例模式（Singleton Pattern）
      - 生成器模式（Builder Pattern）
      - 原型模式（Prototype Pattern）
   - 结构型
      - 外观模式
      - 适配器模式
      - 桥接模式
      - 代理模式
      - 装饰者模式
      - 享元模式
   - 行为型
      - 职责链模式
      - 命令模式
      - 解释器模式
      - 迭代器模式
      - 中介者模式
      - 备忘录模式
      - 观察者模式
      - 状态模式
      - 策略模式
      - 模板方法模式
      - 访问者模式
   - 展示项目：https://github.com/TigrexR/module-spring-demo
- JVM字节码编制技术
   - ASM 
   - javassist
   - byte-buddy
   - java-agent
   - jacoco
   - AST、ANTLR
   - 基础组件项目：https://github.com/TigrexR/bytecode-springboot-demo
- Web基础组件
   - jwt、token
   - jackson、fastjson、protoBuf
   - spring、ioc、aop
   - springmvc
   - springboot
   - mybatis、mybatis-plus
   - druid、hikariCP
   - 基础组件项目：https://github.com/TigrexR/geo
- DUBBO rpc
   - dubbo、dubbo3.0
   - sentinel、slueth（阿里流量监控）
   - -> alibaba tcp、http2.0
   - 基础组件项目：https://github.com/TigrexR/dubbo-springboot-demo
- OPEN-FEIGN rpc
   - feign
   - ribbon
   - hystrix 
   - -> open-feign http、http2.0
   - 基础组件项目：https://github.com/TigrexR/openfeign-springboot-demo
- 规则引擎
   - qlExpress
   - groovy
   - drools
   - flink（流式数据库）、kakfa-stream
   - 基础组件项目：https://github.com/TigrexR/rules-engine
- 微信项目
   - 微信接口
   - 微信公众号平台项目：https://github.com/TigrexR/mhwechat
- 日志监控系统
   - 日志输出
      - 通过java-agent直接植入
         1. skywalking
         2. pinpoint
      - 轻量级的修改代码
         1. zipkin
      - 自己实现java-agent探针，通过开发人员自定义
   - 日志收集
      1. logstash主动拉取
      2. 日志输出服务异步推送kafka
   - 日志处理
      1. flink
      2. kafka-stream
      3. 动态规则也可以和groovy结合
   - 日志存储
      - 短期存储到es
      - 长期存储到mongo
      - 超过一定时间，直接废弃或者结转
   - 日志数据分析
      - 数据分析框架
   - 在线问题排查
      - arthas
   - 日志监控项目：https://github.com/TigrexR/log-monitor
- 前端技术
   - vue-3.0
   - node-js
   - axios
   - JavaScript
   - TypeScript
   - element-plus
   - css
   - single-spa
   - 组件项目：https://github.com/TigrexR/single-spa-demo
- zookeeper、eureka、nacos
- springcloud-gateway（网关）
- mysql、oracle、sharding-jdbc、sharding-sphere、seata
- redis、redisson、elasticsearch、click-house、mongodb
- kafka、rabbitmq、rocketmq
- docker、k8s、Serve Mesh、ELK、jenkins、JMH（测试工具库）
- 微服务、DDD
- 最终目标：https://github.com/TigrexR/hupu

### 篮球论坛
- 球队、交易、球员数据、比赛数据、新闻

- 球员数据 -> 大数据源，存储球员基本信息和球员每场的技术统计
- 球队是操作主体 -> 用户系统、球员交易系统
- 球迷 -> 会员系统、喜爱球员
- 新闻 -> 球员标签、球队标签
- 比赛数据 -> 球员单场数据 -> 球队数据
- 爬虫数据 -> 爬取hupu、nba.office
- 代码：https://github.com/TigrexR/hupu


讲清楚项目中所使用技术，相关最佳实践，总体罗列之后配合重点解析





相亲 1、见个面 -> 聊一下工作，境况、熟悉下兴趣，
如果 -> 还能聊 、继续了解双方、沟通兴趣事实
 -> 聊不下去，gg
然后 -> 如果沟通三观差不多，能接受、那就生活中更多的接触
最难受的就是尬聊、那真是疯狂将耐心

现在就是每天聊铁三样，忙不忙、身体状况、
她也不问我我的兴趣啥的
她喜欢哈利波特、看哥哥、然后就是说下一天的工作状态、看东周、生日
