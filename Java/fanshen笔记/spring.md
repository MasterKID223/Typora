[Spring核心编程_spring项目怎么写核心代码-CSDN博客](https://blog.csdn.net/u013794243/article/details/124542138?spm=1001.2014.3001.5502)

[【一篇搞懂】Sping 容器启动过程详解 - 沙滩de流沙 - 博客园 (cnblogs.com)](https://www.cnblogs.com/imok520/p/16411315.html)

[Spring中的“三级缓存”_spring三级缓存-CSDN博客](https://blog.csdn.net/weixin_44181671/article/details/108630950)

[Spring进阶（十六）之spring生命周期_spring的生命周期的六个阶段-CSDN博客](https://blog.csdn.net/weixin_56644618/article/details/127366307)

[Spring事件详解，Spring-Event源码详解，一文搞透Spring事件管理_spring event源码-CSDN博客](https://blog.csdn.net/A_art_xiang/article/details/128789087)

[Component注解的派生性原理 - 海渊 - 博客园 (cnblogs.com)](https://www.cnblogs.com/liuenyuan1996/p/11134827.html)

[Spring的@Bean注解原理详解_spring @bean-CSDN博客](https://blog.csdn.net/qq_34203492/article/details/126505543)

[spring mvc之注解@EnableWebMvc-CSDN博客](https://blog.csdn.net/x763795151/article/details/85252540)

[spring成神之路第五十五篇：spring 上下文生命周期 - 程序员小明1024 - 博客园 (cnblogs.com)](https://www.cnblogs.com/konglxblog/p/15522298.html)

# <font style="color:rgb(51, 51, 51);">我的小小总结</font>
### <font style="color:rgb(51, 51, 51);">常用接口</font>
```plain
DefaultListableBeanFactory beanFactory = new DefaultListableBeanFactory();//创建一个beanFactory，是beanFactory的默认实现，这个类可以进行层次查找、列表查找等工作。这里创建的beanFactory里面啥都没有，可以在后面将xml里的东西或代码里的类加进去。
 ApplicationContext context = new ClassPathXmlApplicationContext("classpath:bean-create.xml");
 AutowireCapableBeanFactory beanFactory = context.getAutowireCapableBeanFactory();
 
 AnnotationConfigApplicationContext applicationContext = new AnnotationConfigApplicationContext();
 applicationContext.register(TypeSafetyDependencyLookupDemo.class);//将这个类作为配置类注册到注解上下文容器里
 applicationContext.refresh();//这个函数会启动应用上下文。里面会进行各种初始化。注意这里会将实现了PostProcessor接口的Bean加载到对应的成员变量上，从而在创建Bean时调用对应的钩子方法。
 
 //延迟加载Bean
 ObjectFactory<User> objectFactory = (0bjectFactory<User>) beanFactory.getBean( "objectFactory");
 User user =objectFactory.getObject();
 
 //注册Bean
 context.register(AnnotationBeanDefinitionDemo.class);
 context.registerBean("config", Config.class);
 registry.registerBeanDefinition(beanName, definition);
 
 //实例化bean（几种方法：构造器、静态工厂、Bean工厂、FactoryBean），详见笔记
 context.getBean("user", User.class)
 context.getBean("factoryUser")
 context.getBean("userByFactoryBean")
```

# <font style="color:rgb(51, 51, 51);">接口大全</font>
# <font style="color:rgb(51, 51, 51);">IoC</font>
### <font style="color:rgb(51, 51, 51);">IoC发展简史</font>
<font style="color:rgb(51, 51, 51);">IoC是软件工程中的一种编程风格或编程原则。</font>

### <font style="color:rgb(51, 51, 51);">实现IoC的集中方式</font>
1. <font style="color:rgb(51, 51, 51);">服务定位模式，JavaEE中的一种模式，通常通过JNDI获取JavaEE的组件</font>
2. <font style="color:rgb(51, 51, 51);">依赖注入</font>
3. <font style="color:rgb(51, 51, 51);">上下文查询：JavaBeans里的beancontext（依赖查找）</font>
4. <font style="color:rgb(51, 51, 51);">模板方法模式：JDBC里的JDBCTemplate</font>
5. <font style="color:rgb(51, 51, 51);">策略模式</font>

### <font style="color:rgb(51, 51, 51);">IoC的目的</font>
1. <font style="color:rgb(51, 51, 51);">实现于执行的任务的解耦</font>
2. <font style="color:rgb(51, 51, 51);">让模块得以只关注于这个模块设计的目的</font>
3. <font style="color:rgb(51, 51, 51);">让模块之间的合作不再那么依赖于某个协议</font>
4. <font style="color:rgb(51, 51, 51);">减少取消某个模块产生的副作用</font>

### <font style="color:rgb(51, 51, 51);">通用职责</font>
<font style="color:rgb(51, 51, 51);">依赖处理：依赖查找、依赖注入</font>

<font style="color:rgb(51, 51, 51);">生命周期管理：容器、托管的资源（如Bean和POJO、自己加入的时间监听器）</font>

<font style="color:rgb(51, 51, 51);">配置：容器的配置、外部化配置、托管的资源</font>

### <font style="color:rgb(51, 51, 51);">主要实现</font>
<font style="color:rgb(51, 51, 51);">Java SE：Bean、Java ServiceLoader SPI、JNDI</font>

<font style="color:rgb(51, 51, 51);">Java EE：EJB、Servlet</font>

<font style="color:rgb(51, 51, 51);">开源：Apache Avalon、Spring Framework</font>

### <font style="color:rgb(51, 51, 51);">JavaBeans 作为IoC容器</font>
<font style="color:rgb(51, 51, 51);">特性：依赖查找、生命周期管理、配置元信息、事件、自定义、资源管理、持久化</font>

<font style="color:rgb(51, 51, 51);">Java Beans和Spring Beans的区别：</font><u><font style="color:rgb(51, 51, 51);">Java Beans是符合特定规范的Java类，用于在Java应用程序中封装数据和功能。</font></u><font style="color:rgb(51, 51, 51);">具有无参构造函数、私有属性以及公共的getter和setter方法。</font><u><font style="color:rgb(51, 51, 51);">Spring Beans是Spring框架中的组件，用于实现依赖注入和控制反转（IoC）的机制。</font></u>

##### <font style="color:rgb(51, 51, 51);">什么是JavaBean？</font>
+ <font style="color:rgb(51, 51, 51);">将字段称为Property</font>
+ <font style="color:rgb(51, 51, 51);">BeanInfo：javaBeans的一个api：</font>

```plain
BeanInfo beanInfo = Introspector.getBeanInfo(Person.class);
//存储了Bean的一些信息
Stream.of(beanInfo.getPropertyDescriptors()).forEach(propertyDescriptor ->
   {System.out.printin(propertyDescriptor);}
);		//getPropertyDescriptors()可以返回Bean的各种信息。
```

### <font style="color:rgb(51, 51, 51);">依赖查找与依赖注入的对比</font>
### <font style="color:rgb(51, 51, 51);">构造器注入 vs Setter注入（还有个字段注入）</font>
```plain
@Component
public class MyClass {		//构造器注入
    
    private MyDependency dependency;

    @Autowired
    public MyClass(MyDependency dependency) {
        this.dependency = dependency;
    }

    // ...
}

@Component
public class MyClass {		//Setter注入
    private MyDependency dependency;

    @Autowired
    public void setDependency(MyDependency dependency) {
        this.dependency = dependency;
    }

    // ...
}
```

<font style="color:rgb(51, 51, 51);">官方推荐使用构造器注入</font>

1. <font style="color:rgb(51, 51, 51);">构造器注入（Constructor Injection）：</font>
    - <font style="color:rgb(51, 51, 51);">优点：</font>
        * <font style="color:rgb(51, 51, 51);">显式地声明依赖关系，使得</font><font style="color:rgb(0, 0, 0);background-color:rgb(0, 191, 255);">代码的可读性更好</font><font style="color:rgb(51, 51, 51);">。</font>
        * <font style="color:rgb(51, 51, 51);">强制依赖关系的必要性，</font><font style="color:rgb(0, 0, 0);background-color:rgb(0, 191, 255);">确保在对象创建时所有必需的依赖项都被提供</font><font style="color:rgb(51, 51, 51);">。</font>
        * <font style="color:rgb(0, 0, 0);background-color:rgb(0, 191, 255);">可以保证类中的属性不会被修改，及保证不可变性</font><font style="color:rgb(51, 51, 51);">	</font><font style="color:rgb(51, 51, 51);">//这里的不可变是指要创建的对象不可变，不是要注入的对象不可变</font>
    - <font style="color:rgb(51, 51, 51);">缺点：</font>
        * <font style="color:rgb(51, 51, 51);">需要编写更多的代码，包括定义构造器和相应的成员变量，并在每个依赖关系上进行初始化。</font>
        * <font style="color:rgb(51, 51, 51);">参数过多的时候看起来不太好</font>
2. <font style="color:rgb(51, 51, 51);">Setter注入（Setter Injection）：</font>
    - <font style="color:rgb(51, 51, 51);">优点：</font>
        * <font style="color:rgb(51, 51, 51);">灵活性较高，可以方便地添加、移除或更改依赖关系。</font>
        * <font style="color:rgb(51, 51, 51);">对于可选的依赖关系，Setter注入可以更好地处理。</font>
    - <font style="color:rgb(51, 51, 51);">缺点：</font>
        * <font style="color:rgb(51, 51, 51);">对象的状态可能变得不稳定，因为依赖关系可以在任何时候进行更改。</font>
        * <font style="color:rgb(51, 51, 51);">可能需要编写更多的代码来定义Setter方法并在每个依赖关系上进行设置。</font>
3. <font style="color:rgb(51, 51, 51);">字段注入（Field Injection）：</font>
    - <font style="color:rgb(51, 51, 51);">优点：</font>
        * <font style="color:rgb(51, 51, 51);">代码简洁，不需要为每个依赖关系编写构造器或Setter方法。</font>
        * <font style="color:rgb(51, 51, 51);">适用于依赖关系是可选的、可变的或通过反射注入的情况。</font>
    - <font style="color:rgb(51, 51, 51);">缺点：</font>
        * <font style="color:rgb(51, 51, 51);">封装性较差，依赖关系直接暴露在公共字段上，不利于封装和测试。</font>
        * <font style="color:rgb(51, 51, 51);">依赖关系的可见性和可变性可能增加了代码的复杂性和维护难度。</font>

<font style="color:rgb(51, 51, 51);">@AutoWired可以通过设置required属性（true or false）设置是否可以注入空属性。</font>

### <font style="color:rgb(51, 51, 51);">Spring loC 依赖查找</font>
+ <font style="color:rgb(51, 51, 51);">根据 Bean 名称(id)查找</font>
    - <font style="color:rgb(51, 51, 51);">实时查找</font>
    - <font style="color:rgb(51, 51, 51);">延迟查找</font>
+ <font style="color:rgb(51, 51, 51);">根据 Bean 类型查找</font>
    - <font style="color:rgb(51, 51, 51);">单个 Bean 对象</font>
    - <font style="color:rgb(51, 51, 51);">集合 Bean 对象</font>
+ <font style="color:rgb(51, 51, 51);">根据 Bean 名称 +类型查找</font>
+ <font style="color:rgb(51, 51, 51);">根据 Java 注解查找</font>
    - <font style="color:rgb(51, 51, 51);">单个 Bean 对象</font>
    - <font style="color:rgb(51, 51, 51);">集合Bean 对象</font>

```plain
public class DependencyLookupDemo {
    public static void main(String[] args) {
        // 配置 XML 配置文件
        //启动 Spring 应用上下文
        BeanFactory beanFactory = new ClassPathXmlApplicationContext("classpath:/META-INF/dependency-lookup-context,xml");
        lookupInRealTime(beanFactory);
        lookupInLazy(beanFactory);
        lookupCollectionByType(beanFactory);
         
    }
    private static void lookupCollectionByType(BeanFactory beanFactory){
        if (beanFactory instanceof ListableBeanFactory) {
            ListableBeanFactory listableBeanFactory = (ListableBeanFactory) beanFactor;
            Map<String，User> users = (Map)listableBeanFactory.getBeansWithAnnotation(Super.class);
            System.out.println("查找到的所有的 User 集合对象:" + uers);
        }
    }
    
    privatestatic void lookupByAnnotationType(BeanFactory beanFactory){
        if (beanFactory instanceof ListableBeanFactory) {
            ListableBeanFactory listableBeanFactory = (ListableBeanFactory) beanFactory;
            Map<String，User> users = listableBeanFactory.getBeans0fType(User.class);
            System.out.println("查找到的所有的 User 集合对象:" + users);
        }
    }
    
    private static void lookupInLazy(BeanFactory beanFactory){
        ObjectFactory<User> objectFactory = (0bjectFactory<User>) beanFactory.getBean( "objectFactory");
        User user =objectFactory.getObject();
        System.out.println("延迟查找:"+ user);
    }
    
    private static void lookupInRealTime(BeanFactory beanFactory) {
        User user =(User) beanFactory.getBean("user");
        System.out.println("实时查找查找:" + user);  
    }
    
    
}
```

### <font style="color:rgb(51, 51, 51);">Spring loc 依赖注入</font>
+ <font style="color:rgb(51, 51, 51);">根据 Bean 名称注入: 在bean里使用</font><font style="color:rgb(51, 51, 51);"><</font><font style="color:rgb(51, 51, 51);">property</font><font style="color:rgb(51, 51, 51);">></font><font style="color:rgb(51, 51, 51);">标签设置属性依赖的bean</font>
+ <font style="color:rgb(51, 51, 51);">根据 Bean 类型注入: 在bean上设置属性 autowired = "byType"</font>
    - <font style="color:rgb(51, 51, 51);">单个 Bean 对象</font>
    - <font style="color:rgb(51, 51, 51);">集合Bean 对象</font>
+ <font style="color:rgb(51, 51, 51);">注入容器内建 Bean 对象</font>
+ <font style="color:rgb(51, 51, 51);">注入非 Bean 对象: 如按类型自动注入FactoryBean对象,(得到的不是Bean,是内建依赖)</font>
+ <font style="color:rgb(51, 51, 51);">注入类型</font>
    - <font style="color:rgb(51, 51, 51);">实时注入</font>
    - <font style="color:rgb(51, 51, 51);">延迟注入</font>

### <font style="color:rgb(51, 51, 51);">Spring loC 依赖来源</font>
<font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">BeanFactory beanFactory = new ClassPathXmlApplicationContext( cnig.ocaton: "classpath:/META-INF/dependency-injection-ontextxml");</font>

1. <font style="color:rgb(51, 51, 51);">自定义Bean</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">UserRepository userRespository= beanFactory.getBean( "userRepository",UserRepository.class);</font>
2. <font style="color:rgb(51, 51, 51);">容器内建Bean</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">System.out.println(userRepository.getBeanFactory());</font>
3. <font style="color:rgb(51, 51, 51);">容器内建依赖</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">Environment environment = beanFactory.getBean(Environment.class);</font>

### <font style="color:rgb(51, 51, 51);">Spring loc 配置元信息</font>
+ <font style="color:rgb(51, 51, 51);">Bean 定义配置</font>
    - <font style="color:rgb(51, 51, 51);">基于XML文件</font>
    - <font style="color:rgb(51, 51, 51);">基于 Properties 文件</font>
    - <font style="color:rgb(51, 51, 51);">基于Java注解</font>
    - <font style="color:rgb(51, 51, 51);">基于 Java API(专题讨论)</font>
+ <font style="color:rgb(51, 51, 51);">loC 容器配置</font>
    - <font style="color:rgb(51, 51, 51);">基于XML文件</font>
    - <font style="color:rgb(51, 51, 51);">基于Java注解</font>
    - <font style="color:rgb(51, 51, 51);">基于 Java API(专题讨论)</font>
+ <font style="color:rgb(51, 51, 51);">外部化属性配置</font>
    - <font style="color:rgb(51, 51, 51);">基于Java注解</font>

### <font style="color:rgb(51, 51, 51);">Spring loC 容器</font>
<font style="color:rgb(51, 51, 51);">BeanFactory 和 ApplicationContext哪个才是IoC容器?</font>

<font style="color:rgb(51, 51, 51);">ApplicationContext是BeanFactory的子接口.即BeanFactory是一个基本的IoC容器,ApplicationContext提供了更多的企业级功能(如AOP更好的整合,国际化支持,事务的发布).</font>

<font style="color:rgb(51, 51, 51);">ApplicationContext里面组合了一个BeanFactory实现(他俩只是复用了一个接口),所以最好直接用ApplicationContext的getBeanFactory方法.</font>

### <font style="color:rgb(51, 51, 51);">Spring 应用上下文(ApplicationContext)</font>
<font style="color:rgb(51, 51, 51);">ApplicationContext除了BeanFactory有的功能,还提供了:</font>

<font style="color:rgb(51, 51, 51);">面向切面 (AOP)</font><font style="color:rgb(51, 51, 51);">配置元信息 (Configuration Metadata)</font><font style="color:rgb(51, 51, 51);">资源管理 (Resources)</font><font style="color:rgb(51, 51, 51);">事件(Events)</font><font style="color:rgb(51, 51, 51);">国际化 (i18n)</font><font style="color:rgb(51, 51, 51);">注解(Annotations)</font><font style="color:rgb(51, 51, 51);">Environment 抽象 (Environment Abstraction)</font>

### <font style="color:rgb(51, 51, 51);">使用 Spring loC 容器</font>
<font style="color:rgb(51, 51, 51);">BeanFactory是Spring底层的IoC容器.ApplicationContext是具有具体特性的BeanFactory的超集. </font>

<font style="color:rgb(51, 51, 51);">只获取XML中的Bean,且不用AOP等特性时用BeanFactory就够了.</font>

<font style="color:rgb(51, 51, 51);">获取注解方式定义的Bean必须使用applicationContext.</font>

### <font style="color:rgb(51, 51, 51);">Spring loC 容器生命周期</font>
+ <font style="color:rgb(51, 51, 51);">启动</font>
    1. <font style="color:rgb(51, 51, 51);">调用applicationContext.refresh(),启动容器</font>
+ <font style="color:rgb(51, 51, 51);">运行</font>
+ <font style="color:rgb(51, 51, 51);">停止</font>

# <font style="color:rgb(51, 51, 51);">SpringBean基础</font>
### <font style="color:rgb(51, 51, 51);">定义 Spring Bean</font>
<font style="color:rgb(51, 51, 51);">什么是 </font><u><font style="color:rgb(51, 51, 51);">BeanDefinition</font></u><font style="color:rgb(51, 51, 51);">?</font><font style="color:rgb(0, 0, 0);background-color:rgb(0, 191, 255);">BeanDefinition 是Spring Framework 中定义 Bean 的配置元信息接口</font><font style="color:rgb(51, 51, 51);">，包含:</font>

+ <font style="color:rgb(51, 51, 51);">Bean的类名</font>
+ <font style="color:rgb(51, 51, 51);">Bean 行为配置元素，如作用域、自动绑定的模式、生命周期回调等</font>
+ <font style="color:rgb(51, 51, 51);">其他 Bean 引用，又可称作合作者 (Collaborators)或者依赖 (Dependencies)</font>
+ <font style="color:rgb(51, 51, 51);">配置设置，比如 Bean 属性 (Properties)</font>

### <font style="color:rgb(51, 51, 51);">BeanDefinition 元信息</font>
<font style="color:rgb(51, 51, 51);">如何构建BeanDefinition？</font>

+ <font style="color:rgb(51, 51, 51);">通过BeanDefinitionBuilder</font>
+ <font style="color:rgb(51, 51, 51);">通过AbstractBeanDefinition以及派生类</font>

### <font style="color:rgb(51, 51, 51);">命名 Spring Bean</font>
<font style="color:rgb(51, 51, 51);">每个Bean拥有一个或多个识别符，每个容器内的识别符是唯一的。</font>

<font style="color:rgb(51, 51, 51);">Spring Framework 2.0.3引入BeanNameGenerator（名称生成器）接口。</font>

<font style="color:rgb(51, 51, 51);">内建实现：DefaultBeanNameGenerator</font>

<font style="color:rgb(51, 51, 51);">AnnotationBeanNameGenerator（2.5以后）</font>

<font style="color:rgb(51, 51, 51);">若无指定名称，则会通过名称生成器自己生成一个。</font>

### <font style="color:rgb(51, 51, 51);">Spring Bean 的别名（Alias）</font>
### <font style="color:rgb(51, 51, 51);">注册 Spring Bean</font>
### <font style="color:rgb(51, 51, 51);">实例化 Spring Bean</font>
<font style="color:rgb(0, 0, 0);background-color:rgb(0, 191, 255);">构造器</font><font style="color:rgb(51, 51, 51);">： 略</font>

<font style="color:rgb(0, 0, 0);background-color:rgb(0, 191, 255);">静态工厂方法、Bean工厂方法和FactoryBean</font><font style="color:rgb(51, 51, 51);">：</font>

<font style="color:rgb(0, 0, 0);background-color:rgb(0, 191, 255);">ServiceLoaderFactoryBean</font><font style="color:rgb(51, 51, 51);">方式：从ServiceLoader里面加载FactoryBean，再从FactoryBean种获取Bean。</font>

```plain
ApplicationContext applicationContext = new ClassPathXmlApplicationContext("classpath:/SpringContextConfig.xml");

        AutowireCapableBeanFactory beanFactory = applicationContext.getAutowireCapableBeanFactory();
```

##### <font style="color:rgb(51, 51, 51);">BeanDefinition 注册</font>
+ <font style="color:rgb(51, 51, 51);">BeanDefinition 注册</font>
    - <font style="color:rgb(51, 51, 51);">XML 配置元信息</font>
        * <font style="color:rgb(51, 51, 51);"><bean name="...”... /></font>
    - <font style="color:rgb(51, 51, 51);">Java注解配置元信息</font>
        * <font style="color:rgb(51, 51, 51);">@Bean</font>
        * <font style="color:rgb(51, 51, 51);">@Component</font>
        * <font style="color:rgb(51, 51, 51);">@lmport</font>
    - <font style="color:rgb(51, 51, 51);">Java API配置元信息</font>
        * <font style="color:rgb(51, 51, 51);">命名方式: BeanDefinitionRegistry#registerBeanDefinition(String,BeanDefinition)</font>
        * <font style="color:rgb(51, 51, 51);">非命名方式:BeanDefinitionReaderUtils#registerWithGeneratedName(AbstractBeanDefinition,BeanfinitionRegistry)</font>
        * <font style="color:rgb(51, 51, 51);">配置类方式: AnnotatedBeanDefirReader#register(Class...</font>

### <font style="color:rgb(51, 51, 51);">初始化 Spring Bean </font>
<font style="color:rgb(51, 51, 51);">@PostConstruct:</font>

```plain
import javax.annotation.PostConstruct;

public class MyBean {

    private String name;

    public MyBean() {
        // 构造函数
    }

    @PostConstruct
    public void init() {
        // 在依赖注入完成后执行的初始化方法
        System.out.println("Initializing MyBean...");
        // 执行其他初始化逻辑...
    }

    // 其他方法和属性...

}
```

<font style="color:rgb(51, 51, 51);">从这里可以看出执行顺序：PostConstruct -> afterPropertiesSet -> 自定义的init方法。</font>

### <font style="color:rgb(51, 51, 51);">延迟初始化 Spring Bean</font>
<font style="color:rgb(51, 51, 51);">非延迟初始化在Spring应用上下文启动后（applicationContext.refresh()时）。</font>

<font style="color:rgb(51, 51, 51);">延迟初始化在需要用这个bean的时候初始化。</font>

### <font style="color:rgb(51, 51, 51);">销毁 Spring Bean</font>
### <font style="color:rgb(51, 51, 51);">垃圾回收 Spring Bean</font>
1. <font style="color:rgb(51, 51, 51);">applicationContext.close();</font>
2. <font style="color:rgb(51, 51, 51);">System.gc();</font>
3. <font style="color:rgb(51, 51, 51);">重写finalize()方法，则方法里的逻辑可能（不一定，JVM里说的，至于为啥不知道）会在gc的时候被执行。</font>

# <font style="color:rgb(51, 51, 51);">Spring IoC依赖查找</font>
### <font style="color:rgb(51, 51, 51);">1.依赖查找的今世前生</font>
<font style="color:rgb(51, 51, 51);">单一类型</font>

+ <font style="color:rgb(51, 51, 51);">JNDI</font><font style="color:rgb(51, 51, 51);">javax.naming.Context#lookup(javax.naming.Name)</font>
+ <font style="color:rgb(51, 51, 51);">JavaBeans - java.beans.beancontext.BeanContext</font>

<font style="color:rgb(51, 51, 51);">集合类型</font>

+ <font style="color:rgb(51, 51, 51);">java.beans.beancontext.BeanContext</font>

<font style="color:rgb(51, 51, 51);">层次类型</font>

+ <font style="color:rgb(51, 51, 51);">java.beans.beancontext.BeanContext</font>

### <font style="color:rgb(51, 51, 51);">2.单一类型依赖查找</font>
<font style="color:rgb(51, 51, 51);">覆盖默认参数的方法不需要掌握，因为比较危险，一般不用。 </font>

<font style="color:rgb(51, 51, 51);">延迟查找：</font>

### <font style="color:rgb(51, 51, 51);">3.集合类型依赖查找</font>
### <font style="color:rgb(51, 51, 51);">4.层次性依赖查找</font>
<font style="color:rgb(51, 51, 51);">• 层次性依赖查找接口 - HierarchicalBeanFactory </font>

<font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);">• 双亲 BeanFactory：getParentBeanFactory() </font>

<font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);">• 层次性查找</font>

<font style="color:rgb(51, 51, 51);">				</font><font style="color:rgb(51, 51, 51);"> • 根据 Bean 名称查找 </font>

<font style="color:rgb(51, 51, 51);">							</font><font style="color:rgb(51, 51, 51);">• 基于 containsLocalBean 方法实现 </font>

<font style="color:rgb(51, 51, 51);">				</font><font style="color:rgb(51, 51, 51);">• 根据 Bean 类型查找实例列表 </font>

<font style="color:rgb(51, 51, 51);">							</font><font style="color:rgb(51, 51, 51);">• 单一类型：BeanFactoryUtils#beanOfType </font>

<font style="color:rgb(51, 51, 51);">							</font><font style="color:rgb(51, 51, 51);">• 集合类型：BeanFactoryUtils#beansOfTypeIncludingAncestors </font>

<font style="color:rgb(51, 51, 51);">				</font><font style="color:rgb(51, 51, 51);">• 根据 Java 注解查找名称列表 </font>

<font style="color:rgb(51, 51, 51);">							</font><font style="color:rgb(51, 51, 51);">• BeanFactoryUtils#beanNamesForTypeIncludingAncestors</font>

<font style="color:rgb(51, 51, 51);">层次性查找（Hierarchical Lookup）是一种查找依赖对象的机制。它允许在多个层次结构中查找对象，而不仅限于单个层次结构。</font>

```plain
设置父容器：
        HierarchicalBeanFactory parentBeanFactory = createParentBeanFactory();
        beanFactory.setParentBeanFactory(parentBeanFactory);
层次查找Bean：
    	beanFactory.containsLocalBean(beanName)	//不查找父容器	
    	beanFactory.containsBean(beanName)		//查找父容器
```

### <font style="color:rgb(51, 51, 51);">5.延迟依赖查找</font>
<font style="color:rgb(51, 51, 51);">一种通过延迟加载的方式获取Bean的策略。通常情况下，Spring容器在初始化时会预先创建和初始化所有的Bean，但有时候我们希望在需要使用某个Bean时再进行实际的创建和初始化，以提高性能和节省资源。</font>

<font style="color:rgb(51, 51, 51);">使用</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">ObjectFactory</font><font style="color:rgb(51, 51, 51);">或</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">ObjectProvider</font><font style="color:rgb(51, 51, 51);">：</font>

```plain
@Autowired
private ObjectProvider<BeanA> beanAProvider;

public void doSomething() {
    BeanA beanA = beanAProvider.getObject();
    // 使用beanA
}
```
在上述示例中，通过`ObjectProvider`接口延迟查找了`BeanA`的实例。`ObjectProvider`会在需要时动态创建和返回`BeanA`的实例。
```

<font style="color:rgb(51, 51, 51);">使用</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">@Lazy</font><font style="color:rgb(51, 51, 51);">注解:</font>

```plain
@Lazy
@Component
public class BeanA {
    // ...
}
```
在上述示例中，`BeanA`被标记为`@Lazy`，表示该Bean在容器初始化时不会被立即创建和初始化，而是在第一次使用时才会被实际创建和初始化。
```

### <font style="color:rgb(51, 51, 51);">6.类型安全依赖查找</font>
<font style="color:rgb(51, 51, 51);">不安全的意思是这俩会抛出异常？？？</font>

### <font style="color:rgb(51, 51, 51);">7.内建可查找的依赖</font>
### <font style="color:rgb(51, 51, 51);">8.依赖查找中的经典异常</font>
# <font style="color:rgb(51, 51, 51);">依赖注入</font>
### <font style="color:rgb(51, 51, 51);">1. 模式和类型 </font>
<font style="color:rgb(51, 51, 51);">• 手动模式 - 配置或者编程的方式，提前安排注入规则</font>

```plain
• XML 资源配置元信息

	• Java 注解配置元信息
```

<font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);"> • API 配置元信息</font>

<font style="color:rgb(51, 51, 51);">• 自动模式 - 实现方提供依赖自动关联的方式，按照內建的注入规则 </font>

<font style="color:rgb(51, 51, 51);">	</font><font style="color:rgb(51, 51, 51);">	</font><font style="color:rgb(51, 51, 51);">• Autowiring（自动绑定）</font>

### <font style="color:rgb(51, 51, 51);">2. 自动绑定（Autowiring） </font>
### <font style="color:rgb(51, 51, 51);">3. 自动绑定（Autowiring）模式 </font>
```plain
<bean id="userRepository" class="org.geekbang.thinking.in.spring.ioc.overview.repository.UserRepository"
          autowire="byType"> <!-- Auto-Wiring -->
        <!-- 手动配置 -->
        <!--        <property name="users">-->
        <!--            <util:list>-->
        <!--                <ref bean="superUser" />-->
        <!--                <ref bean="user" />-->
        <!--            </util:list>-->
        <!--        </property>-->

    </bean>
```

### <font style="color:rgb(51, 51, 51);">4. 自动绑定（Autowiring）限制和不足</font>
1. <font style="color:rgb(51, 51, 51);">构造器或preporty的设置会覆盖掉autowire的属性</font>

```plain
2. 不能绑定简单类型包括String、class类型
2. 需要精确性，万一bean名称搞错了或是有父子类可能会绑定到其他bean上去。
2. 不好生成文档
```

### <font style="color:rgb(51, 51, 51);">5. Setter 方法依赖注入（Spring默认是Setter注入）</font>
<font style="color:rgb(51, 51, 51);">• 实现方法</font>

<font style="color:rgb(51, 51, 51);">	</font><font style="color:rgb(51, 51, 51);"> • 手动模式</font>

<font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);">• XML 资源配置元信息 </font>

<font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);">• Java 注解配置元信息 </font>

<font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);">• API 配置元信息 </font>

<font style="color:rgb(51, 51, 51);">• 自动模式 </font>

<font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);">• byName </font>

<font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);">• byType</font>

```plain
<bean class="org.geekbang.thinking.in.spring.ioc.dependency.injection.UserHolder">
    <property name="user" ref="superUser" /> 		<!-- UserHolder里面有设置user的setter方法 -->
</bean>
```

```plain
public class AnnotationDependencySetterInjectionDemo {

    public static void main(String[] args) {

        // 创建 BeanFactory 容器
        AnnotationConfigApplicationContext applicationContext = new AnnotationConfigApplicationContext();
        // 注册 Configuration Class（配置类）
        applicationContext.register(AnnotationDependencySetterInjectionDemo.class);

        XmlBeanDefinitionReader beanDefinitionReader = new XmlBeanDefinitionReader(applicationContext);

        String xmlResourcePath = "classpath:/META-INF/dependency-lookup-context.xml";
        // 加载 XML 资源，解析并且生成 BeanDefinition
        beanDefinitionReader.loadBeanDefinitions(xmlResourcePath);

        // 启动 Spring 应用上下文
        applicationContext.refresh();

        // 依赖查找并且创建 Bean
        UserHolder userHolder = applicationContext.getBean(UserHolder.class);
        System.out.println(userHolder);

        // 显示地关闭 Spring 应用上下文
        applicationContext.close();
    }

    @Bean
    public UserHolder userHolder(User user) {//传入的参数为配置的名称为user的bean。若没定义这个bean，则报错
        UserHolder userHolder = new UserHolder();
        userHolder.setUser(user);
        return userHolder;
    }
}
```

```plain
private static BeanDefinition createUserHolderBeanDefinition() {
        BeanDefinitionBuilder definitionBuilder = BeanDefinitionBuilder.genericBeanDefinition(UserHolder.class);
        definitionBuilder.addPropertyReference("user", "superUser");
        return definitionBuilder.getBeanDefinition();
    }
```

```plain
<bean class="org.geekbang.thinking.in.spring.ioc.dependency.injection.UserHolder"
          autowire="byType"
    >
<!--        <property name="user" ref="superUser" /> 替换成 autowiring 模式 -->
    </bean>
```

### <font style="color:rgb(51, 51, 51);">6. 构造器依赖注入</font>
<font style="color:rgb(51, 51, 51);">• 实现方法 </font>

<font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);">• 手动模式</font>

