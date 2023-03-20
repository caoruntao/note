# Spring

Spring Framework版本:5.2.6.RELEASE

## 框架总览

### 特性总览

#### 核心特性

##### Ioc容器(IoC Container)

##### Spring事件(Events)

##### 资源管理(Resources)

##### 国际化(i18n)

##### 校验(Validation)

##### 数据绑定(Data Binding)

##### 类型转换(Type Conversion)

##### Spring表达式(Soring Express Language)

##### 面向切面编程(AOP)

#### 数据存储

##### JDBC

##### 事务抽象(Trasactions)

##### DAO支持(DAO Support)

##### O/R映射(O/R Mapping)

##### XML编列(XML Meashalling)

#### Web技术

##### Web Servlet

###### Spring MVC

###### WebSocket

###### SockJS

##### Web Reactive

###### Spring WebFlux

###### WebClient

###### WebSocket

#### 技术整合

###### 远程调用

###### Java消息服务(JMS)

###### Java连接架构(JCA)

###### Java管理扩展(JMX)

###### Java邮件客户端(Email)

###### 本地任务(Tasks)

###### 本地调度(Scheduling)

###### 缓存抽象(Caching)

###### Spring 测试(Testing)

#### 测试

###### 模拟对象(Mock Objects)

###### TestContext(TestContext Framework)

###### Spring MVC(Spring MVC Test)

###### Web测试客户端(WebTestClient)

### 版本特性

| Spring Framework | Java 标准版 | Java 企业版          |
| ---------------- | ----------- | -------------------- |
| 1.x              | 1.3+        | J2EE 1.3+            |
| 2.x              | 1.4.2+      | J2EE 1.3+            |
| 3.x              | 5+          | J2EE 1.4 和 JavaEE 5 |
| 4.x              | 6+          | JavaEE 6 和 JavaEE 7 |
| 5.x              | 8+          | JavaEE 7             |

### 模块化设计

spring-core:核心模块，包括类型转换

spring-beans:

spring-context:

spring-aop:

spring-aspects: 对AspectJ支持

spring-expression:

spring-instrument:

spring-jdbc:

spring-orm:

spring-tx:

spring-oxm:

spring-jms:

spring-messaging:

spring-web mvc:

spring-web flux:

spring-web:

spring-websocket:

spring-jcl:

spring-test:

spring-r2dbc:

### 技术整合

#### Java语言特性

1.2

反射：AccessibleObject

1.3

动态代理：Proxy、InvocationHandler

5

注解：Annotation

枚举：

泛型：ParameterizedType

自动装箱/拆箱：java.lang.Integer#valueOf(int)

JUC：Executor、Lock

6

@Override接口

7

Diamond语法：List<String> list = new ArrayList<>(); 可以省略第二个<>中的类型。

多Cathch/Try resouce语法糖：AutoCloseable

8

Lambda语法

可重复注解：@Repeatable

接口默认方法

9

模块化

#### JDK API实践

1.2

反射(Reflection):MethodMatcher

1.3

动态代理(Dynamic Proxy):JdkDynamicAopProxy

5

注解

XML处理(DOM，SAX):XMLBeanDefinitionReader

Java管理扩展(JMX):@ManagedResource

JUC:ThreadPoolTaskScheduler

格式化(Formatter):DateFormatter

6

JDBC 4.0:JdbcTemplate

Common Annotations(JSR 250):CommonAnnotationBeanPostProcesser

JAXB 2.0:Jaxb2Marshaller

7

Fork/Join:ForkJoinPoolFactoryBean

NIO 2(JSR 203):PathResource

8

Strem API(JSR 335):StreamConverter

Date And Time Api:DateTimeContext

可重复Annotations(JSR 337) @Repeatable:@PropertySources

lambda
CompletableFuture

#### Java EE API整合

RMI

JMS

JMX

本地任务

本地调度

### 编程模型

#### 面向对象

##### 契约接口

​	Aware：

​	BeanPostProcessor：

##### 设计模式

​	观察者

##### 继承

​	Abstract*

#### 面向切面

​	动态代理：JdkDynamicAopProxy

​	字节码提升：Cglib

#### 面向元数据

##### 注解

​	@Component、@Repository、@Service、@Controller

##### 配置

​	Environment

​	@PropertySources

##### 泛型

​	GenemicTypeResolver

​	ResolvableType

##### 函数驱动

​	Lambda：Function接口

​	Reactive

##### 模型驱动

​	Enable*模式

#### 面试题

1. 什么是Sring Framework
2. Spring Framework有哪些核心模块
3. Spring Framework的优势与不足

## Ioc容器

### 重新认识Ioc容器

#### Ioc发展简介

好莱坞原则：don't call us, we'll call you

#### Ioc主要实现策略

**依赖查找**和依赖注入两种主要实现策略

#### Ioc容器的职责

依赖处理：

​	依赖查找

​	依赖注入

生命周期管理： 

​	容器

​	托管的资源(Java Beans 或其他资源)

配置：

​	容器

​	外部化配置

​	托管的资源(Java Beans 或其他资源)

#### Ioc容器的实现

Java SE：

​	Java Beans

​	Java ServiceLoader SPI

​	JNDI(Java Naming an Directory Interface)

Java EE:

​	EJB(Enterprise Java Beans)

​	Servlet

开源:

​	Apache Avalon

​	PicoContainer

​	Google Guice

​	Spring Framework

#### 传统Ioc容器实现

##### Java Beans

依赖查找

生命周期管理

配置元信息：

Propertys、Descriptor、PropertyEditor

```java
BeanInfo beanInfo = Introspector.getBeanInfo(Clazz);
beanInfo.getPropertyDescriptors();
beanInfo.getMethodDescriptors();
```

事件

自定义

资源管理

持久化

#### 轻量级Ioc容器

##### 特征

管理应用代码运行：如程序启停

快速启动

容器无需特殊配置

