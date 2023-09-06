---
layout: post
title: Spring Boot学习笔记
categories: SpringBoot
description: Spring Boot学习笔记
keywords: SpringBoot
typora-root-url: ..
---

## 创建Spring Boot项目

[Spring Initializr](https://start.spring.io/)

使用IDEA专业版可以直接创建SpringBoot项目

### **在pom文件中加入springboot依赖**

```
<parent>
<groupId>org.springframework.boot</groupId>
<artifactId>spring-boot-starter-parent</artifactId>
<version>2.0.1.RELEASE</version>
</parent>
<dependencies>
<dependency>
<groupId>org.springframework.boot</groupId>
<artifactId>spring-boot-starter-web</artifactId>
</dependency>
</dependencies>
```

### **创建controller类**

要加上`@RestController`和`@SpringBootApplication`注解

Spring Boot 提供了默认的配置，在启动类里加入 `@SpringBootApplication` 注解，则这个类就是整个应用程序的启动类

**Spring Boot 整个应用程序只有一个配置文件**： `.properties` 或 `.yml` 文件。Spring Boot 对每个配置项都有默认值，我们可以通过**添加配置文件**来覆盖配置项的默认值。

**注意：**yaml 使用**换行+ tab** 隔开，这里需要注意的是**冒号后面必须空格**，否则会报错

### **打包，运行**

springboot有2种打包格式：**jar**和**war**

#### **war**方式

在pom文件中加入依赖

```
<packaging>war</packaging>
<build>
<finalName>index</finalName>
<resources>
<resource>
<directory>src/main/resources</directory>
<filtering>true</filtering>
</resource>
</resources>
<plugins>
<plugin>
<groupId>org.springframework.boot</groupId>
<artifactId>spring-boot-maven-plugin</artifactId>
</plugin>
<plugin>
<artifactId>maven-resources-plugin</artifactId>
<version>2.5</version>
<configuration>
<encoding>UTF-8</encoding>
</configuration>
</plugin>
<plugin>
<groupId>org.apache.maven.plugins</groupId>
<artifactId>maven-surefire-plugin</artifactId>
<version>2.18.1</version>
<configuration>
<skipTests>true</skipTests>
</configuration>
</plugin>
</plugins>
</build>
```

运行 mvn package 就会生成 war 包

修改启动类，继承SpringBootServletInitializer类，重写configure方法

```
@RestController
@SpringBootApplication
public class HelloController extends SpringBootServletInitializer{
 
@RequestMapping("hello")
String hello() {
return "Hello World!";
}
 
public static void main(String[] args) {
SpringApplication.run(HelloController.class, args);
}
@Override
protected SpringApplicationBuilder configure(SpringApplicationBuilder application) {
return application.sources(Application.class);
}
 
}
```

#### jar方式

在pom中加入依赖

```
<packaging>jar</packaging>
<build>
<finalName>api</finalName>
<resources>
<resource>
<directory>src/main/resources</directory>
<filtering>true</filtering>
</resource>
</resources>
<plugins>
<plugin>
<groupId>org.springframework.boot</groupId>
<artifactId>spring-boot-maven-plugin</artifactId>
<configuration>
<fork>true</fork>
<mainClass>com.lynn.yiyi.Application</mainClass>
</configuration>
<executions>
<execution>
<goals>
<goal>repackage</goal>
</goals>
</execution>
</executions>
</plugin>
<plugin>
<artifactId>maven-resources-plugin</artifactId>
<version>2.5</version>
<configuration>
<encoding>UTF-8</encoding>
<useDefaultDelimiters>true</useDefaultDelimiters>
</configuration>
</plugin>
<plugin>
<groupId>org.apache.maven.plugins</groupId>
<artifactId>maven-surefire-plugin</artifactId>
<version>2.18.1</version>
<configuration>
<skipTests>true</skipTests>
</configuration>
</plugin>
<plugin>
<groupId>org.apache.maven.plugins</groupId>
<artifactId>maven-compiler-plugin</artifactId>
<version>2.3.2</version>
<configuration>
<source>1.8</source>
<target>1.8</target>
</configuration>
</plugin>
</plugins>
</build>
```

通过 `mvn package` 打包，通过`java -jar api.jar`启动

## springboot项目结构

![image-20230906224055602](/images/posts/Springboot/image-20230906224055602.png)



Application.java 是程序的启动类

Startup.java 是程序启动完成前执行的类

WebConfig.java 是配置类，所有 bean 注入、配置、拦截器注入等都放在这个类里面。

### yaml/properties 文件常用配置项

- **-server.port**	应用程序启动端口	server.port=8080，定义应用程序启动端口为8080
- **server.context-path**	应用程序上下文	server.port=/api,则访问地址为：`http://ip:port/api`
- **spring.http.multipart.maxFileSize**	最大文件上传大小,-1为不限制	spring.http.multipart.maxFileSize=-1
- **spring.jpa.database**	数据库类型	spring.jpa.database=MYSQL，指定数据库为mysql
- **spring.jpa.properties.hibernate.dialect**	hql方言	spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQL5Dialect
- **spring.datasource.url**	数据库连接字符串	spring.datasource.url=jdbc:mysql://localhost:3306/database?useUnicode=true&characterEncoding=UTF-8&useSSL=true
- **spring.datasource.username**	数据库用户名	spring.datasource.username=root
- **spring.datasource.password**	数据库密码	spring.datasource.password=root
- **spring.datasource.driverClassName**	数据库驱动	spring.datasource.driverClassName=com.mysql.jdbc.Driver
- **spring.jpa.showSql**	控制台是否打印sql语句	spring.jpa.showSql=true

### 多环境配置

1. 创建 application.yml 文件，添加以下内容，指定当前项目的默认环境为 dev

```
spring:
  profiles:
    active: dev
```

2. 文件名的格式为：application-{profile}.yml，其中，{profile} 替换为环境名字，在其中添加当前环境的配置信息

## 注意事项

- service层不能调用本层的方法

## 注解

### @SpringBootApplication

指定启动类

可以使用以下3个注解来代替@SpringBootApplication

```
@SpringBootConfiguration
@EnableAutoConfiguration
@ComponentScan

SpringBootConfiguration 表示 Spring Boot 的配置注解
EnableAutoConfiguration 表示自动配置
ComponentScan 表示 Spring Boot 扫描 Bean 的规则，比如扫描哪些包
```

### @Configuration

指定配置类，比如解决跨域问题时的配置类就要加上这个注解

不过 Spring Boot 官方推荐 Spring Boot 项目用 SpringBootConfiguration 来代替 Configuration。

### @Bean

**方法级别**上的注解，主要添加在 `@Configuration` 或 `@SpringBootConfiguration` 注解的类，有时也可以添加在 `@Component` 注解的类。它的作用是定义一个Bean。

#### @Bean和@Component的区别

| @Bean                                                      | @Component |
| ---------------------------------------------------------- | ---------- |
| 方法级别                                                   | 函数级别   |
| 告诉了 `Spring` 这是某个类的实例，当我们需要用它的时候给我 |            |

### @Value

可以用来定义全局变量。server.port 就是我们在 application.yml 里面定义的属性，我们可以自定义任意属性名，通过 `@Value` 注解就可以将其取出来。

```
    @Value("${server.port}")
    String port;
    @RequestMapping("/hello")
    public String home(String name) {
        return "hi "+name+",i am from port:" +port;
    }
```



### @RestController 

表示这个类需要接收处理Web的消息

### @Data

使用在类上，就不需要自己去写构造器和setter，getter方法

```
@Data
public class Company {
    private Long id;
    private String name;
}
```

### 常用的几个注解：

@Data ： 注在类上，提供类的get、set、equals、hashCode、canEqual、toString方法
@AllArgsConstructor ： 注在类上，提供类的全参构造
@NoArgsConstructor ： 注在类上，提供类的无参构造
@Setter ： 注在属性上，提供 set 方法
@Getter ： 注在属性上，提供 get 方法
@EqualsAndHashCode ： 注在类上，提供对应的 equals 和 hashCode 方法
@Log4j/@Slf4j ： 注在类上，提供对应的 Logger 对象，变量名为 log


## spring boot添加lambok依赖

在build.gradle中

```
dependencies {
    implementation 'org.projectlombok:lombok:1.18.20'
    annotationProcessor 'org.projectlombok:lombok:1.18.20'
}
```

## spring boot处理web请求

```
@RestController
@RequestMapping("/employees")
public class EmployeeController {

    @Autowired
    private EmployeeService employeeService;

    @PostMapping
    @ResponseStatus(HttpStatus.CREATED)
    public Employee createEmployee(@RequestBody Employee employee) {
       return employeeService.createEmployee(employee);
    }

    @GetMapping
    public List<Employee> getEmployees() {
        return employeeService.getEmployees();
    }

    @GetMapping("/{id}")
    public Employee queryEmployeeById(@PathVariable Long id) {
        return employeeService.queryEmployeeById(id);
    }


    @GetMapping(params = {"gender"})
    public List<Employee> queryEmployeeByGender(@RequestParam Gender gender) {
        return employeeService.queryEmployeeByGender(gender);

    }

    @PutMapping("/{id}")
    public Employee updateEmployeeAgeAndSalary(@PathVariable Long id, @RequestBody Employee employee) {
        return employeeService.updateEmployeeAgeAndSalary(id,employee);

    }

    @DeleteMapping("/{id}")
    @ResponseStatus(HttpStatus.NO_CONTENT)
    public void deleteEmployee(@PathVariable Long id) {
        employeeService.deleteEmployee(id);
    }

    @GetMapping(params = {"page", "size"})
    public List<Employee> queryEmployeePage(@RequestParam int page, int size) {
        return employeeService.queryEmployeePage(page,size);
    }

}

```

## 内存数据库测试service层

配置文件：

```
spring:
  datasource:
    url: jdbc:h2:mem:employee_db
    driver-class-name: org.h2.Driver
    username: sa
    password: ''
  jpa:
    database-platform: org.hibernate.dialect.H2Dialect
    show-sql: true
    hibernate:
      ddl-auto: create-drop
```

## Mapper层隐藏信息

Spring boot Mapper, EmployeeRequest, EmployeeResponse可以隐藏前端获取不到的字段，或者不想让前端看到的字段，比如EmployeeQuest的时候前端并没有生成id，而后端给前端返回EmployeeResponse的时候，不希望让其他用户看到薪资信息。

## Spring boot的设计模式

[Spring Boot源码中设计模式应用浅析-阿里云开发者社区 (aliyun.com)](https://developer.aliyun.com/article/1245307#:~:text=Spring Boot源码中设计模式应用浅析 1 1. 工厂模式 在 Spring Boot,5 5. 模板方法模式 在 Spring Boot 中，模板方法模式通常用于实现通用的业务逻辑。 )

### 工厂模式

工厂模式主要体现在 BeanFactory 和 ApplicationContext 接口的实现上

- BeanFactory ：它负责创建和管理 Bean 对象

- ApplicationContext 是 BeanFactory 的一个子接口，它增加了许多企业级的特性，如国际化、事件传递、AOP 等。ApplicationContext 的实现类包括 ClassPathXmlApplicationContext、FileSystemXmlApplicationContext、AnnotationConfigApplicationContext 等。

我们通常使用注解（如 @Component、@Service、@Repository 等）来标记需要创建的对象，Spring 容器会根据这些注解来创建对象并管理它们的生命周期。具体实现可以参考 Spring Framework 的 BeanFactory 和 ApplicationContext 接口



#### DefaultListableBeanFactory

DefaultListableBeanFactory 是 Spring Framework 中的工厂模式的实现之一，它是 BeanFactory 接口的默认实现类。它负责创建和管理 Bean 对象，并提供了许多与 Bean 相关的操作，如 Bean 的注册、依赖注入、生命周期管理等。



DefaultListableBeanFactory 通过解析 XML 配置文件或者注解来创建 Bean 对象，并将其缓存在一个 Map 中，当需要获取 Bean 对象时，通过 getObjectForBeanInstance() 方法来获取对应 Bean 的实例对象。如果缓存中不存在该 Bean 的实例对象，则通过 createBean() 方法来创建一个新的实例对象并放入缓存中。

DefaultListableBeanFactory 是 Spring Framework 中的一个核心类，它实现了 BeanFactory 接口，并提供了创建、管理、销毁 Bean 对象的功能。

首先，我们来看一下 DefaultListableBeanFactory 的类定义：



```
public class DefaultListableBeanFactory extends AbstractAutowireCapableBeanFactory
        implements ConfigurableListableBeanFactory, BeanDefinitionRegistry, Serializable {
    // ...
}
```

可以看到，DefaultListableBeanFactory 继承了AbstractAutowireCapableBeanFactory，并实现了

ConfigurableListableBeanFactory、BeanDefinitionRegistry 和 Serializable接口。其中,AbstractAutowireCapableBeanFactory 提供了 Bean自动装配的功能，ConfigurableListableBeanFactory 定义了可配置的 ListableBeanFactory接口，BeanDefinitionRegistry 定义了 BeanDefinition 的注册接口，而 Serializable则是为了支持对象序列化。

接下来，我们来看一下 DefaultListableBeanFactory 中的一些重要属性：

```
@Nullable
private ClassLoader beanClassLoader = ClassUtils.getDefaultClassLoader();
private final Map<String, BeanDefinition> beanDefinitionMap = new ConcurrentHashMap<>(256);
private final List<String> beanDefinitionNames = new ArrayList<>(256以上是 DefaultListableBeanFactory 中的一些重要属性，其中：
```

- beanClassLoader：Bean 的类加载器，默认为 ClassUtils.getDefaultClassLoader()，即当前线程的上下文类加载器。

- beanDefinitionMap：BeanDefinition 对象的缓存，key 为 Bean 的名称，value 为 BeanDefinition 对象。

- beanDefinitionNames：Bean 的名称列表，用于快速遍历。

接下来我们来看一下 DefaultListableBeanFactory 中的一些重要方法：



```
public void registerBeanDefinition(String beanName, BeanDefinition beanDefinition)
public void removeBeanDefinition(String beanName)
public BeanDefinition getBeanDefinition(String beanName)
public boolean containsBeanDefinition(String beanName)
public String[] getBeanDefinitionNames()
public int getBeanDefinitionCount()
public boolean isBeanNameInUse(String beanName)
```

可以看到，这些方法主要用于 BeanDefinition 对象的注册、查询、删除和遍历操作。

接下来，我们来看一下 DefaultListableBeanFactory 中的一些重要方法：

```
public Object getBean(String name)
public <T> T getBean(String name, Class<T> requiredType)
public <T> T getBean(Class<T> requiredType)
public Object getBean(String name, Object... args)
public <T> T getBean(Class<T> requiredType,Object... args)
```

这些方法是 DefaultListableBeanFactory 中最核心的方法，它们用于获取 Bean 对象。其中，getBean() 方法是最常用的方法，它可以根据 Bean 的名称或类型来获取对应的 Bean 实例对象。具体来说，getBean()方法会先从缓存中查找对应的 Bean 实例对象，如果缓存中不存在，则通过 createBean() 方法来创建一个新的 Bean实例对象，并将其放入缓存中。



除了上述方法之外，DefaultListableBeanFactory 还提供了许多其他的方法和接口，用于处理 Bean 的生命周期、作用域、AOP 等方面的功能。例如，DefaultListableBeanFactory 中提供了以下方法：



```
public void destroySingletons()
public void registerSingleton(String name, Object singletonObject)
public Object getSingleton(String beanName)
public boolean containsSingleton(String beanName)
public int getSingletonCount()
```

这些方法主要用于管理单例对象的生命周期，包括单例对象的创建、销毁和缓存等操作。

最后，我们来看一下 DefaultListableBeanFactory 中 createBean() 方法的源码，该方法用于创建 Bean 实例对象。

```
protectedObject createBean(String beanName, RootBeanDefinition mbd, @Nullable Object[] args) throws BeanCreationException {
    // Resolve before instantiating the bean to allow for short-circuits.
    BeanWrapper instanceWrapper = null;
    if (mbd.isSingleton()) {
        instanceWrapper = this.factoryBeanInstanceCache.remove(beanName);
    }
    if (instanceWrapper == null) {
        instanceWrapper = createBeanInstance(beanName, mbd, args);
    }
    final Object bean = instanceWrapper.getWrappedInstance();
    Class<?> beanType = instanceWrapper.getWrappedClass();
    if (beanType != NullBean.class) {
        mbd.resolvedTargetType = beanType;
    }

    // Allow post-processors to modify the merged bean definition.
    synchronized (mbd.postProcessingLock) {
        if (!mbd.postProcessed) {
            applyMergedBeanDefinitionPostProcessors(mbd, beanType, beanName);
            mbd.postProcessed = true;
        }
    }

    // Eagerly cache singletons to be able to resolve circular references
    // even when triggered by lifecycle interfaces like BeanFactoryAware.
    boolean earlySingletonExposure = (mbd.isSingleton() && this.allowCircularReferences &&
            isSingletonCurrentlyInCreation(beanName));
    if (earlySingletonExposure) {
        if (logger.isDebugEnabled()) {
            logger.debug("Eagerly caching bean '" + beanName +
                    "' to allow for resolving很好，接下来我们继续解析 createBean() 方法的源码。

// Initialize the bean instance.
Object exposedObject = bean;
try {
    populateBean(beanName, mbd, instanceWrapper);
    if (exposedObject != null) {
        exposedObject = initializeBean(beanName, exposedObject, mbd);
    }
} catch (Throwable ex) {
    if (ex instanceof BeanCreationException && beanName.equals(((BeanCreationException) ex).getBeanName())) {
        throw (BeanCreationException) ex;
    } else {
        throw new BeanCreationException(mbd.getResourceDescription(), beanName, "Initialization of bean failed", ex);
    }
}

if (earlySingletonExposure) {
    addSingletonFactory(beanName, () -> getEarlyBeanReference(beanName, mbd, exposedObject));
    singletonObjects.remove(beanName);
    earlySingletonObjects.remove(beanName);
    registeredSingletons.add(beanName);
}

return exposedObject;
```

可以看到，createBean() 方法主要分为以下几个步骤：



创建 Bean 实例对象，并将其封装为 BeanWrapper 对象。如果 Bean 是单例对象，则从 factoryBeanInstanceCache 缓存中获取，否则通过 createBeanInstance() 方法来创建一个新的实例对象。

应用 MergedBeanDefinitionPostProcessor 对象到 Bean 上，以修改其 BeanDefinition 属性值和 Bean 实例对象。

初始化 Bean 实例对象，包括属性注入、初始化方法调用等操作。如果 Bean 是单例对象，则在初始化前进行缓存操作，以便后续解决循环依赖等问题。

如果 Bean 是单例对象，并且需要提前暴露，则将其缓存到 singletonFactories 中，并从 singletonObjects 和 earlySingletonObjects 缓存中移除。

返回 Bean 实例对象。

DefaultListableBeanFactory 的源码比较庞大，涉及的功能也比较复杂，需要结合具体的使用场景和实现细节来进行深入理解和分析。不过，通过对DefaultListableBeanFactory 的源码解析，我们可以更好地理解 Spring Framework 中的BeanFactory 设计模式，并从中获得一些启发和思考。



###  单例模式

在 Spring Boot 中，单例模式主要体现在 Bean 的创建和管理上。默认情况下，Spring 容器会将 Bean 创建为单例对象，并在整个应用程序生命周期中保持唯一。这种单例模式的实现方式可以避免多线程竞争和资源浪费，同时也方便了对象的管理和维护。



在 Spring Boot 中，单例模式的实现可以参考 Spring Framework 的 DefaultSingletonBeanRegistry 接口。这个类维护了一个单例对象的缓存，通过 getObjectForBeanInstance() 方法来获取对应 Bean 的实例对象，如果缓存中不存在该 Bean 的实例对象，则通过 createBean() 方法来创建一个新的实例对象并放入缓存中。下面我们来逐步解析 DefaultListableBeanFactory 。



#### 详解 DefaultSingletonBeanRegistry

首先，我们来看一下 DefaultSingletonBeanRegistry 中定义的方法：

```
public interface DefaultSingletonBeanRegistry {
    void registerSingleton(String beanName, Object singletonObject);
    Object getSingleton(String beanName);
    boolean containsSingleton(String beanName);
    String[] getSingletonNames();
    int getSingletonCount();
}
```

可以看到，DefaultSingletonBeanRegistry 定义了单例 Bean 的注册、缓存和查询接口，包括 registerSingleton()、getSingleton()、containsSingleton()、getSingletonNames()和 getSingletonCount() 等方法。其中，registerSingleton() 方法用于将一个单例 Bean注册到缓存中，getSingleton() 方法用于获取指定名称的单例 Bean，containsSingleton()方法用于判断指定名称的单例 Bean 是否存在，getSingletonNames() 方法用于获取所有单例 Bean 的名称，getSingletonCount() 方法用于获取单例 Bean 的数量。

 接下来我们看下 DefaultSingletonBeanRegistry 的实现，我给源码中添加一些注释方便大家理解

尤其大家可以看下spring 在**单例实现中的线程安全**是怎么做到额

```
public class DefaultListableBeanFactory extends AbstractAutowireCapableBeanFactory
        implements ConfigurableListableBeanFactory, BeanDefinitionRegistry, Serializable, DefaultSingletonBeanRegistry {
    // ...

    private final Map<String, Object> singletonObjects = new ConcurrentHashMap<>(256); // 单例对象缓存
    private final Map<String, ObjectFactory<?>> singletonFactories = new HashMap<>(16); // 单例对象工厂缓存
    private final Map<String, Object> earlySingletonObjects = new ConcurrentHashMap<>(16); // 提前暴露的单例对象缓存
    private final Set<String> registeredSingletons = new LinkedHashSet<>(256); // 已注册的单例对象集合
    private final Set<String> disposableBeans = new LinkedHashSet<>(256); // 需要销毁的单例对象集合

    // ...

    @Override
    public void registerSingleton(String beanName, Object singletonObject) throws IllegalStateException {
        Assert.notNull(beanName, "Bean name must not be null"); // beanName 不能为空
        synchronized (this.singletonObjects) { // 加锁，确保线程安全
            Object oldObject = this.singletonObjects.get(beanName); // 查找缓存中是否已存在同名单例对象
            if (oldObject != null) {
                throw new IllegalStateException("Could not register object [" + singletonObject +
                        "] under bean name '" + beanName + "': there is already object [" + oldObject + "] bound"); // 如果已存在同名单例对象，则抛出异常
            }
            this.singletonObjects.put(beanName, singletonObject); // 将单例对象放入缓存中
            this.singletonFactories.remove(beanName); // 从单例对象工厂缓存中移除该对象
            this.earlySingletonObjects.remove(beanName); // 从提前暴露的单例对象缓存中移除该对象
            this.registeredSingletons.add(beanName); // 将该对象名称添加到已注册的单例对象集合中
        }
    }

    @Override
    public Object getSingleton(String beanName) {
        return getSingleton(beanName, true); // 调用带有 allowEarlyReference 参数的 getSingleton() 方法
    }

    protected Object getSingleton(String beanName, boolean allowEarlyReference) {
        Object singletonObject = this.singletonObjects.get(beanName); // 从缓存中获取指定名称的单例对象
        if (singletonObject == null && isSingletonCurrentlyInCreation(beanName)) { // 如果缓存中不存在该单例对象，并且该对象正在创建过程中
            synchronized (this.singletonObjects) { // 加锁，确保线程安全
                singletonObject = this.earlySingletonObjects.get(beanName); // 从提前暴露的单例对象缓存中获取该对象
                if (singletonObject == null && allowEarlyReference) { // 如果提前暴露的单例对象缓存中仍未找到该对象，并且允许提前暴露
                    ObjectFactory<?> singletonFactory = this.singletonFactories.get(beanName); // 从单例对象工厂缓存中获取该对象的 ObjectFactory
                    if (singletonFactory != null) { // 如果单例对象工厂存在
                        singletonObject = singletonFactory.getObject(); // 获取新的单例对象
                        this.earlySingletonObjects.put(beanName, singletonObject); // 将新的单例对象放入提前暴露的单例对象缓存中
                        this.singletonFactories.remove(beanName); // 从单例对象工厂缓存中移除该对象
                    }
                }
            }
        }
        return singletonObject;    }

    @Override
    public boolean containsSingleton(String beanName) {
        return this.singletonObjects.containsKey(beanName); // 判断单例对象缓存中是否存在指定名称的单例对象
    }

    @Override
    public String[] getSingletonNames() {
        synchronized (this.singletonObjects) { // 加锁，确保线程安全
            return StringUtils.toStringArray(this.registeredSingletons); // 将已注册的单例对象集合转换为数组返回
        }
    }

    @Override
    public int getSingletonCount() {
        synchronized (this.singletonObjects) { // 加锁，确保线程安全
            return this.registeredSingletons.size(); // 返回已注册的单例对象集合的大小
        }
    }

    // ...
}
```

除了上述方法外，DefaultListableBeanFactory 还提供了一些其他方法来管理单例 Bean，例如 destroySingletons() 方法用于销毁所有的单例 Bean，getSingletonMutex() 方法用于获取单例对象的互斥锁等。



综上所述，DefaultSingletonBeanRegistry 接口及其默认实现类 DefaultListableBeanFactory 提供了一系列方法来管理单例对象的生命周期，包括注册、缓存、查询、销毁等操作，为 Spring Framework 的IoC 容器实现了核心的单例对象管理机制，确保了单例对象的唯一性和正确性。

  

### 观察者模式

在 Spring Boot 中，观察者模式通常用于实现**事件驱动**的编程模型。Spring Framework 中的 **ApplicationEvent** 和 **ApplicationListener** 接口就是观察者模式的实现。ApplicationEvent 是事件对象的抽象类，它定义了事件发生时需要携带的数据。ApplicationListener 是事件监听器的接口，它定义了监听器需要实现的方法，当事件发生时，监听器会自动执行相应的处理逻辑。



在 Spring Boot 中，我们可以通过继承 ApplicationEvent 类来自定义事件对象，通过实现 ApplicationListener 接口来定义事件监听器。Spring 容器会自动扫描所有实现了 ApplicationListener 接口的 Bean，并将其注册为事件监听器。当事件发生时，Spring 容器会自动调用对应监听器的 onApplicationEvent() 方法来处理事件。



具体实现可以参考 Spring Framework 的 ApplicationEvent 和 ApplicationListener 接口，以及 AbstractApplicationContext、SimpleApplicationEventMulticaster 等类。



### 适配器模式

在 Spring Boot 中，适配器模式通常用于**将不兼容的接口转换成可兼容的接口**。

Spring Framework 中的适配器模式主要体现在以下两个方面：

- **控制器方法适配器**：Spring MVC 中的控制器方法可以返回多种类型的结果，例如 ModelAndView、String、void 等，但是 Spring Boot 的 RESTful API 通常需要返回 JSON 或 XML格式的数据。为了将控制器方法的返回值转换成符合 RESTful API 要求的格式，Spring Boot 提供了多种适配器类，例如 MappingJackson2HttpMessageConverter、Jaxb2RootElementHttpMessageConverter 等。



具体实现可以参考 Spring Framework 的 HttpMessageConverter 接口及其实现类。



- **数据库驱动适配器**：在 Spring Boot 中，JDBC 模板可以适配各种不同的数据库驱动，只需配置相应的数据源和驱动类即可。Spring Boot 中已经预置了许多常用的数据库驱动适配器，包括 H2、MySQL、PostgreSQL、Oracle 等。

具体实现可以参考 Spring Framework 的 JdbcTemplate 和 DataSource 接口及其实现类，以及 DriverManagerDataSource、HikariDataSource 等数据源实现类。



### 模板方法模式

在 Spring Boot 中，模板方法模式通常用于**实现通用的业务逻辑**。Spring Framework 中的 **JdbcTemplate** 和 **HibernateTemplate** 就是模板方法模式的实现。这些模板类**定义了通用的数据访问操作，如查询、插入、更新、删除等**，而具体的数据访问细节则由子类（如 JdbcDaoSupport、HibernateDaoSupport 等）来实现。



我们可以使用 JdbcTemplate 来执行 SQL 操作，它封装了 JDBC的基本操作，如打开和关闭连接、创建和执行语句等。我们可以通过定义 RowMapper 接口来映射查询结果集到对象上，**JdbcTemplate会自动将查询结果集转换成对象列表**。具体实现可以参考 Spring Framework 的 JdbcTemplate 和 RowMapper接口及其实现类，以及 NamedParameterJdbcTemplate、SimpleJdbcInsert 等模板类。