<font style="color:rgb(51, 51, 51);">				</font><font style="color:rgb(51, 51, 51);">• XML 资源配置元信息 </font>

<font style="color:rgb(51, 51, 51);">				</font><font style="color:rgb(51, 51, 51);">• Java 注解配置元信息 </font>

<font style="color:rgb(51, 51, 51);">				</font><font style="color:rgb(51, 51, 51);">• API 配置元信息 </font>

<font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);">• 自动模式 </font>

<font style="color:rgb(51, 51, 51);">				</font><font style="color:rgb(51, 51, 51);">• constructor</font>

```plain
<bean class="org.geekbang.thinking.in.spring.ioc.dependency.injection.UserHolder" >
        <constructor-arg name="user" ref="superUser" /> <!--替换成 autowiring 模式 -->
    </bean>
```

```plain
//将setter注入中的稍微改一下    
@Bean
public UserHolder userHolder(User user) {//传入的参数为配置的名称为user的bean。若没定义这个bean，则报错
    UserHolder userHolder = new UserHolder(user);
    return userHolder;
}
```

```plain
//将setter注入中的稍微改一下    
private static BeanDefinition createUserHolderBeanDefinition() {
    BeanDefinitionBuilder definitionBuilder = BeanDefinitionBuilder.genericBeanDefinition(UserHolder.class);
    definitionBuilder.addConstructorArgReference("superUser");
    return definitionBuilder.getBeanDefinition();
}
```

```plain
<bean class="org.geekbang.thinking.in.spring.ioc.dependency.injection.UserHolder"
          autowire="constructor">
        <!--        <property name="user" ref="superUser" /> 替换成 autowiring 模式 -->
    </bean>
```

### <font style="color:rgb(51, 51, 51);">7. 字段注入 </font>
<font style="color:rgb(51, 51, 51);">• 实现方法</font>

<font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);"> • 手动模式</font>

<font style="color:rgb(51, 51, 51);">				</font><font style="color:rgb(51, 51, 51);"> • Java 注解配置元信息</font>

<font style="color:rgb(51, 51, 51);">						</font><font style="color:rgb(51, 51, 51);">• @Autowired </font>

<font style="color:rgb(51, 51, 51);">						</font><font style="color:rgb(51, 51, 51);">• @Resource </font>

<font style="color:rgb(51, 51, 51);">						</font><font style="color:rgb(51, 51, 51);">• @Inject（可选）</font>

1. <font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">@Autowired</font><font style="color:rgb(51, 51, 51);"> 是Spring框架的注解，它通过byType的方式进行自动装配。它会根据类型自动查找并注入相应的Bean。如果存在多个匹配的Bean，它会根据特定的解析规则进行选择注入。</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">@Autowired</font><font style="color:rgb(51, 51, 51);"> 注解还可以用于构造函数、方法、字段和参数上。</font>
2. <font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">@Resource</font><font style="color:rgb(51, 51, 51);"> 是Java EE的注解，也可以用于自动装配Bean。它支持byName和byType两种方式进行自动装配。当使用 </font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">@Resource</font><font style="color:rgb(51, 51, 51);"> 注解时，可以通过 </font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">name</font><font style="color:rgb(51, 51, 51);"> 属性指定要注入的Bean的名称，或者通过 </font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">type</font><font style="color:rgb(51, 51, 51);"> 属性指定要注入的Bean的类型。如果没有指定这两个属性，则默认按照byName的方式进行自动装配。</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">@Resource</font><font style="color:rgb(51, 51, 51);"> 注解可以应用在字段、方法和参数上。</font>
3. <font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">@Inject</font><font style="color:rgb(51, 51, 51);"> 是JSR-330规范定义的注解，也可以用于自动装配Bean。它与 </font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">@Autowired</font><font style="color:rgb(51, 51, 51);"> 的功能类似，都是通过byType的方式进行自动装配。但是，</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">@Inject</font><font style="color:rgb(51, 51, 51);"> 注解更加通用，可以用于Java EE和Java SE环境，而 </font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">@Autowired</font><font style="color:rgb(51, 51, 51);"> 注解是Spring特定的。</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">@Inject</font><font style="color:rgb(51, 51, 51);"> 注解可以应用在构造函数、方法、字段和参数上。</font>

```plain
@Autowired
private UserService userService;
@Resource
private UserService userService;
@Inject
private UserService userService;
```

### <font style="color:rgb(51, 51, 51);">8. 方法注入 </font>
<font style="color:rgb(51, 51, 51);">• 实现方法 </font>

<font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);">• 手动模式 </font>

<font style="color:rgb(51, 51, 51);">				</font><font style="color:rgb(51, 51, 51);">• Java 注解配置元信息</font>

<font style="color:rgb(51, 51, 51);">						</font><font style="color:rgb(51, 51, 51);"> • @Autowired</font>

<font style="color:rgb(51, 51, 51);">						</font><font style="color:rgb(51, 51, 51);"> • @Resource </font>

<font style="color:rgb(51, 51, 51);">						</font><font style="color:rgb(51, 51, 51);"> • @Inject（可选） </font>

<font style="color:rgb(51, 51, 51);">						</font><font style="color:rgb(51, 51, 51);"> • @Bean</font>

```plain
@Autowired
    public void init1(UserHolder userHolder) {
        this.userHolder = userHolder;
    }

    @Resource
    public void init2(UserHolder userHolder2) {
        this.userHolder2 = userHolder2;
    }
```

### <font style="color:rgb(51, 51, 51);">9. 回调注入 </font>
```plain
public class AwareInterfaceDependencyInjectionDemo implements BeanFactoryAware, ApplicationContextAware {

    private static BeanFactory beanFactory;

    private static ApplicationContext applicationContext;


    public static void main(String[] args) {

        // 创建 BeanFactory 容器
        AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext();
        // 注册 Configuration Class（配置类） -> Spring Bean
        context.register(AwareInterfaceDependencyInjectionDemo.class);

        // 启动 Spring 应用上下文
        context.refresh();

        System.out.println(beanFactory == context.getBeanFactory());
        System.out.println(applicationContext == context);

        // 显示地关闭 Spring 应用上下文
        context.close();
    }

    @Override
    public void setBeanFactory(BeanFactory beanFactory) throws BeansException {
        AwareInterfaceDependencyInjectionDemo.beanFactory = beanFactory;
    }

    @Override
    public void setApplicationContext(ApplicationContext applicationContext) throws BeansException {
        AwareInterfaceDependencyInjectionDemo.applicationContext = applicationContext;
    }
}
```

### <font style="color:rgb(51, 51, 51);">10. 依赖注入类型选择 </font>
<font style="color:rgb(51, 51, 51);">低依赖：构造器注入 </font>

<font style="color:rgb(51, 51, 51);">多依赖：Setter 方法注入 </font><font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);">有个缺点：注入时机取决于用户操作，可能会出问题。</font>

<font style="color:rgb(51, 51, 51);">便利性：字段注入 </font>

<font style="color:rgb(51, 51, 51);">声明类：方法注入</font>

### <font style="color:rgb(51, 51, 51);">11. 基础类型注入 </font>
<font style="color:rgb(51, 51, 51);">原生类型（Primitive）：boolean、byte、char、short、int、float、long、double </font>

<font style="color:rgb(51, 51, 51);">标量类型（Scalar）：Number、Character、Boolean、Enum、Locale、Charset、Currency、 Properties、UUID </font>

<font style="color:rgb(51, 51, 51);">常规类型（General）：Object、String、TimeZone、Calendar、Optional 等</font>

<font style="color:rgb(51, 51, 51);">Spring 类型：Resource、InputSource、Formatter 等</font>

<font style="color:rgb(51, 51, 51);">基本上就是将配置的字符串转换成需要注入的类型。</font>

### <font style="color:rgb(51, 51, 51);">12. 集合类型注入 </font>
<font style="color:rgb(51, 51, 51);">数组类型（Array）：原生类型、标量类型、常规类型、Spring 类型</font>

<font style="color:rgb(51, 51, 51);">集合类型（Collection） </font>

<font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);">• Collection：List、Set（SortedSet、NavigableSet、EnumSet）</font>

<font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);">• Map：Properties</font>

```plain
<bean id="user" class="org.geekbang.thinking.in.spring.ioc.overview.domain.User">
    <property name="id" value="1"/>
    <property name="name" value="小马哥"/>
    <property name="city" value="HANGZHOU"/>
    <property name="workCities" value="BEIJING,HANGZHOU"/>
    <property name="lifeCities">
        <list>
            <value>BEIJING</value>
            <value>SHANGHAI</value>
        </list>
    </property>
    <property name="configFileLocation" value="classpath:/META-INF/user-config.properties"/>
</bean>
```

```plain
City[] workCities;
	List<City> lifeCities;
```

### <font style="color:rgb(51, 51, 51);">13. 限定注入</font>
<font style="color:rgb(51, 51, 51);">• 使用注解 @Qualifier 限定 </font>

<font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);">• 通过 Bean 名称限定 </font>

<font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);">• 通过分组限定 </font>

<font style="color:rgb(51, 51, 51);">• 基于注解 @Qualifier 扩展限定 </font>

<font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);">• 自定义注解 - 如 Spring Cloud @LoadBalanced</font>

```plain
@Autowired
    private User user; // superUser -> primary =true

    @Autowired
    @Qualifier("user") // 指定 Bean 名称或 ID
    private User namedUser;

    // 整体应用上下文存在 4 个 User 类型的 Bean:
    // superUser
    // user
    // user1 -> @Qualifier
    // user2 -> @Qualifier

    @Autowired
    private Collection<User> allUsers; // 2 Beans = user + superUser

    @Autowired
    @Qualifier
    private Collection<User> qualifiedUsers; // 2 Beans = user1 + user2 -> 4 Beans = user1 + user2 + user3 + user4

    @Autowired
    @UserGroup
    private Collection<User> groupedUsers; // 2 Beans = user3 + user4

    @Bean
    @Qualifier // 进行逻辑分组
    public User user1() {
        return createUser(7L);
    }

    @Bean
    @Qualifier // 进行逻辑分组
    public static User user2() {
        return createUser(8L);

    }

    @Bean
    @UserGroup
    public static User user3() {
        return createUser(9L);
    }

    @Bean
    @UserGroup
    public static User user4() {
        return createUser(10L);
    }
```

```plain
@Target({ElementType.FIELD, ElementType.METHOD, ElementType.PARAMETER, ElementType.TYPE, ElementType.ANNOTATION_TYPE})
@Retention(RetentionPolicy.RUNTIME)
@Inherited
@Documented
@Qualifier
public @interface UserGroup {
}
```

### <font style="color:rgb(51, 51, 51);">14. 延迟依赖注入</font>
<font style="color:rgb(51, 51, 51);">• 使用 API ObjectFactory 延迟注入</font>

<font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);"> • 单一类型 </font>

<font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);"> • 集合类型 </font>

<font style="color:rgb(51, 51, 51);">• 使用 API ObjectProvider 延迟注入（推荐） ,这种方式可以避免NoSuchBeanException</font>

<font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);"> • 单一类型 </font>

<font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);"> • 集合类型 </font>

```plain
@Autowired
    private ObjectProvider<User> userObjectProvider; // 延迟注入

    @Autowired
    private ObjectFactory<Set<User>> usersObjectFactory;

    public static void main(String[] args) {

        // 创建 BeanFactory 容器
        AnnotationConfigApplicationContext applicationContext = new AnnotationConfigApplicationContext();
        // 注册 Configuration Class（配置类） -> Spring Bean
        applicationContext.register(LazyAnnotationDependencyInjectionDemo.class);

        XmlBeanDefinitionReader beanDefinitionReader = new XmlBeanDefinitionReader(applicationContext);

        String xmlResourcePath = "classpath:/META-INF/dependency-lookup-context.xml";
        // 加载 XML 资源，解析并且生成 BeanDefinition
        beanDefinitionReader.loadBeanDefinitions(xmlResourcePath);

        // 启动 Spring 应用上下文
        applicationContext.refresh();

        // 依赖查找 QualifierAnnotationDependencyInjectionDemo Bean
        LazyAnnotationDependencyInjectionDemo demo = applicationContext.getBean(LazyAnnotationDependencyInjectionDemo.class);

        // 期待输出 superUser Bean
        System.out.println("demo.user = " + demo.user);
        // 期待输出 superUser Bean
        System.out.println("demo.userObjectProvider = " + demo.userObjectProvider.getObject()); // 继承 ObjectFactory
        // 期待输出 superUser user Beans
        System.out.println("demo.usersObjectFactory = " + demo.usersObjectFactory.getObject());

        demo.userObjectProvider.forEach(System.out::println);


        // 显示地关闭 Spring 应用上下文
        applicationContext.close();
    }
```

### <font style="color:rgb(51, 51, 51);">15. 依赖处理过程 </font>
<font style="color:rgb(51, 51, 51);">基础知识 </font>

<font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);">入口 - DefaultListableBeanFactory#resolveDependency</font>

<font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);">依赖描述符 - DependencyDescriptor</font>

<font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);">自定绑定候选对象处理器 - AutowireCandidateResolver</font>

<font style="color:rgb(51, 51, 51);">(1) 在Spring的依赖注入过程中，当一个Bean需要依赖其他Bean时，Spring容器会调用</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">DefaultListableBeanFactory</font><font style="color:rgb(51, 51, 51);">的</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">resolveDependency</font><font style="color:rgb(51, 51, 51);">方法来解析这些依赖关系。</font>

public Object resolveDependency(DependencyDescriptor descriptor, String requestingBeanName, Set<String> autowiredBeanNames, TypeConverter typeConverter) throws BeansException

<font style="color:rgb(51, 51, 51);">参数说明：</font>

+ <font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">descriptor</font><font style="color:rgb(51, 51, 51);">：表示要解析的依赖描述符，其中包含了依赖的类型、注解等信息。</font>
+ <font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">requestingBeanName</font><font style="color:rgb(51, 51, 51);">：表示请求解析依赖的Bean的名称。</font>
+ <font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">autowiredBeanNames</font><font style="color:rgb(51, 51, 51);">：表示已经自动装配的Bean的名称集合。</font>
+ <font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">typeConverter</font><font style="color:rgb(51, 51, 51);">：用于执行类型转换的</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">TypeConverter</font><font style="color:rgb(51, 51, 51);">实例。</font>

<font style="color:rgb(51, 51, 51);">(2) </font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">DependencyDescriptor</font><font style="color:rgb(51, 51, 51);">是Spring框架中用于描述依赖关系的类。它包含了依赖的类型、注解、名称等信息，用于解析和获取依赖对象。</font>

```plain
`DependencyDescriptor`类具有以下成员变量（实例变量）：

 1. `MethodParameter methodParameter`：表示依赖的方法参数，包含了参数的类型、泛型信息等。
 2. `boolean required`：指示依赖是否为必需的。
 3. `boolean eager`：指示是否急切地解析依赖关系。
 4. `Annotation[] annotations`：表示依赖上的所有注解。
 5. `@Nullable String containingClassName`：依赖所在的类的名称。
 6. `@Nullable String methodName`：依赖所在的方法的名称。
 7. `@Nullable String fieldName`：依赖所在的字段的名称。
 8. `@Nullable ResolvableType resolvableType`：依赖的可解析类型。
 9. `@Nullable String[] typeIndexesPerLevel`：类型索引数组。
 10. `@Nullable Integer autowiredMethodType`：自动装配方法的类型。
```

<font style="color:rgb(51, 51, 51);">(3) </font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">AutowireCandidateResolver</font><font style="color:rgb(51, 51, 51);">是Spring框架中的一个接口，用于解析自动装配候选对象的策略。它定义了用于判断候选对象是否符合自动装配条件的方法。</font>

```plain
`AutowireCandidateResolver`接口的主要方法包括：

 1. `boolean isAutowireCandidate(BeanDefinitionHolder bdHolder, DependencyDescriptor descriptor)`：判断给定的Bean定义持有者（`BeanDefinitionHolder`）和依赖描述符（`DependencyDescriptor`）对应的Bean是否是自动装配的候选对象。返回值为`true`表示是候选对象，`false`表示不是候选对象。
 2. `Object getSuggestedValue(DependencyDescriptor descriptor)`：获取建议的值以满足给定的依赖描述符。如果无法提供建议值，则返回`null`。
 3. `boolean isRequired(DependencyDescriptor descriptor)`：判断给定的依赖描述符是否表示一个必需的依赖。返回值为`true`表示是必需的依赖，`false`表示不是必需的依赖。
```

##### <font style="color:rgb(51, 51, 51);">处理流程：</font>
1. <font style="color:rgb(51, 51, 51);">第一步：判断是否是延迟加载，是则返回代理对象（getAutowireCandidateResolver().getLazyResolutionProxyIfNecessary( </font><font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);">descriptor, requestingBeanName);）</font>
2. <font style="color:rgb(51, 51, 51);">第二步：判断是否是集合类型bean，是则返回该集合类型的bean</font>
3. <font style="color:rgb(51, 51, 51);">第三步：将找到所有符合条件的bean加入到map</font>
4. <font style="color:rgb(51, 51, 51);">第四步：对该map做判断：如果map的大小大于1，则去找有primary属性的bean；</font>
5. <font style="color:rgb(51, 51, 51);">第五步：获取到bean，然后返回</font>

### <font style="color:rgb(51, 51, 51);">16. @Autowired 注入原理</font>
<font style="color:rgb(51, 51, 51);">@Autowired 注入规则 </font>

<font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);">• 非静态字段 </font>

<font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);">• 非静态方法 </font>

<font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);">• 构造器</font>

<font style="color:rgb(51, 51, 51);">解析@Autowired的类AutowiredAnnotationBeanPostProcessor</font>

public class AutowiredAnnotationBeanPostProcessor extends InstantiationAwareBeanPostProcessorAdapter implements MergedBeanDefinitionPostProcessor, PriorityOrdered, BeanFactoryAware

<font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">@Autowired</font><font style="color:rgb(51, 51, 51);">是Spring框架中用于自动装配依赖的注解。通过</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">@Autowired</font><font style="color:rgb(51, 51, 51);">注解，Spring能够自动识别和注入相应的依赖对象。</font>

<font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">@Autowired</font><font style="color:rgb(51, 51, 51);">注解的注入原理如下：</font>

1. <font style="color:rgb(51, 51, 51);">依赖查找：当Spring容器启动时，会先通过Bean的名称或类型查找到对应的依赖对象。这个过程是通过</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">BeanFactory</font><font style="color:rgb(51, 51, 51);">或</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">ApplicationContext</font><font style="color:rgb(51, 51, 51);">的实现类（如</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">DefaultListableBeanFactory</font><font style="color:rgb(51, 51, 51);">）来完成的。</font>
2. <font style="color:rgb(51, 51, 51);">自动装配：一旦找到依赖对象，Spring会检查被注解的字段、方法或构造函数参数上是否存在</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">@Autowired</font><font style="color:rgb(51, 51, 51);">注解。如果存在注解，Spring会尝试自动装配对应的依赖对象。</font>
3. <font style="color:rgb(51, 51, 51);">解析依赖对象：Spring会根据被注解的字段、方法或构造函数参数的类型和其他限定条件，从容器中找到匹配的依赖对象。匹配的依赖对象可能有多个，根据装配规则选择最合适的依赖对象进行注入。</font>
4. <font style="color:rgb(51, 51, 51);">注入依赖对象：一旦找到匹配的依赖对象，Spring会将依赖对象注入到被注解的字段、方法或构造函数参数中，完成自动装配的过程。</font>

<font style="color:rgb(51, 51, 51);">在自动装配过程中，Spring支持多种方式来解决依赖对象的匹配问题，包括按类型匹配、按名称匹配、按限定符匹配等。通过使用</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">@Qualifier</font><font style="color:rgb(51, 51, 51);">注解可以进一步指定具体的依赖对象。</font>

<font style="color:rgb(51, 51, 51);">需要注意的是，</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">@Autowired</font><font style="color:rgb(51, 51, 51);">注解默认要求依赖对象必须存在，如果找不到匹配的依赖对象，会抛出异常。可以通过设置</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">required</font><font style="color:rgb(51, 51, 51);">属性为</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">false</font><font style="color:rgb(51, 51, 51);">来允许依赖对象不存在时，注入</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">null</font><font style="color:rgb(51, 51, 51);">或忽略该依赖。</font>

<font style="color:rgb(51, 51, 51);">总结起来，</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">@Autowired</font><font style="color:rgb(51, 51, 51);">注解的原理就是通过自动查找和装配依赖对象，简化了手动编写依赖注入的代码，提高了开发效率。</font>

### <font style="color:rgb(51, 51, 51);">17. JSR-330 @Inject 注入原理 </font>
<font style="color:rgb(51, 51, 51);">• @Inject 注入过程 </font>

<font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);">• 如果 JSR-330 存在于 ClassPath 中，复用 AutowiredAnnotationBeanPostProcessor 实现</font>

### <font style="color:rgb(51, 51, 51);">18. Java通用注解注入原理 </font>
<font style="color:rgb(51, 51, 51);">CommonAnnotationBeanPostProcessor </font>

<font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);">• 注入注解 </font>

<font style="color:rgb(51, 51, 51);">				</font><font style="color:rgb(51, 51, 51);">• javax.xml.ws.WebServiceRef </font>

<font style="color:rgb(51, 51, 51);">				</font><font style="color:rgb(51, 51, 51);">• javax.ejb.EJB </font>

<font style="color:rgb(51, 51, 51);">				</font><font style="color:rgb(51, 51, 51);">• javax.annotation.Resource </font>

<font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);">• 生命周期注解 </font>

<font style="color:rgb(51, 51, 51);">				</font><font style="color:rgb(51, 51, 51);">• javax.annotation.PostConstruct </font>

<font style="color:rgb(51, 51, 51);">				</font><font style="color:rgb(51, 51, 51);">• javax.annotation.PreDestroy</font>

### <font style="color:rgb(51, 51, 51);">19. 自定义依赖注入注解</font>
<font style="color:rgb(51, 51, 51);">• 基于 AutowiredAnnotationBeanPostProcessor 实现 </font>

<font style="color:rgb(51, 51, 51);">• 自定义实现 </font>

<font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);">• 生命周期处理 </font>

<font style="color:rgb(51, 51, 51);">				</font><font style="color:rgb(51, 51, 51);">• InstantiationAwareBeanPostProcessor </font>

<font style="color:rgb(51, 51, 51);">				</font><font style="color:rgb(51, 51, 51);">• MergedBeanDefinitionPostProcessor </font>

<font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);">• 元数据 </font>

<font style="color:rgb(51, 51, 51);">				</font><font style="color:rgb(51, 51, 51);">• InjectedElement </font>

<font style="color:rgb(51, 51, 51);">				</font><font style="color:rgb(51, 51, 51);">• InjectionMetadata</font>

# <font style="color:rgb(51, 51, 51);">Spring IoC 依赖来源</font>
### <font style="color:rgb(51, 51, 51);">1. 依赖查找的来源</font>
### <font style="color:rgb(51, 51, 51);">2. 依赖注入的来源</font>
### <font style="color:rgb(51, 51, 51);">3. Spring容器管理和游离对象</font>
### <font style="color:rgb(51, 51, 51);">4. Spring BeanDefinition 作为依赖来源</font>
<font style="color:rgb(51, 51, 51);">要素 </font>

<font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);">• 元数据：BeanDefinition </font>

<font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);">• 注册：BeanDefinitionRegistry#registerBeanDefinition </font>

<font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);">• 类型：延迟和非延迟 </font>

<font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);">• 顺序：Bean 生命周期顺序按照注册顺序</font>

<font style="color:rgb(51, 51, 51);">有个beanDefinitionMap(ConcurrentHashMap),存储已经注册的Bean.</font>