容器轻量级占用以及最小API依赖

容器需要可管控

##### 好处

释放掉一些容器

最大化代码复用

更大程度的面向对象

更大程度的产品化

更好的可测试性

#### 依赖查找 VS 依赖注入

| 类型     | 依赖处理 | 实现便利性 | 代码入侵性 | API依赖性   | 可读性 |
| -------- | -------- | ---------- | ---------- | ----------- | ------ |
| 依赖查找 | 主动获取 | 相对繁琐   | 高侵入性   | 依赖容器API | 好     |
| 依赖注入 | 被动提供 | 相对便利   | 低侵入性   | 不依赖API   | 一般   |

#### 构造器注入 VS Setter注入

##### 构造器注入

相对稳定(无法修改)，并且可以控制字段的注入顺序

##### Setter注入

相对灵活，字段注入顺序不可控

#### 面试题

1. 什么是IoC
2. 依赖查找和依赖注入的区别
3. Spring作为IoC容器有什么优势

## Spring IoC容器

### 依赖查找

+ 按Bean名称查找
  +	实时查找：org.springframework.beans.factory.BeanFactory#getBean(java.lang.String)
+ 按Bean类型查找

  + 单个Bean对象：org.springframework.beans.factory.BeanFactory#getBean(java.lang.Class<T>)
  + 集合Bean对象：org.springframework.beans.factory.ListableBeanFactory#getBeansOfType(java.lang.Class<T>)
  + 延迟查找：org.springframework.beans.factory.BeanFactory#getBeanProvider(java.lang.Class<T>)
+ 按Bean名称+类型查找：org.springframework.beans.factory.BeanFactory#getBean(java.lang.String, java.lang.Class<T>)
+ 根据Java注解查找
  + 单个Bean对象：org.springframework.beans.factory.ListableBeanFactory#findAnnotationOnBean
  + 集合Bean对象：org.springframework.beans.factory.ListableBeanFactory#getBeansWithAnnotation

#### 前世今生

+ 单一类型依赖查找

  + JNDI：javax.naming.Context#lookup(javax.naming.Name)
  + JavaBeans：java.beans.beancontext.BeanContext

  BeanContext继承了Collection，BeanContext中可以包含多个元素，也就是它的Bean。

+ 集合类型依赖查找

  + java.beans.beancontext.BeanContextServices#getCurrentServiceSelectors

+ 层次性依赖查找

  + java.beans.beancontext.BeanContext

#### 单一类型依赖查找 - BeanFactory

+ 按Bean名称查找
  +	实时查找：org.springframework.beans.factory.BeanFactory#getBean(java.lang.String)
+ 按Bean类型查找

  + 实时查找
    + org.springframework.beans.factory.BeanFactory#getBean(java.lang.Class<T>)
  + 延迟查找
    + org.springframework.beans.factory.BeanFactory#getBeanProvider(java.lang.Class<T>)
    + org.springframework.beans.factory.BeanFactory#getBeanProvider(org.springframework.core.ResolvableType)
+ 按Bean名称+类型查找：org.springframework.beans.factory.BeanFactory#getBean(java.lang.String, java.lang.Class<T>)
+ 按Bean名称+注解：org.springframework.beans.factory.ListableBeanFactory#findAnnotationOnBean

#### 集合类型依赖查找 - ListableBeanFactory

+ 按Bean类型查找
  + 获取同类型Bean名称列表
    + org.springframework.beans.factory.ListableBeanFactory#getBeanNamesForType(org.springframework.core.ResolvableType)
    + Spring 4.2引入：org.springframework.beans.factory.ListableBeanFactory#getBeanNamesForType(org.springframework.core.ResolvableType) 
  + 获取同类型Bran实例列表
    + org.springframework.beans.factory.ListableBeanFactory#getBeansOfType(java.lang.Class<T>)

+ 通过注解类型查找
  + 获取标注类型Bean名称列表
    + Spring 4.0引入：org.springframework.beans.factory.ListableBeanFactory#getBeanNamesForAnnotation
  + 获取标注类型Bran实例列表
    + Spring 3.0引入：org.springframework.beans.factory.ListableBeanFactory#getBeansWithAnnotation

#### 层次性依赖查找 - HierarchicalBeanFactory

+ 双亲BeanFactory：org.springframework.beans.factory.HierarchicalBeanFactory#getParentBeanFactory

+ 层次性查找

  + 根据Bean名称查找

    + org.springframework.beans.factory.HierarchicalBeanFactory#containsLocalBean

    LocalBean指当前容器所包含的Bean，忽略双亲容器包含的Bean。

  + 根据Bean类型查找名称列表

    + org.springframework.beans.factory.BeanFactoryUtils#beanNamesForAnnotationIncludingAncestors
    + org.springframework.beans.factory.BeanFactoryUtils#beanNamesForAnnotationIncludingAncestors

  + 根据Bean类型查找实例列表

    + org.springframework.beans.factory.BeanFactoryUtils#beansOfTypeIncludingAncestors(org.springframework.beans.factory.ListableBeanFactory, java.lang.Class<T>)

  + 根据注解查找名称列表

    + org.springframework.beans.factory.BeanFactoryUtils#beanNamesForAnnotationIncludingAncestors

#### 延迟依赖查找

+ org.springframework.beans.factory.BeanFactory
+ Spring 4.3引入：org.springframework.beans.factory.ObjectProvider

#### 安全依赖查找

​	依赖查找接口没有声明抛出org.springframework.beans.BeansException异常就是安全的，否则就是非安全的。

```
BeansException
	NoSuchBeanDefinitionException:没有匹配的Bean，可能因为不存在Bean。
		NoUniqueBeanDefinitionException:不存在唯一匹配的Bean，可能存在多个匹配的Bean。
	FatalBeanException
		BeanCreationException
		BeanInstantiationException:不能实例化，如BeanClass是接口/抽象类。
		BeanInitializationException
```