<font style="color:rgb(51, 51, 51);">还有个beanDefinitionNames的List,用来保证按顺序存储Bean.</font>

### <font style="color:rgb(51, 51, 51);">5. 单例对象作为依赖来源</font>
<font style="color:rgb(51, 51, 51);">要素</font><font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);">• 来源：外部普通 Java 对象（不一定是 POJO）</font><font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);">• 注册：SingletonBeanRegistry#registerSingleton</font><font style="color:rgb(51, 51, 51);"> 限制</font><font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);">• 无生命周期管理(因为没有被Spring的IoC容器管理)</font><font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);">• 无法实现延迟初始化 Bean</font>

```plain
// 创建 BeanFactory 容器
        AnnotationConfigApplicationContext applicationContext = new AnnotationConfigApplicationContext();
        // 创建一个外部 UserFactory 对象
        UserFactory userFactory = new DefaultUserFactory();
        SingletonBeanRegistry singletonBeanRegistry = applicationContext.getBeanFactory();
        // 注册外部单例对象
        singletonBeanRegistry.registerSingleton("userFactory", userFactory);
```

### <font style="color:rgb(51, 51, 51);">6. 非 Spring 容器管理对象作为依赖来源</font>
<font style="color:rgb(51, 51, 51);">• 要素</font><font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);">• 注册：ConfigurableListableBeanFactory#registerResolvableDependency</font><font style="color:rgb(51, 51, 51);">• 限制</font><font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);">• 无生命周期管理</font><font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);">• 无法实现延迟初始化 Bean</font><font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);">• 无法通过依赖查找</font>

### <font style="color:rgb(51, 51, 51);">7. 外部化配置作为依赖来源</font>
<font style="color:rgb(51, 51, 51);">• 要素</font><font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);">• 类型：非常规 Spring 对象依赖来源</font><font style="color:rgb(51, 51, 51);">• 限制</font><font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);">• 无生命周期管理</font><font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);">• 无法实现延迟初始化 Bean</font><font style="color:rgb(51, 51, 51);">	</font><font style="color:rgb(51, 51, 51);"> • 无法通过依赖查找</font>

```plain
@PropertySource(value = "META-INF/default.properties",encoding="UTF-8")
public class ExternalConfigurationDependencySourceDemo {

    @Value("${user.id:-1}")
    private Long id;

    @Value("${usr.name}")
    private String name;

    @Value("${user.resource:classpath://default.properties}")
    private Resource resource;
...
}
```

```plain
employee.(class)=MyClass // 等同于：<bean class="MyClass" />
employee.(abstract)=true // 等同于：<bean abstract="true" />
employee.group=Insurance // 为属性设置值，等同于：<property name="group" value="Insurance" />
employee.usesDialUp=false // 为employee这个bean中的usesDialUp属性设置值,等同于：<property name="usesDialUp" value="false" />
salesrep.(parent)=employee // 定义了一个id为salesrep的bean，指定父bean为employee，等同于：<bean id="salesrep" parent="employee" />
salesrep.(lazy-init)=true // 设置延迟初始化，等同于：<bean lazy-init="true" />
salesrep.manager(ref)=tony // 设置这个bean的manager属性值，是另外一个bean，名称为tony，等同于：<property name="manager" ref="tony" />
salesrep.department=Sales // 等同于：<property name="department" value="Sales" />
techie.(parent)=employee // 定义了一个id为techie的bean，指定父bean为employee，等同于：<bean id="techie" parent="employee" />
techie.(scope)=prototype // 设置bean的作用域，等同于<bean scope="prototype" />
techie.manager(ref)=jeff // 等同于：<property name="manager" ref="jeff" />
techie.department=Engineering // <property name="department" value="Engineering" />
techie.usesDialUp=true // <property name="usesDialUp" value="true" />
ceo.$0(ref)=secretary // 设置构造函数第1个参数值，等同于：<constructor-arg index="0" ref="secretary" />
ceo.$1=1000000 // 设置构造函数第2个参数值，等同于：<constructor-arg index="1" value="1000000" />
```

# <font style="color:rgb(51, 51, 51);">Spring Bean 作用域</font>
### <font style="color:rgb(51, 51, 51);">1. Spring Bean作用域</font>
### <font style="color:rgb(51, 51, 51);">2. "singleton" Bean作用域(单例模式)</font>
<font style="color:rgb(51, 51, 51);">单例模式:在一定范围内共享对象</font>

<font style="color:rgb(51, 51, 51);">Java中一个ClassLoader对应一个static成员</font>

<font style="color:rgb(51, 51, 51);">Spring中一个SpringIoC容器对应一个单例Bean.</font>

<font style="color:rgb(51, 51, 51);">全局缓存或无状态的bean可用单例模式.</font>

### <font style="color:rgb(51, 51, 51);">3. "prototype" Bean作用域(原型模式)</font>
<font style="color:rgb(51, 51, 51);">每ref一次(依赖注入一次)都生成一个新的bean.</font>

<font style="color:rgb(51, 51, 51);">Spring 容器没有办法管理 prototype Bean 的完整生命周期，也没有办法记录实例的存 在。销毁回调方法将不会执行，可以利用 BeanPostProcessor 进行清扫工作。</font>

### <font style="color:rgb(51, 51, 51);">4. "request" Bean作用域(web中使用,不用掌握)</font>
<font style="color:rgb(51, 51, 51);">• 配置 </font>

<font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);">• XML - /<bean class="..." scope = “request" /></font>

<font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);">• Java 注解 - @RequestScope 或 @Scope(WebApplicationContext.SCOPE_REQUEST) </font>

<font style="color:rgb(51, 51, 51);">• 实现 </font>

<font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);">• API - RequestScope</font>

<font style="color:rgb(51, 51, 51);">每次HTTP请求都会创建一个新的Bean，该作用域仅适用于web的Spring WebApplicationContext环境。</font>

### <font style="color:rgb(51, 51, 51);">5. "session" Bean作用域(web中使用,不用掌握)</font>
<font style="color:rgb(51, 51, 51);">• 配置 </font>

<font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);">• XML - /<bean class="..." scope = “session" /></font>

<font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);">• Java 注解 - @SessionScope 或 @Scope(WebApplicationContext.SCOPE_SESSION) • 实现 • API - SessionScope</font>

<font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);">每次HTTP请求都会创建一个新的Bean，该作用域仅适用于web的SpringWebApplicationContext环境。</font>

### <font style="color:rgb(51, 51, 51);">6. "application" Bean作用域(web中使用,不用掌握)</font>
<font style="color:rgb(51, 51, 51);">• 配置 </font>

<font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);">• XML - /<bean class="..." scope = “application" /></font>

<font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);">• Java 注解 - @ApplicationScope 或@Scope(WebApplicationContext.SCOPE_APPLICATION) </font>

<font style="color:rgb(51, 51, 51);">• 实现 </font>

<font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);">• API - ServletContextScope</font>

<font style="color:rgb(51, 51, 51);">限定一个Bean的作用域为</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">ServletContext</font><font style="color:rgb(51, 51, 51);">的生命周期。该作用域仅适用于web的Spring WebApplicationContext环境。</font>

### <font style="color:rgb(51, 51, 51);">7. 自定义Bean作用域</font>
<font style="color:rgb(51, 51, 51);">•实现 Scope </font>

<font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);">• org.springframework.beans.factory.config.Scope </font>

<font style="color:rgb(51, 51, 51);">•注册 Scope </font>

1. <font style="color:rgb(51, 51, 51);">创建自定义作用域的类：实现</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">org.springframework.beans.factory.config.Scope</font><font style="color:rgb(51, 51, 51);">接口。该接口定义了作用域的行为，包括Bean的创建、获取、移除等操作。你可以根据自己的需求实现这些方法。</font>
2. <font style="color:rgb(51, 51, 51);">注册自定义作用域：将你的自定义作用域注册到Spring容器中。有两种方式可以实现：</font>
    - <font style="color:rgb(51, 51, 51);">使用XML配置：在Spring的配置文件中添加</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);"><bean></font><font style="color:rgb(51, 51, 51);">元素，设置</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">scope</font><font style="color:rgb(51, 51, 51);">属性为你的自定义作用域的名称，然后指定</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">class</font><font style="color:rgb(51, 51, 51);">属性为你实现的作用域类的全限定名。</font>
    - <font style="color:rgb(51, 51, 51);">使用Java配置：创建一个继承自</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">org.springframework.context.annotation.ScopeMetadataResolver</font><font style="color:rgb(51, 51, 51);">的类，并重写</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">resolveScopeMetadata()</font><font style="color:rgb(51, 51, 51);">方法，在该方法中返回你的自定义作用域的元数据。然后将该类注册为Spring的</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">@Configuration</font><font style="color:rgb(51, 51, 51);">类中的一个</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">@Bean</font><font style="color:rgb(51, 51, 51);">。</font>
3. <font style="color:rgb(51, 51, 51);">在定义Bean时使用自定义作用域：在定义Bean时，使用</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">@Scope</font><font style="color:rgb(51, 51, 51);">注解指定你的自定义作用域的名称。</font>

```plain
import org.springframework.beans.factory.ObjectFactory;
   import org.springframework.beans.factory.config.Scope;
   
   import java.util.HashMap;
   import java.util.Map;
   
   public class CustomScope implements Scope {
       private Map<String, Object> scopedObjects = new HashMap<>();
   
       @Override
       public Object get(String name, ObjectFactory<?> objectFactory) {
           if (!scopedObjects.containsKey(name)) {
               scopedObjects.put(name, objectFactory.getObject());
           }
           return scopedObjects.get(name);
       }
   
       @Override
       public Object remove(String name) {
           return scopedObjects.remove(name);
       }
       // 其他方法省略...
   }
```

```plain
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.context.annotation.Scope;

@Configuration
public class AppConfig {

    @Bean
    @Scope("customScope")
    public MyBean myBean() {
        return new MyBean();
    }

}
```

# <font style="color:rgb(51, 51, 51);">Spring Bean生命周期</font>
[Spring进阶（十六）之spring生命周期_spring的生命周期的六个阶段-CSDN博客](https://blog.csdn.net/weixin_56644618/article/details/127366307)

[Spring进阶（十七）之spring生命周期-CSDN博客](https://blog.csdn.net/weixin_56644618/article/details/127553730)

### <font style="color:rgb(51, 51, 51);">1. Spring Bean 元信息配置阶段</font>
<font style="color:rgb(51, 51, 51);">Spring容器启动的过程中，会将Bean解析成Spring内部的BeanDefinition结构。 </font><font style="color:rgb(0, 0, 0);background-color:rgb(0, 191, 255);">不管是是通过xml配置文件的标签，还是通过注解配置的 @Bean ，还是 @Compontent 标注的类，还是扫描得到的类等，它最终都会被解析成一个BeanDefinition对象</font><font style="color:rgb(51, 51, 51);">，最后我们的Bean工厂就会根据这份Bean的定义信 息，对bean进行实例化、初始化等等操作。</font>

<font style="color:rgb(0, 0, 0);background-color:rgb(0, 191, 255);">你可以把BeanDefinition丢给Bean工厂，然后Bean工厂就会根据这个信息帮你生产一个Bean实例，拿去使用。</font>

<font style="color:rgb(51, 51, 51);">除了Bean的基本描述信息外，BeanDefinition还实现了两个接口：</font>

+ <font style="color:rgb(51, 51, 51);">AttributeAccessor//这个接口相当于key->value数据结构的一种操作，BeanDefinition继承这个，内部实际上是使用了 LinkedHashMap来实现这个接口中的所有方法，通常我们通过这些方法来保存BeanDefinition定义过程中产生的一些附加信息。</font>
+ <font style="color:rgb(51, 51, 51);">BeanMetadataElement//返回BeanDefinition定义的来源，比如我们通过xml定义 BeanDefinition的，此时getSource就表示定义bean的xml资源；若我们通过api的方式定义 BeanDefinition，我们可以将source设置为定义BeanDefinition时所在的类，出错时，可以根据这个来源方便排错。</font>

<font style="color:rgb(51, 51, 51);">以下类实现了BeanDefinition接口:</font>

<font style="color:rgb(0, 0, 0);background-color:rgb(0, 191, 255);">RootBeanDefinition类</font><font style="color:rgb(51, 51, 51);">：表示根bean定义信息</font>

<font style="color:rgb(51, 51, 51);">通常bean中没有父bean的就使用这种表示。</font>

<font style="color:rgb(0, 0, 0);background-color:rgb(0, 191, 255);">ChildBeanDefinition类</font><font style="color:rgb(51, 51, 51);">：表示子bean定义信息</font>

<font style="color:rgb(51, 51, 51);">如果需要指定父bean的，可以使用ChildBeanDefinition来定义子bean的配置信息，里面有个 parentName 属性，用来指定父bean的名称。</font>

<font style="color:rgb(0, 0, 0);background-color:rgb(0, 191, 255);">GenericBeanDefinition类</font><font style="color:rgb(51, 51, 51);">：通用的bean定义信息</font>

<font style="color:rgb(51, 51, 51);">既可以表示没有父bean的bean配置信息，也可以表示有父bean的子bean配置信息，这个类里面也有 parentName属性，用来指定父bean的名称。 </font>

<font style="color:rgb(0, 0, 0);background-color:rgb(0, 191, 255);">ConfigurationClassBeanDefinition类</font><font style="color:rgb(51, 51, 51);">：表示通过配置类中@Bean方法定义 bean信息 </font>

<font style="color:rgb(51, 51, 51);">可以通过配置类中使用@Bean来标注一些方法，通过这些方法来定义bean，这些方法配置的bean信息最后会转换为ConfigurationClassBeanDefinition类型的对象。</font>

<font style="color:rgb(0, 0, 0);background-color:rgb(0, 191, 255);">AnnotatedBeanDefinition接口</font><font style="color:rgb(51, 51, 51);">：表示通过注解的方式定义的bean信息</font>

<font style="color:rgb(51, 51, 51);">里面有个方法getMetadata()用来获取定义这个bean的类上的所有注解信息。</font>

<font style="color:rgb(0, 0, 0);background-color:rgb(0, 191, 255);">BeanDefinitionBuilder</font><font style="color:rgb(51, 51, 51);">：构建BeanDefinition的工具类 </font>

<font style="color:rgb(51, 51, 51);">spring中为了方便操作BeanDefinition，提供了一个类： BeanDefinitionBuilder ，内部提供了很多 静态方法，通过这些方法可以非常方便的组装BeanDefinition对象。</font>

### <font style="color:rgb(51, 51, 51);">2. Spring Bean 元信息解析阶段</font>
<font style="color:rgb(51, 51, 51);">三种方式:</font>

1. <font style="color:rgb(51, 51, 51);">解析xml方式定义的bean</font>
2. <font style="color:rgb(51, 51, 51);">解析properties文件定义的bean</font>
3. <font style="color:rgb(51, 51, 51);">解析注解方式定义的bean</font>

<font style="color:rgb(51, 51, 51);">对应三个接口:</font>

<font style="color:rgb(51, 51, 51);">XmlBeanDefinitionReader</font>

<font style="color:rgb(51, 51, 51);">PropertiesBeanDefinitionReader</font>

<font style="color:rgb(51, 51, 51);">AnnotatedBeanDefinitionReader</font>

```plain
@Test
public void test1(){

    //创建一个spring容器
    DefaultListableBeanFactory factory = new DefaultListableBeanFactory();

    //定义一个xml方式的bean的读取器，需要传入一个bean的注册器
    XmlBeanDefinitionReader xmlBeanDefinitionReader = new XmlBeanDefinitionReader(factory);

    //根据xml文件的位置解析定义的bean，并将其注册到我们上面指定的spring容器中
    String location="applicationContext.xml";
    xmlBeanDefinitionReader.loadBeanDefinitions(location);

    for (String beanName:factory.getBeanDefinitionNames()){
        System.out.println(beanName+"===>"+factory.getBean(beanName));
    }
}

@Test
public void test2(){

    DefaultListableBeanFactory beanFactory = new DefaultListableBeanFactory();

    PropertiesBeanDefinitionReader propertiesBeanDefinitionReader = new PropertiesBeanDefinitionReader(beanFactory);

    String location="applicationContext.properties";
    propertiesBeanDefinitionReader.loadBeanDefinitions(location);

    for (String beanName:beanFactory.getBeanDefinitionNames()){
        System.out.println(beanName+"===>"+beanFactory.getBean(beanName));
    }
}

@Test
public void test3(){

    DefaultListableBeanFactory factory = new DefaultListableBeanFactory();

    AnnotatedBeanDefinitionReader annotatedBeanDefinitionReader = new AnnotatedBeanDefinitionReader(factory);

    annotatedBeanDefinitionReader.register(Car.class,User.class);	//User和Car类上不用加@Component注解也能解析.

    for (String beanName:factory.getBeanDefinitionNames()){
        System.out.println(beanName+"===>"+ factory.getBean(beanName));
    }
}
```

### <font style="color:rgb(51, 51, 51);">3. Spring Bean 注册阶段</font>
<font style="color:rgb(51, 51, 51);">Bean注册接口：BeanDefinitionRegistry,包含了注册Bean,移除Bean,获取BeanDefinition等的方法</font>

<font style="color:rgb(51, 51, 51);">DefaultListableBeanFactory实现了这个接口</font>

### <font style="color:rgb(51, 51, 51);">4. Spring BeanDefinition 合并阶段</font>
<font style="color:rgb(51, 51, 51);">可能我们定义bean的时候有父子bean关系，此时子BeanDefinition中的信息是不完整的，比如设置属性的时候配置在父BeanDefinition中，此时子BeanDefinition中是没有这些信息的，或者子bean和父bean中都设置了属性，那我们此时的子beanDefinition肯定是不完整的，需要将子bean的 BeanDefinition和父bean的BeanDefinition进行合并，</font><font style="color:rgb(0, 0, 0);background-color:rgb(0, 191, 255);">如果有冲突的属性，子bean的属性会覆盖父bean的</font><font style="color:rgb(51, 51, 51);">，经过上面的操作最终就会得到一个 RootBeanDefinition ，</font><font style="color:rgb(0, 0, 0);background-color:rgb(0, 191, 255);">合并之后得到的 RootBeanDefinition 包含bean定义的所有信息</font><font style="color:rgb(51, 51, 51);">，包含了从父bean中继继承过来的所有信息，后续bean的所有创建工作就是依靠合并之后BeanDefinition来进行的。合并BeanDefinition会使用下面这个方法：</font>

<font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">org.springframework.beans.factory.support.AbstractBeanFactory#getMergedBeanDefin ition</font>

<font style="color:rgb(0, 0, 0);background-color:rgb(0, 191, 255);">Spring BeanDefinition的合并是递归合并</font>

<font style="color:rgb(51, 51, 51);">父子bean的配置:</font>

```plain
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
 
 
    <bean id="course" class="com.example.Course"></bean>
 
    <bean id="course1" parent="course">
        <property name="courseName" value="java"></property>
        <property name="description" value="java核心技术课程"></property>
    </bean>
 
    <bean id="course2" parent="course1">
        <property name="description" value="javaWeb课程"></property>
    </bean>
 
</beans>
```

### <font style="color:rgb(51, 51, 51);">5. Spring Bean Class 加载阶段</font>
<font style="color:rgb(51, 51, 51);">将bean的class名称转换为Class类型的对象</font>

<font style="color:rgb(51, 51, 51);">BeanDefinition中有个Object类型的字段：beanClass</font>

<font style="color:rgb(51, 51, 51);">通常这个字段的值有2种类型，一种是bean对应的Class类型的对象，另一 种是bean对应的Class的完整类名，第一种情况不需要解析，第二种情况：即这个字段是bean的类名的时候，就需要通过类加载器将其转换为一个Class对象。 此时会对阶段4中合并产生的 RootBeanDefinition 中的 beanClass 进行解析，将bean的类名转换为 Class对象 ，然后赋值给 beanClass 字段。 </font>

### <font style="color:rgb(51, 51, 51);">6. Spring Bean 实例化前阶段</font>
<font style="color:rgb(51, 51, 51);">DefaultListableBeanFactory有个重要的属性（从父类AbstractBeanFactory继承去的）:</font>

private final List<BeanPostProcessor> beanPostProcessors = new CopyOnWriteArrayList<>();

```plain
//bean实例化之前会调用一段代码：

@Nullable
protected Object applyBeanPostProcessorsBeforeInstantiation(Class<?> beanClass, String beanName) {
    for (BeanPostProcessor bp : getBeanPostProcessors()) {
        if (bp instanceof InstantiationAwareBeanPostProcessor) {
            InstantiationAwareBeanPostProcessor ibp = (InstantiationAwareBeanPostProcessor) bp;
            Object result = ibp.postProcessBeforeInstantiation(beanClass, beanName);
            if (result != null) {
                return result;
            }
        }
    }
    return null;
}
```

```plain
@Test
public void test(){
 
    DefaultListableBeanFactory beanFactory = new DefaultListableBeanFactory();
 
    beanFactory.addBeanPostProcessor(new InstantiationAwareBeanPostProcessor() {
        @Override
        public Object postProcessBeforeInstantiation(Class<?> beanClass, String beanName) throws BeansException {
 
            if (beanClass==User.class){
                User user = new User();
                user.setName("李四");
                return user;
            }
            return null;
        }
    });
    
    BeanDefinitionBuilder beanDefinitionBuilder = BeanDefinitionBuilder.rootBeanDefinition(User.class.getName());
    beanDefinitionBuilder.addPropertyValue("name","张三");
    AbstractBeanDefinition beanDefinition = beanDefinitionBuilder.getBeanDefinition();
    beanFactory.registerBeanDefinition("user",beanDefinition);
 
    System.out.println(beanFactory.getBean("user"));
}
```

<font style="color:rgb(51, 51, 51);">上面代码中轮询 beanPostProcessors 列表，如果类型是 InstantiationAwareBeanPostProcessor ， 尝试调用 InstantiationAwareBeanPostProcessor#postProcessBeforeInstantiation 获取bean的实例对 象，如果能够获取到，那么将返回值作为当前bean的实例，那么spring自带的实例化bean的过程就被跳过了。</font>

<font style="color:rgb(0, 0, 0);background-color:rgb(0, 191, 255);">实际上，在实例化前阶段对bean的创建进行干预的情况，用的非常少，所以大部分bean的创建还会继续走下面的阶段。</font>

### <font style="color:rgb(51, 51, 51);">7. Spring Bean 实例化阶段</font>
##### <font style="color:rgb(51, 51, 51);">(1)通过反射来调用bean的构造器来创建bean的实例</font>
```plain
for (BeanPostProcessor bp : getBeanPostProcessors()) {
     if (bp instanceof SmartInstantiationAwareBeanPostProcessor) {
        SmartInstantiationAwareBeanPostProcessor ibp = (SmartInstantiationAwareBeanPostProcessor) bp;
        Constructor<?>[] ctors = ibp.determineCandidateConstructors(beanClass, beanName);
        if (ctors != null) {
             return ctors;
        }
     }
}
```

<font style="color:rgb(0, 0, 0);background-color:rgb(0, 191, 255);">会调用 SmartInstantiationAwareBeanPostProcessor接口的determineCandidateConstructors 方 法，这个方法会返回候选的构造器列表，但默认是返回空。</font>

<font style="color:rgb(51, 51, 51);">这个方法的实现类:</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">org.springframework.beans.factory.annotation.AutowiredAnnotationBeanPostProcessor</font>

<font style="color:rgb(51, 51, 51);">可以将 @Autowired 标注的构造方法作为候选构造器返回.</font>

```plain
//这段代码将被MyAutowire注解注解的构造器作为构建Bean的构造器.

public class MySmartInstantiationAwareBeanPostProcessor implements SmartInstantiationAwareBeanPostProcessor {
 
    @Override
    public Constructor<?>[] determineCandidateConstructors(Class<?> beanClass, String beanName) throws BeansException {
 
        System.out.println(beanClass);
        System.out.println("调用 MySmartInstantiationAwareBeanPostProcessor.determineCandidateConstructors 方法");
        Constructor<?>[] declaredConstructors = beanClass.getDeclaredConstructors();
 
 
        //获取有@MyAutowire注解的构造器列表
        List<Constructor<?>> collect = Arrays
                .stream(declaredConstructors)
                .filter(constructor -> constructor.isAnnotationPresent(MyAutowire.class))
                .collect(Collectors.toList());
        Constructor[] constructors = collect.toArray(new Constructor[collect.size()]);
        return constructors.length != 0 ? constructors : null;
    }
}
```

##### <font style="color:rgb(51, 51, 51);">(2)处理合并后的BeanDefinition</font>
```plain
//源码
protected void applyMergedBeanDefinitionPostProcessors(RootBeanDefinition mbd, Class<?> beanType, String beanName) {
    for (MergedBeanDefinitionPostProcessor processor : getBeanPostProcessorCache().mergedDefinition) {
        processor.postProcessMergedBeanDefinition(mbd, beanType, beanName);
    }
}
```

<font style="color:rgb(51, 51, 51);">会调用 MergedBeanDefinitionPostProcessor接口的postProcessMergedBeanDefinition 方法:</font>

<font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">void postProcessMergedBeanDefinition(RootBeanDefinition beanDefinition, Class<?> beanType, String beanNam</font>

<font style="color:rgb(51, 51, 51);">两个实现类:</font>

```plain
org.springframework.beans.factory.annotation.AutowiredAnnotationBeanPostProcessor

在 postProcessMergedBeanDefinition 方法中对 @Autowired、@Value 标注的方法和字段进行缓存

org.springframework.context.annotation.CommonAnnotationBeanPostProcessor

在 postProcessMergedBeanDefinition 方法中对 @Resource 标注的字段和方法、

@PostConstruct 标注的方法、 @PreDestroy标注的方法进行缓存
```

### <font style="color:rgb(51, 51, 51);">8. Spring Bean 实例化后阶段</font>
<font style="color:rgb(51, 51, 51);">会调用 InstantiationAwareBeanPostProcessor 接口的 postProcessAfterInstantiation 这个方 法.</font>

```plain
for (BeanPostProcessor bp : getBeanPostProcessors()) {
    if (bp instanceof InstantiationAwareBeanPostProcessor) {
        InstantiationAwareBeanPostProcessor ibp = (InstantiationAwareBeanPostProcessor) bp;
        if (!ibp.postProcessAfterInstantiation(bw.getWrappedInstance(), beanName)) {
            return;
        }
    }
}
```

<font style="color:rgb(0, 0, 0);background-color:rgb(0, 191, 255);">postProcessAfterInstantiation 方法返回false的时候，后续的Bean属性赋值前处理、Bean 属性赋值都会被跳过了</font>

```plain
public class test4 {
 
    @Test
    public void test(){
 
        DefaultListableBeanFactory beanFactory = new DefaultListableBeanFactory();
 
        beanFactory.addBeanPostProcessor(new InstantiationAwareBeanPostProcessor() {
            @Override
            public boolean postProcessAfterInstantiation(Object bean, String beanName) throws BeansException {
                if (beanName.equals("user1")){
                    return false;
                }
                return true;
            }
        });
 
        BeanDefinitionBuilder beanDefinitionBuilder1 = BeanDefinitionBuilder.rootBeanDefinition(User.class.getName());
        beanDefinitionBuilder1.addPropertyValue("name","张三");
        AbstractBeanDefinition beanDefinition1 = beanDefinitionBuilder1.getBeanDefinition();
 
        BeanDefinitionBuilder beanDefinitionBuilder2 = BeanDefinitionBuilder.rootBeanDefinition(User.class.getName());
        beanDefinitionBuilder2.addPropertyValue("name","李四");
        AbstractBeanDefinition beanDefinition2 = beanDefinitionBuilder2.getBeanDefinition();
 
        beanFactory.registerBeanDefinition("user1",beanDefinition1);
        beanFactory.registerBeanDefinition("user2",beanDefinition2);
 
        System.out.println(beanFactory.getBean("user1"));
        System.out.println(beanFactory.getBean("user2"));
    }
 
}
```

```plain
输出:
User{name='null'}
User{name='李四'}
```

### <font style="color:rgb(51, 51, 51);">9. Spring Bean 属性赋值阶段</font>
##### <font style="color:rgb(51, 51, 51);">(1)赋值前阶段</font>
<font style="color:rgb(0, 0, 0);background-color:rgb(0, 191, 255);">调用 InstantiationAwareBeanPostProcessor 接口的 postProcessProperties 方法</font>

```plain
for (BeanPostProcessor bp : getBeanPostProcessors()) {
    if (bp instanceof InstantiationAwareBeanPostProcessor) {
        InstantiationAwareBeanPostProcessor ibp = (InstantiationAwareBeanPostProcessor) bp;
        PropertyValues pvsToUse = ibp.postProcessProperties(pvs, bw.getWrappedInstance(), beanName);
        if (pvsToUse == null) {
            if (filteredPds == null) {
                filteredPds = filterPropertyDescriptorsForDependencyCheck(bw, mbd.allowCaching);
            }
            pvsToUse = ibp.postProcessPropertyValues(pvs, filteredPds, bw.getWrappedInstance(), beanName);
            if (pvsToUse == null) {
                return;
            }
        }
        pvs = pvsToUse;
    }
}
```

<font style="color:rgb(51, 51, 51);">从上面可以看出，如果 InstantiationAwareBeanPostProcessor 中的 postProcessProperties 和 postProcessPropertyValues 都返回空的时候，表示这个bean不需要设置属性，直接返回了，直接进入下一个阶段。</font>

<font style="color:rgb(51, 51, 51);">两个实现类:</font>

```plain
AutowiredAnnotationBeanPostProcessor在这个方法中对@Autowired、@Value标注的字段、方法注入值。

CommonAnnotationBeanPostProcessor在这个方法中对@Resource标注的字段和方法注入值。
```

##### <font style="color:rgb(51, 51, 51);">(2)赋值阶段</font>
<font style="color:rgb(51, 51, 51);">属性赋值前阶段完成后，循环处理 PropertyValues 中的属性值信息，通过反射调用set方法将属性的值设置到bean实例中。 PropertyValues中的值是通过bean xml中property元素配置的，或者调用MutablePropertyValues中 add方法设置的值。</font>

### <font style="color:rgb(51, 51, 51);">10. Spring Bean Aware接口回调阶段</font>
```plain
private void invokeAwareMethods(final String beanName, final Object bean) {
    if (bean instanceof Aware) {
        if (bean instanceof BeanNameAware) {
            ((BeanNameAware) bean).setBeanName(beanName);
        }
        if (bean instanceof BeanClassLoaderAware) {
            ClassLoader bcl = getBeanClassLoader();
            if (bcl != null) {
                ((BeanClassLoaderAware) bean).setBeanClassLoader(bcl);
            }
        }
        if (bean instanceof BeanFactoryAware) {
            ((BeanFactoryAware) bean).setBeanFactory(AbstractAutowireCapableBeanFactory.this);
        }
    }
}
```

<font style="color:rgb(51, 51, 51);">如果我们的bean实例实现了上面的接口，会按照下面的顺序依次进行调用：</font>

<font style="color:rgb(51, 51, 51);">BeanNameAware：将bean的名称注入进去</font>

<font style="color:rgb(51, 51, 51);">BeanClassLoaderAware：将BeanClassLoader注入进去</font>

<font style="color:rgb(51, 51, 51);">BeanFactoryAware：将BeanFactory注入进去 </font>

### <font style="color:rgb(51, 51, 51);">11. Spring Bean 初始化前阶段</font>
```plain
@Override
public Object applyBeanPostProcessorsBeforeInitialization(Object existingBean, String beanName)
        throws BeansException {

    Object result = existingBean;
    for (BeanPostProcessor processor : getBeanPostProcessors()) {
        Object current = processor.postProcessBeforeInitialization(result, beanName);
        if (current == null) {
            return result;
        }
        result = current;
    }
    return result;
}
```

<font style="color:rgb(51, 51, 51);">会调用 BeanPostProcessor的postProcessBeforeInitialization 方法，若返回null，当前方法将结束。 通常称postProcessBeforeInitialization这个方法为：bean初始化前操作。</font>

<font style="color:rgb(51, 51, 51);">两个比较重要的实现类:</font>

```plain
org.springframework.context.support.ApplicationContextAwareProcessor 
org.springframework.context.annotation.CommonAnnotationBeanPostProcessor
```

### <font style="color:rgb(51, 51, 51);">12. Spring Bean 初始化阶段</font>
1. <font style="color:rgb(51, 51, 51);">调用InitializingBean接口的afterPropertiesSet方法</font>
2. <font style="color:rgb(51, 51, 51);">调用定义bean的时候指定的初始化方法。(@Bean(initMethod = ""))</font>

### <font style="color:rgb(51, 51, 51);">13. Spring Bean 初始化后阶段</font>
```plain
@Override
public Object applyBeanPostProcessorsAfterInitialization(Object existingBean, String beanName)
        throws BeansException {
    Object result = existingBean;
    for (BeanPostProcessor processor : getBeanPostProcessors()) {
        Object current = processor.postProcessAfterInitialization(result, beanName);
        if (current == null) {
            return result;
        }
        result = current;
    }
    return result;
}
```

<font style="color:rgb(51, 51, 51);">调用 BeanPostProcessor接口的postProcessAfterInitialization方法 ，返回null的时候，会中断上面的操作。</font>

<font style="color:rgb(51, 51, 51);">通常称postProcessAfterInitialization这个方法为：bean初始化后置操作。</font>

### <font style="color:rgb(51, 51, 51);">14. Spring Bean 初始化完成阶段</font>
```plain
public interface SmartInitializingSingleton {
    void afterSingletonsInstantiated();
}
```

### <font style="color:rgb(51, 51, 51);">15. Spring Bean 销毁前阶段</font>
1. <font style="color:rgb(51, 51, 51);">轮询beanPostProcessors列表，如果是DestructionAwareBeanPostProcessor这种类型的，会调用其内部的postProcessBeforeDestruction方法</font>
2. <font style="color:rgb(51, 51, 51);">如果bean实现了org.springframework.beans.factory.DisposableBean接口，会调用这个接口中的destroy方法</font>
3. <font style="color:rgb(51, 51, 51);">调用bean自定义的销毁方法</font>

### <font style="color:rgb(51, 51, 51);">16. Spring Bean 销毁阶段</font>
<font style="color:rgb(51, 51, 51);">触发bean销毁的几种方式</font><font style="color:rgb(51, 51, 51);">调用org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory#destroyB ean</font><font style="color:rgb(51, 51, 51);">调用org.springframework.beans.factory.config.ConfigurableBeanFactory#destroySingletons</font><font style="color:rgb(51, 51, 51);">调用ApplicationContext中的close方法</font>

### <font style="color:rgb(51, 51, 51);">17. Spring Bean 垃圾收集</font>
<font style="color:rgb(51, 51, 51);">关闭应用上下文,执行GC,finalize()方法被回调(不是100%的,例如G1垃圾回收器就默认不执行finalize()方法)</font>

# <font style="color:rgb(51, 51, 51);">配置元信息</font>
[10. Spring 配置元信息_beanbuilder.addpropertyvalue-CSDN博客](https://blog.csdn.net/u013794243/article/details/124542488)<font style="color:rgb(51, 51, 51);"> (跟视频差不多,视频的增强版)</font>

### <font style="color:rgb(51, 51, 51);">1. Spring 配置元信息</font>
<font style="color:rgb(51, 51, 51);">• Spring Bean 配置元信息 - BeanDefinition</font><font style="color:rgb(51, 51, 51);">• Spring Bean 属性元信息 - PropertyValues</font><font style="color:rgb(51, 51, 51);">• Spring 容器配置元信息</font><font style="color:rgb(51, 51, 51);">• Spring 外部化配置元信息 - PropertySource</font><font style="color:rgb(51, 51, 51);">• Spring Profile 元信息 - @Profile</font>

### <font style="color:rgb(51, 51, 51);">2. Spring Bean 配置元信息</font>
<font style="color:rgb(51, 51, 51);">• GenericBeanDefinition：通用型 BeanDefinition </font>

<font style="color:rgb(51, 51, 51);">			</font><font style="color:rgb(51, 51, 51);">继承了abstractDefinition,主要实现了里面的操作</font><font style="color:rgb(51, 51, 51);">• RootBeanDefinition：无 Parent 的 BeanDefinition 或者合并后 BeanDefinition</font>

<font style="color:rgb(51, 51, 51);">			</font><font style="color:rgb(51, 51, 51);">调用setParentName的时候会返回错误</font><font style="color:rgb(51, 51, 51);">• AnnotatedBeanDefinition：注解标注的 BeanDefinition</font>

<font style="color:rgb(51, 51, 51);">			</font><font style="color:rgb(51, 51, 51);">包含AnntiationMetadata</font>

### <font style="color:rgb(51, 51, 51);">3. Spring Bean 属性元信息</font>
<font style="color:rgb(51, 51, 51);">BeanDefinition中的成员:</font>

<font style="color:rgb(51, 51, 51);">• Bean 属性元信息 - PropertyValues</font><font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);">• 可修改实现 - MutablePropertyValues</font><font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);">• 元素成员 - PropertyValue</font><font style="color:rgb(51, 51, 51);">• Bean 属性上下文存储 - AttributeAccessor </font><font style="color:rgb(51, 51, 51);">• Bean 元信息元素 - BeanMetadataElement</font>

```plain
public abstract class AbstractBeanDefinition extends BeanMetadataAttributeAccessor
		implements BeanDefinition, Cloneable{
    ......
    @Nullable
	private MutablePropertyValues propertyValues;
    ......
}

public class BeanMetadataAttributeAccessor extends AttributeAccessorSupport implements BeanMetadataElement {
	......
}
```

### <font style="color:rgb(51, 51, 51);">4. Spring 容器配置元信息</font>
### <font style="color:rgb(51, 51, 51);">5. 基于XML文件装载Spring Bean配置元信息</font>
### <font style="color:rgb(51, 51, 51);">6. 基于Properties文件装载Spring Bean配置元信息</font>
```plain
# User BeanDefinition
user.(class) = org.geekbang.thinking.in.spring.ioc.overview.domain.User

# <property name="id" value="1"/>
user.id = 1

# <property name="name" value="小马哥"/>
user.name = 小马哥

# <property name="city" value="HANGZHOU"/>
user.city = HANGZHOU

# <property name="workCities" value="BEIJING,HANGZHOU"/>
user.workCities = BEIJING,HANGZHOU

# <property name="lifeCities">
## <list>
## <value>BEIJING</value>
## <value>SHANGHAI</value>
##</list>
# </property>
user.lifeCities = BEIJING,SHANGHAI

# <property name="configFileLocation" value="classpath:/META-INF/user-config.properties"/>
user.configFileLocation = classpath:/META-INF/user-config.properties
```

### <font style="color:rgb(51, 51, 51);">7. 基于Java注解装载Spring Bean配置元信息</font>
### <font style="color:rgb(51, 51, 51);">8. Spring Bean 配置元信息底层实现</font>
| **<font style="color:rgb(51, 51, 51);">实现场景</font>** | **<font style="color:rgb(51, 51, 51);">实现类</font>** | **<font style="color:rgb(51, 51, 51);">起始版本</font>** |
| :--- | :--- | :--- |
| <font style="color:rgb(51, 51, 51);">XML 资源</font> | <font style="color:rgb(51, 51, 51);">XmlBeanDefinitionReader</font> | <font style="color:rgb(51, 51, 51);">1.0</font> |
| <font style="color:rgb(51, 51, 51);">Properties 资源</font> | <font style="color:rgb(51, 51, 51);">PropertiesBeanDefinitionReader</font> | <font style="color:rgb(51, 51, 51);">1.0</font> |
| <font style="color:rgb(51, 51, 51);">Java 注解</font> | <font style="color:rgb(51, 51, 51);">AnnotatedBeanDefinitionReader</font> | <font style="color:rgb(51, 51, 51);">3.0</font> |


<font style="color:rgb(51, 51, 51);">XmlBeanDefinitionReader 和 PropertiesBeanDefinitionReader 都属于 BeanDenitionReader 实现</font>

<font style="color:rgb(0, 0, 0);background-color:rgb(0, 191, 255);">AnnotatedBeanDefinitionReader 和 BeanDefinitionReader 这个接口没有关系</font>

<font style="color:rgb(51, 51, 51);">10.8.1 Spring XML 资源 BeanDefinition 解析与注册</font>

<font style="color:rgb(51, 51, 51);">核心 API——XmlBeanDefinitionReader</font>

<font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);">资源——Resource</font>

<font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);">底层——BeanDefinitionDocumentReader</font>

<font style="color:rgb(51, 51, 51);">				</font><font style="color:rgb(51, 51, 51);">XML 解析——Java DOM Level 3 API</font>

<font style="color:rgb(51, 51, 51);">				</font><font style="color:rgb(51, 51, 51);">BeanDefinition 解析——BeanDefinitionParserDelegate</font>

<font style="color:rgb(51, 51, 51);">				</font><font style="color:rgb(51, 51, 51);">BeanDefinition 注册——BeanDefinitionRegistrar</font>

<font style="color:rgb(51, 51, 51);">10.8.2 Spring Properties 资源 BeanDefinition 解析与注册</font>

<font style="color:rgb(51, 51, 51);">核心 API——PropertiesBeanDefinitionReader</font>

<font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);">资源</font>

<font style="color:rgb(51, 51, 51);">				</font><font style="color:rgb(51, 51, 51);">字节流——Resource</font>

<font style="color:rgb(51, 51, 51);">				</font><font style="color:rgb(51, 51, 51);">字符流——EncodedResource</font>

<font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);">底层</font>

<font style="color:rgb(51, 51, 51);">				</font><font style="color:rgb(51, 51, 51);">存储——java.util.Properties</font>

<font style="color:rgb(51, 51, 51);">				</font><font style="color:rgb(51, 51, 51);">BeanDefinition 解析——API 内部实现</font>

<font style="color:rgb(51, 51, 51);">				</font><font style="color:rgb(51, 51, 51);">BeanDefinition 注册——BeanDefinitionRegistry</font>

<font style="color:rgb(51, 51, 51);">10.8.3 Spring Java 注册 BeanDefinition 解析与注册</font>

<font style="color:rgb(51, 51, 51);">核心 API——AnnotatedBeanDefinitionReader</font>

<font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);">资源——类对象 java.lang.Class</font>

<font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);">底层</font>

<font style="color:rgb(51, 51, 51);">				</font><font style="color:rgb(51, 51, 51);">条件评估——ConditionEvaluattor</font>

<font style="color:rgb(51, 51, 51);">				</font><font style="color:rgb(51, 51, 51);">Bean 范围解析——ScopeMetadataResolver</font>

<font style="color:rgb(51, 51, 51);">				</font><font style="color:rgb(51, 51, 51);">BeanDefinition 解析——内部 API 实现</font>

<font style="color:rgb(51, 51, 51);">				</font><font style="color:rgb(51, 51, 51);">BeanDefinition 处理——AnnotationConfigUtils.processCommonDefinitionAnnotations</font>

<font style="color:rgb(51, 51, 51);">				</font><font style="color:rgb(51, 51, 51);">BeanDefinition 注册——BeanDefinitionRegistry</font>