#### 内建可查找依赖

| Bean名称                    | Bean实例                             | 使用场景                                                     |
| --------------------------- | ------------------------------------ | ------------------------------------------------------------ |
| environment                 | Environment对象                      | 外部化配置以及Profiles                                       |
| systemProperties            | java.util.Properties对象             | Java系统属性                                                 |
| systemEnvironment           | java.util.Map对象                    | 操作系统环境变量                                             |
| messageSource               | MessageSource对象                    | 国际化文案                                                   |
| lifecycleProcessor          | LifecycleProcessor对象               | Lifecycle Bean处理器                                         |
| applicationEventMulticaster | ApplicationEventMulticaster对象      | Spring事件广播器                                             |
|                             | ConfigurationClassPostProcessor      | 处理@Configuration配置类                                     |
|                             | AutowiredAnnotationBeanPostProcessor | 处理@Autowired和@Value注解                                   |
|                             | CommonAnnotationBeanPostProcessor    | 处理@Resource、@PostConstruct和@PreDestroy注解               |
|                             | EventListenerMethodProcessor         | 处理@EventListener注解                                       |
|                             | DefaultEventListenerFactory          | 将@EventListener注解方法转换为ApplicationListenerMethodAdapter实例 |

#### 面试题

1. ObjectFactory与BeanFactory的区别
2. BeanFactory.getBean是否是线程安全的
3. 

### 依赖注入

+ 按Bean名称注入
+ 按Bean类型注入
  + 单个Bean对象
  + 集合Bean对象
+ 注入容器内建Bean对象
+ 注入非Bean对象：如BeanFactory
+ 注入类型
  + 实时注入
  + 延迟注入

#### 模式

+ 手动模式 - 配置或者编程的方式，提前安排注入规则
  + XML资源配置元信息
  + Java注解配置元信息
  + API配置元信息
+ 自动模式 - 实现方提供依赖自动关联的方式，按照内建的注入规则
  + Autowiring（自动绑定）

##### 手动模式

| 依赖注入类型 | 配置元数据举例                                               |
| ------------ | ------------------------------------------------------------ |
| Setter方法   | <property name="user" ref="userBean">                        |
| 构造器       | <constructor-arg name="user" ref="userBean">                 |
| 字段         | @Autowired User user;  @Resource User user;  @InjectUser user; |
| 方法         | @Autowired public void user(User user){...}                                                                @Beanpublic void userHolder(User user){...} |
| 接口回调     | BeanFactoryAware、ApplicationContextAware等Aware接口         |

##### 自动绑定（Autowiring）

自动处理依赖关系，无需显示指定。

| 模式        | 说明                                                         |
| ----------- | ------------------------------------------------------------ |
| no          | 默认值，未激活Autowiring，需要手动指定依赖注入对象           |
| byName      | 根据被注入属性的名称作为Bean名称进行依赖查找，并将对象设置到该属性 |
| byType      | 根据被注入属性的类型作为依赖类型进行查找，并将对象设置到该属性 |
| constructor | 特殊byType类型，用于构造器参数                               |

限制和不足：

+ 手动指定依赖关系将覆盖自动绑定
+ 不能绑定简单类型，包括原生类型、String类型、Class类型等
+ 不能精确绑定，自动绑定是猜测性的
+ 存在多个匹配的Bean时，会抛出NoUniqueBeanDefinitionException

#### 类型

##### 基础类型注入

+ 原生类型(Primitive)：boolean、byte、char、short、integer、float、long、double
+ 标量类型(Scalar)：Number、Character、Boolean、Enum、Locale、Charset、Currency、Properties、UUID
+ 常规类型(General)：Object、String、TimeZone、Claendar、Optional
+ Spring类型：Resource、InputSource、Formatter

##### 集合类型注入

+ 数组类型(Array)：原生类型、标量类型、常规类型、Spring类型
+ 集合类型(Collection)
  + Collection：List、Set
  + Map：Properties

##### 限定注入

+ 使用@Qualifier
  + 通过Bean名称
  + 通过分组限定
+ 基于@Qualifier扩展
  + 自定义注解：如@LoadBalanced

因为自定义注解会被@Qualifier标注，因此自定义注解也会被认为@Qualifier（类似 Java类的继承）。@Qualifier依赖注入时会将自定义标注的Bean也注入。但是自定义注解依赖注入时，不会将@Qualifier标注的Bean注入(子类是父类，但是父类不能为子类)。

##### 延迟注入

ObjectProvider和ObjectFactory。

@Lazy代表**现在不进行依赖处理**，在使用时在进行处理。ObjectProvider和ObjectFactory 代表**现在进行依赖处理**，只不过注入的是一个代理对象，使用时，代理对象会去容器中获取真正要注入的对象。

#### 依赖处理过程

##### 依赖描述符(DependencyDescriptor)

```java
public class DependencyDescriptor extends InjectionPoint implements Serializable {
    // 依赖所在声明类
	private final Class<?> declaringClass;
	// 如果依赖是成员方法的某个参数，这里记录该成员方法名
	@Nullable
	private String methodName;
	// 如果依赖是成员方法的某个参数，这里记录该参数类型
	@Nullable
	private Class<?>[] parameterTypes;
	// 如果依赖是成员方法的某个参数，这里记录该参数所在的索引
	private int parameterIndex;
	// 如果依赖字段，这里记录字段名
	@Nullable
	private String fieldName;

	private final boolean required;

	private final boolean eager;

	private int nestingLevel = 1;
	// 依赖的包含者类，通常和declaringClass一样
	@Nullable
	private Class<?> containingClass;
	// 泛型依赖相关的类型描述符
	@Nullable
	private transient volatile ResolvableType resolvableType;
	// 依赖相关的类型描述符
	@Nullable
	private transient volatile TypeDescriptor typeDescriptor;
	
	...
}
```

##### 依赖处理入口(AutowireCapableBeanFactory#resolveDependency)