### <font style="color:rgb(51, 51, 51);">9. 基于XML文件装载 Spring IoC 容器配置元信息</font>
### <font style="color:rgb(51, 51, 51);">10. 基于Java注解装载 Spring IoC 容器配置元信息</font>
### <font style="color:rgb(51, 51, 51);">11. 基于 Extensible XML authoring 扩展Spring XML元素</font>
### <font style="color:rgb(51, 51, 51);">12. Extensible XML authoring扩展原理</font>
### <font style="color:rgb(51, 51, 51);">13. 基于Properties文件装载外部化配置</font>
### <font style="color:rgb(51, 51, 51);">14. 基于YAML文件装载外部化配置</font>
# <font style="color:rgb(51, 51, 51);">事件</font>
### <font style="color:rgb(51, 51, 51);">1. Java 事件/监听器编程模型</font>
<font style="color:rgb(51, 51, 51);">设计模式 - </font>[观察者模式](https://so.csdn.net/so/search?q=%E8%A7%82%E5%AF%9F%E8%80%85%E6%A8%A1%E5%BC%8F&spm=1001.2101.3001.7020)

[观察者模式](https://so.csdn.net/so/search?q=%E8%A7%82%E5%AF%9F%E8%80%85%E6%A8%A1%E5%BC%8F&spm=1001.2101.3001.7020)<font style="color:rgb(51, 51, 51);">（又被称为发布-订阅（Publish/Subscribe）模式，属于行为型模式的一种</font>

<font style="color:rgb(51, 51, 51);">在观察者模式中有如下角色：</font>

<u><font style="color:rgb(51, 51, 51);">Subject</font></u><font style="color:rgb(51, 51, 51);">：抽象主题（抽象被观察者），抽象主题角色把所有观察者对象保存在一个集合里，每个主题都可以有任意数量的观察者，抽象主题提供一个接口，可以增加和删除观察者对象。</font>

```plain
public interface Subject {
    /**
     * 增加订阅者
     * @param observer
     */
    public void attach(Observer observer);
    /**
     * 删除订阅者
     * @param observer
     */
    public void detach(Observer observer);
    /**
     * 通知订阅者更新消息
     */
    public void notify(String message);
}
```

<u><font style="color:rgb(51, 51, 51);">ConcreteSubject</font></u><font style="color:rgb(51, 51, 51);">：具体主题（具体被观察者），该角色将有关状态存入具体观察者对象，在具体主题的内部状态发生改变时，给所有注册过的观察者发送通知。</font>

```plain
public class SubscriptionSubject implements Subject {
    //储存订阅公众号的微信用户
    private List<Observer> weixinUserlist = new ArrayList<Observer>();

    @Override
    public void attach(Observer observer) {
        weixinUserlist.add(observer);
    }

    @Override
    public void detach(Observer observer) {
        weixinUserlist.remove(observer);
    }

    @Override
    public void notify(String message) {
        for (Observer observer : weixinUserlist) {
            observer.update(message);
        }
    }
}
```

<u><font style="color:rgb(51, 51, 51);">Observer</font></u><font style="color:rgb(51, 51, 51);">：抽象观察者，是观察者者的抽象类，它定义了一个更新接口，使得在得到主题更改通知时更新自己。</font>

```plain
public interface Observer {
    public void update(String message);
}
```

<u><font style="color:rgb(51, 51, 51);">ConcrereObserver</font></u><font style="color:rgb(51, 51, 51);">：具体观察者，实现抽象观察者定义的更新接口，以便在得到主题更改通知时更新自身的状态。</font>

```plain
public class WeixinUser implements Observer {
    // 微信用户名
    private String name;
    public WeixinUser(String name) {
        this.name = name;
    }
    @Override
    public void update(String message) {
        System.out.println(name + "-" + message);
    }
}
```

```plain
public class ObserverDemo {
    public static void main(String[] args) {
        EventObservable observable = new EventObservable();
        EventObserver observer = new EventObserver();
        observable.addObserver(observer);
        observable.notifyObservers("Event");
    }

    static class EventObservable extends Observable {
        @Override
        public void notifyObservers(Object arg) {
            setChanged();
            super.notifyObservers(new EventObject(arg));
            clearChanged();
        }
    }

    static class EventObserver implements Observer, EventListener {

        @Override
        public void update(Observable o, Object arg) {
            EventObject event = (EventObject) arg;
            System.out.println("receive msg: " + event);
        }
    }
}
```

<font style="color:rgb(0, 0, 0);background-color:rgb(0, 191, 255);">标准化接口</font><font style="color:rgb(0, 0, 0);background-color:rgb(0, 191, 255);">• 事件对象 - java.util.EventObject</font><font style="color:rgb(0, 0, 0);background-color:rgb(0, 191, 255);">• 事件监听器 - java.util.EventListener</font>

<font style="color:rgb(51, 51, 51);">一个不咋用的参考实现：</font>

<font style="color:rgb(51, 51, 51);">• 可观者对象（消息发送者） - java.util.Observable</font><font style="color:rgb(51, 51, 51);">• 观察者 - java.util.Observer</font>

<font style="color:rgb(51, 51, 51);">Observable/Observer 是观察者模型在 JDK 中的实现，而 EventObject 和 EventListener 是事件驱动的接口，这里有涉及实现，实现可以利用 Observable/Observer 或者扩展来完成。</font>

<font style="color:rgb(51, 51, 51);">Observable/Observer 是jdk中观察者模式的实现标准，有具体实现。但是事件驱动只是建议基于EventObject/EventListener来拓展，并没有具体实现。Spring事件并没有用到Observable/Observer ，并且Observable/Observer 在 jdk 9 被推荐转为java.util.concurrent.Flow实现。</font>

<font style="color:rgb(0, 0, 0);background-color:rgb(0, 191, 255);">JDK 中的 Observable/Observer 只是一个参考</font><font style="color:rgb(51, 51, 51);">，它的执行顺序和插入顺序是相反，也即是它是 Stack 的方式，无法实现自定义顺序，并且它使用了 Vector 线程安全的集合容器，无法提升高性能，所以 </font><font style="color:rgb(0, 0, 0);background-color:rgb(0, 191, 255);">Spring 没有必要用到它</font><font style="color:rgb(51, 51, 51);">。</font>

### <font style="color:rgb(51, 51, 51);">2. 面向接口的事件/监听器设计模式</font>
<font style="color:rgb(51, 51, 51);">一般事件系统中事件需要继承 EventObject 类，监听器接口需要继承 EventListener 接口</font>

### <font style="color:rgb(51, 51, 51);">3. 面向注解的事件/监听器设计模式</font>
### <font style="color:rgb(51, 51, 51);">4. Spring 标准事件-ApplicationEvent</font>
<font style="color:rgb(51, 51, 51);">Spring 应用上下文 ApplicationEvent 扩展就是 ApplicationContextEvent，Spring 应用上下文（ApplicationContext）作为事件源。(被观察者？)</font><font style="color:rgb(51, 51, 51);">具体实现：</font><font style="color:rgb(51, 51, 51);">• org.springframework.context.event.ContextClosedEvent</font><font style="color:rgb(51, 51, 51);">• org.springframework.context.event.ContextRefreshedEvent</font><font style="color:rgb(51, 51, 51);">• org.springframework.context.event.ContextStartedEvent</font><font style="color:rgb(51, 51, 51);">• org.springframework.context.event.ContextStoppedEvent</font>

<font style="color:rgb(51, 51, 51);">继承关系：ContextRefreshedEvent 继承 ApplicationContextEvent 继承 ApplicationEvent 继承 ObjectEvent</font>

<font style="color:rgb(51, 51, 51);">其中 ApplicationEvent 新增 timestamp 属性记录时间</font>

<font style="color:rgb(51, 51, 51);">ApplicationContextEvent 则将 ApplicationContext 作为事件源，方便 Listener 中和 ApplicationContext 做交互</font>

<font style="color:rgb(51, 51, 51);">ApplicationContextEvent就是Spring应用上下文的一个事件源，提供了获取ApplicationContext方法，事件的source就是ApplicationContext。</font>

<font style="color:rgb(51, 51, 51);">ApplicationContextEvent有以上四个实现：ContextClosedEvent、ContextRefreshedEvent、ContextStartedEvent、ContextStoppedEvent。</font>

### <font style="color:rgb(51, 51, 51);">5. 基于接口的 Spring 事件监听器</font>
<font style="color:rgb(51, 51, 51);">Java 标准事件监听器 java.util.EventListener 扩展</font>

<font style="color:rgb(51, 51, 51);">扩展接口——org.springframework.context.ApplicationListener</font>

<font style="color:rgb(51, 51, 51);">设计特点：单一类型事件处理</font>

<font style="color:rgb(51, 51, 51);">处理方法：onApplicationEvent(ApplicationEvent)</font>

<font style="color:rgb(51, 51, 51);">事件类型：org.springframework.context.ApplicationEvent</font>

```plain
public class ApplicationListenerDemo {
    public static void main(String[] args) {
        GenericApplicationContext context = new GenericApplicationContext();
        context.addApplicationListener(e -> {
            if (e instanceof ContextRefreshedEvent) {
                System.out.println("refresh");
            } else if (e instanceof ContextClosedEvent) {
                System.out.println("close");
            }
        });

        context.refresh();

        context.close();
    }
}
```

### <font style="color:rgb(51, 51, 51);">6. 基于注解的 Spring 事件监听器</font>
| **<font style="color:rgb(51, 51, 51);">特性</font>** | **<font style="color:rgb(51, 51, 51);">说明</font>** |
| :--- | :--- |
| <font style="color:rgb(51, 51, 51);">设计特点</font> | <font style="color:rgb(51, 51, 51);">支持多 ApplicationEvent 类型，无需接口约束</font> |
| <font style="color:rgb(51, 51, 51);">注解目标</font> | <font style="color:rgb(51, 51, 51);">方法</font> |
| <font style="color:rgb(51, 51, 51);">是否支持异步执行</font> | <font style="color:rgb(51, 51, 51);">支持</font> |
| <font style="color:rgb(51, 51, 51);">是否支持泛型类型事件</font> | <font style="color:rgb(51, 51, 51);">支持</font> |
| <font style="color:rgb(51, 51, 51);">是否支持顺序控制</font> | <font style="color:rgb(51, 51, 51);">支持，配合 @Order 注解控制</font> |


<font style="color:rgb(51, 51, 51);">@org.springframework.context.event.EventListener</font>

```plain
@EnableAsync
public class AnnotationApplicationListenerDemo {

    @EventListener
    @Order(2)
    public void listener(ContextRefreshedEvent event) {
        println("refresh");
    }

    @EventListener
    @Order(1)
    public void listener1(ContextRefreshedEvent event) {
        println("refresh1");
    }

    @EventListener
    @Async
    public void listener(ContextStartedEvent event) {
        println("start");
    }

    @EventListener
    public void listener(ContextClosedEvent event) {
        println("close");
    }

    public static void main(String[] args) {
        AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext();
        context.register(AnnotationApplicationListenerDemo.class);
        context.refresh();
        context.start();
        context.close();
    }

    private static void println(String msg) {
        System.out.printf("[%s] handle %s%n", Thread.currentThread().getName(), msg);
    }
}
```

### <font style="color:rgb(51, 51, 51);">7. ApplicationListener 作为 Spring Bean 注册</font>
```plain
public class SpringBeanApplicationListener {

    @Bean
    public ApplicationListener<ContextRefreshedEvent> myListener() {
        return new MyApplicationListener();
    }

    public static void main(String[] args) {
        AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext();
        context.register(SpringBeanApplicationListener.class);
        context.refresh();
        context.close();
    }

    static class MyApplicationListener implements ApplicationListener<ContextRefreshedEvent> {
        @Override
        public void onApplicationEvent(ContextRefreshedEvent event) {
            System.out.println("my refresh");
        }
    }
}
```

### <font style="color:rgb(51, 51, 51);">8. Spring 事件发布器</font>
<font style="color:rgb(51, 51, 51);">• 方法一：通过 ApplicationEventPublisher 发布 Spring 事件</font><font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);">• 获取 ApplicationEventPublisher </font><font style="color:rgb(51, 51, 51);">				</font><font style="color:rgb(51, 51, 51);">• 依赖注入</font><font style="color:rgb(51, 51, 51);">• 方法二：通过 ApplicationEventMulticaster 发布 Spring 事件</font><font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);">• 获取 ApplicationEventMulticaster</font><font style="color:rgb(51, 51, 51);">				</font><font style="color:rgb(51, 51, 51);">• 依赖注入</font><font style="color:rgb(51, 51, 51);">				</font><font style="color:rgb(51, 51, 51);">• 依赖查找</font>

<font style="color:rgb(51, 51, 51);">ApplicationEventPublisher接口有两个方法，其中有个方法是Spring4.2引入的。</font>

```plain
@FunctionalInterface
public interface ApplicationEventPublisher {

	default void publishEvent(ApplicationEvent event) {
		publishEvent((Object) event);
	}

	void publishEvent(Object event);
}
```

<font style="color:rgb(51, 51, 51);">ApplicationEventMulticaster接口会在ApplicationEventPublisher接口的基础上增加很多东西，包括对ApplicationListener的增删改查，multicastEvent方法就是事件广播方法。</font>

<font style="color:rgb(51, 51, 51);">获取ApplicationEventPublisher 有两种方式，一种是</font><font style="color:rgb(0, 0, 0);background-color:rgb(0, 191, 255);">通过 ApplicationEventPublisherAware 回调接口</font><font style="color:rgb(51, 51, 51);">；一种是通过 </font><font style="color:rgb(0, 0, 0);background-color:rgb(0, 191, 255);">@Autowired ApplicationEventPublisher</font><font style="color:rgb(51, 51, 51);">。</font>

<font style="color:rgb(51, 51, 51);">依赖查找 ApplicationEventMulticaster</font><font style="color:rgb(51, 51, 51);">查找条件</font><font style="color:rgb(51, 51, 51);">• </font><font style="color:rgb(0, 0, 0);background-color:rgb(0, 191, 255);">Bean 名称：“applicationEventMulticaster”</font><font style="color:rgb(0, 0, 0);background-color:rgb(0, 191, 255);">• Bean 类型：org.springframework.context.event.ApplicationEventMulticaster</font>

<font style="color:rgb(51, 51, 51);">事实上，我们调用context.addApplicationListener()方法时，会委派给applicationEventMulticaster调用它的addApplicationListener方法</font>

```plain
// org.springframework.context.support.AbstractApplicationContext#addApplicationListener
@Override
public void addApplicationListener(ApplicationListener<?> listener) {
	Assert.notNull(listener, "ApplicationListener must not be null");
	if (this.applicationEventMulticaster != null) {
		this.applicationEventMulticaster.addApplicationListener(listener);
	}
	this.applicationListeners.add(listener);
}
```

<font style="color:rgb(51, 51, 51);">此处的applicationEventMulticaster初始化方法：</font>

```plain
// org.springframework.context.support.AbstractApplicationContext#initApplicationEventMulticaster
protected void initApplicationEventMulticaster() {
	ConfigurableListableBeanFactory beanFactory = getBeanFactory();
	if (beanFactory.containsLocalBean(APPLICATION_EVENT_MULTICASTER_BEAN_NAME)) { // applicationEventMulticaster
		this.applicationEventMulticaster =
				beanFactory.getBean(APPLICATION_EVENT_MULTICASTER_BEAN_NAME, ApplicationEventMulticaster.class);
		if (logger.isTraceEnabled()) {
			logger.trace("Using ApplicationEventMulticaster [" + this.applicationEventMulticaster + "]");
		}
	}
	else {
		this.applicationEventMulticaster = new SimpleApplicationEventMulticaster(beanFactory); // 默认使用这个
		beanFactory.registerSingleton(APPLICATION_EVENT_MULTICASTER_BEAN_NAME, this.applicationEventMulticaster);
		if (logger.isTraceEnabled()) {
			logger.trace("No '" + APPLICATION_EVENT_MULTICASTER_BEAN_NAME + "' bean, using " +
					"[" + this.applicationEventMulticaster.getClass().getSimpleName() + "]");
		}
	}
}
```

<font style="color:rgb(51, 51, 51);">initApplicationEventMulticaster这个方法是在springIOC容器refresh时被调用的。</font>

<font style="color:rgb(51, 51, 51);">而实际上ApplicationEventPublisher 发布事件的底层实现，也是通过getApplicationEventMulticaster().multicastEvent(applicationEvent, eventType); 实现的。ApplicationEventPublisher 没有直接实现。</font>

```plain
public class ApplicationPublisherDemo implements ApplicationEventPublisherAware {

    @Override
    public void setApplicationEventPublisher(ApplicationEventPublisher applicationEventPublisher) {
        applicationEventPublisher.publishEvent(new ApplicationEvent("hello world") {
        });
        applicationEventPublisher.publishEvent("generic object");
    }

    public static void main(String[] args) {
        AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext();
        context.addApplicationListener(System.out::println);
        context.register(ApplicationPublisherDemo.class);
        context.refresh();
        context.start();
        context.close();
    }
}
```

<font style="color:rgb(51, 51, 51);">实现了ApplicationEventPublisherAware 接口可以获取到ApplicationEventPublisher ，从而直接发送事件（这种事件貌似只能通过addApplicationListener添加的监听器接收到，通过注解的方式是接收不到的，具体原因尚不明确）。</font><font style="color:rgb(51, 51, 51);">也可以通过通过 @Autowired ApplicationEventPublisher 来依赖注入ApplicationEventPublisher 。</font>

##### <font style="color:rgb(51, 51, 51);">ApplicationEventPublisher与ApplicationEventMulticaster的关联</font>
<font style="color:rgb(51, 51, 51);">两个的接口之间没有关系。</font>

<font style="color:rgb(51, 51, 51);">ApplicationEventPublisher的publishEvent方法底层其实是调用了ApplicationEventMulticaster的multicastEvent方法，而SimpleApplicationEventMulticaster作为ApplicationEventMulticaster的一个默认实现，是支持异步事件发送的：</font>

```plain
// org.springframework.context.event.SimpleApplicationEventMulticaster#multicastEvent(org.springframework.context.ApplicationEvent, org.springframework.core.ResolvableType)
@Override
public void multicastEvent(final ApplicationEvent event, @Nullable ResolvableType eventType) {
	ResolvableType type = (eventType != null ? eventType : resolveDefaultEventType(event));
	Executor executor = getTaskExecutor();
	for (ApplicationListener<?> listener : getApplicationListeners(event, type)) {
		if (executor != null) {
			executor.execute(() -> invokeListener(listener, event));
		}
		else {
			invokeListener(listener, event);
		}
	}
}
```

### <font style="color:rgb(51, 51, 51);">9. Spring 层次性上下文事件传播</font>
<font style="color:rgb(51, 51, 51);">当 Spring 应用出现多层次 Spring 应用上下文（ApplicationContext）时，如 Spring WebMVC、Spring Boot 或 Spring Cloud 场景下，由子 ApplicationContext 发起的 Spring 事件可能会传递到其 Parent ApplicationContext（直到 Root）的过程.</font>

<font style="color:rgb(51, 51, 51);">应该如何避免事件传播呢？可通过定位 Spring 事件源（ApllicationEvent）进行过滤处理，可通过缓存已处理事件来解决</font>

```plain
public class HierarchicalEventDemo {
    public static void main(String[] args) {
        // create parent context
        AnnotationConfigApplicationContext parent = new AnnotationConfigApplicationContext();
        parent.setId("parent");

        // create sub context
        AnnotationConfigApplicationContext current = new AnnotationConfigApplicationContext();
        current.setId("current");

        current.setParent(parent);

        parent.register(MyListener.class);
        current.register(MyListener.class);

        parent.refresh();
        current.refresh();

        current.close();
        parent.close();
    }
}
```

<font style="color:rgb(51, 51, 51);">运行结果：</font>

```plain
receive ContextRefreshedEvent event from id [parent]
receive ContextRefreshedEvent event from id [current]
receive ContextClosedEvent event from id [current]
receive ContextClosedEvent event from id [parent]
```

### <font style="color:rgb(51, 51, 51);">10. Spring 内建事件</font>
<font style="color:rgb(51, 51, 51);">ApplicationContextEvent 派生事件</font>

<font style="color:rgb(51, 51, 51);">ContextRefreashEvent：Spring 应用上下文就绪事件——context#refreash</font>

<font style="color:rgb(51, 51, 51);">ContextStartedEvent：Spring 应用上下文启动事件——context#start</font>

<font style="color:rgb(51, 51, 51);">ContextStopedEvent：Spring 应用上下文停止事件——context#stop</font>

<font style="color:rgb(51, 51, 51);">ContextClosedEvent：Spring 应用上下文关闭事件——context#close</font>

<font style="color:rgb(51, 51, 51);">context的refresh方法最终会调用finishRefresh方法，会调用publishEvent方法发送ContextRefreshedEvent事件。</font>

<font style="color:rgb(51, 51, 51);">AbstractApplicationContext实现了ApplicationContext，ApplicationContext继承了ApplicationEventPublisher，所以在底层是可以发布事件的。</font>

### <font style="color:rgb(51, 51, 51);">11. Spring 4.2 Payload 事件</font>
<font style="color:rgb(51, 51, 51);">Spring Payload 事件——org.springframework.context.PayloadApplicationEvent</font>

<font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">PayloadApplicationEvent</font><font style="color:rgb(51, 51, 51);">是一个特殊类型的事件，用于传递自定义的负载（payload）数据。它允许开发者在应用程序中定义和传递自定义事件，以及相关的负载数据。</font>

<font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">PayloadApplicationEvent</font><font style="color:rgb(51, 51, 51);">类继承自</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">ApplicationEvent</font><font style="color:rgb(51, 51, 51);">，并添加了一个泛型参数用于指定负载数据的类型。通过使用</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">PayloadApplicationEvent</font><font style="color:rgb(51, 51, 51);">，可以在事件发布和监听的过程中传递自定义的负载数据。</font>

### <font style="color:rgb(51, 51, 51);">12. 自定义 Spring 事件</font>
### <font style="color:rgb(51, 51, 51);">13. 依赖注入 ApplicationEventPublisher</font>
### <font style="color:rgb(51, 51, 51);">14. 依赖查找 ApplicationEventMulticaster</font>
### <font style="color:rgb(51, 51, 51);">15. ApplicationEventPublisher 底层实现</font>
### <font style="color:rgb(51, 51, 51);">16. 同步和异步 Spring 事件广播</font>
<font style="color:rgb(51, 51, 51);">ApplicationEventMulticaster的一个默认实现就是SimpleApplicationEventMulticaster，它的multicastEvent如下：</font>

```plain
// org.springframework.context.event.SimpleApplicationEventMulticaster#multicastEvent(org.springframework.context.ApplicationEvent, org.springframework.core.ResolvableType)
@Override
public void multicastEvent(final ApplicationEvent event, @Nullable ResolvableType eventType) {
	ResolvableType type = (eventType != null ? eventType : resolveDefaultEventType(event));
	Executor executor = getTaskExecutor();
	for (ApplicationListener<?> listener : getApplicationListeners(event, type)) {
		if (executor != null) {
			executor.execute(() -> invokeListener(listener, event));
		}
		else {
			invokeListener(listener, event);
		}
	}
}
```

### <font style="color:rgb(51, 51, 51);">17. Spring 4.1 事件异常处理</font>
### <font style="color:rgb(51, 51, 51);">18. Spring 事件/监听器实现原理</font>
<font style="color:rgb(51, 51, 51);">SimpleApplicationEventMulticaster先继承了AbstractApplicationEventMulticaster，</font><font style="color:rgb(51, 51, 51);">AbstractApplicationEventMulticaster又实现了ApplicationEventMulticaster, BeanClassLoaderAware, BeanFactoryAware。</font>

```plain
// org.springframework.context.event.AbstractApplicationEventMulticaster#addApplicationListener
@Override
public void addApplicationListener(ApplicationListener<?> listener) {
	synchronized (this.retrievalMutex) {
		// Explicitly remove target for a proxy, if registered already,
		// in order to avoid double invocations of the same listener.
		Object singletonTarget = AopProxyUtils.getSingletonTarget(listener);
		if (singletonTarget instanceof ApplicationListener) {
			this.defaultRetriever.applicationListeners.remove(singletonTarget);
		}
		this.defaultRetriever.applicationListeners.add(listener);
		this.retrieverCache.clear();
	}
}
```

<font style="color:rgb(51, 51, 51);">defaultRetriever就是ListenerRetriever一个内部类，保存着ApplicationListener的集合：</font>

public final Set<ApplicationListener<?>> applicationListeners = new LinkedHashSet<>();

<font style="color:rgb(51, 51, 51);">在AbstractApplicationEventMulticaster定义了一个</font>

final Map<ListenerCacheKey, ListenerRetriever> retrieverCache = new ConcurrentHashMap<>(64);

<font style="color:rgb(51, 51, 51);">ListenerCacheKey就是将ApplicationEvent的泛型，里面存着ResolvableType。</font>

```plain
//实际上，我们上面分析到，调用multicastEvent方法时，会获取所有的ApplicationListener：
org.springframework.context.event.SimpleApplicationEventMulticaster#multicastEvent(org.springframework.context.ApplicationEvent, org.springframework.core.ResolvableType)
@Override
public void multicastEvent(final ApplicationEvent event, @Nullable ResolvableType eventType) {
	ResolvableType type = (eventType != null ? eventType : resolveDefaultEventType(event));
	Executor executor = getTaskExecutor();
	for (ApplicationListener<?> listener : getApplicationListeners(event, type)) {
		if (executor != null) {
			executor.execute(() -> invokeListener(listener, event));
		}
		else {
			invokeListener(listener, event);
		}
	}
}
```

```plain
org.springframework.context.event.AbstractApplicationEventMulticaster#getApplicationListeners(org.springframework.context.ApplicationEvent, org.springframework.core.ResolvableType)
protected Collection<ApplicationListener<?>> getApplicationListeners(
		ApplicationEvent event, ResolvableType eventType) {

	Object source = event.getSource();
	Class<?> sourceType = (source != null ? source.getClass() : null);
	ListenerCacheKey cacheKey = new ListenerCacheKey(eventType, sourceType);
	
	// Quick check for existing entry on ConcurrentHashMap...
	ListenerRetriever retriever = this.retrieverCache.get(cacheKey);
	if (retriever != null) {
		return retriever.getApplicationListeners(); // 一个类型关联多个监听器
	}
	
	if (this.beanClassLoader == null ||
			(ClassUtils.isCacheSafe(event.getClass(), this.beanClassLoader) &&
					(sourceType == null || ClassUtils.isCacheSafe(sourceType, this.beanClassLoader)))) {
		// Fully synchronized building and caching of a ListenerRetriever
		synchronized (this.retrievalMutex) {
			retriever = this.retrieverCache.get(cacheKey);
			if (retriever != null) {
				return retriever.getApplicationListeners();
			}
			retriever = new ListenerRetriever(true);
			Collection<ApplicationListener<?>> listeners =
					retrieveApplicationListeners(eventType, sourceType, retriever);
			this.retrieverCache.put(cacheKey, retriever);
			return listeners;
		}
	}
	else {
		// No ListenerRetriever caching -> no synchronization necessary
		return retrieveApplicationListeners(eventType, sourceType, null);
	}
```

在获取所有的Listener时，会首先通过泛型构造一个ListenerCacheKey，来确定查找监听指定类型的监听器，迭代这些监听器挨个进行通知。

<font style="color:rgb(51, 51, 51);">这也是可以解释了，为什么可以单独监听指定事件的类型了：</font>

```plain
context.addApplicationListener(new ApplicationListener<ApplicationEvent>() {
    @Override
    public void onApplicationEvent(ApplicationEvent event) {
        println("ApplicationListener - 接收到 Spring 事件：" + event);
    }
});

context.addApplicationListener(new ApplicationListener<ContextRefreshedEvent>() {
    @Override
    public void onApplicationEvent(ContextRefreshedEvent event) {
        println("ApplicationListener - 接收到 Spring 事件：" + event);
    }
});
```

<font style="color:rgb(51, 51, 51);">基于注解的监听器如何注册</font><font style="color:rgb(51, 51, 51);">1.org.springframework.context.annotation.AnnotationConfigUtils#registerAnnotationConfigProcessors(org.springframework.beans.factory.support.BeanDefinitionRegistry) 注册所有相关注解的post processor到beanRegistry里面，其中就包括监 听器相关的EventListenerMethodProcessor</font>

<font style="color:rgb(51, 51, 51);">2.该类的这个方法org.springframework.context.event.EventListenerMethodProcessor#afterSingletonsInstantiated会在bean实例化的中被调用。</font>

<font style="color:rgb(51, 51, 51);">3.org.springframework.context.event.EventListenerMethodProcessor#processBean 最终在这个方法找到相关注解并不listener注册到ApplicationContext中</font>

<font style="color:rgb(51, 51, 51);">其实spring的很多功能都是通过扩展post processor来完成的。</font>

# <font style="color:rgb(51, 51, 51);">注解驱动开发</font>
### <font style="color:rgb(51, 51, 51);">1. Spring 注解驱动编程发展历程</font>
### <font style="color:rgb(51, 51, 51);">2. Spring 核心注解场景分类</font>
<font style="color:rgb(51, 51, 51);">Spring 模式注解</font><font style="color:rgb(51, 51, 51);">@Repository</font><font style="color:rgb(51, 51, 51);">			</font><font style="color:rgb(51, 51, 51);">数据仓储模式注解</font><font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);">2.0</font><font style="color:rgb(51, 51, 51);"> @Component</font><font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);"> 通用组件模式注解</font><font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);">2.5</font><font style="color:rgb(51, 51, 51);"> @Service</font><font style="color:rgb(51, 51, 51);">				</font><font style="color:rgb(51, 51, 51);"> 服务模式注解</font><font style="color:rgb(51, 51, 51);">				</font><font style="color:rgb(51, 51, 51);">2.5</font><font style="color:rgb(51, 51, 51);"> @Controller Web 控制器模式注解</font><font style="color:rgb(51, 51, 51);">			</font><font style="color:rgb(51, 51, 51);">2.5</font><font style="color:rgb(51, 51, 51);"> @Configuration</font><font style="color:rgb(51, 51, 51);">	</font><font style="color:rgb(51, 51, 51);"> 配置类模式注解</font><font style="color:rgb(51, 51, 51);">			</font><font style="color:rgb(51, 51, 51);">3.0</font>

<font style="color:rgb(51, 51, 51);">•装配注解</font><font style="color:rgb(51, 51, 51);">@ImportResource</font><font style="color:rgb(51, 51, 51);">								</font><font style="color:rgb(51, 51, 51);">替换 XML 元素 </font><font style="color:rgb(167, 167, 167);"><import></font><font style="color:rgb(51, 51, 51);">										</font><font style="color:rgb(51, 51, 51);"> 2.5</font><font style="color:rgb(51, 51, 51);"> @Import 导入 Configuration类</font><font style="color:rgb(51, 51, 51);">			</font><font style="color:rgb(51, 51, 51);">								</font><font style="color:rgb(51, 51, 51);"> 2.5</font><font style="color:rgb(51, 51, 51);"> @ComponentScan</font><font style="color:rgb(51, 51, 51);">							</font><font style="color:rgb(51, 51, 51);"> 扫描指定 package 下标注 Spring 模式注解的类</font><font style="color:rgb(51, 51, 51);">	</font><font style="color:rgb(51, 51, 51);"> 3.1</font>

<font style="color:rgb(51, 51, 51);">•依赖注入注解</font><font style="color:rgb(51, 51, 51);">@Autowired Bean </font><font style="color:rgb(51, 51, 51);">				</font><font style="color:rgb(51, 51, 51);">依赖注入，支持多种依赖查找方式 </font><font style="color:rgb(51, 51, 51);">	</font><font style="color:rgb(51, 51, 51);">2.5</font><font style="color:rgb(51, 51, 51);"> @Qualifier</font><font style="color:rgb(51, 51, 51);">							</font><font style="color:rgb(51, 51, 51);"> 细粒度的@Autowired 依赖查找</font><font style="color:rgb(51, 51, 51);">						</font><font style="color:rgb(51, 51, 51);">2.5</font>

### <font style="color:rgb(51, 51, 51);">3. Spring 注解编程模型</font>
<font style="color:rgb(51, 51, 51);">略</font>

### <font style="color:rgb(51, 51, 51);">4. Spring 元注解（Meta-Annotations）</font>
<font style="color:rgb(51, 51, 51);">Java 5 定义了4个注解，分别是 @Documented、@Target、@Retention 和 @Inherited。 Java 8 又增加了 @Repeatable 和 @Native 两个注解。</font>

### <font style="color:rgb(51, 51, 51);">5. Spring 模式注解（Stereotype Annotations）</font>
<font style="color:rgb(51, 51, 51);">@Component 派生性原理</font>

<font style="color:rgb(0, 0, 0);background-color:rgb(0, 191, 255);">派生性：@Component注解作为Spring容器托管的通用模式组件,</font>_<font style="color:rgb(0, 0, 0);background-color:rgb(0, 191, 255);">任何被@Component标注的组件均为组件扫描的候选对象。</font>_

<font style="color:rgb(0, 0, 0);background-color:rgb(0, 191, 255);">Java语言规定,Annotation不允许继承,没有类派生子类的特性,因此Spring采用元标注的方式实现注解之间的派生。</font>

<font style="color:rgb(51, 51, 51);">核心组件——orgspringframework.context.annotation.ClassPathBeanDefinitionScanner</font>

<font style="color:rgb(51, 51, 51);">orgspringframework.context.annotation.ClassPathScanningCandidateComponentProvider</font>

<font style="color:rgb(51, 51, 51);">当</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">ClassPathBeanDefinitionScanner#doScan(String... basePackages)</font><font style="color:rgb(51, 51, 51);">调用时,它利用basePackages参数迭代执行的</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">findCandidateComponents(String basePackage)</font><font style="color:rgb(51, 51, 51);">,每次执行结果都生成候选的BeanDefinition集合,即candidates变量</font>

```plain
public class ClassPathBeanDefinitionScanner extends ClassPathScanningCandidateComponentProvider{
    ...
 protected Set<BeanDefinitionHolder> doScan(String... basePackages) {
        Assert.notEmpty(basePackages, "At least one base package must be specified");
        //获取候选的BeanDefinition集合
        Set<BeanDefinitionHolder> beanDefinitions = new LinkedHashSet<BeanDefinitionHolder>();
        for (String basePackage : basePackages) {
            Set<BeanDefinition> candidates = findCandidateComponents(basePackage);
            ...
        }
        return beanDefinitions;
    }   
    ...
}
```

<font style="color:rgb(51, 51, 51);">findCandidateComponents(String basePackage)从父类ClassPathScanningCandidateComponentProvider中继承。</font>

<font style="color:rgb(51, 51, 51);">ClassPathScanningCandidateComponentProvider构造参数</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">useDefaultFilters为true</font><font style="color:rgb(51, 51, 51);">,并且显示传递给父类构造参数。该方法给属性</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">includeFilters</font><font style="color:rgb(51, 51, 51);">增添了</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">@Component</font><font style="color:rgb(51, 51, 51);">类型AnnotationTypeFilter的TypeFilter。</font>

<font style="color:rgb(0, 0, 0);background-color:rgb(0, 191, 255);">ClassPathBeanDefinitionScanner默认过滤器引入标注@Component,@Repository,@Service或者@Controller等类。</font><font style="color:rgb(0, 0, 0);background-color:rgb(243, 244, 244);">同理,它也能够标注所有@Component的"派生"注解。</font>

<font style="color:rgb(51, 51, 51);">Dubbo实现</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">@Service</font><font style="color:rgb(51, 51, 51);">注解扫描实例:</font>

**<font style="color:rgb(119, 119, 119);">ClassPathBeanDefinitionScanner</font>**<font style="color:rgb(119, 119, 119);">允许自定义类型过滤规则。因此,Dubbo的@Service没有标注@Component情况下，通过scanner.addIncludeFilter(new AnnotationTypeFilter(Service.class))方式达到识别@Service标注类情况。但是没有使用</font><font style="color:rgb(119, 119, 119);background-color:rgb(243, 244, 244);">@Component</font><font style="color:rgb(119, 119, 119);">注解的派生性。</font>

<font style="color:rgb(0, 0, 0);background-color:rgb(0, 191, 255);">我的理解：ClassPathBeanDefinitionScanner中识别了所有带@Component注解的注解，然后通过自定义Scanner可以在不标注@Component注解的情况下被扫描。</font>

<font style="color:rgb(51, 51, 51);">Mybatis的@Mapper注解的Scanner：</font>

```plain
public class ClassPathMapperScanner extends ClassPathBeanDefinitionScanner{
    
    ...
        
  public ClassPathMapperScanner(BeanDefinitionRegistry registry) {
    super(registry, false);
  }
```

<font style="color:rgb(51, 51, 51);">资源处理——org.springframework.core.io.support.ResourcePatternResolver</font>

<font style="color:rgb(51, 51, 51);">资源-类元信息</font>

<font style="color:rgb(51, 51, 51);">org.springframework.core.type.classreading.MetadataReaderFactory</font>

<font style="color:rgb(51, 51, 51);">类元信息——orgspringframework.core.type.ClassMetadata</font>

<font style="color:rgb(51, 51, 51);">ASM 实现——org.springframework.core.type.classreading.ClassMetadataReadingVisitor</font>

<font style="color:rgb(51, 51, 51);">反射实现——org.springframework.core.type.StandardAnnotationMetadata</font>

<font style="color:rgb(51, 51, 51);">注解元信息——orgspringframework.core.type.AnnotationMetadata</font>

<font style="color:rgb(51, 51, 51);">ASM 实现——org.springframework.core.type.classreading.AnnotationMetadataReadingVisitor</font>

<font style="color:rgb(51, 51, 51);">反射实现——org.springframework.core.type.StandardAnnotationMetadata</font>

### <font style="color:rgb(51, 51, 51);">6. Spring 组合注解（Composed Annotations）</font>
### <font style="color:rgb(51, 51, 51);">7. Spring 注解属性别名（Attribute Aliases）</font>
**<font style="color:rgb(51, 51, 51);">@AliasFor</font>**

```plain
import org.springframework.core.annotation.AliasFor;

@MyAnnotation
public class MyClass {

    @MyAttribute("value1")
    public void method1() {
        // 方法逻辑
    }

    @MyAttribute("value2")
    public void method2() {
        // 方法逻辑
    }
}

@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.METHOD)
public @interface MyAttribute {
    @AliasFor("value")
    String name() default "";

    @AliasFor("name")
    String value() default "";
}

@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.TYPE)
public @interface MyAnnotation {
    String value() default "";
}
```

<font style="color:rgb(51, 51, 51);">在注解中，属性方法与其他类/接口方法写法类似，但是存在一些区别。</font>

<font style="color:rgb(51, 51, 51);">注解属性方法的返回类型仅限为八种基本类型(包装类不支持)，字符串，class，enum，Annotation以及前面类型的数组。</font>

<font style="color:rgb(51, 51, 51);">在 Spring 中，有一些注解，使用不同属性方法，却能到达相同结果。典型的如 RequestMapping 。</font>

<font style="color:rgb(51, 51, 51);">在 WEB 项目中，设置 url 路径，我们可以在方法是这样声明：</font>

```plain
@RequestMapping("hello")	
    public String helloAnnotation() {	
  。。。。	
    }
```

<font style="color:rgb(51, 51, 51);">上面方法本质使用注解 value 属性。当注解声明时只需要设置一个方法时，如果属性方法为 value，不需要使用 key=value 的语法，只需要直接设置属性值即可。</font>

<font style="color:rgb(51, 51, 51);">另外也可以使用 path 属性方法设置。</font>

```plain
@RequestMapping(path = "hello")	
    public String helloAnnotation() {	
  。。。。	
    }
```

<font style="color:rgb(51, 51, 51);">在 Spring 中别名可以分为以下几类：</font>

1. <font style="color:rgb(51, 51, 51);">显式别名（</font>**<font style="color:rgb(51, 51, 51);">xplicit Aliases</font>**<font style="color:rgb(51, 51, 51);">）:如果一个注解中的两个成员通过 @AliasFor声明后互为别名，那么它们是显式别名。</font>
2. <font style="color:rgb(51, 51, 51);">隐式别名（</font>**<font style="color:rgb(51, 51, 51);">Implicit Aliases</font>**<font style="color:rgb(51, 51, 51);">）:如果一个注解中的两个或者更多成员通过@AliasFor声明去覆盖同一个元注解的成员值，它们就是隐式别名。</font>
3. <font style="color:rgb(51, 51, 51);">传递隐式别名（</font>**<font style="color:rgb(51, 51, 51);">Transitive Implicit Aliases</font>**<font style="color:rgb(51, 51, 51);">）:如果一个注解中的两个或者更多成员通过@AliasFor声明去覆盖元注解中的不同成员，但是实际上因为[覆盖的传递性]</font>

<font style="color:rgb(51, 51, 51);">以上三类都需要满足以下条件：</font>

1. <font style="color:rgb(51, 51, 51);">属性类型相同</font>
2. <font style="color:rgb(51, 51, 51);">属性方法必须存在默认值</font>
3. <font style="color:rgb(51, 51, 51);">属性默认值必须相同</font>

### <font style="color:rgb(51, 51, 51);">8. Spring注解属性覆盖（Attribute Overrides）</font>
<font style="color:rgb(51, 51, 51);">属性覆盖指的是注解的一个成员覆盖另一个成员，最后两者成员属性值一致。</font>

1. <font style="color:rgb(51, 51, 51);">隐式覆盖（</font>**<font style="color:rgb(51, 51, 51);">Implicit Overrides</font>**<font style="color:rgb(51, 51, 51);">）:当一个注解 @One 被元注解 @Two 标注，两个注解存在同样的属性方法 name。@Two#name 将会被 @One#name 属性覆盖。</font>
2. <font style="color:rgb(51, 51, 51);">显示覆盖（</font>_**<font style="color:rgb(51, 51, 51);">*</font>**__**<font style="color:rgb(51, 51, 51);">Explicit Overrides</font>**__**<font style="color:rgb(51, 51, 51);">*</font>**_<font style="color:rgb(51, 51, 51);">）:显示覆盖就比较简单了，使用 @AliasFor 注解之后，就成为显示覆盖。</font>
3. <font style="color:rgb(51, 51, 51);">传递式显式覆盖（</font>**<font style="color:rgb(51, 51, 51);">Transitive Explicit Overrides</font>**<font style="color:rgb(51, 51, 51);">）:如果注解 @One#name 显示覆盖了 @Two#nameAlias,而 @Two#nameAlias显示覆盖了 @Three#nameAlias，最后因为传递性，@One#name 实际覆盖了@Three#nameAlias。</font>

### <font style="color:rgb(51, 51, 51);">9. Spring @Enable 模块驱动</font>
<font style="color:rgb(51, 51, 51);">@Enable 模块驱动：@Enable 模块驱动是以 @Enable 为前缀的注解驱动编程模型。所谓"模块"是指具备相同领域的功能组件集合，组合所形成一个独立的单元。比如 Web MVC 模块、AspectJ 代理模块、Caching（缓存）模块、JMX（Java 管理扩展）模块、Async（异步处理）模块等。</font>

<font style="color:rgb(51, 51, 51);">举例说明：</font>

<font style="color:rgb(51, 51, 51);">@EnableWebMvc</font>

<font style="color:rgb(51, 51, 51);">@EnableTransactionManagement</font>

<font style="color:rgb(51, 51, 51);">@EnableCaching</font>

<font style="color:rgb(51, 51, 51);">@EnableMBeanExport</font>

<font style="color:rgb(51, 51, 51);">@EnableAsync</font>

```plain
@Configuration
@EnableWebMvc
public class WebMvcConfig extends WebMvcConfigurerAdapter {
    // 配置其他的 MVC 相关内容
}
```

<font style="color:rgb(51, 51, 51);">需要注意的是，</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">@EnableWebMvc</font><font style="color:rgb(51, 51, 51);"> 注解通常与其他的配置类一起使用，例如继承自 </font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">WebMvcConfigurerAdapter</font><font style="color:rgb(51, 51, 51);"> 的配置类，用于进一步自定义和配置 MVC 的行为。在这个配置类中，你可以重写一些方法，以提供自定义的配置，例如添加拦截器、配置消息转换器、设置静态资源路径等。</font>

<font style="color:rgb(51, 51, 51);">@Enable 模块驱动编程模式</font>

<font style="color:rgb(51, 51, 51);">驱动注解：@EnableXXX</font>

<font style="color:rgb(51, 51, 51);">导入注解：@Import 具体实现</font>

<font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">@Import</font><font style="color:rgb(51, 51, 51);"> 是一个注解，用于在 Spring 中导入其他配置类或组件类。通过使用 </font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">@Import</font><font style="color:rgb(51, 51, 51);"> 注解，可以将其他类引入到当前的配置类中，从而实现配置的组合和重用。</font>

<font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">@Import</font><font style="color:rgb(51, 51, 51);"> 注解可以用于以下几种情况：</font>

1. <font style="color:rgb(51, 51, 51);">导入配置类：可以使用 </font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">@Import</font><font style="color:rgb(51, 51, 51);"> 注解将其他的配置类导入到当前的配置类中，从而将它们的配置合并在一起。这样可以方便地组合多个配置类，使得配置更加模块化和可维护。</font>
2. <font style="color:rgb(51, 51, 51);">导入组件类：除了配置类，</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">@Import</font><font style="color:rgb(51, 51, 51);"> 注解还可以用于导入其他的组件类（例如普通的 Java 类、接口等）。通过导入组件类，可以将它们交由 Spring 管理，并在应用程序中进行使用。</font>

```plain
@Configuration
@Import({DatabaseConfig.class, SecurityConfig.class})
public class AppConfig {
    // 配置内容
}
```

<font style="color:rgb(51, 51, 51);">具体实现：</font>

<font style="color:rgb(51, 51, 51);">基于 Configuration Class</font>

<font style="color:rgb(51, 51, 51);">基于 ImportSelector 接口实现</font>

<font style="color:rgb(51, 51, 51);">基于 ImportBeanDefinitionRegistrar 接口实现</font>

### <font style="color:rgb(51, 51, 51);">10. Spring 条件注解</font>
<font style="color:rgb(51, 51, 51);">@Profile</font>

<font style="color:rgb(51, 51, 51);">@Conditional </font>

### <font style="color:rgb(51, 51, 51);">11. @PropertySource</font>
# <font style="color:rgb(51, 51, 51);">Spring Environment 抽象</font>
### <font style="color:rgb(51, 51, 51);">1. 什么是Spring Environment 抽象</font>
<font style="color:rgb(51, 51, 51);">Spring Environment 抽象是 Spring 框架提供的一个核心组件，用于封装应用程序的配置信息和环境变量，并提供统一的访问方式。主要目的是为了解耦应用程序的配置和具体的配置来源，使得应用程序可以更加灵活地适应不同的部署环境和配置方式。它提供了一种统一的编程接口，用于获取和操作应用程序的配置属性。</font>

<font style="color:rgb(51, 51, 51);">通过 Spring Environment 抽象，开发人员可以通过编程方式访问和操作配置属性，而不需要直接依赖具体的配置文件或环境变量。这样可以降低代码的耦合度，提高代码的可维护性和可测试性。</font>

<font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">Environment</font><font style="color:rgb(51, 51, 51);">接口是在容器中抽象集成，应用环境包括两个重要的方面：</font>[profiles](https://link.zhihu.com/?target=https%3A//docs.spring.io/spring/docs/5.2.6.RELEASE/spring-framework-reference/core.html%23beans-definition-profiles)<font style="color:rgb(51, 51, 51);"> 和 </font>[properties](https://link.zhihu.com/?target=https%3A//docs.spring.io/spring/docs/5.2.6.RELEASE/spring-framework-reference/core.html%23beans-property-source-abstraction)<font style="color:rgb(51, 51, 51);">。</font>

```plain
//`Environment`接口定义了一些常用的方法，如：
getProperty(String key);//根据指定的键获取配置属性的值。
getProperty(String key, String defaultValue);//根据指定的键获取配置属性的值，如果属性不存在，则返回默认值。
getRequiredProperty(String key);//根据指定的键获取配置属性的值，如果属性不存在，则抛出异常。
containsProperty(String key);//判断是否存在指定键的配置属性。
```

### <font style="color:rgb(51, 51, 51);">2.使用场景</font>
1. <font style="color:rgb(51, 51, 51);">配置属性访问：通过Environment接口，可以方便地获取应用程序的配置属性。这些属性可以存储在各种配置文件（如.properties、.yml等）中，也可以作为系统环境变量或命令行参数传递给应用程序。使用Environment接口，可以轻松地获取这些属性的值，以便在应用程序中进行配置。</font>
2. <font style="color:rgb(51, 51, 51);">环境变量访问：Environment接口还提供了方便的方式来获取操作系统的环境变量。这对于需要根据不同的环境（例如开发、测试、生产）加载不同配置的应用程序非常有用。</font>
3. <font style="color:rgb(51, 51, 51);">多环境支持：Spring Framework支持多个环境（如开发、测试、生产等），并提供了相应的配置文件来区分这些环境。通过Environment接口，可以获取当前应用程序运行的环境名称，从而根据不同的环境加载相应的配置。</font>
4. <font style="color:rgb(51, 51, 51);">Profile支持：Spring Framework的Profile功能允许在不同的环境中使用不同的配置。通过Environment接口，可以获取当前活动的Profile列表，并根据需要进行相应的配置。</font>
5. <font style="color:rgb(51, 51, 51);">属性解析：Environment接口提供了属性解析的功能，可以解析配置文件中的占位符，例如</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">${my.property}</font><font style="color:rgb(51, 51, 51);">。这对于构建动态配置非常有用，可以根据其他属性的值动态计算属性值。</font>

### <font style="color:rgb(51, 51, 51);">3.占位符处理</font>
<font style="color:rgb(51, 51, 51);">Environment接口提供了属性解析的功能，可以处理配置文件中的占位符。占位符是一种特殊的标记，用于表示将在运行时动态替换的值。</font>

<font style="color:rgb(51, 51, 51);">在Spring Framework中，Environment接口提供了属性解析的功能，可以处理配置文件中的占位符。占位符是一种特殊的标记，用于表示将在运行时动态替换的值。</font>

<font style="color:rgb(51, 51, 51);">Spring Framework提供了几种占位符处理的方式：</font>

1. <font style="color:rgb(51, 51, 51);">属性占位符：属性占位符是最常见的一种占位符形式，使用</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">${}</font><font style="color:rgb(51, 51, 51);">包裹属性的名称。在配置文件中，可以使用</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">${propertyName}</font><font style="color:rgb(51, 51, 51);">的形式定义一个属性占位符，然后在运行时通过Environment接口解析并替换为实际的属性值。</font><font style="color:rgb(51, 51, 51);">示例：</font>

```plain
my.property=Hello, ${name}!
```

在上面的示例中，`${name}`是一个属性占位符，它将被解析为实际的属性值。
```

2. <font style="color:rgb(51, 51, 51);">默认值占位符：默认值占位符是属性占位符的一种扩展形式，用于在属性值不存在时提供一个默认值。默认值占位符使用</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">${}</font><font style="color:rgb(51, 51, 51);">包裹属性的名称，并在名称后面使用冒号</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">:</font><font style="color:rgb(51, 51, 51);">和默认值。</font><font style="color:rgb(51, 51, 51);">示例：</font>

```plain
my.property=${name:default}
```

在上面的示例中，如果属性`name`存在，则`${name}`将被解析为属性值；如果属性`name`不存在，则`${name:default}`将被解析为`default`。
```

3. <font style="color:rgb(51, 51, 51);">系统属性占位符：除了在配置文件中定义属性占位符，还可以在运行时使用系统属性来提供属性值。系统属性占位符使用</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">${}</font><font style="color:rgb(51, 51, 51);">包裹系统属性的名称，并在名称前面添加</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">sys</font><font style="color:rgb(51, 51, 51);">前缀。</font><font style="color:rgb(51, 51, 51);">示例：</font>

```plain
my.property=${sys:user.home}
```

在上面的示例中，`${sys:user.home}`是一个系统属性占位符，它将被解析为系统属性`user.home`的值。
```

4. <font style="color:rgb(51, 51, 51);">环境变量占位符：环境变量占位符用于引用操作系统环境变量的值。环境变量占位符使用</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">${}</font><font style="color:rgb(51, 51, 51);">包裹环境变量的名称，并在名称前面添加</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">env</font><font style="color:rgb(51, 51, 51);">前缀。</font><font style="color:rgb(51, 51, 51);">示例：</font>

```plain
my.property=${env:JAVA_HOME}
```
在上面的示例中，`${env:JAVA_HOME}`是一个环境变量占位符，它将被解析为环境变量`JAVA_HOME`的值。
```

<font style="color:rgb(51, 51, 51);">通过使用这些占位符处理方式，可以在配置文件中使用动态的属性值，使配置更加灵活和可配置化。在运行时，Spring Framework会自动解析占位符并替换为实际的值。这样，可以根据不同的环境、系统属性或环境变量来动态配置应用程序。</font>

<font style="color:rgb(51, 51, 51);">• Spring 3.1 前占位符处理</font><font style="color:rgb(51, 51, 51);">• 组件：org.springframework.beans.factory.config.PropertyPlaceholderConfigurer</font><font style="color:rgb(51, 51, 51);"> • 接口：org.springframework.util.StringValueResolver</font><font style="color:rgb(51, 51, 51);"> • Spring 3.1 + 占位符处理</font><font style="color:rgb(51, 51, 51);">• 组件：org.springframework.context.support.PropertySourcesPlaceholderConfigurer</font><font style="color:rgb(51, 51, 51);"> • 接口：org.springframework.beans.factory.config.EmbeddedValueResolver</font>

### <font style="color:rgb(51, 51, 51);">4. 条件配置 Spring Profiles</font>
<font style="color:rgb(51, 51, 51);">• Spring 3.1 条件配置</font><font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);">• API：org.springframework.core.env.ConfigurableEnvironment</font><font style="color:rgb(51, 51, 51);">				</font><font style="color:rgb(51, 51, 51);">• 修改：addActiveProfile(String)、setActiveProfiles(String...) 和 setDefaultProfiles(String...)</font><font style="color:rgb(51, 51, 51);">				</font><font style="color:rgb(51, 51, 51);">• 获取：getActiveProfiles() 和 getDefaultProfiles()</font><font style="color:rgb(51, 51, 51);">				</font><font style="color:rgb(51, 51, 51);"> • 匹配：#acceptsProfiles(String...) 和 acceptsProfiles(Profiles)</font><font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);">• 注解：@org.springframework.context.annotation.Profile</font>

<font style="color:rgb(51, 51, 51);">Spring 4 重构 @Profile</font><font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);">• 基于 Spring 4 org.springframework.context.annotation.Condition 接口实现</font><font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);"> • org.springframework.context.annotation.ProfileCondition</font>

### <font style="color:rgb(51, 51, 51);">5.获取Environment</font>
```plain
//间接依赖注入 
//通过 ApplicationContextAware 接口回调 
//通过 @Autowired 注入 ApplicationContext(略)
import org.springframework.beans.BeansException;
import org.springframework.context.ApplicationContext;
import org.springframework.context.ApplicationContextAware;
import org.springframework.core.env.Environment;

public class MyBean implements ApplicationContextAware {
    private ApplicationContext applicationContext;

    @Override
    public void setApplicationContext(ApplicationContext applicationContext) throws BeansException {
        this.applicationContext = applicationContext;
    }

    public void doSomethingWithEnvironment() {
        Environment environment = applicationContext.getEnvironment();
        // 使用Environment接口的方法
    }
}
```

```plain
//直接依赖注入
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.core.env.Environment;

public class MyBean {
    @Autowired
    private Environment environment;

    // 使用Environment接口的方法
}
------------------------------------------------------------------------------------------------
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.core.env.Environment;

public class MyBean {
    private Environment environment;

    @Autowired
    public MyBean(Environment environment) {
        this.environment = environment;
    }

    // 使用Environment接口的方法
}
------------------------------------------------------------------------------------------------
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.core.env.Environment;

public class MyBean {
    private Environment environment;

    @Autowired
    public void setEnvironment(Environment environment) {
        this.environment = environment;
    }

    // 使用Environment接口的方法
}
```

```plain
//依赖查找
//直接依赖查找：通过 org.springframework.context.ConfigurableApplicationContext#ENVIRONMENT_BEAN_NAME。
Environment environment = context.getBean(ConfigurableApplicationContext.ENVIRONMENT_BEAN_NAME, Environment.class);
------------------------------------------------------------------------------------------------
//间接依赖查找(如下)
import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;
import org.springframework.core.env.Environment;

public class MyApp {
    public static void main(String[] args) {
        ApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");
        Environment environment = context.getEnvironment();

        // 使用Environment接口的方法
    }
}
```

### <font style="color:rgb(51, 51, 51);">6. 依赖注入@Value</font>
<font style="color:rgb(51, 51, 51);">org.springframework.beans.factory.annotation.AutowiredAnnotationBeanPostProcessor</font>

### <font style="color:rgb(51, 51, 51);">7.Spring 配置属性源 PropertySource(s)</font>
<font style="color:rgb(51, 51, 51);">在Spring中，可以使用</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">@PropertySource</font><font style="color:rgb(51, 51, 51);">注解或配置文件来定义属性源（PropertySource）。属性源用于提供应用程序的配置属性，例如数据库连接信息、日志级别等。</font>

```plain
@Configuration
@PropertySource("classpath:config.properties")
public class AppConfig {
    // 配置其他的Bean和属性
}

<context:property-placeholder location="classpath:config.properties" />
    
@Component
public class MyComponent {
    @Autowired
    private Environment environment;

    public void doSomething() {
        String myProperty = environment.getProperty("my.property");//使用Environment接口获取属性值，当然还可以设置
        // 使用myProperty属性
    }
}

------------------------------------------------------------------------------------------------

@Configuration
@PropertySources({
    @PropertySource("classpath:config1.properties"),
    @PropertySource("classpath:config2.properties")
})
public class AppConfig {
    // 配置其他的Bean和属性
}

<context:property-placeholder location="classpath:config1.properties" />
<context:property-placeholder location="classpath:config2.properties" />
    

public class MyApp {
    public static void main(String[] args) {
        MutablePropertySources propertySources = new MutablePropertySources();

        // 创建一个属性源
        PropertySource<?> propertySource = new PropertiesPropertySource("myPropertySource", myProperties);

        // 添加属性源
        propertySources.addFirst(propertySource);

        // 使用属性源
        // ...

        // 删除属性源
        propertySources.remove("myPropertySource");
    }
}
```

### <font style="color:rgb(51, 51, 51);">8.Spring 內建的配置属性源</font>
# <font style="color:rgb(51, 51, 51);">Spring应用上下文生命周期</font>
### <font style="color:rgb(51, 51, 51);">1、创建spring应用上下文</font>
AnnotationConfigApplicationContext configApplicationContext = new AnnotationConfigApplicationContext();

<font style="color:rgb(51, 51, 51);">AnnotationConfigApplicationContext继承了GenericApplicationContext类。</font>

```plain
public GenericApplicationContext() {
    this.beanFactory = new DefaultListableBeanFactory();
}
```

```plain
public AnnotationConfigApplicationContext() {
    //创建AnnotatedBeanDefinitionReader：用来读取及注册通过注解方式定义的bean
    this.reader = new AnnotatedBeanDefinitionReader(this); //@1
    //创建ClassPathBeanDefinitionScanner：bean定义扫描器，可以扫描包中的类，对满足条件的类，会将其注册到spring容器中
    this.scanner = new ClassPathBeanDefinitionScanner(this);
}
```

<font style="color:rgb(51, 51, 51);">new AnnotatedBeanDefinitionReader(this)内部，会向spring容器中注册5个关键的bean：</font>

**<font style="color:rgb(51, 51, 51);">ConfigurationClassPostProcessor</font>**<font style="color:rgb(51, 51, 51);">：基本上我们自定义的bean都是通过这个类注册的</font>

**<font style="color:rgb(51, 51, 51);">AutowiredAnnotationBeanPostProcessor</font>**<font style="color:rgb(51, 51, 51);">：负责处理@Autowire注解</font>

**<font style="color:rgb(51, 51, 51);">CommonAnnotationBeanPostProcessor</font>**<font style="color:rgb(51, 51, 51);">：负责处理@Resource注解</font>

**<font style="color:rgb(51, 51, 51);">EventListenerMethodProcessor</font>**<font style="color:rgb(51, 51, 51);">：负责处理@EventListener标注的方法，即事件处理器</font>

**<font style="color:rgb(51, 51, 51);">DefaultEventListenerFactory</font>**<font style="color:rgb(51, 51, 51);">：负责将@EventListener标注的方法包装为ApplicationListener对象</font>

### <font style="color:rgb(51, 51, 51);">接下来的2</font><font style="color:rgb(51, 51, 51);">~</font><font style="color:rgb(51, 51, 51);">14阶段全部位于refresh方法中</font>
```plain
org.springframework.context.support.AbstractApplicationContext#refresh

@Override
public void refresh() throws BeansException, IllegalStateException {
    // 阶段2：Spring应用上下文启动准备阶段
    prepareRefresh();

    // 阶段3：BeanFactory创建阶段
    ConfigurableListableBeanFactory beanFactory = obtainFreshBeanFactory();

    // 阶段4：BeanFactory准备阶段
    prepareBeanFactory(beanFactory);

    try {
        // 阶段5：BeanFactory后置处理阶段
        postProcessBeanFactory(beanFactory);

        // 阶段6：BeanFactory注册BeanPostProcessor阶段
        invokeBeanFactoryPostProcessors(beanFactory);

        // 阶段7：注册BeanPostProcessor
        registerBeanPostProcessors(beanFactory);

        // 阶段8：初始化内建Bean：MessageSource
        initMessageSource();

        // 阶段9：初始化内建Bean：Spring事件广播器
        initApplicationEventMulticaster();

        // 阶段10：Spring应用上下文刷新阶段，由子类实现
        onRefresh();

        // 阶段11：Spring事件监听器注册阶段
        registerListeners();

        // 阶段12：实例化所有剩余的（非lazy init）单例。
        finishBeanFactoryInitialization(beanFactory);

        // 阶段13：刷新完成阶段
        finishRefresh();
    }
}
```

### <font style="color:rgb(51, 51, 51);">2、上下文启动准备阶段(prepareRefresh())</font>
```plain
protected void prepareRefresh() {
    // 标记启动时间
    this.startupDate = System.currentTimeMillis();
    // 是否关闭：false
    this.closed.set(false);
    // 是否启动：true
    this.active.set(true);

    // 初始化PropertySource，留个子类去实现的，可以在这个方法中扩展属性配置信息，丢到this.environment中
    initPropertySources();

    // 验证环境配置中是否包含必须的配置参数信息，比如我们希望上下文启动中，this.environment中必须要有某些属性的配置，才可以启动，那么可以在这个里面验证
    getEnvironment().validateRequiredProperties();

    // earlyApplicationListeners用来存放早期的事件监听器
    if (this.earlyApplicationListeners == null) {
        this.earlyApplicationListeners = new LinkedHashSet<>(this.applicationListeners);
    }
    else {
        // Reset local application listeners to pre-refresh state.
        this.applicationListeners.clear();
        this.applicationListeners.addAll(this.earlyApplicationListeners);
    }

    // earlyApplicationEvents用来存放早期的事件
    this.earlyApplicationEvents = new LinkedHashSet<>();
}
```

**<font style="color:rgb(51, 51, 51);">早期事件与早期的事件监听器</font>**<font style="color:rgb(51, 51, 51);">：当事件广播器</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">applicationEventMulticaster</font><font style="color:rgb(51, 51, 51);">还未准备好的时候，此时向上下文中添加的事件就是早期的事件，会被放到</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">this.earlyApplicationEvents</font><font style="color:rgb(51, 51, 51);">中，此时这个事件暂时没办法广播</font>

### <font style="color:rgb(51, 51, 51);">3、BeanFactory创建阶段（ConfigurableListableBeanFactory beanFactory = obtainFreshBeanFactory();）</font>
```plain
protected ConfigurableListableBeanFactory obtainFreshBeanFactory() {
    //刷新BeanFactory，由子类实现
    refreshBeanFactory();
    //返回spring上下文中创建好的BeanFacotry
    return getBeanFactory();
}
```

### <font style="color:rgb(51, 51, 51);">4、BeanFactory准备阶段（prepareBeanFactory(beanFactory);）</font>
```plain
protected void prepareBeanFactory(ConfigurableListableBeanFactory beanFactory) {
    // 设置类加载器
    beanFactory.setBeanClassLoader(getClassLoader());
    // 设置spel表达式解析器
    beanFactory.setBeanExpressionResolver(new StandardBeanExpressionResolver(beanFactory.getBeanClassLoader()));
    // 设置属性编辑器注册器
    beanFactory.addPropertyEditorRegistrar(new ResourceEditorRegistrar(this, getEnvironment()));

    // @1：添加一个BeanPostProcessor：ApplicationContextAwareProcessor，当你的bean实现了spring中xxxAware这样的接口，那么bean创建的过程中，将由ApplicationContextAwareProcessor来回调这些接口，将对象注入进去
    beanFactory.addBeanPostProcessor(new ApplicationContextAwareProcessor(this));
    // @2：自动注入的时候，下面这些接口定义的方法，将会被跳过自动注入，为什么？因为这部分接口将由ApplicationContextAwareProcessor来回调注入
    beanFactory.ignoreDependencyInterface(EnvironmentAware.class);
    beanFactory.ignoreDependencyInterface(EmbeddedValueResolverAware.class);
    beanFactory.ignoreDependencyInterface(ResourceLoaderAware.class);
    beanFactory.ignoreDependencyInterface(ApplicationEventPublisherAware.class);
    beanFactory.ignoreDependencyInterface(MessageSourceAware.class);
    beanFactory.ignoreDependencyInterface(ApplicationContextAware.class);

    // @3:注册依赖注入的时候查找的对象，比如你的bean中想用ResourceLoader，那么可以写：@Autowire private ResourceLoader resourceLoader，那么spring容器会将spring容器上下文注入进去
    beanFactory.registerResolvableDependency(BeanFactory.class, beanFactory);
    beanFactory.registerResolvableDependency(ResourceLoader.class, this);
    beanFactory.registerResolvableDependency(ApplicationEventPublisher.class, this);
    beanFactory.registerResolvableDependency(ApplicationContext.class, this);

    // @4:注入一个beanpostprocessor：ApplicationListenerDetector
    beanFactory.addBeanPostProcessor(new ApplicationListenerDetector(this));

    // @5:将Environment注册到spring容器，对应的bean名称是environment
    if (!beanFactory.containsLocalBean(ENVIRONMENT_BEAN_NAME)) {
        beanFactory.registerSingleton(ENVIRONMENT_BEAN_NAME, getEnvironment());
    }
    // @6:将系统属性注册到spring容器，对应的bean名称是systemProperties
    if (!beanFactory.containsLocalBean(SYSTEM_PROPERTIES_BEAN_NAME)) {
        beanFactory.registerSingleton(SYSTEM_PROPERTIES_BEAN_NAME, getEnvironment().getSystemProperties());
    }
    // @7:将系统环境变量配置信息注入到spring容器，对应的bean名称是systemEnvironment
    if (!beanFactory.containsLocalBean(SYSTEM_ENVIRONMENT_BEAN_NAME)) {
        beanFactory.registerSingleton(SYSTEM_ENVIRONMENT_BEAN_NAME, getEnvironment().getSystemEnvironment());
    }
}
```

### <font style="color:rgb(51, 51, 51);">5、BeanFactory后置处理阶段(postProcessBeanFactory(beanFactory);)</font>
<font style="color:rgb(51, 51, 51);">这个方法留给子类实现的，此时beanFactory已经创建好了，但是容器中的bean还没有被实例化，子类可以实现这个方法，可以对BeanFactory做一些特殊的配置，比如可以添加一些自定义BeanPostProcessor等等，主要是留给子类去扩展的。</font>

### <font style="color:rgb(51, 51, 51);">6、BeanFactory注册BeanPostProcessor阶段</font>
invokeBeanFactoryPostProcessors(beanFactory);

<font style="color:rgb(51, 51, 51);">从spring容器中找到BeanFactoryPostProcessor接口的所有实现类，然后调用，完成所有bean注册的功能，注意是bean注册，即将bean的定义信息转换为BeanDefinition对象，然后注册到spring容器中，此时bean还未被实例化，下面继续。</font>

<font style="color:rgb(51, 51, 51);">再回头看一下阶段1，阶段1在spring容器中注册了一个非常关键的bean：ConfigurationClassPostProcessor</font>

<font style="color:rgb(51, 51, 51);">ConfigurationClassPostProcessor就实现了BeanFactoryPostProcessor接口，所以ConfigurationClassPostProcessor会在阶段6中被调用，</font><font style="color:rgb(0, 0, 0);background-color:rgb(0, 191, 255);">下面这些注解都是在这个类中处理的</font><font style="color:rgb(51, 51, 51);">，所以想研究下面这些注解原理的，直接看去看ConfigurationClassPostProcessor的源码，非常关键重要的一个类，研究spring源码，此类必看</font>

```plain
@Configuration
@Component
@PropertySource
@PropertySources
@ComponentScan
@ComponentScans
@Import
@ImportResource
@Bean
```

registerBeanPostProcessors(beanFactory);

<font style="color:rgb(51, 51, 51);">注册BeanPostProcessor，这个阶段会遍历spring容器bean定义列表，把所有实现了BeanPostProcessor接口的bean撸出来，然后将他们添加到spring容器的BeanPostProcessor列表中。</font>

<font style="color:rgb(51, 51, 51);">BeanPostProcessor是bean后置处理器，其内部提供了很多方法，用来对bean创建的过程进行扩展的。</font>

### <font style="color:rgb(51, 51, 51);">7、初始化内建Bean：MessageSource</font>
initMessageSource();

### <font style="color:rgb(51, 51, 51);">8、初始化内建Bean：Spring事件广播器(initApplicationEventMulticaster();)</font>
<font style="color:rgb(51, 51, 51);">ApplicationEventMulticaster是事件广播器，用来广播事件的，这个阶段会将ApplicationEventMulticaster创建好.</font>

### <font style="color:rgb(51, 51, 51);">9、Spring应用上下文刷新阶段</font>
onRefresh();

<font style="color:rgb(51, 51, 51);">用来初始化其他特殊的bean，由子类去实现。</font>

### <font style="color:rgb(51, 51, 51);">10、Spring事件监听器注册阶段</font>
registerListeners();