```
AutowireCapableBeanFactory#resolveDependency
	createOptionalDependency: 对于Optional类型的依赖，使用doResolveDependency()解决依赖，然后包装。
	DependencyObjectProvider: 对于ObjectFactory/ObjectProvider类型的依赖，会创建DependencyObjectProvider，延时进行依赖处理。
	createDependencyProvider: 对于JSR330中@Provider，延迟进行依赖处理。
	doResolveDependency: 依赖处理
		DependencyDescriptor#getDependencyType：从字段/方法参数中获取依赖的类型
		AutowireCandidateResolver#getSuggestedValue： 处理@Value注解，此处不展开
		resolveEmbeddedValue: 处理@Value注解，此处不展开
		TypeConverter#convertIfNecessary： 对@Value解析出来的值进行类型转换，以匹配依赖类型，此处不展开
		resolveMultipleBeans：处理多数据依赖的类型，如StreamDependencyDescriptor、Array、Collection、Map
		findAutowireCandidates： 获取候选者列表
			BeanFactoryUtils#beanNamesForTypeIncludingAncestors：根据依赖类型获取候选者名字的列表
			resolvableDependencies：从缓存中取
			addCandidateEntry: 
				DependencyDescriptor#resolveCandidate: 根据beanName去BeanFactory中取。
		determineAutowireCandidate: 如果候选者不唯一，则决定最终候选者
			determinePrimaryCandidate： 标记@Primary注解
			determineHighestPriorityCandidate：标记@Priority注解，且优先级最高
			matchesBeanName： 匹配指定的依赖名(字段名/方法参数名)
	
```

#### 依赖注入过程

##### @Autowired/@Inject/@Value

```
AutowiredAnnotationBeanPostProcessor#postProcessMergedBeanDefinition: 构建依赖注入元信息缓存
	findAutowiringMetadata: 查找依赖注入元信息
		buildAutowiringMetadata: 构建依赖注入元信息，直到父类为空或者为Object
			ReflectionUtils#doWithLocalFields:	查找依赖注入字段，不支持静态字段
				AutowiredAnnotationBeanPostProcessor#findAutowiredAnnotation:
					autowiredAnnotationTypes：查找字段中是否含有集合中的任意注解
			ReflectionUtils#doWithLocalMethods:	查找依赖注入方法，不支持静态方法
				AutowiredAnnotationBeanPostProcessor#findAutowiredAnnotation:
					autowiredAnnotationTypes：查找方法中是否含有集合中的任意注解
AutowiredAnnotationBeanPostProcessor#postProcessProperties: 处理依赖注入
	findAutowiringMetadata: 从缓存中获取依赖注入元信息
		InjectionMetadata#inject: 依赖注入元信息处理
			InjectionMetadata.InjectedElement#inject:
				AutowiredFieldElement#resolveFieldValue:
					resolveFieldValue: 
						AutowireCapableBeanFactory#resolveDependency: 依赖处理
					java.lang.reflect.Field#set: 字段注入
				AutowiredMethodElement#resolveMethodArguments: 
					resolveMethodArguments: 
						AutowireCapableBeanFactory#resolveDependency: 依赖处理
					java.lang.reflect.Method#invoke: 方法注入
```

依赖注入过程大概分为3步：

	1.	元信息解析
	1.	依赖处理
	1.	依赖注入（字段/方法）

InstantiationAwareBeanPostProcessor#postProcessProperties虽然方法名为Properties后置处理，其实发生在属性赋值前(set方法调用前)。

##### @Resource/@EJB/@WebServiceRef

```
CommonAnnotationBeanPostProcessor#postProcessMergedBeanDefinition:
	findResourceMetadata:
		buildResourceMetadata:
CommonAnnotationBeanPostProcessor#postProcessProperties：
	findResourceMetadata：
		InjectionMetadata#inject：
```

CommonAnnotationBeanPostProcessor和AutowiredAnnotationBeanPostProcessor依赖注入处理过程类似，不在重复展开。

###### @PostConstruct/@PreDestroy

CommonAnnotationBeanPostProcessor会在postProcessBeforeInitialization阶段处理@PostConstruct和@PreDestroy：

```
CommonAnnotationBeanPostProcessor#postProcessMergedBeanDefinition:
    super(InitDestroyAnnotationBeanPostProcessor)#postProcessBeforeInitialization:
        findLifecycleMetadata:
            buildLifecycleMetadata: 查找@PostConstruct/@PreDestroy的元信息
                ReflectionUtils#doWithLocalMethods:  
InitDestroyAnnotationBeanPostProcessor#postProcessBeforeInitialization:
	findLifecycleMetadata：
	LifecycleMetadata#invokeInitMethods: 执行初始化方法
		LifecycleElement#invoke:
			java.lang.reflect.Method#invoke:
InitDestroyAnnotationBeanPostProcessor#postProcessBeforeDestruction: 触发于DisposableBeanAdapter#destroy
	findLifecycleMetadata:
		LifecycleMetadata#invokeDestroyMethods: 执行销毁前方法
			LifecycleElement#invoke:
				java.lang.reflect.Method#invoke:
```

#### 自定义依赖注入注解

##### @Autowired元标注

##### AutowiredAnnotationBeanPostProcessor#autowiredAnnotationTypes添加自定义注解

#### 面试题

1. 有多少中依赖注入的方式？

   Setter方法注入、构造器注入、字段注入、方法注入和接口回调注入。

2. 偏好构造器注入还是Setter注入？

   没有绝对的好坏，只有相对的合理。

   看情况，如果依赖较少，或依赖注入的顺序有要求，或不要求重复注入，则考虑构造器注入；如果依赖项多，或依赖注入的顺序无要求，或要求重复注入，则考虑Setter注入。

3. Spring依赖注入的来源有哪些？

    自定义的业务Bean

    外部注册的单例

    Spring内建Bean

    Spring内部可解析依赖