```plain
protected void registerListeners() {
    // @1:先注册静态指定的侦听器,即将spring上下文中添加的时间监听器，添加到时间广播器（ApplicationEventMulticaster）中
    for (ApplicationListener<?> listener : getApplicationListeners()) {
        getApplicationEventMulticaster().addApplicationListener(listener);
    }

    // @2:将spring容器中定义的事件监听器，添加到时间广播器（ApplicationEventMulticaster）中
    String[] listenerBeanNames = getBeanNamesForType(ApplicationListener.class, true, false);
    for (String listenerBeanName : listenerBeanNames) {
        getApplicationEventMulticaster().addApplicationListenerBean(listenerBeanName);
    }

    // @3:此时事件广播器准备好了，所以此时发布早期的事件（早期的事件由于事件广播器还未被创建，所以先被放在了earlyApplicationEvents中，而此时广播器创建好了，所以将早期的时间发布一下）
    Set<ApplicationEvent> earlyEventsToProcess = this.earlyApplicationEvents;
    this.earlyApplicationEvents = null;
    if (earlyEventsToProcess != null) {
        for (ApplicationEvent earlyEvent : earlyEventsToProcess) {
            getApplicationEventMulticaster().multicastEvent(earlyEvent);
        }
    }
}
```

<font style="color:rgb(51, 51, 51);">如果你在阶段10之前，调用了下面方法发布事件，那么可能此时你看不到事件产生的效果</font>

applicationContext.publishEvent(事件对象)

### <font style="color:rgb(51, 51, 51);">11、单例bean实例化阶段:实例化所有剩余的（非lazy init）单例</font>
finishBeanFactoryInitialization(beanFactory);

```plain
protected void finishBeanFactoryInitialization(ConfigurableListableBeanFactory beanFactory) {
    // 添加${}表达式解析器
    if (!beanFactory.hasEmbeddedValueResolver()) {
        beanFactory.addEmbeddedValueResolver(strVal -> getEnvironment().resolvePlaceholders(strVal));
    }

    // 冻结所有bean定义，表示已注册的bean定义不会被进一步修改或后处理。这允许工厂主动缓存bean定义元数据。
    beanFactory.freezeConfiguration();

    // @1：实例化所有单例bean（不包含需延迟实例化的bean），通常scope=singleton的bean都会在下面这个方法中完成初始化。
    beanFactory.preInstantiateSingletons();
}
```

```plain
protected void finishBeanFactoryInitialization(ConfigurableListableBeanFactory beanFactory) {
    // 添加${}表达式解析器
    if (!beanFactory.hasEmbeddedValueResolver()) {
        beanFactory.addEmbeddedValueResolver(strVal -> getEnvironment().resolvePlaceholders(strVal));
    }

    // 冻结所有bean定义，表示已注册的bean定义不会被进一步修改或后处理。这允许工厂主动缓存bean定义元数据。
    beanFactory.freezeConfiguration();

    // @1：实例化所有单例bean（不包含需延迟实例化的bean），通常scope=singleton的bean都会在下面这个方法中完成初始化。
    beanFactory.preInstantiateSingletons();
}
```

### <font style="color:rgb(51, 51, 51);">12、BeanFactory初始化完成阶段(finishRefresh();)</font>
```plain
protected void finishRefresh() {
    // @1：清理一些资源缓存
    clearResourceCaches();

    // @2：为此上下文初始化生命周期处理器
    initLifecycleProcessor();

    // @3：首先将刷新传播到生命周期处理器
    getLifecycleProcessor().onRefresh();

    // @4：发布ContextRefreshedEvent事件
    publishEvent(new ContextRefreshedEvent(this));
}
```

### <font style="color:rgb(51, 51, 51);">13、Spring应用上下文启动完成阶段</font>
### <font style="color:rgb(51, 51, 51);">14、Spring应用上下文关闭阶段(applicationContext.close())</font>
```plain
org.springframework.context.support.AbstractApplicationContext#doClose

protected void doClose() {
    // 判断是不是需要关闭（active为tue的时候，才能关闭，并用cas确保并发情况下只能有一个执行成功）
    if (this.active.get() && this.closed.compareAndSet(false, true)) {
        
        //@1：发布关闭事件ContextClosedEvent
        publishEvent(new ContextClosedEvent(this));

        // @2：调用生命周期处理器的onClose方法
        if (this.lifecycleProcessor != null) {
            this.lifecycleProcessor.onClose();
        }

        // @3：销毁上下文的BeanFactory中所有缓存的单例
        destroyBeans();

        // @4：关闭BeanFactory本身
        closeBeanFactory();

        // @5：就给子类去扩展的
        onClose();

        // @6：恢复事件监听器列表至刷新之前的状态，即将早期的事件监听器还原
        if (this.earlyApplicationListeners != null) {
            this.applicationListeners.clear();
            this.applicationListeners.addAll(this.earlyApplicationListeners);
        }

        // @7：标记活动状态为：false
        this.active.set(false);
    }
}
```

# <font style="color:rgb(51, 51, 51);">问题</font>
### <font style="color:rgb(51, 51, 51);">1. 控制反转到底反转了什么？</font>
<font style="color:rgb(51, 51, 51);">反转了获取依赖对象的过程。传统的模式思自己实例化对象交给容器，控制反转中是从容器中拿实例化好的对象。</font>

### <font style="color:rgb(51, 51, 51);">2. java反射的三种方式？</font>
<font style="color:rgb(51, 51, 51);">有三种方法获得类的Class对象：Class.forName(String className)、className.class、实例对象.getClass()。</font>

### <font style="color:rgb(51, 51, 51);">3. java反射的三个部分？</font>
+ <font style="color:rgb(51, 51, 51);">类的加载：Java的类在需要使用时才会被加载到JVM中。这个过程是由类加载器（ClassLoader）完成的。类加载器首先检查这个类是否已经被加载过，如果还没有加载，那么就会从磁盘上加载类的字节码并创建一个Class对象。</font>
+ <font style="color:rgb(51, 51, 51);">获取类的信息：当一个对象被创建后，我们可以使用反射来获取这个对象的Class对象。通过这个Class对象，我们可以获取到这个类的所有属性和方法。</font>
+ <font style="color:rgb(51, 51, 51);">方法的调用：通过反射，我们可以动态的调用一个对象的方法。即使这个方法是一个私有的方法，也能够通过反射来调用。</font>

### <font style="color:rgb(51, 51, 51);">4. java反射可以获取哪些信息?</font>
<font style="color:rgb(51, 51, 51);">类的方法、属性、构造函数等.</font>

```plain
Class 类:
forName(String className)：根据类的全限定名获取对应的Class对象。

newInstance()：创建该类的一个实例对象。

getConstructor(Class<?>... parameterTypes)：获取该类的指定构造函数。

getDeclaredConstructor(Class<?>... parameterTypes)：获取该类的指定构造函数，不考虑其访问权限。

getMethod(String name, Class<?>... parameterTypes)：获取该类的指定公共方法。

getDeclaredMethod(String name, Class<?>... parameterTypes)：获取该类的指定方法，不考虑其访问权限。

getField(String name)：获取该类的指定公共字段。

getDeclaredField(String name)：获取该类的指定字段，不考虑其访问权限。
    
Constructor类:

newInstance(Object... initargs)：使用指定的参数创建该构造函数所表示的类的新实例。

getParameterTypes()：获取该构造函数的参数类型。

getModifiers()：获取该构造函数的修饰符。

isVarArgs()：判断该构造函数是否支持可变参数。

isAccessible()：判断该构造函数是否可以被访问。

setAccessible(boolean flag)：设置该构造函数的可访问标志。
    
Method类:
getMethod(String name, Class<?>... parameterTypes)：返回具有指定名称和参数类型的公共方法。

getDeclaredMethod(String name, Class<?>... parameterTypes)：返回具有指定名称和参数类型的方法，无论是否为公共方法。
    
Field类:

Field类：表示一个类的字段，可以通过它获取和设置类的属性值。Field类代表类或接口的字段，即类或接口中的变量。Field类提供了访问和操作字段的方法，包括获取字段的名称、类型、修饰符、值等。
```

### <font style="color:rgb(51, 51, 51);">5.有什么办法访问一个对象的私有成员吗?</font>
<font style="color:rgb(51, 51, 51);">通过反射可以访问和操作对象的私有成员，包括私有字段、私有方法和私有构造函数。下面是通过反射访问另一个对象的私有成员的一般步骤：</font>

1. <font style="color:rgb(51, 51, 51);">获取目标类的Class对象，可以使用Class.forName()方法或者直接使用目标类的.class属性获取。</font>
2. <font style="color:rgb(51, 51, 51);">获取私有成员的Field、Method或Constructor对象，需要使用对应的方法，如getDeclaredField()、getDeclaredMethod()或getDeclaredConstructor()。</font>
3. <font style="color:rgb(51, 51, 51);">设置私有成员的可访问性，通过调用setAccessible(true)来设置私有成员的可访问性，这将允许我们绕过访问权限限制。</font>
4. <font style="color:rgb(51, 51, 51);">使用获取到的Field、Method或Constructor对象来读取或修改私有成员的值，或者调用私有方法。</font>

```plain
import java.lang.reflect.Field;

public class Main {
    public static void main(String[] args) throws Exception {
        // 创建对象
        MyClass myObject = new MyClass();

        // 获取私有属性的Field对象
        Field privateField = MyClass.class.getDeclaredField("privateField");

        // 设置私有属性可访问
        privateField.setAccessible(true);

        // 获取私有属性的值
        int fieldValue = (int) privateField.get(myObject);
        System.out.println("Private field value: " + fieldValue);
    }
}

class MyClass {
    private int privateField = 42;
}
```

<u><font style="color:rgb(51, 51, 51);">本质上是修改class对象的属性,从而绕过访问权限.</font></u><font style="color:rgb(51, 51, 51);">注意不修改私有属性会抛出IllegalAccessException异常.</font>

<u><font style="color:rgb(51, 51, 51);">class对象是几种情况下被classLoader加载的,在需要访问class对象时需要通过classLoad进行查找(ClassLoader的上下文中存放了加载类的相关信息</font></u><font style="color:rgb(51, 51, 51);">，如类加载器的状态、已加载的类的链接信息等。这些上下文信息有助于ClassLoader进行类的查找和加载。).</font>

<font style="color:rgb(51, 51, 51);">当使用new关键字创建对象时，会通过类加载器（ClassLoader）来查找并加载对应的类。</font>

<font style="color:rgb(51, 51, 51);">具体的步骤如下：</font>

1. <font style="color:rgb(51, 51, 51);">JVM首先根据类的</font><u><font style="color:rgb(51, 51, 51);">全限定名</font></u><font style="color:rgb(51, 51, 51);">（例如：com.example.MyClass）获取当前线程的类加载器（ClassLoader）。</font>
2. <font style="color:rgb(51, 51, 51);">类加载器会根据类的全限定名，按照一定的规则和策略来查找类的字节码文件（通常是以.class文件形式存在）。</font>
3. <font style="color:rgb(51, 51, 51);">如果找到了类的字节码文件，类加载器会将字节码文件加载到内存中，并创建对应的Class对象。</font>
4. <font style="color:rgb(51, 51, 51);">最后，使用new关键字创建对象时，会通过Class对象实例化一个新的对象，并分配内存空间。</font>

<font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">反射库其实也是通过类加载器加载类的.</font>

### <font style="color:rgb(51, 51, 51);">6.class对象存在哪里?</font>
<font style="color:rgb(51, 51, 51);">由classLoader存在内存里。</font>

### <font style="color:rgb(51, 51, 51);">7. JNDI？</font>
<font style="color:rgb(51, 51, 51);">JNDI(Java Naming and Directory Interface )，即</font>[Java命名和目录接口](https://so.csdn.net/so/search?q=Java%E5%91%BD%E5%90%8D%E5%92%8C%E7%9B%AE%E5%BD%95%E6%8E%A5%E5%8F%A3&spm=1001.2101.3001.7020)<font style="color:rgb(51, 51, 51);">。</font>

<font style="color:rgb(51, 51, 51);">是SUN公司提供的一种标准的Java命名系统接口，JNDI提供统一的客户端API，通过不同的访问提供者接口JNDI服务供应接口(SPI)的实现，由管理者将JNDI API映射为特定的命名服务和目录系统，使得Java应用程序可以和这些命名服务和目录服务之间进行交互。</font>

<font style="color:rgb(51, 51, 51);">就好比在一个中心注册一个东西，以后要用的时候，只需要根据名字去注册中心查找，注册中心返回你要的东西。web程序，我们可以将一些东西(比如数据库相关的)交给服务器软件去配置和管理(有全局配置和单个web程序的配置)，在程序代码中只要通过名称查找就能得到我们注册的东西。</font>

<font style="color:rgb(51, 51, 51);">如果注册的东西有变，比如更换了数据库，我们只需要修改注册信息，名称不改，因此代码也不需要修改。</font>

```plain
//使用JNDI连接数据库
import javax.naming.Context;
import javax.naming.InitialContext;
import javax.naming.NamingException;
import javax.sql.DataSource;
import java.sql.Connection;
import java.sql.SQLException;

public class JndiExample {
    public static void main(String[] args) {
        try {
            // 创建JNDI上下文
            Context context = new InitialContext();
            
            // 查找数据源
            DataSource dataSource = (DataSource) context.lookup("java:/comp/env/jdbc/myDataSource");
            
            // 获取数据库连接
            Connection connection = dataSource.getConnection();
            
            // 执行数据库操作
            // ...
            
            // 关闭数据库连接
            connection.close();
            
            // 关闭JNDI上下文
            context.close();
        } catch (NamingException | SQLException e) {
            e.printStackTrace();
        }
    }
}
```

### <font style="color:rgb(51, 51, 51);">8. EJB与SpringFramework的关系？</font>
1. <font style="color:rgb(51, 51, 51);">EJB的起源较早，最早是在Java 2 Enterprise Edition（J2EE）规范中引入的。它</font><font style="color:rgb(0, 0, 0);background-color:rgb(0, 191, 255);">是一种基于组件的开发模型</font><font style="color:rgb(51, 51, 51);">，旨在简化企业级应用程序的开发。EJB</font><font style="color:rgb(0, 0, 0);background-color:rgb(0, 191, 255);">提供了一种将业务逻辑封装到可重用的组件中的方式，并提供了事务管理、远程访问、安全性和并发控制等功能。</font>
2. <font style="color:rgb(51, 51, 51);">Spring Framework是由Rod Johnson在2003年创建的，它是一个轻量级的开源框架，旨在简化企业级Java开发。Spring提供了一个全面的编程和配置模型，帮助开发人员构建可维护、可扩展和松耦合的应用程序。它包含了许多模块，例如依赖注入（Dependency Injection）、面向切面编程（Aspect-Oriented Programming）、数据访问、Web开发等。</font>
3. <font style="color:rgb(51, 51, 51);">Spring Framework最初是作为EJB的替代方案而出现的。在当时，</font><font style="color:rgb(0, 0, 0);background-color:rgb(0, 191, 255);">EJB的配置和开发复杂性较高，而Spring提供了更简单和灵活的替代方案。</font><font style="color:rgb(51, 51, 51);">Spring的核心概念之一是依赖注入（DI），它允许开发人员通过配置将组件之间的依赖关系委托给容器管理，从而降低了开发的复杂性。</font>
4. <font style="color:rgb(51, 51, 51);">随着时间的推移，Spring Framework发展壮大，并成为Java企业开发中最受欢迎的框架之一。它不仅提供了与EJB类似的功能，还引入了许多新的特性和改进，使开发变得更加简单和灵活。</font>
5. <font style="color:rgb(51, 51, 51);">最近的Java Enterprise Edition（Java EE）规范也对EJB进行了改进，并提供了更简化的EJB 3.0规范。这个版本的EJB更加注重简化配置和开发，并借鉴了一些Spring Framework的设计思想。因此，EJB和Spring在某种程度上开始趋同，提供了相似的功能和开发体验。</font>

### <font style="color:rgb(51, 51, 51);">9.为什么不推荐使用字段注入？</font>
1. <font style="color:rgb(51, 51, 51);">违反单一责任原则，容易不知不觉间创建一个身兼多职的类。使用构造函数注入，如果一个构造函数有多个依赖，我们会思考这可能在设计上存在问题。构造函数参数过多，甚至 IDE 也会给出警告。</font>
2. <font style="color:rgb(51, 51, 51);">由于依赖是在需要时注入，而不是在加载 context 时注入，因此 Spring 不会抛出 </font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">BeanCurrentlyInCreationException</font><font style="color:rgb(51, 51, 51);"> 异常。</font><font style="color:rgb(51, 51, 51);">通过构造函数注入，可以在编译时检测到循环依赖关系，因为它们会产生无法解决的错误。不过，自 Spring Boot 2.6 版本起，</font>[默认情况下不再允许循环依赖](https://github.com/spring-projects/spring-boot/wiki/Spring-Boot-2.6-Release-Notes#circular-references-prohibited-by-default)<font style="color:rgb(51, 51, 51);">。</font>

### <font style="color:rgb(51, 51, 51);">10. SpringAOP和AspectJ AOP 的区别？</font>
+ <font style="color:rgb(51, 51, 51);">AspectJ 是 AOP 完整实现，Spring AOP 则是部分实现Spring AOP 比AspectJ 使用更简单</font>
+ <font style="color:rgb(51, 51, 51);">Spring AOP 整合 AspectJ 注解与 Spring loC 容器</font>
+ <font style="color:rgb(51, 51, 51);">Spring AOP 仅支持基于代理模式的 AOP</font>
+ <font style="color:rgb(51, 51, 51);">Spring AOP 仅支持方法级别的 Pointcuts , 不支持字段级别的。 </font>

### <font style="color:rgb(51, 51, 51);">11.CGLib动态代理和JDK动态代理的区别？Spring用哪一个？</font>
<font style="color:rgb(51, 51, 51);">JDK：</font>

+ <font style="color:rgb(51, 51, 51);">基于接口来创建被代理对象的代理实例。当对象要被代理时，它必须实现一个或多个接口并依赖JDK库。JDK动态代理利用反射机制生成一个包含被代理对象的所有接口的代理类，并覆盖接口中的所有方法，可以对目标对象进行代理。</font>
+ <font style="color:rgb(51, 51, 51);">优点：无需引用第三方库，在JRE运行环境中就可以运行，生成代理对象更加简单、快捷；缺点：仅支持基于接口进行代理，无法对类进行代理，所以它的作用有限。</font>

<font style="color:rgb(51, 51, 51);">CGLib：</font>

+ <font style="color:rgb(51, 51, 51);">基于继承的方式对被代理类生成子类，从而添加代理逻辑。因为它是继承了被代理类，所以它会受到final类、private、static等不可继承属性的影响。</font>
+ <font style="color:rgb(51, 51, 51);">优点：Cglib支持对类进行代理，即使没有接口，也可通过设置回调接口间接地实现。性能比JDK动态代理更高，能够代理那些没有实现任何接口的目标对象。</font>

<font style="color:rgb(51, 51, 51);">Cglib在生成代理类的过程中，采用动态生成字节码的方式，在被代理类加载之前就完成了代理类的创建并缓存到内存中，以后每次调用时，都直接使用缓存的代理类。在大多数情况下，Cglib代理比JDK动态代理更适合于大规模的方法拦截和增强等场景。</font>

<font style="color:rgb(51, 51, 51);">Spring是在createProxy方法中创建代理的。在这个函数中会调用isConfigurationCallbackInterface方法来评估是否使用JDK动态代理。</font>

<font style="color:rgb(51, 51, 51);">以下几种情况使用不适用jdk动态代理：</font>

1. <font style="color:rgb(51, 51, 51);">接口是生命周期的回调接口，包括初始化、销毁和关闭容器。</font>
2. <font style="color:rgb(51, 51, 51);">接口的方法数为0.</font>
3. <font style="color:rgb(51, 51, 51);">没有实现接口.</font>

### <font style="color:rgb(51, 51, 51);">12. Spring是如何解决循环依赖的?</font>
### <font style="color:rgb(51, 51, 51);">13.BeanFactory FactoryBean 和 ObjectBean的区别？</font>
<font style="color:rgb(51, 51, 51);">BeanFactory是IoC的底层容器</font>

<font style="color:rgb(51, 51, 51);">FactoryBean是创建Bean的一种方式,帮助实现复杂的初始化逻辑</font>

<font style="color:rgb(51, 51, 51);">FactoryBean也是一个接口,通过实现里面的方法可以实现一个Bean的创建(比如一个类是由第三方实现的,想创建这个类的Bean就可以通过这个方式实现).例如重写FactoryBean中的isSingleton方法可以控制获取到的Bean是否都是同一实例. </font>

<font style="color:rgb(51, 51, 51);">ObjectFactory 与 BeanFactory 均提供依赖查找的能力。 不过 ObjectFactory 仅关注一个或一种类型的 Bean 依赖查找，并且自身不具备依赖查找的能力，能力则由 BeanFactory 输出。 BeanFactory 则提供了单一类型、集合类型以及层次性等多种依赖查 找方式</font>

<font style="color:rgb(0, 0, 0);background-color:rgb(0, 191, 255);">ObjectFactory是一个接口，获取bean时还是需要是由BeanFactory生成的。</font>

### <font style="color:rgb(51, 51, 51);">14. ApplicationContext和BeanFactory的区别?</font>
<font style="color:rgb(51, 51, 51);">ApplicationContext和BeanFactory是Spring框架中用于获取Bean对象的两个关键接口.ApplicationContext是BeanFactory的超集.ApplicationContext除了BeanFactory有的功能,还提供了:</font>

<font style="color:rgb(51, 51, 51);">面向切面 (AOP)</font><font style="color:rgb(51, 51, 51);">配置元信息 (Configuration Metadata)</font><font style="color:rgb(51, 51, 51);">资源管理 (Resources)</font><font style="color:rgb(51, 51, 51);">事件(Events)</font><font style="color:rgb(51, 51, 51);">国际化 (i18n)</font><font style="color:rgb(51, 51, 51);">注解(Annotations)</font><font style="color:rgb(51, 51, 51);">Environment 抽象 (Environment Abstraction)</font>

<font style="color:rgb(51, 51, 51);">要是只获取XML中bean对象,且不用事件和资源管理的时候,用BeanFactory即可;若想获取通过注解产生的Bean对象或高级特性,则需要用ApplicationContext.</font>

### <font style="color:rgb(51, 51, 51);">15.Spring loC 容器启动时做了哪些准备?</font>
<font style="color:rgb(51, 51, 51);">loC 配置元信息读取和解析、loC 容器生命周期、Spring 事件发布、国际化等，更多答案将在后续专题章节逐一讨论</font>

### <font style="color:rgb(51, 51, 51);">16. Spring AOP支持哪些类型的Advice（通知）？</font>
+ <font style="color:rgb(51, 51, 51);">Around Advice</font>
+ <font style="color:rgb(51, 51, 51);">Before Advice</font>
+ <font style="color:rgb(51, 51, 51);">After Advice</font>
    - <font style="color:rgb(51, 51, 51);">After</font>
    - <font style="color:rgb(51, 51, 51);">AfterReturningAfterThrowing</font>

### <font style="color:rgb(51, 51, 51);">17. Spring AOP 编程模型有哪些，代表组件有哪些?</font>
+ <font style="color:rgb(51, 51, 51);">注解驱动: 解释和整合 AspectJ 注解，如 @EnableAspectJAutoProxyXML </font>
+ <font style="color:rgb(51, 51, 51);">配置: AOP 与 loC Schema-Based 相结合</font>
+ <font style="color:rgb(51, 51, 51);">API 编程: 如 Joinpoint、Pointcut、Advice 和 ProxyFactory 等</font>

### <font style="color:rgb(51, 51, 51);">18. Spring AOP三种实现方式是如何设计的?</font>
### <font style="color:rgb(51, 51, 51);">19. Bean的名称和id？</font>
<font style="color:rgb(51, 51, 51);">id和name属性都可以在XML元数据中唯一标识某个Bean实例。通常情况下，id用于定义Bean实例的名称(beanName)，而name用于定义Bean实例的别名(aliases)。一个Bean实例可以有多个别名，在name属性中用半角逗号或分号分隔各个别名即可，如下。</font>

<font style="color:rgb(167, 167, 167);"><bean name="map,java_map;jdk_map" class="java.util.HashMap" /></font>

### <font style="color:rgb(51, 51, 51);">20. Spring的父子容器？SpringMVC中为什么最好配置父子容器？</font>
<font style="color:rgb(51, 51, 51);">创建Spring容器的时候，可以给当前容器指定一个父容器。</font>

<font style="color:rgb(51, 51, 51);">1.父容器和子容器是相互隔离的，他们内部可以存在名称相同的bean</font>

<font style="color:rgb(51, 51, 51);">2.子容器可以访问父容器中的bean，而父容器不能访问子容器中的bean</font>

<font style="color:rgb(51, 51, 51);">3.调用子容器的getBean万法获取bean的时候，会沿着当前容器开始向上面的容器进行查找，直到找到对应的bean为止</font>

<font style="color:rgb(51, 51, 51);">4.子容器中可以通过任何注入方式注入父容器中的bean，而父容器中是无法注入子容器中的bean，原因是第2点</font>

<font style="color:rgb(51, 51, 51);">SpringMVC种最好配置Service 为 Controller的父容器，这样可以防止Servicec层注入Controller层的bean，导致依赖混乱。</font>

### <font style="color:rgb(51, 51, 51);">21. Java 是一种类型安全的编程语言。</font>
<font style="color:rgb(51, 51, 51);">类型安全是指在编程过程中，对于每个变量和表达式都能够在编译时进行类型检查，以确保类型的一致性和正确性。Java 的类型系统是静态类型的，这意味着类型检查是在编译时完成的，而不是在运行时。</font>

### <font style="color:rgb(51, 51, 51);">22. </font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">@Primary</font>
<font style="color:rgb(51, 51, 51);">是一个在Spring框架中用于解决依赖注入冲突的注解。当存在多个相同类型的Bean时，使用</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">@Primary</font><font style="color:rgb(51, 51, 51);">注解可以指定其中一个Bean作为首选的主要Bean，以便在注入时优先选择该Bean</font>

### <font style="color:rgb(51, 51, 51);">23. BeanFactory.getBean操作是否线程安全？</font>
<font style="color:rgb(51, 51, 51);">BeanFactory.getBean 方法的执行是线程安全的，操作过程中会增加互 斥锁</font>

<font style="color:rgb(51, 51, 51);">Java6以后有偏向锁（虽然最近已经快没了），建议将容器初始化放在主线程内，可以减少锁竞争。</font>

### <font style="color:rgb(51, 51, 51);">24. Spring 依赖查找与注入在来源上的区别? goto 31</font>
### <font style="color:rgb(51, 51, 51);">25.有多少种依赖注入的方式？</font>
<font style="color:rgb(51, 51, 51);">构造器注入</font>

<font style="color:rgb(51, 51, 51);">Setter 注入</font>

<font style="color:rgb(51, 51, 51);">字段注入</font>

<font style="color:rgb(51, 51, 51);">方法注入</font>

<font style="color:rgb(51, 51, 51);">接口回调注入</font>

### <font style="color:rgb(51, 51, 51);">26. 你偏好构造器注入还是 Setter 注入？ </font>
<font style="color:rgb(51, 51, 51);">答：两种依赖注入的方式均可使用，如果是必须依赖的话，那么推荐使用构 造器注入，Setter 注入用于可选依赖</font>

### <font style="color:rgb(51, 51, 51);">27.AutoWired会忽略掉静态字段</font>
<font style="color:rgb(51, 51, 51);">@AutoWired放在静态字段上时不会注入</font>

### <font style="color:rgb(51, 51, 51);">28. @Autowired @Resource @Inject的区别？</font>
<font style="color:rgb(51, 51, 51);">	</font><font style="color:rgb(51, 51, 51);">@Autowired是Spring独有的，@Resource是JavaEE的， @Inject是JSR-330的（JavaSE也有）</font>

<font style="color:rgb(51, 51, 51);">	</font><font style="color:rgb(51, 51, 51);">@Resource不能用在构造器上，其他两个可以</font>

### <font style="color:rgb(51, 51, 51);">29.aware系列接口？（以BeanFactoryAware为例） </font>
<font style="color:rgb(51, 51, 51);">当一个类实现了 </font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">BeanFactoryAware</font><font style="color:rgb(51, 51, 51);"> 接口并注册为 Spring Bean 时，Spring 容器在将该 Bean 实例化后，会主动调用该 Bean 的 </font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">setBeanFactory()</font><font style="color:rgb(51, 51, 51);"> 方法，并将容器的 </font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">BeanFactory</font><font style="color:rgb(51, 51, 51);"> 实例传递给该方法。</font>

```plain
public class MyBean implements BeanFactoryAware {
    private BeanFactory beanFactory;

    @Override
    public void setBeanFactory(BeanFactory beanFactory) throws BeansException {
        this.beanFactory = beanFactory;
    }

    public void doSomething() {
        OtherBean otherBean = beanFactory.getBean(OtherBean.class);
        // 使用获取到的 OtherBean 实例进行操作
    }
}
```

### <font style="color:rgb(51, 51, 51);">30.Spring BeanDefinition?</font>
<font style="color:rgb(51, 51, 51);">在Spring框架的上下文中，BeanDefinition（Bean定义）是一种配置元数据，用于定义Spring容器如何创建和管理bean。它充当了创建应用程序中bean实例的蓝图。</font>

<font style="color:rgb(51, 51, 51);">BeanDefinition通常包含以下信息：</font>

1. <font style="color:rgb(51, 51, 51);">Bean的类名：指定要创建的bean的类。</font>
2. <font style="color:rgb(51, 51, 51);">Bean的作用域（Scope）：定义bean的生命周期和可见范围，例如单例（Singleton）、原型（Prototype）、会话（Session）等。</font>
3. <font style="color:rgb(51, 51, 51);">Bean的构造函数参数：指定创建bean实例时所需的构造函数参数。</font>
4. <font style="color:rgb(51, 51, 51);">Bean的属性值：定义bean的属性及其对应的值。</font>
5. <font style="color:rgb(51, 51, 51);">Bean的依赖关系：指定bean与其他bean之间的依赖关系，包括依赖注入和依赖查找。</font>
6. <font style="color:rgb(51, 51, 51);">Bean的初始化方法和销毁方法：定义bean的初始化操作和销毁操作。</font>

<font style="color:rgb(51, 51, 51);">Spring容器使用BeanDefinition来解析配置文件或注解，将其转换为运行时的bean实例。通过BeanDefinition，我们可以灵活地配置和管理应用程序中的bean，以满足不同的需求和场景。</font>

### <font style="color:rgb(51, 51, 51);">31. 注入和查找的依赖来源是否相同？</font>
<font style="color:rgb(51, 51, 51);">否，依赖查找的来源仅限于 Spring BeanDefinition 以及单例 对象，而依赖注入的来源还包括 Resolvable Dependency 以及 @Value 所标注的外部化配置</font>

### <font style="color:rgb(51, 51, 51);">32.单例对象能在 IoC 容器启动后注册吗？</font>
<font style="color:rgb(51, 51, 51);">可以的，单例对象的注册与 BeanDefinition 不同，BeanDefinition 会被 ConfigurableListableBeanFactory#freezeConfiguration() 方法影 响，从而冻结注册，单例对象则没有这个限制。</font>

### <font style="color:rgb(51, 51, 51);">33.Spring Cloud RefreshScope是如何控制Bean的动态刷新？(小马哥87,可以不管)</font>
### <font style="color:rgb(51, 51, 51);">34.“application”Bean 是否被其他方案替代？</font>
<font style="color:rgb(51, 51, 51);">可以的，实际上，“application” Bean 与“singleton” Bean 没有 本质区别</font>

### <font style="color:rgb(51, 51, 51);">35. @Conditional注解?</font>
<font style="color:rgb(51, 51, 51);">从spring4.0才有的，可以用在类，接口或者方法上面，通过@Conditional注解可以配置一些条件判断，当所有条件都满足的时候，被@Conditional标注的目标才会被spring容器处理。</font>

<font style="color:rgb(51, 51, 51);">这个注解只有一个value参数，Condition类型的数组，Condition是一个函数式接口，表示一个条件判断，内部有个方法返回true或false，当所有Condition都成立的时候，@Conditional的结果才成立。</font>

<font style="color:rgb(51, 51, 51);">该函数式接口内部只有一个</font>[matches方法](https://so.csdn.net/so/search?q=matches%E6%96%B9%E6%B3%95&spm=1001.2101.3001.7020)<font style="color:rgb(51, 51, 51);">，用来判断条件是否成立的，2个参数：</font>

+ <font style="color:rgb(51, 51, 51);">context：条件上下文，ConditionContext接口类型的，可以用来获取容器中的个人信息</font>
+ <font style="color:rgb(51, 51, 51);">metadata：用来获取被@Conditional标注的对象上的所有注解信息</font>

### <font style="color:rgb(51, 51, 51);">36. SpringBoot和SpringCloud</font>
### <font style="color:rgb(51, 51, 51);">37.BeanPostProcessor 的使用场景有哪些？</font>
<font style="color:rgb(51, 51, 51);">答：BeanPostProcessor 提供 Spring Bean 初始化前和初始化后的 生命周期回调，分别对应 postProcessBeforeInitialization 以及 postProcessAfterInitialization 方法，允许对关心的 Bean 进行 扩展，甚至是替换。 </font>

<font style="color:rgb(51, 51, 51);">加分项：其中，ApplicationContext 相关的 Aware 回调也是基于 BeanPostProcessor 实现，即 ApplicationContextAwareProcessor</font>

### <font style="color:rgb(51, 51, 51);">38. BeanFactoryPostProcessor 与 BeanPostProcessor 的区别?</font>
<font style="color:rgb(51, 51, 51);">BeanFactoryPostProcessor 是 Spring BeanFactory（实际为 ConfigurableListableBeanFactory） 的后置处理器，用于扩展 BeanFactory，或通过 BeanFactory 进行依赖查找和依赖注入。</font>

<font style="color:rgb(51, 51, 51);">BeanFactoryPostProcessor 必须有 Spring ApplicationContext 执行，BeanFactory 无法与其直接交互。 而BeanPostProcessor 则直接与BeanFactory 关联，属于 N 对 1 的关系 。(这一点比较偏门,不问就别答)</font>

### <font style="color:rgb(51, 51, 51);">39. 什么是BeanWrapper？</font>
<font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">BeanWrapper</font><font style="color:rgb(51, 51, 51);">是Spring框架提供的一个用于访问和操作Java对象属性的工具类。它是对Java反射机制的封装，提供了一种方便的方式来操作对象的属性。</font>

<font style="color:rgb(51, 51, 51);">通过</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">BeanWrapper</font><font style="color:rgb(51, 51, 51);">，你可以通过名称或索引访问和设置对象的属性值，而无需直接使用Java的反射API。它还提供了一些便捷的方法来处理属性的类型转换、嵌套属性访问等功能。</font>

<font style="color:rgb(51, 51, 51);">下面是</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">BeanWrapper</font><font style="color:rgb(51, 51, 51);">的一些常用方法：</font>

+ <font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">getPropertyValue(String propertyName)</font><font style="color:rgb(51, 51, 51);">: 根据属性名获取对象的属性值。</font>
+ <font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">setPropertyValue(String propertyName, Object value)</font><font style="color:rgb(51, 51, 51);">: 根据属性名设置对象的属性值。</font>
+ <font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">getPropertyDescriptor(String propertyName)</font><font style="color:rgb(51, 51, 51);">: 根据属性名获取属性的描述符，包括属性的类型、读写方法等信息。</font>
+ <font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">getPropertyType(String propertyName)</font><font style="color:rgb(51, 51, 51);">: 根据属性名获取属性的类型。</font>
+ <font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">isReadableProperty(String propertyName)</font><font style="color:rgb(51, 51, 51);">: 判断属性是否可读。</font>
+ <font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">isWritableProperty(String propertyName)</font><font style="color:rgb(51, 51, 51);">: 判断属性是否可写。</font>
+ <font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">getWrappedInstance()</font><font style="color:rgb(51, 51, 51);">: 获取包装的对象实例。</font>

### <font style="color:rgb(51, 51, 51);">40.spring三种方法添加的事件的执行顺序？</font>
<font style="color:rgb(51, 51, 51);">基于注解的Listener先执行，而后是基于接口的，最后才是注册为Bean的。</font>

### <font style="color:rgb(51, 51, 51);">41.事件的传播机制？</font>
<font style="color:rgb(51, 51, 51);">触发原因示例：</font>

```plain
//源码中context的refresh方法触发的finishRefresh方法中publishEvent触发的事件
// org.springframework.context.support.AbstractApplicationContext#publishEvent(java.lang.Object, org.springframework.core.ResolvableType)
protected void publishEvent(Object event, @Nullable ResolvableType eventType) {
	Assert.notNull(event, "Event must not be null");

	// Decorate event as an ApplicationEvent if necessary
	ApplicationEvent applicationEvent;
	if (event instanceof ApplicationEvent) {
		applicationEvent = (ApplicationEvent) event;
	}
	else {
		applicationEvent = new PayloadApplicationEvent<>(this, event);
		if (eventType == null) {
			eventType = ((PayloadApplicationEvent<?>) applicationEvent).getResolvableType();
		}
	}

	// Multicast right now if possible - or lazily once the multicaster is initialized
	if (this.earlyApplicationEvents != null) {
		this.earlyApplicationEvents.add(applicationEvent);
	}
	else {
		getApplicationEventMulticaster().multicastEvent(applicationEvent, eventType);
	}
	
    //罪魁祸首就是这一段代码
	// Publish event via parent context as well...
	if (this.parent != null) { // 递归，如果有parent的话，就传递给parent进行事件发布
		if (this.parent instanceof AbstractApplicationContext) {
			((AbstractApplicationContext) this.parent).publishEvent(event, eventType);
		}
		else {
			this.parent.publishEvent(event);
		}
	}
}
```

<font style="color:rgb(51, 51, 51);">比较简单的方式就是定义一个全局变量，如上我们的代码实例，定义了一个static的set做去重处理，同一个事件保证只能监听一次。</font>

<font style="color:rgb(51, 51, 51);">也可以注入ApplicationContext，判断事件的上下文对象是否是当前的上下文对象。从而进行过滤。</font>

event.getApplicationContext()//获取事件的上下文

### <font style="color:rgb(51, 51, 51);">42.一个Spring的小bug？</font>
<font style="color:rgb(51, 51, 51);">static class HelloPayloadApplicationEvent extends PayloadApplicationEvent</font><font style="color:rgb(167, 167, 167);"><String></font><font style="color:rgb(51, 51, 51);"> {</font>

```plain
static class HelloPayloadApplicationEvent extends PayloadApplicationEvent<String> {
    public HelloPayloadApplicationEvent(Object source, String payload) {
        super(source, payload);
    }
}
```

<font style="color:rgb(51, 51, 51);">会报错Mismatched number of generics specified，应改为</font>

```plain
static class HelloPayloadApplicationEvent<String> extends PayloadApplicationEvent<String> {
    public HelloPayloadApplicationEvent(Object source, String payload) {
        super(source, payload);
    }
}
```

<font style="color:rgb(51, 51, 51);">原文链接：</font>[https://blog.csdn.net/A_art_xiang/article/details/128789087](https://blog.csdn.net/A_art_xiang/article/details/128789087)

### <font style="color:rgb(51, 51, 51);">43.Indexed注解？</font>
<font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">5.0</font><font style="color:rgb(51, 51, 51);">版本中新增了</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">@Indexed</font><font style="color:rgb(51, 51, 51);">注解。</font>

<font style="color:rgb(51, 51, 51);">@Indexed注解的引入正是为了解决这个问题，项目编译打包时，会在自动生成META-INF/spring.components文件，文件包含被@Indexed注释的类的模式解析结果。当Spring应用上下文进行组件扫描时，META-INF/spring.components会被org.springframework.context.index.CandidateComponentsIndexLoader读取并加载，转换为CandidateComponentsIndex对象，此时组件扫描会读取CandidateComponentsIndex，而不进行实际扫描，从而提高组件扫描效率，减少应用启动时间。</font>

<font style="color:rgb(51, 51, 51);">org.springframework.stereotype包下的注解@Component、@Controller、@Service、@Repository，除@Component外，@Controller、@Service、@Repository注解也同时标记有@Component注解，所以默认情况下，索引机制针对这四个注解。当然可以自定义注解，有两种途径：</font>

<font style="color:rgb(51, 51, 51);">① 使用@Indexed作为元注解声明注解。</font>

<font style="color:rgb(51, 51, 51);">② 使用@Component、@Controller、@Service、@Repository中任一个作为元注解声明注解。</font>

### <font style="color:rgb(51, 51, 51);">44. Spring模式注解有哪些？</font>
<font style="color:rgb(51, 51, 51);">@org.springframework.stereotype.Component</font>

<font style="color:rgb(51, 51, 51);">@org.springframework.stereotype.Repository</font>

<font style="color:rgb(51, 51, 51);">@org.springframework.stereotype.Service</font>

<font style="color:rgb(51, 51, 51);">@org.springframework.stereotype.Controller</font>

<font style="color:rgb(51, 51, 51);">@org.springframework.stereotype.Configuration</font>

### <font style="color:rgb(51, 51, 51);">45.@EventListener 的工作原理？</font>
<font style="color:rgb(51, 51, 51);">org.springframework.context.event.EventListenerMethodProcessor</font>

<font style="color:rgb(51, 51, 51);">spring在真正开始初始化bean之前，需要完成的工作：大体主要包括三部分</font>

1. <font style="color:rgb(51, 51, 51);">初始化AnnotatedBeanDefinitionReader</font>
2. <font style="color:rgb(51, 51, 51);">初始化ClassPathBeanDefinitionScanner</font>
3. <font style="color:rgb(51, 51, 51);">将配置类注册到BeanDefinitionMap中</font>

<font style="color:rgb(51, 51, 51);">其中，有两个bean，就是EventListenerMethodProcessor和DefaultEventListenerFactory.</font>

### <font style="color:rgb(51, 51, 51);">46.@ComponentScan和@ComponentScans?</font>
+ <font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">@ComponentScan</font><font style="color:rgb(51, 51, 51);"> 注解是 Spring 框架的核心注解之一，用于启用组件扫描并指定要扫描的包或类路径。</font>
+ <font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">@ComponentScans</font><font style="color:rgb(51, 51, 51);"> 注解是 Spring 5 引入的注解，也用于启用组件扫描，但它的功能更加灵活。</font>
+ <font style="color:rgb(51, 51, 51);">与 </font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">@ComponentScan</font><font style="color:rgb(51, 51, 51);"> 注解不同的是，</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">@ComponentScans</font><font style="color:rgb(51, 51, 51);"> 注解可以同时指定多个 </font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">@ComponentScan</font><font style="color:rgb(51, 51, 51);"> 注解的配置。</font>
+ <font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">@ComponentScans</font><font style="color:rgb(51, 51, 51);"> 注解接受一个数组参数，每个数组元素都是一个 </font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">@ComponentScan</font><font style="color:rgb(51, 51, 51);"> 注解的配置，可以指定不同的包或类路径进行扫描。</font>

```plain
@Configuration
@ComponentScans({
    @ComponentScan("com.example.app.service"),
    @ComponentScan("com.example.app.repository")
})
public class AppConfig {
    // 配置内容
}
```

<font style="color:rgb(51, 51, 51);">注意ComponentScan会扫描子包</font>

### <font style="color:rgb(51, 51, 51);">47.@Configuration？</font>
<font style="color:rgb(51, 51, 51);">这个注解组合了@Component注解，会被当成Bean管理。</font>

<font style="color:rgb(51, 51, 51);">加上@Configuration注解主要是给我们的类加上了cglib代理。在执行我们的配置类的方法时，会执行cglib代理类中的方法，其中有一个非常重要的判断，当我们的执行方法和我们的调用方法是同一个方法时，会执行父类的方法new（cglib代理基于继承）；当执行方法和调用方法不是同一个方法时会调用beanFactory.getBean获取。</font>

<font style="color:rgb(51, 51, 51);">通过使用 CGLIB 代理，Spring 能够拦截对 </font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">@Bean</font><font style="color:rgb(51, 51, 51);"> 方法的调用，实现对 Bean 的创建、依赖注入等操作，并确保这些操作符合 Spring 容器的行为和规范。</font>

<font style="color:rgb(51, 51, 51);">需要注意的是，CGLIB 代理是基于类级别的代理，只会代理被 </font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">@Configuration</font><font style="color:rgb(51, 51, 51);"> 注解标记的类本身，而不会代理类中的其他非 </font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">@Bean</font><font style="color:rgb(51, 51, 51);"> 方法。对于类内部的方法调用，CGLIB 代理将会绕过代理，直接调用原始的方法。</font>

<font style="color:rgb(51, 51, 51);">在Spring中只要被</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">@Configuration</font><font style="color:rgb(51, 51, 51);">注解修饰的类，Spring就会为其生成代理对象，至于这样做的主要原因就是为了解决生成对象的</font>[单例](https://so.csdn.net/so/search?q=%E5%8D%95%E4%BE%8B&spm=1001.2101.3001.7020)<font style="color:rgb(51, 51, 51);">问题。</font>

<font style="color:rgb(51, 51, 51);">如果Spring不做处理，下面输出的一定的是</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">false</font><font style="color:rgb(51, 51, 51);">，但是实际上输出的结果是</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">true</font><font style="color:rgb(51, 51, 51);">，那么只有可能是代理类做了特殊处理。</font>

```plain
@Configuration
public class MyConfiguration {
    @Bean
    public TestA a(){
        return new TestA();
    }
    @Bean
    public TestB b(){
        TestA a = a();
        TestA b = a();
        System.out.println(a == b);
        return new TestB();
    }
}
```

### <font style="color:rgb(51, 51, 51);">48.为什么Dubbo的@Service注解不注上@Component？</font>
<font style="color:rgb(51, 51, 51);">为了区分 Dubbo 的服务暴露和 Spring 的组件扫描。</font>

### <font style="color:rgb(51, 51, 51);">49. 复杂对象构建考虑使用</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">FactoryBean</font><font style="color:rgb(51, 51, 51);">实现类</font>
### <font style="color:rgb(51, 51, 51);">50.简单介绍 Spring Environment 接口？</font>
<font style="color:rgb(51, 51, 51);">• 核心接口 - org.springframework.core.env.Environment</font><font style="color:rgb(51, 51, 51);"> • 父接口 - org.springframework.core.env.PropertyResolver</font><font style="color:rgb(51, 51, 51);"> • 可配置接口 - org.springframework.core.env.ConfigurableEnvironment </font><font style="color:rgb(51, 51, 51);">• 职责：</font><font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);">• 管理 Spring 配置属性源</font><font style="color:rgb(51, 51, 51);">		</font><font style="color:rgb(51, 51, 51);">• 管理 Profiles</font>

### <font style="color:rgb(51, 51, 51);">51.如何控制 PropertySource 的优先级？</font>
<font style="color:rgb(51, 51, 51);">可以使用</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">Ordered</font><font style="color:rgb(51, 51, 51);">接口或</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">@Order</font><font style="color:rgb(51, 51, 51);">注解来控制</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">PropertySource</font><font style="color:rgb(51, 51, 51);">的优先级。</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">Ordered</font><font style="color:rgb(51, 51, 51);">接口是Spring提供的一个接口，用于表示对象的顺序或优先级。</font>

```plain
import org.springframework.core.Ordered;
import org.springframework.core.env.PropertySource;

public class MyPropertySource extends PropertySource<String> implements Ordered {
    // 构造函数和其他方法

    @Override
    public int getOrder() {
        // 返回属性源的优先级，值越小优先级越高
        return 1;
    }
}
```

```plain
import org.springframework.core.Ordered;
import org.springframework.core.annotation.Order;
import org.springframework.core.env.PropertySource;

@Order(1)
public class MyPropertySource extends PropertySource<String> {
    // 构造函数和其他方法
}
```

<font style="color:rgb(51, 51, 51);">也可以通过 MutablePropertySources的api addFirst、addLast 等进行控制</font>

### <font style="color:rgb(51, 51, 51);">52.什么是早期事件？</font>**<font style="color:rgb(51, 51, 51);">什么是早期的事件监听器呢？</font>**
<font style="color:rgb(51, 51, 51);">当使用spring上下文发布事件的时候，如下代码</font>

applicationContext.publishEvent(事件对象)

<font style="color:rgb(51, 51, 51);">其内部最终会用到</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">AbstractApplicationContext</font><font style="color:rgb(51, 51, 51);">下面这个属性来发布事件，但是可能此时</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">applicationEventMulticaster</font><font style="color:rgb(51, 51, 51);">还没有创建好，是空对象，所以此时是无法广播事件的，那么此时发布的时间就是早期的时间，就会被放在</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">this.earlyApplicationEvents</font><font style="color:rgb(51, 51, 51);">中暂时存放着，当时间广播器</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">applicationEventMulticaster</font><font style="color:rgb(51, 51, 51);">创建好了之后，才会会将早期的事件广播出去</font>

private ApplicationEventMulticaster applicationEventMulticaster;

<font style="color:rgb(51, 51, 51);">同理，当</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">applicationEventMulticaster</font><font style="color:rgb(51, 51, 51);">还未准备好的时候，调用下面下面代码向spring上下文中添加事件监听器的时候，这时放进去的监听器就是早期的事件监听器。</font>

applicationContext.addApplicationListener(事件监听器对象)

<font style="color:rgb(51, 51, 51);">说了这么多，理解起来很简单，</font><font style="color:rgb(0, 0, 0);background-color:rgb(0, 191, 255);">就是当事件广播器</font><font style="color:rgb(0, 0, 0);background-color:rgb(243, 244, 244);">applicationEventMulticaster</font><font style="color:rgb(0, 0, 0);background-color:rgb(0, 191, 255);">还未准备好的时候，此时向上下文中添加的事件就是早期的事件，会被放到</font><font style="color:rgb(0, 0, 0);background-color:rgb(243, 244, 244);">this.earlyApplicationEvents</font><font style="color:rgb(0, 0, 0);background-color:rgb(0, 191, 255);">中，此时这个事件暂时没办法广播，得等广播器</font><font style="color:rgb(0, 0, 0);background-color:rgb(243, 244, 244);">applicationEventMulticaster</font><font style="color:rgb(0, 0, 0);background-color:rgb(0, 191, 255);">创建好了之后。才能广播。</font>

### <font style="color:rgb(51, 51, 51);">53.上下文的start()方法和refresh（）方法的区别？</font>
1. <font style="color:rgb(51, 51, 51);">功能不同：</font>
    - <font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">start()</font><font style="color:rgb(51, 51, 51);"> 方法主要用于启动应用程序上下文，包括初始化和刷新上下文、执行生命周期回调和启动注册的组件。</font>
    - <font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">refresh()</font><font style="color:rgb(51, 51, 51);"> 方法用于刷新应用程序上下文，它重新加载上下文的配置并重建所有的 bean 定义和实例。它会关闭当前的上下文并创建一个新的上下文实例。</font>
2. <font style="color:rgb(51, 51, 51);">调用时机不同：</font>
    - <font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">start()</font><font style="color:rgb(51, 51, 51);"> 方法在应用程序上下文创建之后，当准备好启动应用程序时调用。它通常在配置完成、bean 定义加载完毕后调用，用于启动生命周期回调和组件的启动逻辑。</font>
    - <font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">refresh()</font><font style="color:rgb(51, 51, 51);"> 方法在应用程序上下文创建之后，当需要重新加载上下文配置并重建 bean 定义时调用。它通常在应用程序运行过程中的某个时刻需要动态地刷新上下文时调用。</font>
3. <font style="color:rgb(51, 51, 51);">影响范围不同：</font>
    - <font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">start()</font><font style="color:rgb(51, 51, 51);"> 方法主要影响启动和启用在应用程序上下文中注册的组件，以及触发生命周期回调。它不会重新加载上下文配置或重建 bean 定义。</font>
    - <font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">refresh()</font><font style="color:rgb(51, 51, 51);"> 方法会关闭当前的应用程序上下文，并重新加载配置文件、重建 bean 定义和实例。它会影响整个应用程序上下文的状态。</font>

### <font style="color:rgb(51, 51, 51);">54. 为什么说 ObjectFactory 提供的是延迟依赖查找？</font>
<font style="color:rgb(51, 51, 51);">原因</font>

<font style="color:rgb(51, 51, 51);">ObjectFactory（或ObjectProvider）可关联某一类型 Bean</font>

<font style="color:rgb(51, 51, 51);">ObejctFactory 和 ObjectProvider 对象在被依赖注入和依赖查询时并未试试查找关联类型的 Bean</font>

<font style="color:rgb(51, 51, 51);">当 ObjectFactory（或 ObjectProvider）调用 getObject 方法时，目标 Bean 才被依赖查找</font>

<font style="color:rgb(51, 51, 51);">总结</font>

<font style="color:rgb(51, 51, 51);">ObjectFactory（或 ObjectProvider）相当于某一类型 Bean 依赖查找对象</font>

### <font style="color:rgb(51, 51, 51);">55.依赖查找（注入）的 Bean 会被缓存吗？</font>
<font style="color:rgb(51, 51, 51);">单例 Bean（Singleton）——会缓存</font>

<font style="color:rgb(51, 51, 51);">缓存位置：org.springframework.beans.factory.support.DefaultSingletonBeanRegistry#singletonObjects</font>

<font style="color:rgb(51, 51, 51);">原型 Bean（Prototype）——不会缓存</font>

<font style="color:rgb(51, 51, 51);">当以来查询或依赖注入时，根据 BeanDefinition 每次创建</font>

<font style="color:rgb(51, 51, 51);">其他 Scope Bean</font>

<font style="color:rgb(51, 51, 51);">request：每个 ServletRequest 内部缓存，生命周期维持在每次 HTTP 请求</font>

<font style="color:rgb(51, 51, 51);">session：每个 HttpSession 内部缓存，生命周期维持在每个用户 HTTP 会话</font>

<font style="color:rgb(51, 51, 51);">application：当前 Servlet 应用内部缓存</font>

### <font style="color:rgb(51, 51, 51);">56.@Bean 的处理流程是怎样的？</font>
+ <font style="color:rgb(51, 51, 51);">解析范围——Configuration Class 中的 @Bean 方法</font>
+ <font style="color:rgb(51, 51, 51);">方法类型——静态 @Bean 方法和实例 @Bean 方法</font>

### <font style="color:rgb(51, 51, 51);">57.BeanFactory 如何处理循环依赖？</font>
<font style="color:rgb(51, 51, 51);">预备知识</font>

<font style="color:rgb(51, 51, 51);">循环依赖开关（方法）——AbstractAutowireCapableBeanFactory#setAllowCirclarReferences</font>

<font style="color:rgb(51, 51, 51);">单例工厂（属性）——DefaultSingletonBeanRegistry#singletonFactories</font>

<font style="color:rgb(51, 51, 51);">获取早期未处理 Bean （方法）——AbstractAutowireCapableBeanFactory#getEarlyBeanReference</font>

<font style="color:rgb(51, 51, 51);">早期未处理 Bean （属性）——DefaultSingletonBeanRegistry#earlySingletonObjects</font>

<font style="color:rgb(51, 51, 51);">案例分析</font>

<font style="color:rgb(51, 51, 51);">三个 Map：singletonObject、singletonFactories、earlySingletonObjects（三级缓存）</font>

### <font style="color:rgb(51, 51, 51);">58.MyBatis 与 Spring Feamework 是如何集成的？</font>
<font style="color:rgb(51, 51, 51);">AbstractAutowiredCapableBeanFactory：populateBean</font>

<font style="color:rgb(51, 51, 51);">DefaultListableBeanFacotry：doResolveDependency（解析占位符）</font>

### <font style="color:rgb(51, 51, 51);">59.Spring源码中是在哪里将单例Bean加入缓存的？</font>
<font style="color:rgb(51, 51, 51);">单例 Bean 被加入缓存的地方是在 </font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">DefaultSingletonBeanRegistry</font><font style="color:rgb(51, 51, 51);"> 类中的 </font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">getSingleton()</font><font style="color:rgb(51, 51, 51);"> 方法中进行的。</font>

<font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">DefaultSingletonBeanRegistry</font><font style="color:rgb(51, 51, 51);"> 是 Spring 中用于管理单例 Bean 的默认实现类。在 </font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">getSingleton()</font><font style="color:rgb(51, 51, 51);"> 方法中，Spring 首先尝试从单例缓存（</font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">singletonObjects</font><font style="color:rgb(51, 51, 51);">）中获取单例 Bean 实例。如果找到了对应的实例，则直接返回。</font>

<font style="color:rgb(51, 51, 51);">如果在缓存中没有找到对应的单例 Bean 实例，那么 Spring 将尝试创建该 Bean。创建 Bean 的过程中，会调用 </font><font style="color:rgb(51, 51, 51);background-color:rgb(243, 244, 244);">createBean()</font><font style="color:rgb(51, 51, 51);"> 方法创建 Bean 实例，并在创建成功后将其加入到单例缓存中。</font>

  