### 依赖来源

+ 用户自定义 BeanDefinition 创建出来的Bean
+ 外部注册的 单例对象
+ Spring容器内建 BeanDefinition 创建出来的Bean
  + ConfigurationClassPostProcessor
  + AutowiredAnnotationBeanPostProcessor
  + CommonAnnotationPostProcessor
  + EventListenerMethodProcessor

+ Spring容器内建 单例对象
  + Environment
  + MessageSource
  + LifecycleProcessor
  + ApplicationEventMulticaster
+ Spring容器内建可处理依赖(ResolvableDependency)
  + BeanFactory
  + ResourceLoader
  + ApplicationEventPublisher
  + ApplicationContext

#### 依赖查找的依赖来源

+ 用户自定义 BeanDefinition 创建出来的Bean
+ 外部注册的单例对象
+ Spring容器内建 BeanDefinition 创建出来的Bean
+ Spring容器内建 单例对象

#### 依赖注入的依赖来源

+ 用户自定义 BeanDefinition 创建出来的Bean
+ 外部注册的单例对象
+ Spring容器内建 BeanDefinition 创建出来的Bean
+ Spring容器内建 单例对象
+ **Spring容器内建可处理依赖(ResolvableDependency)**

#### Spring BeanDefinition作为依赖来源

元数据：BeanDefinition

注册：DefaultListableBeanFactory#registerBeanDefinition

顺序：按BeanDefinition注册顺序(DefaultListableBeanFactory#beanDefinitionNames是有序列表)

其他：生命周期由Spring容器管理，而且可以延迟初始化Bean

#### 单列对象作为依赖来源

注册：DefaultListableBeanFactory#registerSingleton

顺序：按单列对象注册顺序（DefaultSingletonBeanRegistry#registeredSingletons是插入有序集合）

限制：生命周期不由Spring容器管理，而且无法延迟初始化有序的。

#### ResolvableDependency作为依赖来源

注册：DefaultListableBeanFactory#registerResolvableDependency

```java
Spring容器内建可处理依赖解析：
AbstractApplicationContext#prepareBeanFactory: 会注册四个ResolvableDependency
		beanFactory.registerResolvableDependency(BeanFactory.class, beanFactory);
		beanFactory.registerResolvableDependency(ResourceLoader.class, this);
		beanFactory.registerResolvableDependency(ApplicationEventPublisher.class, this);
		beanFactory.registerResolvableDependency(ApplicationContext.class, this);
DefaultListableBeanFactory#resolveDependency：
	doResolveDependency：
		findAutowireCandidates：查找ResolvableDependency
```

限制：生命周期不由Spring容器管理，无法延迟初始化，且不可用于依赖查找。

#### 外部化配置作为依赖来源

外部化配置使用@Value进行依赖注入的处理，@Value注解由AutowiredAnnotationBeanPostProcessor处理。

```java
元信息解析
AutowiredAnnotationBeanPostProcessor#postProcessMergedBeanDefinition： 构建依赖注入元信息缓存
	findAutowiringMetadata：
		buildAutowiringMetadata：
			ReflectionUtils#doWithLocalFields：筛选标注autowiredAnnotationTypes中注解的字段
				findAutowiredAnnotation： 
			ReflectionUtils#doWithLocalMethods：标注autowiredAnnotationTypes中注解的方法参数
				findAutowiredAnnotation： 
依赖处理
AbstractApplicationContext#finishBeanFactoryInitialization：
	beanFactory.addEmbeddedValueResolver(strVal -> getEnvironment().resolvePlaceholders(strVal))： 注册一个默认的StringValueResolver

DefaultListableBeanFactory#resolveDependency：
	doResolveDependency：
		AutowireCandidateResolver#getSuggestedValue： 获取@Value中的value值
			AbstractBeanFactory#resolveEmbeddedValue： 解析@Value的值
				PropertySourcesPropertyResolver#resolvePlaceholders： 
					AbstractPropertyResolver#doResolvePlaceholders：
						PropertyPlaceholderHelper#replacePlaceholders：
							PropertyPlaceholderHelper#parseStringValue：
								PropertyPlaceholderHelper.PlaceholderResolver#resolvePlaceholder： helper.replacePlaceholders(text, this::getPropertyAsRawString)
								org.springframework.core.env.PropertySourcesPropertyResolver#getPropertyAsRawString：
								getProperty：
									PropertySource#getProperty: 从properties文件取
```

@Value处理逻辑简单化：

​	StringValueReslover -> PropertyReslover(PropertySourcePropertyReslover) -> PropertyPlaceholderHelper -> PlaceholderReslover

#### 面试题

1. 依赖注入和依赖查找的来源是否相同？

​		不同。依赖查找可以来源于Spring BeanDefinition和单例对象，依赖注入的来源还包括ReslovableDepency以及@Value所标注的外部化配置。

2. 单例对象在IoC容器启动后还能注册吗？

​		可以的，没有任何影响。相反，BeanDefinition在启动后会冻结配置（DefaultListableBeanFactory#configurationFrozen），冻结配置不代表无法注册BeanDefinition，只是启动后注册的BeanDefinition并不能作为启动前Spring Bean的依赖来源。

2. 依赖注入的来源？
   + Spring BeanDefinition
   + 单例对象
   + ReslovableDepency
   + 外部化配置

### 配置元信息

+ Bean定义配置
  + 基于配置文件，如XML文件/Properties文件
  + 基于Java 注解
  + 基于Java API
+ Ioc容器配置
  + 基于配置文件
  + 基于Java注解
  + 基于Java API
+ 外部化属性配置
  + 基于Java 注解

#### 实现

​	BeanFactory是真正的IoC容器底层，负责管理对象(包括不仅限于Bean)。

​	ApplicationContext extends BeanFactory，是BeanFactory的超集，以组合的方式添加了DefaultListableBeanFactory，并将BeanFactory相关的功能都委派给了DefaultListableBeanFactory实现，同时添加了AOP、环境、资源管理、事件和消息资源(国际化相关)等高级特性功能。

#### 容器生命周期

+ 启动：org.springframework.context.support.AbstractApplicationContext#refresh

```java
			// Prepare this context for refreshing.
			prepareRefresh();

			// Tell the subclass to refresh the internal bean factory.
			ConfigurableListableBeanFactory beanFactory = obtainFreshBeanFactory();

			// Prepare the bean factory for use in this context.
			prepareBeanFactory(beanFactory);

			try {
				// Allows post-processing of the bean factory in context subclasses.
				postProcessBeanFactory(beanFactory);

				// Invoke factory processors registered as beans in the context.
				invokeBeanFactoryPostProcessors(beanFactory);

				// Register bean processors that intercept bean creation.
				registerBeanPostProcessors(beanFactory);

				// Initialize message source for this context.
				initMessageSource();

				// Initialize event multicaster for this context.
				initApplicationEventMulticaster();

				// Initialize other special beans in specific context subclasses.
				onRefresh();

				// Check for listener beans and register them.
				registerListeners();

				// Instantiate all remaining (non-lazy-init) singletons.
				finishBeanFactoryInitialization(beanFactory);

				// Last step: publish corresponding event.
				finishRefresh();
			}
```



+ 运行
+ 停止：org.springframework.context.support.AbstractApplicationContext#close

```

			// Publish shutdown event.
			publishEvent(new ContextClosedEvent(this));

			// Stop all Lifecycle beans, to avoid delays during individual destruction.
			if (this.lifecycleProcessor != null) {
				try {
					this.lifecycleProcessor.onClose();
				}
				catch (Throwable ex) {
					logger.warn("Exception thrown from LifecycleProcessor on context close", ex);
				}
			}

			// Destroy all cached singletons in the context's BeanFactory.
			destroyBeans();

			// Close the state of this context itself.
			closeBeanFactory();

			// Let subclasses do some final clean-up if they wish...
			onClose();
```

#### 面试题

1. 什么是Spring IoC容器
2. BeanFactory 与 FactoryBean
3. Spring IoC容器启动时做了哪些准备

## Bean

### Bean实例

#### 定义Bean

​	BeanDefinition是Spring Framework中定义Bean的配置元信息接口，包含：

+	Bean的类名
+	Bean行为配置元素，如作用域、自动绑定的模式、生命周期回调等
+	其他Bean引用，又可称为依赖
+	配置设置，如Bean属性(Properties)

| 属性                    | 说明                                         |
| ----------------------- | -------------------------------------------- |
| Class                   | Bean全类名，必须是具体类，不能用抽象类或接口 |
| Name                    | Bean的名称或ID                               |
| Scope                   | Bean的作用域（如signleton、prototype等）     |
| Constructor arguments   | Bean构造器参数（用于依赖注入）               |
| Properties              | Bean属性设置（用于依赖注入）                 |
| Autowiring mode         | Bean自动绑定模式（如byName、byType）         |
| Lazy initialzation mode | Bean延迟初始化模式（延迟和非延迟）           |
| Initialzation method    | Bean初始化回调方法名称                       |
| Destruction method      | Bean销毁回调方法名称                         |

​	BeanDefinition构建：

+	BeanDefinitionBuilder 
+	AbstractBeanDefinition以及派生类

#### 命名Bean

​	每个Bean拥有一个或多个标识符（identifiers），这些标识符在Bean所在的容器中是唯一的。通常。一个Bean仅有一个标识符，如果需要额外的，可以使用别名（Alias）扩充。

​	Bean的id或那么属性并非必须指定，如果不指定的化，容器会为Bean生成一个唯一的名称。

​	Bean名称生成器（BeanNameGenerator）

+	DefaultBeanNameGenerator。2.0.3引入
+	AnnotationBeanNameGenerator。2.5引入

```java
public interface BeanNameGenerator {

	String generateBeanName(BeanDefinition definition, BeanDefinitionRegistry registry);

}

```

​	Bean别名（Alias）可以复用现有的BeanDefinition、可以给第三方框架引入的Bean起一个自己命名规范的名字。

```java
public interface AliasRegistry {

	void registerAlias(String name, String alias);
	
	...
}
```

#### 注册Bean

​	BeanDefinition注册

 +	XML配置元信息：<bean name="..." .../>
 +	Java注解配置元信息
   +	@Bean
   +	@Component
   +	@Import
 +	Java API配置元信息
   +	命名方式：org.springframework.beans.factory.support.BeanDefinitionRegistry#registerBeanDefinition
   +	非命名方式：org.springframework.beans.factory.support.BeanDefinitionReaderUtils#registerWithGeneratedName
   +	配置类方法：org.springframework.context.annotation.AnnotatedBeanDefinitionReader#register

### Bean作用域

Bean作用域由BeanFactory记录。

#### 单例(SINGLETON)

​	ConfigurableBeanFactory#SCOPE_SINGLETON，全局(BeanFactory)共享一个Bean实例，生命周期（初始化和销毁）由BeanFactory托管。

#### 原型(PROTOTYPE)

​	 ConfigurableBeanFactory#SCOPE_PROTOTYPE， 每次获取一个新的实例，由BeanFactory创建，因此负责初始化周期，但是BeanFactory不持有该Bean，因此不负责销毁周期。可在所属类销毁时手动调用prototype Bean销毁。

#### 请求级别(RequestScope)

​	每次请求(Request)都会获取一个新的实例。

```JAVA
public abstract class AbstractRequestAttributesScope implements Scope {

	@Override
	public Object get(String name, ObjectFactory<?> objectFactory) {
		RequestAttributes attributes = RequestContextHolder.currentRequestAttributes();
		Object scopedObject = attributes.getAttribute(name, getScope());
		if (scopedObject == null) {
			scopedObject = objectFactory.getObject();
			attributes.setAttribute(name, scopedObject, getScope());
			// Retrieve object again, registering it for implicit session attribute updates.
			// As a bonus, we also allow for potential decoration at the getAttribute level.
			Object retrievedObject = attributes.getAttribute(name, getScope());
			if (retrievedObject != null) {
				// Only proceed with retrieved object if still present (the expected case).
				// If it disappeared concurrently, we return our locally created instance.
				scopedObject = retrievedObject;
			}
		}
		return scopedObject;
	}
	
	...
}
```

```
public class RequestScope extends AbstractRequestAttributesScope {

	@Override
	protected int getScope() {
		return RequestAttributes.SCOPE_REQUEST;
	}

	/**
	 * There is no conversation id concept for a request, so this method
	 * returns {@code null}.
	 */
	@Override
	@Nullable
	public String getConversationId() {
		return null;
	}

}
```

RequestScope继承于AbstractRequestAttributesScope，且Scope#getConversationId为NULL，则每次会获取新的RequestAttributes，RequestAttributes没有对应实例，因此每次获取都会创建一个新实例，然后放进去(RequestScope每次都会获取新的RequestAttributes，因此放进去也不会被使用)。

#### 会话级别(SessionScope)

​	每个新的会话会创建一个新实例，相同的会话共享一个实例。

```java
public class SessionScope extends AbstractRequestAttributesScope {

	@Override
	public String getConversationId() {
		return RequestContextHolder.currentRequestAttributes().getSessionId();
	}

	@Override
	public Object get(String name, ObjectFactory<?> objectFactory) {
		Object mutex = RequestContextHolder.currentRequestAttributes().getSessionMutex();
		synchronized (mutex) {
			return super.get(name, objectFactory);
		}
	}

	...

}
```

SessionScope继承于AbstractRequestAttributesScope，且Scope#getConversationId返回SessionId，这样同一个会话会返回同一个RequestAttributes，此时，实例没有时会创建然后放入，后续从RequestAttributes取之前放入的实例即可实现会话级别的实例共享。

SessionScope重写get()方法，添加互斥锁，是因为可能一个会话同时发起多个请求，引发线程安全问题，因此添加互斥锁保证线程安全。RequestScope是请求级别，每个请求绑定一个线程，因此不会有线程安全问题。

#### 应用级别(ServletContextScope)

​	ServletContextScope没有继承AbstractRequestAttributesScope，是因为应用级别实现实例共享简单，只需要将实例放入ServletContext中即可。

```java
public class ServletContextScope implements Scope, DisposableBean {

	private final ServletContext servletContext;

	@Override
	public Object get(String name, ObjectFactory<?> objectFactory) {
		Object scopedObject = this.servletContext.getAttribute(name);
		if (scopedObject == null) {
			scopedObject = objectFactory.getObject();
			this.servletContext.setAttribute(name, scopedObject);
		}
		return scopedObject;
	}

	...
}
```

#### 自定义生成周期

​	先实现Scope，然后将Scope注册(ConfigurableBeanFactory#registerScope)到容器中。

​	自定义生命周期无非是将实例保存到该生命周期共享的数据中，如RequestAttributes，有则获取，无则添加。如自定义线程级别的生命周期，ThreadLocal就是线程级别的，每个线程都有自己的ThreadLocal，此时就可以从ThreadLocal获取实例，有则获取成功，无责添加，以供后续获取。

```java
public class ThreadScope implements Scope {
    private ThreadLocal<Map<String, Object>> instanceThreadLocal = ThreadLocal.withInitial(HashMap::new);

    @Override
    public Object get(String name, ObjectFactory<?> objectFactory) {
        Map<String, Object> instanceMap = instanceThreadLocal.get();
        return instanceMap.putIfAbsent(name, objectFactory.getObject());
    }

    @Override
    public Object remove(String name) {
        Map<String, Object> instanceMap = instanceThreadLocal.get();
        return instanceMap.remove(name);
    }

	...
}
```

#### RefreshScope

​	RefreshScope继承GenericScope，功能大部分由GenericScope实现。

```java
public class RefreshScope extends GenericScope
		implements ApplicationContextAware, ApplicationListener<ContextRefreshedEvent>, Ordered {
    public void refreshAll() {
        super.destroy();
        this.context.publishEvent(new RefreshScopeRefreshedEvent());
    }

    ...
}
```

```java
public class GenericScope
		implements Scope, BeanFactoryPostProcessor, BeanDefinitionRegistryPostProcessor, DisposableBean {
    private BeanLifecycleWrapperCache cache = new BeanLifecycleWrapperCache(new StandardScopeCache());
    	
    // 从缓存中获取实例，有则获取，无则创建
    @Override
	public Object get(String name, ObjectFactory<?> objectFactory) {
        // Put a value in the cache if the key is not already used. If one is already present with the name provided, it is not replaced, but is returned to the caller.
		BeanLifecycleWrapper value = this.cache.put(name, new BeanLifecycleWrapper(name, objectFactory));
		this.locks.putIfAbsent(name, new ReentrantReadWriteLock());
		try {
			return value.getBean();
		}
		catch (RuntimeException e) {
			this.errors.put(name, e);
			throw e;
		}
	}
 
    // 清空缓存，这样下次只能新建实例
    @Override
	public void destroy() {
		List<Throwable> errors = new ArrayList<Throwable>();
		Collection<BeanLifecycleWrapper> wrappers = this.cache.clear();
		for (BeanLifecycleWrapper wrapper : wrappers) {
			try {
				Lock lock = this.locks.get(wrapper.getName()).writeLock();
				lock.lock();
				try {
					wrapper.destroy();
				}
				finally {
					lock.unlock();
				}
			}
			catch (RuntimeException e) {
				errors.add(e);
			}
		}
		if (!errors.isEmpty()) {
			throw wrapIfNecessary(errors.get(0));
		}
		this.errors.clear();
	}
    
    // 注册Scope
    @Override
	public void postProcessBeanFactory(ConfigurableListableBeanFactory beanFactory) throws BeansException {
		this.beanFactory = beanFactory;
		beanFactory.registerScope(this.name, this);
		setSerializationId(beanFactory);
	}
}
```

​	RefreshScope#refreshAll会清空缓存，这样就能完成刷新，下次就会获取新的实例。RefreshScope#refreshAll会被ContextRefresher#refresh调用，ContextRefresher#refresh会被

+ RefreshEndpoint端点调用(/actuator/refresh)
+ 监听RefreshEvent事件的RefreshEventListener调用

#### ScopedProxyMode

​	@Scope标注的Bean，可能在不同的周期内获取不同的实例，如RequestScope，每个请求获取一个实例，但是依赖注入时只依赖查找一次Bean实例，然后注入，后续就使用了注入的具体实例，这样就无法实现在不同的周期内获取不同的实例。

​	Spring会针对上述情况，在依赖注入时注入一个代理对象，然后通过代理对象会获取实例，这样代理对象没获取一次都是一个新的实例。

​	当Scope#proxyMode为ScopedProxyMode#INTERFACES或ScopedProxyMode#TARGET_CLASS时，Spring会注入一个代理对象（AnnotationConfigUtils#applyScopedProxyMode）。

```JAVA
AnnotationConfigUtils#applyScopedProxyMode:
	ScopedProxyCreator#createScopedProxy:
		ScopedProxyUtils#createScopedProxy: 会创建一个ScopedProxyFactoryBean的BeanDefinition，然后注册到容器中
            DefaultScopedObject#getTargetObject：
            	BeanFactory#getBean
```

#### 面试题

1. Spring内建的Bean有哪些作用域？

   singleton、pototype、request、session、application

2. singleton Bean 是否在一个应用中是唯一的？

   在应用中不是唯一的。singleton的作用域是BeanFactory，在BeanFactory中是唯一的，一个应用可能有多个BeanFactory。好比静态变量在ClassLoader中是唯一的，而非JVM。

3. application作用域是否有代替方案？

   application作用域是针对于ServletContext的，一个ServletContext可以关联多个ApplicationContext(Spring应用上下文)。Web类型的ApplicationContext会关联到ServletContext(WebApplicationContext#getServletContext)。

### Bean生命周期

#### Bean元信息配置

##### 资源配置

Properties资源

XML资源

Groovy资源

##### 注解配置

@Compoment、@Repository、@Service、@Controller、@Configuration

@Bean

##### API配置

BeanDefinitionBuilder

创建BeanDefinition对象

#### Bean元信息解析

##### 面向资源BeanDefinition解析

+ BeanDefinitionReader
+ XML 解析器 - BeanDefinitionParse

##### 面向注解BeanDefinition解析

+ AnnotatedBeanDefinitionReader

#### BeanDefinition注册

+ BeanDefinitionRegistry

#### Bean实例化(Instantiation)

 + 常规方式

   +	通过构造器
   +	通过静态工厂方法，指定BeanDefinition中的factoryMethodName属性。org.springframework.beans.factory.config.BeanDefinition#setFactoryMethodName
   +	通过Bean工厂方法，指定BeanDefinition中的factoryBeanName属性和factoryMethodName属性。org.springframework.beans.factory.config.BeanDefinition#setFactoryBeanName;org.springframework.beans.factory.config.BeanDefinition#setFactoryMethodName

   +	通过FactoryBean，实现org.springframework.beans.factory.FactoryBean，然后注册到IoC容器中。

 + 特殊方式

   +	通过ServiceLoaderFactoryBean，注册org.springframework.beans.factory.serviceloader.AbstractServiceLoaderBasedFactoryBean的派生类，指定serviceType。Spring会通过java.util.ServiceLoader#load(java.lang.Class<S>)去加载serviceType对应的实例。
   +	通过org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory#createBean(java.lang.Class<T>)
   +	通过org.springframework.beans.factory.support.BeanDefinitionRegistry#registerBeanDefinition

#### Bean初始化(Initialzation)

+ @PostConstruct 标注方法。由org.springframework.beans.factory.annotation.CommonAnnotationBeanPostProcessor#postProcessBeforeInitialization处理。
+ 实现org.springframework.beans.factory.InitializingBean#afterPropertiesSet方法。org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory#invokeInitMethods处理。
+ 指定BeanDefinition的initMethodName属性。org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory#invokeCustomInitMethod处理。



@Lazy标记的Bean可以延迟加载。

#### Bean销毁(Destroy)

+ @PreDestroy标注方法。由org.springframework.beans.factory.annotation.CommonAnnotationBeanPostProcessor#postProcessBeforeDestruction处理。

+ 实现org.springframework.beans.factory.DisposableBean#destroy方法。org.springframework.beans.factory.support.DefaultSingletonBeanRegistry#destroyBean处理。

+ 指定BeanDefinition的destroyMethodName属性。org.springframework.beans.factory.support.DisposableBeanAdapter#invokeCustomDestroyMethod处理。

  如果Bean指定了销毁方法，则会在org.springframework.beans.factory.support.AbstractBeanFactory#registerDisposableBeanIfNecessary处理时在IoC容器中注册DisposableBeanAdapter。

#### 注册外部单例对象

​	可以在IoC容器中注册外部单例对象，该单例生命周期不由容器托管。

​	org.springframework.beans.factory.config.SingletonBeanRegistry#registerSingleton

#### 面试题

1. 如何注册一个Spring Bean
2. 什么是Spring BeanDefinition
3. Spring容器如何管理注册Bean

## 元信息

### 注解

### 配置元信息

### 外部化属性

## 基础设施

### 资源管理

### 类型转换

### 数据绑定

### 数据校验

### 国际化

### 事件

### 泛型处理



