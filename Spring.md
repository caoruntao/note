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

## Spring Bean

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

​	通过DefaultListableBeanFactory#registerBeanDefinition注册，注册时DefaultListableBeanFactory#beanDefinitionMap存储BeanDefinition，DefaultListableBeanFactory#beanDefinitionNames保存BeanDefinition注册顺序。

#### BeanDefinition合并

AbstractBeanFactory#getMergedBeanDefinition: 获取合并后的BeanDefinition
	1.	使用AbstractBeanFactory#mergedBeanDefinitions加锁，保证线程安全
	1.	从AbstractBeanFactory#mergedBeanDefinitions获取，有则返回
	1.	如果当前BeanDefinition#getParentName为空(没有父引用)，则判断是否是**RootBeanDefinition**，是的话克隆一个返回，不是的话则为**GenericBeanDefinition**，将其包装成RootBeanDefinition返回
	1.	获取**父引用合并后**的RootBeanDefinition，然后深度克隆一个，并使用当前BeanDefinition中的属性去覆盖克隆出来的那个RootBeanDefinition，然后返回

#### Bean Class加载

AbstractBeanFactory#resolveBeanClass: 解析Bean Class

1. AbstractBeanDefinition#hasBeanClass会判断是否Bean Class是否已经加载。AbstractBeanDefinition#beanClass是一个Object类型的
   + 当AbstractBeanDefinition#beanClass实际类型为Class时，代表Bean Class已经加载；
   + 当AbstractBeanDefinition#beanClass实际类型为String时，代表Bean Class的全限定名称，此时需要使用ClassLoader进行类加载。
2. 获取当前BeanFactory的ClassLoader，根据AbstractBeanDefinition#beanClass代表的类全限定名称，调用Class#forName进行类加载

```java
AbstractBeanFactory#resolveBeanClass:
	AbstractBeanDefinition#hasBeanClass: 判断是否Bean Class是否已经加载，已加载则返回
	AbstractBeanFactory#doResolveBeanClass: 加载Bean Class
		AbstractBeanFactory#getBeanClassLoader: 获取当前BeanFactory的ClassLoader
			AbstractBeanDefinition#resolveBeanClass: 
				ClassUtils#forName:
				加载好Bean Class后，AbstractBeanDefinition#beanClass会从类的全限定名称变为Class
```



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

##### 实例化前

```java
public interface InstantiationAwareBeanPostProcessor extends BeanPostProcessor {

	@Nullable
	default Object postProcessBeforeInstantiation(Class<?> beanClass, String beanName) throws BeansException {
		return null;
	}
	...
}
```

当InstantiationAwareBeanPostProcessor#postProcessBeforeInstantiation返回一个非空的Object时，会跳过实例化阶段，使用返回的非空Object作为Bean实例。返回Null时，则调用AbstractAutowireCapableBeanFactory#doCreateBean创建Bean。

```JAVA
InstantiationAwareBeanPostProcessor#postProcessBeforeInstantiation:
	AbstractAutowireCapableBeanFactory#applyBeanPostProcessorsBeforeInstantiation:
		AbstractAutowireCapableBeanFactory#resolveBeforeInstantiation:
			AbstractAutowireCapableBeanFactory#createBean:
				// 返回一个非空的Object时，使用返回的非空Object作为Bean实例
				Object bean = resolveBeforeInstantiation(beanName, mbdToUse);
                if (bean != null) {
                    return bean;
                }
```

##### 实例化

实例化方式：

+ 传统实例化方式
  + 实例化策略：InstantiationStrategy
+ 构造器依赖注入：构造器参数(Spring Bean类型)会根据类型注入，而非参数名

```JAVA
AbstractAutowireCapableBeanFactory#doCreateBean:
	#createBeanInstance
		AbstractBeanFactory#resolveBeanClass: Bean Class加载
		
		AbstractBeanDefinition#getInstanceSupplier: 提供Supplier
		AbstractAutowireCapableBeanFactory#obtainFromSupplier: 从Supplier中获取实例
		
		AbstractBeanDefinition#getFactoryMethodName: 指定工厂方法
		#instantiateUsingFactoryMethod: 
			ConstructorResolver#instantiateUsingFactoryMethod:
				AbstractBeanDefinition#getFactoryBeanName: 如果指定工厂Bean，则从BeanFactory中获取工厂Bean实例；否则为本Class中的静态方法
				#resolvePreparedArguments: 解析方法参数
				// TODO 中间还有很多逻辑
				#instantiate: 
					InstantiationStrategy#instantiate: 使用实例化策略创建实例。调用本Class中的静态FactoryMethod创建，或者调用工厂Bean实例的FactoryMethod创建。
        AbstractAutowireCapableBeanFactory#autowireConstructor: 指定构造器。通过SmartInstantiationAwareBeanPostProcessor#determineCandidateConstructors/AUTOWIRE_CONSTRUCTOR(根据构造器自动注入)/BeanDefinition指定构造器参数/AbstractBeanFactory#getBean时指定参数
           ConstructorResolver#autowireConstructor:
			#resolvePreparedArguments: 解析方法参数
            	#instantiate: 
					InstantiationStrategy#instantiate: 使用指定构造器和参数实例化。
        AbstractAutowireCapableBeanFactory#instantiateBean: 传统实例化
           InstantiationStrategy#instantiate: 获取无参构造器实例化
```

##### BeanDefinition合并后置处理

```java
public interface MergedBeanDefinitionPostProcessor extends BeanPostProcessor {

	/**
	 * Post-process the given merged bean definition for the specified bean.
	 * @param beanDefinition the merged bean definition for the bean
	 * @param beanType the actual type of the managed bean instance
	 * @param beanName the name of the bean
	 * @see AbstractAutowireCapableBeanFactory#applyMergedBeanDefinitionPostProcessors
	 */
	void postProcessMergedBeanDefinition(RootBeanDefinition beanDefinition, Class<?> beanType, String beanName);
	... 

}
```

```java
	protected Object doCreateBean(String beanName, RootBeanDefinition mbd, @Nullable Object[] args)
			throws BeanCreationException {

		// Instantiate the bean.
		BeanWrapper instanceWrapper = null;
		... 
		if (instanceWrapper == null) {
			instanceWrapper = createBeanInstance(beanName, mbd, args);
		}
		Object bean = instanceWrapper.getWrappedInstance();
		...
            
		// Allow post-processors to modify the merged bean definition.
		synchronized (mbd.postProcessingLock) {
			if (!mbd.postProcessed) {
				try {
					applyMergedBeanDefinitionPostProcessors(mbd, beanType, beanName);
				}
				catch (Throwable ex) {
					throw new BeanCreationException(mbd.getResourceDescription(), beanName,
							"Post-processing of merged bean definition failed", ex);
				}
				mbd.postProcessed = true;
			}
		}
```

##### 实例化后

```java
public interface InstantiationAwareBeanPostProcessor extends BeanPostProcessor {

	default boolean postProcessAfterInstantiation(Object bean, String beanName) throws BeansException {
		return true;
	}
	
	...
```

当InstantiationAwareBeanPostProcessor#postProcessAfterInstantiation返回false时，则跳过属性赋值阶段(AbstractAutowireCapableBeanFactory#applyPropertyValues)，直接进入初始化阶段。返回true时，会执行InstantiationAwareBeanPostProcessor#postProcessProperties对PropertyValues进行使用(赋值)前最后的修改。

```Java
protected void populateBean(String beanName, RootBeanDefinition mbd, @Nullable BeanWrapper bw) {

		// Give any InstantiationAwareBeanPostProcessors the opportunity to modify the
		// state of the bean before properties are set. This can be used, for example,
		// to support styles of field injection.
		if (!mbd.isSynthetic() && hasInstantiationAwareBeanPostProcessors()) {
			for (InstantiationAwareBeanPostProcessor bp : getBeanPostProcessorCache().instantiationAware) {
				if (!bp.postProcessAfterInstantiation(bw.getWrappedInstance(), beanName)) {
					return;
				}
			}
		}
		...    
		PropertyDescriptor[] filteredPds = null;
		if (hasInstAwareBpps) {
			if (pvs == null) {
				pvs = mbd.getPropertyValues();
			}
			for (InstantiationAwareBeanPostProcessor bp : getBeanPostProcessorCache().instantiationAware) {
				PropertyValues pvsToUse = bp.postProcessProperties(pvs, bw.getWrappedInstance(), beanName);
				if (pvsToUse == null) {
					if (filteredPds == null) {
						filteredPds = filterPropertyDescriptorsForDependencyCheck(bw, mbd.allowCaching);
					}
					pvsToUse = bp.postProcessPropertyValues(pvs, filteredPds, bw.getWrappedInstance(), beanName);
					if (pvsToUse == null) {
						return;
					}
				}
				pvs = pvsToUse;
			}

		...
		if (pvs != null) {
			applyPropertyValues(beanName, mbd, bw, pvs);
		}
	}
```

AbstractAutowireCapableBeanFactory#populateBean会执行实例化后阶段。

#### Bean 属性赋值

```JAVA
AbstractAutowireCapableBeanFactory#createBean
	#doCreateBean:
		#populateBean:
			InstantiationAwareBeanPostProcessor#postProcessAfterInstantiation: 决定是否执行属性赋值
			InstantiationAwareBeanPostProcessor#postProcessPropertyValues: 属性赋值前对PropertyValues做最后的修改
		AbstractAutowireCapableBeanFactory#applyPropertyValues: 属性赋值
	
```

```java
public interface InstantiationAwareBeanPostProcessor extends BeanPostProcessor {
	...
	@Nullable
	default PropertyValues postProcessProperties(PropertyValues pvs, Object bean, String beanName)
			throws BeansException {

		return null;
	}
	...
}
```

InstantiationAwareBeanPostProcessor#postProcessProperties在属性赋值前对属性做最后的修改，返回null代表不做任何修改。

​	AutowiredAnnotationBeanPostProcessor#postProcessProperties，Spring容器的依赖注入就是在该阶段进行注入的。

#### Bean Aware 接口回调

##### BeanFactory相关Aware接口

```java
AbstractAutowireCapableBeanFactory#initializeBean:
	#invokeAwareMethods: 执行Aware接口回调
```

```java
	private void invokeAwareMethods(String beanName, Object bean) {
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

在Bean初始化前阶段之前会进行Aware接口的回调，Aware接口包括BeanNameAware、BeanClassLoaderAware和BeanFactoryAware，会依次执行回调注入。

##### ApplicationContext相关Aware接口

​	ApplicationContext相关Bean的回调会在ApplicationContextAwareProcessor#postProcessBeforeInitialization(初始化前阶段)中执行。

```java
class ApplicationContextAwareProcessor implements BeanPostProcessor {

	@Override
	@Nullable
	public Object postProcessBeforeInitialization(Object bean, String beanName) throws BeansException {
		if (!(bean instanceof EnvironmentAware || bean instanceof EmbeddedValueResolverAware ||
				bean instanceof ResourceLoaderAware || bean instanceof ApplicationEventPublisherAware ||
				bean instanceof MessageSourceAware || bean instanceof ApplicationContextAware ||
				bean instanceof ApplicationStartupAware)) {
			return bean;
		}

		invokeAwareInterfaces(bean);

		return bean;
	}

	private void invokeAwareInterfaces(Object bean) {
		if (bean instanceof EnvironmentAware) {
			((EnvironmentAware) bean).setEnvironment(this.applicationContext.getEnvironment());
		}
		if (bean instanceof EmbeddedValueResolverAware) {
			((EmbeddedValueResolverAware) bean).setEmbeddedValueResolver(this.embeddedValueResolver);
		}
		if (bean instanceof ResourceLoaderAware) {
			((ResourceLoaderAware) bean).setResourceLoader(this.applicationContext);
		}
		if (bean instanceof ApplicationEventPublisherAware) {
			((ApplicationEventPublisherAware) bean).setApplicationEventPublisher(this.applicationContext);
		}
		if (bean instanceof MessageSourceAware) {
			((MessageSourceAware) bean).setMessageSource(this.applicationContext);
		}
		if (bean instanceof ApplicationStartupAware) {
			((ApplicationStartupAware) bean).setApplicationStartup(this.applicationContext.getApplicationStartup());
		}
		if (bean instanceof ApplicationContextAware) {
			((ApplicationContextAware) bean).setApplicationContext(this.applicationContext);
		}
	}

}

```

在初始化前阶段会进行ApplicationContext Aware相关的回调，包括EnvironmentAware、EmbeddedValueResolverAware、ResourceLoaderAware、ApplicationEventPublisherAware、MessageSourceAware、ApplicationStartupAware、ApplicationContextAware，按顺序依次注入。

```java
AbstractApplicationContext#refresh
	#prepareBeanFactory:
		beanFactory.addBeanPostProcessor(new ApplicationContextAwareProcessor(this)): 注册
```

##### 

#### Bean初始化(Initialzation)

+ @PostConstruct 标注方法。由org.springframework.beans.factory.annotation.CommonAnnotationBeanPostProcessor#postProcessBeforeInitialization处理。
+ 实现org.springframework.beans.factory.InitializingBean#afterPropertiesSet方法。org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory#invokeInitMethods处理。
+ 指定BeanDefinition的initMethodName属性。org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory#invokeCustomInitMethod处理。



@Lazy标记的Bean可以延迟加载。

##### 初始化前

```java
public interface BeanPostProcessor {

	/**
	 * Apply this {@code BeanPostProcessor} to the given new bean instance <i>before</i> any bean
	 * initialization callbacks (like InitializingBean's {@code afterPropertiesSet}
	 * or a custom init-method). The bean will already be populated with property values.
	 * The returned bean instance may be a wrapper around the original.
	 * <p>The default implementation returns the given {@code bean} as-is.
	 * @param bean the new bean instance
	 * @param beanName the name of the bean
	 * @return the bean instance to use, either the original or a wrapped one;
	 * if {@code null}, no subsequent BeanPostProcessors will be invoked
	 * @throws org.springframework.beans.BeansException in case of errors
	 * @see org.springframework.beans.factory.InitializingBean#afterPropertiesSet
	 */
	@Nullable
	default Object postProcessBeforeInitialization(Object bean, String beanName) throws BeansException {
		return bean;
	}
}
```

​	会在调用初始化方法之前进行一些操作，如CommonAnnotationBeanPostProcessor#postProcessBeforeInitialization就会在该阶段执行Bean部分初始化方法(@PostConstruct标注的)。

```java
AbstractAutowireCapableBeanFactory#initializeBean
	#applyBeanPostProcessorsBeforeInitialization
		BeanPostProcessor#postProcessBeforeInitialization: 执行初始化前阶段的处理
```

##### 初始化

```
AbstractAutowireCapableBeanFactory#createBean
	#doCreateBean:
		#initializeBean:
			#invokeInitMethods:
				InitializingBean#afterPropertiesSet: 执行实现InitializingBean接口的afterPropertiesSet方法
				#invokeCustomInitMethod: 执行在BeanDefinition中指定initMethodName对应的方法
```

​	因为@PostConstruct标注的方法在Bean初始化前阶段执行，因此优先级最高。

​	初始化方法优先级： 

	1.	 @PostConstruct
	1.	 InitializingBean#afterPropertiesSet
	1.	 AbstractBeanDefinition#initMethodName对应的方法

##### 初始化后

```java
public interface BeanPostProcessor {
	...

	/**
	 * Apply this {@code BeanPostProcessor} to the given new bean instance <i>after</i> any bean
	 * initialization callbacks (like InitializingBean's {@code afterPropertiesSet}
	 * or a custom init-method). The bean will already be populated with property values.
	 * The returned bean instance may be a wrapper around the original.
	 * <p>In case of a FactoryBean, this callback will be invoked for both the FactoryBean
	 * instance and the objects created by the FactoryBean (as of Spring 2.0). The
	 * post-processor can decide whether to apply to either the FactoryBean or created
	 * objects or both through corresponding {@code bean instanceof FactoryBean} checks.
	 * <p>This callback will also be invoked after a short-circuiting triggered by a
	 * {@link InstantiationAwareBeanPostProcessor#postProcessBeforeInstantiation} method,
	 * in contrast to all other {@code BeanPostProcessor} callbacks.
	 * <p>The default implementation returns the given {@code bean} as-is.
	 * @param bean the new bean instance
	 * @param beanName the name of the bean
	 * @return the bean instance to use, either the original or a wrapped one;
	 * if {@code null}, no subsequent BeanPostProcessors will be invoked
	 * @throws org.springframework.beans.BeansException in case of errors
	 * @see org.springframework.beans.factory.InitializingBean#afterPropertiesSet
	 * @see org.springframework.beans.factory.FactoryBean
	 */
	@Nullable
	default Object postProcessAfterInitialization(Object bean, String beanName) throws BeansException {
		return bean;
	}

}
```

​	在初始化方法执行之后做一些操作，如AspectJAwareAdvisorAutoProxyCreator#postProcessAfterInitialization会在该阶段创建代理对象。

```java
AbstractAutowireCapableBeanFactory#createBean
	#doCreateBean:
		#initializeBean：
			#applyBeanPostProcessorsAfterInitialization：
				#postProcessAfterInitialization： 执行初始化后阶段的处理
```

#### Bean初始化完成

```java
public interface SmartInitializingSingleton {

	/**
	 * Invoked right at the end of the singleton pre-instantiation phase,
	 * with a guarantee that all regular singleton beans have been created
	 * already. {@link ListableBeanFactory#getBeansOfType} calls within
	 * this method won't trigger accidental side effects during bootstrap.
	 * <p><b>NOTE:</b> This callback won't be triggered for singleton beans
	 * lazily initialized on demand after {@link BeanFactory} bootstrap,
	 * and not for any other bean scope either. Carefully use it for beans
	 * with the intended bootstrap semantics only.
	 */
	void afterSingletonsInstantiated();

}
```

```java
AbstractApplicationContext#refresh
	#finishBeanFactoryInitialization  
		DefaultListableBeanFactory#preInstantiateSingletons
			SmartInitializingSingleton#afterSingletonsInstantiated
```



#### Bean销毁(Destroy)

+ @PreDestroy标注方法。由org.springframework.beans.factory.annotation.CommonAnnotationBeanPostProcessor#postProcessBeforeDestruction处理。

+ 实现org.springframework.beans.factory.DisposableBean#destroy方法。org.springframework.beans.factory.support.DefaultSingletonBeanRegistry#destroyBean处理。

+ 指定BeanDefinition的destroyMethodName属性。org.springframework.beans.factory.support.DisposableBeanAdapter#invokeCustomDestroyMethod处理。

  如果Bean指定了销毁方法，则会在org.springframework.beans.factory.support.AbstractBeanFactory#registerDisposableBeanIfNecessary处理时在IoC容器中注册DisposableBeanAdapter。

##### 销毁前

````java
public interface DestructionAwareBeanPostProcessor extends BeanPostProcessor {

	/**
	 * Apply this BeanPostProcessor to the given bean instance before its
	 * destruction, e.g. invoking custom destruction callbacks.
	 * <p>Like DisposableBean's {@code destroy} and a custom destroy method, this
	 * callback will only apply to beans which the container fully manages the
	 * lifecycle for. This is usually the case for singletons and scoped beans.
	 * @param bean the bean instance to be destroyed
	 * @param beanName the name of the bean
	 * @throws org.springframework.beans.BeansException in case of errors
	 * @see org.springframework.beans.factory.DisposableBean#destroy()
	 * @see org.springframework.beans.factory.support.AbstractBeanDefinition#setDestroyMethodName(String)
	 */
	void postProcessBeforeDestruction(Object bean, String beanName) throws BeansException;
}
````

##### 销毁

```JAVA
AbstractAutowireCapableBeanFactory#createBean
	#doCreateBean
		#registerDisposableBeanIfNecessary: 
			DefaultSingletonBeanRegistry#registerDisposableBean:如果是单例对象，并且具有销毁方法，则会创建一个相应的DisposableBeanAdapter Bean，然后注册到容器中
```

```java
class DisposableBeanAdapter implements DisposableBean, Runnable, Serializable {
	@Override
	public void destroy() {
		if (!CollectionUtils.isEmpty(this.beanPostProcessors)) {
			for (DestructionAwareBeanPostProcessor processor : this.beanPostProcessors) {
				processor.postProcessBeforeDestruction(this.bean, this.beanName);
			}
		}

		if (this.invokeDisposableBean) {

			((DisposableBean) this.bean).destroy();

		}

		if (this.destroyMethod != null) {
			invokeCustomDestroyMethod(this.destroyMethod);
		}
		else if (this.destroyMethodName != null) {
			Method methodToInvoke = determineDestroyMethod(this.destroyMethodName);
			if (methodToInvoke != null) {
				invokeCustomDestroyMethod(ClassUtils.getInterfaceMethodIfPossible(methodToInvoke));
			}
		}
	}
}
```

​	依次执行DestructionAwareBeanPostProcessor#postProcessBeforeDestruction(CommonAnnotationBeanPostProcessor#postProcessBeforeDestruction处理@PreDestroy标注方法)、DisposableBean#destroy和AbstractBeanDefinition#destroyMethodName对应的方法。

#### Bean GC

管理Spring容器后，Bean强引用会失效，然后执行GC便会回收Bean。但是GC执行时机不确定。

还可以实现java.lang.Object#finalize方法在回收前执行清理工作，不过该方法不一定执行，而且被标记为启用。

要想实现对象回收前的清理工作，可以使用ReferenceQueue实现。

#### 注册外部单例对象

​	可以在IoC容器中注册外部单例对象，该单例生命周期不由容器托管。

​	org.springframework.beans.factory.config.SingletonBeanRegistry#registerSingleton

#### 面试题

1. 如何注册一个Spring Bean
2. 什么是Spring BeanDefinition
3. Spring容器如何管理注册Bean
3. BeanpPostProcessor的使用场景

BeanPostProcessor提供对Spring Bean初始化前和初始化后阶段的生命周期回调，分别对应postProcessBeforeInitiaztion和postProcessAfterInitiaztion，允许对于Bean进行扩展或者替换

5. BeanFactoryPostProcessor和BeanPostProcessor的区别

BeanFactoryPostProcessor提供了对BeanFactory的后置操作，用于扩展BeanFactory，如添加BeanPostProcessor或获取Bean，需要结合AplplicationContext使用。

BeanPostProcessor和BeanFactory的关系是N：1，一个BeanFacroty可以关联多个BeanPostProcessor。

	6.	BeanFactory如何处理Bean的生命周期

BeanFactory的默认实现是DefaultListableBeanFactory，提供了以下Bean的生命周期：

1. BeanDefinition注册。registerBeanDefinition
2. BeanDefinition合并阶段，变成RootBeanDefinition。getMergedBeanDefinition
3. Bean实例化前阶段。resolveBeforeInstantiation
4. Bean实例化阶段。createBeanInstance
5. Bean实例化后阶段。postProcessAfterInstantiation
6. Bean属性赋值前阶段。postProcessPropertyValues
7. Bean属性赋值阶段。applyPropertyValues
8. Bean Aware接口回调。invokeAwareMethods
9. Bean初始化前阶段。initializeBean
10. Bean初始化阶段。initization
11. Bean初始化后阶段。initization
12. Bean初始化完成阶段。preInstantiateSingletons
13. Bean销毁前阶段。destroyBean
14. Bean销毁阶段。destroyBean



## Spring 配置元信息

### Bean配置元信息 - BeanDefinition

#### BeanDefinition类型

##### GenericBeanDefinition

```java
public class GenericBeanDefinition extends AbstractBeanDefinition {
    ...
    @Override
	public void setParentName(@Nullable String parentName) {
		this.parentName = parentName;
	}
    ...
}
```

​	通用的BeanDefinition，可以设置parentName

##### RootBeanDefinition

```java
public class RootBeanDefinition extends AbstractBeanDefinition {
    ...
    @Override
	public void setParentName(@Nullable String parentName) {
		if (parentName != null) {
			throw new IllegalArgumentException("Root bean cannot be changed into a child bean with parent reference");
		}
	}
    ...
}
```

​	没有parentName的BeanDefinition，或者有parentName的GenericBeanDefinition经过合并后获得的BeanDefinition

##### AnnotatedBeanDefinition

```java
public interface AnnotatedBeanDefinition extends BeanDefinition {

	/**
	 * Obtain the annotation metadata (as well as basic class metadata)
	 * for this bean definition's bean class.
	 * @return the annotation metadata object (never {@code null})
	 */
	AnnotationMetadata getMetadata();

	/**
	 * Obtain metadata for this bean definition's factory method, if any.
	 * @return the factory method metadata, or {@code null} if none
	 * @since 4.1.1
	 */
	@Nullable
	MethodMetadata getFactoryMethodMetadata();

}
```

​	从注解中解析出的BeanDefinition，含有AnnotationMetadata(注解元信息)。AnnotationMetadata有两种实现方式，

​	StandardAnnotationMetadata利用标准的JAVA反射从类中获取注解元信息。

​	SimpleAnnotationMetadata利用ASM获取注解元信息，因为ASM基于字节码进行操作，省略了类加载的过程，因此效率会高一些。

#### BeanDefinition装载

```java
public interface BeanDefinitionReader {

   BeanDefinitionRegistry getRegistry();

   @Nullable
   ResourceLoader getResourceLoader();

   @Nullable
   ClassLoader getBeanClassLoader();

   BeanNameGenerator getBeanNameGenerator();

   int loadBeanDefinitions(Resource resource) throws BeanDefinitionStoreException;

   int loadBeanDefinitions(Resource... resources) throws BeanDefinitionStoreException;

   int loadBeanDefinitions(String location) throws BeanDefinitionStoreException;

   int loadBeanDefinitions(String... locations) throws BeanDefinitionStoreException;
}
```

##### 基于XML

Spring XML 资源BeanDefinition 解析与注册

+ 核心API - XMLBeanDeinitionReader
  + 资源 - Resource
  + 底层 - BeanDefinitionDocumentReader
    + XML解析 - Java DOM Level 3 API
    + BeanDefinition解析 - BeanDefinitionParserDelegate
    + BeanDefinition注册 - BeanDefinitionRegistry

```
XmlBeanDefinitionReader#loadBeanDefinitions(String)
	#loadBeanDefinitions
		ResourceLoader#getResource: 根据location加载Resource
		#loadBeanDefinitions(Resource)
			#doLoadBeanDefinitions
				#doLoadDocument
					DefaultDocumentLoader#loadDocument
						DocumentBuilder#parse: 返回Document
				#registerBeanDefinitions
					BeanDefinitionDocumentReader#registerBeanDefinitions
						DefaultBeanDefinitionDocumentReader#doRegisterBeanDefinitions
							这里还会处理profile，如果profile不符合，则直接返回
							#parseBeanDefinitions
								#parseDefaultElement
									#importBeanDefinitionResource: 处理import导入的资源
									#processAliasRegistration: 注册别名
									#processBeanDefinition: 注册BeanDefinition
										BeanDefinitionParserDelegate#parseBeanDefinitionElement
										
									#doRegisterBeanDefinitions: 重复上层操作
```

##### 基于Properties

Spring Properties资源BeanDefinition解析与注册

+ 核心API PropertiesBeanDefinitionReader
  + 资源
    + 字节流 - Resource
    + 字符流 - EncodedResource
  + 底层
    + Properties解析 - PropertiesPersister
    + BeanDefinition解析 - API内部实现
    + BeanDefinition注册 - BeanDefinitionRegistry

```
PropertiesBeanDefinitionReader#loadBeanDefinitions
	PropertiesPersister#load: 将Resource的inputStream加载到之前创建的Properties
		#registerBeanDefinitions: 根据分隔符获取beanName,然后根据beanName去注册BeanDefinition
			#registerBeanDefinition: 按照规则去获取BeanDefinition相关的数据
				BeanDefinitionReaderUtils#createBeanDefinition: 根据数据生成GenericBeanDefinition
				BeanDefinitionRegistry#registerBeanDefinition：注册
```

##### 基于注解

Spring Java注册 BeanDefinition 解析与注册

+ 核心API - AnnotatedBeanDefinitionReader
  + 资源
    + 类对象 - java.lang.Class
  + 底层
    + 条件评估 - ConditionEvaluator
    + Bean范围解析 - ScopeMetadateResolver
    + BeanDefinition解析 - 内部API实现
    + BeanDefinition处理 - AnnotationConfigUtils.processCommonDefinitionAnnotations
    + BeanDefinition注册 - BeanDefinitionReaderUtils#registerBeanDefinition

```
AnnotatedBeanDefinitionReader#registerBean:
	#doRegisterBean:
		AnnotatedGenericBeanDefinition: 创建
		ConditionEvaluator#shouldSkip: 是否跳过注册
		ScopeMetadataResolver#resolveScopeMetadata: 解析作用域
		BeanNameGenerator#generateBeanName: 不指定BeanName则生成
		AnnotationConfigUtils#processCommonDefinitionAnnotations:
			#processCommonDefinitionAnnotations: 处理@Lazy、@Primary、@DependsOn、@Description注解
		BeanDefinitionCustomizer#customize： 自定义BeanDefinition处理
		AnnotationConfigUtils#applyScopedProxyMode: 根据代理模式确定是否生成代理对象(如ReqeustScope，会使用代理，依赖注入时注入一个代理对象，然后根据请求的不同会获取到不同的对象)
		BeanDefinitionReaderUtils#registerBeanDefinition: 注册BeanDefinition
```



### Bean属性元信息 - PropertyValues

#### MutablePropertyValues

```java
public class MutablePropertyValues implements PropertyValues, Serializable {
	...
    public void addPropertyValue(String propertyName, Object propertyValue) {
		addPropertyValue(new PropertyValue(propertyName, propertyValue));
	}
    
    public void removePropertyValue(String propertyName) {
		this.propertyValueList.remove(getPropertyValue(propertyName));
	}
    ...
}
```

```java
public interface PropertyValues extends Iterable<PropertyValue> {
	...
    PropertyValue[] getPropertyValues();
    ...
}
```

​	PropertyValues是PropertyValue的集合，一个PropertyValues可以包含多个PropertyValue。MutablePropertyValues是可变的PropertyValues，可以对PropertyValue进行添加删除。

​	PropertyValue中name和value都是final修饰的，这代表着PropertyValue一经创建便无法改变，因此想要修改PropertyValue只能将老的PropertyValue删除，然后在添加具有相同propertyName的新PropertyValue。

#### AttributeAccessor

```java
public interface BeanDefinition extends AttributeAccessor, BeanMetadataElement {
	...
}
```

​	BeanDefinition继承了AttributeAccessor和BeanMetadataElement接口。

```java
/**
 * Interface defining a generic contract for attaching and accessing metadata
 * to/from arbitrary objects.
 *
 * @author Rob Harrop
 * @author Sam Brannen
 * @since 2.0
 */
public interface AttributeAccessor {

	/**
	 * Set the attribute defined by {@code name} to the supplied {@code value}.
	 * <p>If {@code value} is {@code null}, the attribute is {@link #removeAttribute removed}.
	 * <p>In general, users should take care to prevent overlaps with other
	 * metadata attributes by using fully-qualified names, perhaps using
	 * class or package names as prefix.
	 * @param name the unique attribute key
	 * @param value the attribute value to be attached
	 */
	void setAttribute(String name, @Nullable Object value);

	/**
	 * Get the value of the attribute identified by {@code name}.
	 * <p>Return {@code null} if the attribute doesn't exist.
	 * @param name the unique attribute key
	 * @return the current value of the attribute, if any
	 */
	@Nullable
	Object getAttribute(String name);
	... 

}
```

​	AttributeAccessor可以让我们在BeanDefinition中设置一些附加属性，帮助我们更好地定义BeanDefinition。

#### BeanMetadataElement

```java
/**
 * Interface to be implemented by bean metadata elements
 * that carry a configuration source object.
 *
 * @author Juergen Hoeller
 * @since 2.0
 */
public interface BeanMetadataElement {

	/**
	 * Return the configuration source {@code Object} for this metadata element
	 * (may be {@code null}).
	 */
	@Nullable
	default Object getSource() {
		return null;
	}

}
```

​	BeanMetadataElement可以使我们在BeanDefinition中设置属性来源，如来自哪个类，或者哪个文件等。

### 容器配置元信息

| beans 元素属性              | 默认值  | 使用场景                                                    |
| --------------------------- | ------- | ----------------------------------------------------------- |
| profile                     | null    | Spring Profiles配置值                                       |
| default-lazy-init           | default | 当outter beans 存在default-lazy-init属性则继承，否则为false |
| default-merge               | default | 当outter beans 存在default-merge属性则继承，否则为false     |
| default-autowire            | default | 当outter beans 存在default-autowire属性则继承，否则为no     |
| default-autowire-candidates | null    | 默认Spring Beans名称 pattern                                |
| default-init-method         | null    | 默认Spring Beans自定义初始化方法                            |
| default-destroy-method      | null    | 默认Spring Beans自定义销毁方法                              |



| XML元素                           | 使用场景                             |
| --------------------------------- | ------------------------------------ |
| \<context:annotation-config />    | 激活Spring注解驱动                   |
| \<context:component-scan />       | Spring @Component 以及自定义注解扫描 |
| \<context:load-time-weaver />     | 激活Spring LoadTimeWeaver            |
| \<context:mbean-export />         | 暴露Spring Beans 作为JMX Beans       |
| \<context:mbean-server />         | 将当前平台作为 MBeanServer           |
| \<context:property-placeholder /> | 加载外部化配置作为Spring属性配置     |
| \<context:property-override />    | 利用外部化配置资源覆盖Spring属性值   |

#### 基于XML

| 命名空间 | 所属模块       | Scheme资源URL                                                |
| -------- | -------------- | ------------------------------------------------------------ |
| beans    | spring-beans   | https://www.springframework.org/schema/beans/spring-beans.xsd |
| context  | spring-context | https://www.springframework.org/schema/context/spring-context.xsd |
| aop      | spring-aop     | https://www.springframework.org/schema/aop/spring-aop.xsd    |
| tx       | spring-tx      | https://www.springframework.org/schema/tx/spring-tx.xsd      |
| util     | spring-util    | https://www.springframework.org/schema/util/spring-util.xsd  |
| tool     | spring-tool    | https://www.springframework.org/schema/tool/spring-util.xsd  |

spring.scheme

spring.handler：NamespaceHandlerSupport、BeanDefinitionDecorator

#### 基于注解

##### Spring IoC容器装配注解

| Spring注解      | 场景说明                                | 起始版本 |
| --------------- | --------------------------------------- | -------- |
| @ImportResource | 替换XML元素\<import>                    | 3.0      |
| @Import         | 导入Configuration Class                 | 3.0      |
| @ComponentScan  | 扫描指定package下标注Spring模式注解的类 | 3.1      |

##### Spring IoC 配置属性注解

| Spring注解       | 场景说明                        | 起始版本 |
| ---------------- | ------------------------------- | -------- |
| @PropertySource  | 配置属性抽象PropertySource 注解 | 3.1      |
| @PropertySources | @PropertySource 集合注解        | 4.0      |

#### Spring XML 扩展

+ 编写 XML Scheme文件： 定义 XML结构
+ 自定义 NamespaceHandler实现： 命名空间绑定
+ 自定义 BeanDefinitionParser实现： XML元素与BeanDefinition解析
+ 注册XML 扩展： 命名空间与XML Scheme映射

### 外部化配置元信息 - PropertySource

#### 基于Properties 资源

##### 基于注解

```java
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Repeatable(PropertySources.class)
public @interface PropertySource {

	String name() default "";
	
    ...
        
	String encoding() default "";

	Class<? extends PropertySourceFactory> factory() default PropertySourceFactory.class;
}
```

​	使用@PropertySource，其中name指明外部化文件位置，factory指明如何将外部化文件解析为PropertySource。

​	默认的PropertySourceFactory为DefaultPropertySourceFactory，可以将properties文件解析为PropertySource。

##### 基于API

```java
public interface ConfigurableEnvironment extends Environment, ConfigurablePropertyResolver {
	...
	
	MutablePropertySources getPropertySources();

	...
}
```

​	PropertySource可以从ConfigurableEnvironment中获取，ConfigurableEnvironment绑定多个PropertySource，取值时顺序从PropertySource中取，取到就返回，因此自定义一个PropertySource到ConfigurableEnvironment，并且放到首位。

#### 基于YML资源

##### 基于API

+ YamlProcessor
  + YamlPropertiesFactoryBean
  + YamlMapFactoryBean

##### 基于注解

​	使用@PropertySource，使用YamlProcessor扩展PropertySourceFactory，然后通过factory指定扩展类。

### Profile元信息 - @Profile

### 面试题

1. Spring 内建XML Scheme有哪些

+ beans
+ context
+ aop
+ tx
+ util
+ tool

2. Spring 配置元信息具体有哪些

+ Bean 配置元信息： 通过媒介(XML、Properties等)，解析BeanDefinition
+ IoC容器配置元信息：通过媒介(XML、Properties等)，控制IoC容器的行为，如注解驱动，AOP等
+ 外部化配置： 通过资源抽象（Properties、YAML等）， 控制PropertySource
+ Spring Profile： 通过外部化配置，提供条件分支流程

3. XML 扩展的缺点

+ 高复杂度
+ 嵌套元素支持较弱
+ XML处理性能较差
+ XML框架移植性差



## 基础设施

### 资源管理

#### Java资源管理

##### Java标准资源定位

| 职责         | 说明                                                         |
| ------------ | ------------------------------------------------------------ |
| 面向资源     | 文件系统、artfact(jar、war、ear)和远程资源(FTP、HTTP、HTTPS等) |
| API整合      | ClassLoader#getResource、File、URL                           |
| 资源定位     | URL 或 URI                                                   |
| 面向流式存储 | URLConnection                                                |
| 协议扩展     | URLStreamHandler 或 URLStreamHandlerFactory                  |

##### Java  URL 协议扩展

+ 基于URLStreamHandlerFactory

  ```
  java.net.URLStreamHandlerFactory#createURLStreamHandler: 创建URLStreamHandler
  	java.net.URLStreamHandler#openConnection(java.net.URL)： 打开URLConnect
  		java.net.URLConnection#getInputStream： 获取输入流
  ```

  URLStreamHandlerFactory通过java.net.URL#setURLStreamHandlerFactory设置，由JVM调用，只可设置一次。

+ 基于URLStreamHandler

JDK 1.8 内建协议实现

| 协议   | 实现类                              |
| ------ | ----------------------------------- |
| file   | sun.net.www.protocol.file.Handler   |
| ftp    | sun.net.www.protocol.ftp.Handler    |
| http   | sun.net.www.protocol.http.Handler   |
| https  | sun.net.www.protocol.https.Handler  |
| jar    | sun.net.www.protocol.jar.Handler    |
| mailto | sun.net.www.protocol.mailto.Handler |
| netdoc | sun.net.www.protocol.netdoc.Handler |

扩展

| 实现类名规则 | 说明                                                         |
| ------------ | ------------------------------------------------------------ |
| 默认         | sun.net.www.protocol.{protocol}.Handler                      |
| 自定义       | 通过java.protocol.handler.pkgs指定实现包名，实现类必须为“Handler”。如果存在多个包名，用“\|”分隔。 |

#### Spring资源管理

##### 资源接口

| 类型       | 接口                                                |
| ---------- | --------------------------------------------------- |
| 输入流     | org.springframework.core.io.InputStreamSource       |
| 只读资源   | org.springframework.core.io.Resource                |
| 可写资源   | org.springframework.core.io.WritableResource        |
| 编码资源   | org.springframework.core.io.support.EncodedResource |
| 上下文资源 | org.springframework.core.io.ContextResource         |

​	Resource有一个漏洞，即使Resource不是可写资源，也有可能进行写操作

```java
org.springframework.core.io.Resource#getURL
	java.net.URL#openConnection
		java.net.URLConnection#getOutputStream
```

##### 内建实现

| 资源来源       | 资源协议      | 实现类                                                       |
| -------------- | ------------- | ------------------------------------------------------------ |
| Bean 定义      | 无            | org.springframework.beans.factory.support.BeanDefinitionResource |
| 数组           | 无            | org.springframework.core.io.ByteArrayResource                |
| 类路径         | classpth:/    | org.springframework.core.io.ClassPathResource                |
| 文件系统       | file:/        | org.springframework.core.io.FileSystemResource               |
| URL            | URL支持的协议 | org.springframework.core.io.UrlResource                      |
| ServletContext | 无            | org.springframework.web.context.support.ServletContextResource |

##### 资源加载器 - ResourceLoader

```java
public interface ResourceLoader {

	Resource getResource(String location);

	@Nullable
	ClassLoader getClassLoader();

}
```

​	ResourceLoader默认实现为DefaultResourceLoader

```java
public class DefaultResourceLoader implements ResourceLoader {

	@Nullable
	private ClassLoader classLoader;

	private final Set<ProtocolResolver> protocolResolvers = new LinkedHashSet<>(4);
	...

	@Override
	public Resource getResource(String location) {
		Assert.notNull(location, "Location must not be null");

		for (ProtocolResolver protocolResolver : getProtocolResolvers()) {
			Resource resource = protocolResolver.resolve(location, this);
			if (resource != null) {
				return resource;
			}
		}

		if (location.startsWith("/")) {
			return getResourceByPath(location);
		}
		else if (location.startsWith(CLASSPATH_URL_PREFIX)) {
			return new ClassPathResource(location.substring(CLASSPATH_URL_PREFIX.length()), getClassLoader());
		}
		else {
			try {
				// Try to parse the location as a URL...
				URL url = new URL(location);
				return (ResourceUtils.isFileURL(url) ? new FileUrlResource(url) : new UrlResource(url));
			}
			catch (MalformedURLException ex) {
				// No URL -> resolve as resource path.
				return getResourceByPath(location);
			}
		}
	}

	/**
	 * Return a Resource handle for the resource at the given path.
	 * <p>The default implementation supports class path locations. This should
	 * be appropriate for standalone implementations but can be overridden,
	 * e.g. for implementations targeted at a Servlet container.
	 */
	protected Resource getResourceByPath(String path) {
		return new ClassPathContextResource(path, getClassLoader());
	}

}
```

​	DefaultResourceLoader主要有几个重要实现：

 + FileSystemResourceLoader
 + ClassRelativeResourceLoader
 + AbstractApplicationContext
 + ServletContextResourceLoader


##### 通配路径资源加载器 - ResourcePatternResolver

```JAVA
public interface ResourcePatternResolver extends ResourceLoader {
	...
        
	Resource[] getResources(String locationPattern) throws IOException;

}
```

​	PathMatchingResourcePatternResolver：路径匹配资源加载器，ResourcePatternResolver默认实现。主要包括PathMatcher和ResourceLoader，通过PathMatcher去进行路径匹配，匹配成功后使用ResourceLoader进行资源加载。

​	PathMatcher：路径匹配器，默认实现为AntPathMatcher，使用ant模式去匹配，*.jsp匹配所有jsp后缀的文件，\*.\*匹配所有文件。

​	可以实现PathMatcher去自定义路径匹配的规则。

##### 依赖注入Resource

基于@Value实现

```java
@Value("classpath:/...")
private Resource resource;
```

##### 依赖注入ResourceLoader

+ ResourceLoaderAware回调注入，由ApplicationContextAwareProcessor#postProcessBeforeInitialization
+ @Autowired注入ResourceLoader
+ 注入ApplicationContext作为ResourceLoader

#### 面试题

1. Spring 配置资源中有哪些常见类型
   1.  XML
   2. Properties
   3. Yaml
2. 列举不同类型Spring配置资源
   1. XML
      1. 普通Bean Definition XML配置资源 - *.xml
      2. Spring Scheme资源 - *.xsd
   2. Properties
      1. 普通 Properties格式资源 - *.properties
      2. Spring Handler 实现映射文件 - META-INF/spring.handlers
      3. Spring Scheme 资源映射文件 - META-INF/spring.shemas
      4. Spring Boot中自动装配文件 - META-INF/spring.factories
   3. YAML
      1. 普通YAML 配置资源 - \*.yaml或\*.yml
3. Java 标准资源管理扩展步骤

### 国际化

#### 使用场景

+ 普通国际化文案
+ Bean Validation校验国际化文案
+ Web站点页面渲染
+ Spring MVC错误信息提示

#### Spring 国际化接口 - MessageSource

```java
public interface MessageSource {

	/**
	 * Try to resolve the message. Return default message if no message was found.
	 * @param code the message code to look up, e.g. 'calculator.noRateSet'.
	 * MessageSource users are encouraged to base message names on qualified class
	 * or package names, avoiding potential conflicts and ensuring maximum clarity.
	 * @param args an array of arguments that will be filled in for params within
	 * the message (params look like "{0}", "{1,date}", "{2,time}" within a message),
	 * or {@code null} if none
	 * @param defaultMessage a default message to return if the lookup fails
	 * @param locale the locale in which to do the lookup
	 * @return the resolved message if the lookup was successful, otherwise
	 * the default message passed as a parameter (which may be {@code null})
	 * @see #getMessage(MessageSourceResolvable, Locale)
	 * @see java.text.MessageFormat
	 */
	@Nullable
	String getMessage(String code, @Nullable Object[] args, @Nullable String defaultMessage, Locale locale);


	String getMessage(String code, @Nullable Object[] args, Locale locale) throws NoSuchMessageException;

	/**
	 * Try to resolve the message using all the attributes contained within the
	 * {@code MessageSourceResolvable} argument that was passed in.
	 * <p>NOTE: We must throw a {@code NoSuchMessageException} on this method
	 * since at the time of calling this method we aren't able to determine if the
	 * {@code defaultMessage} property of the resolvable is {@code null} or not.
	 * @param resolvable the value object storing attributes required to resolve a message
	 * (may include a default message)
	 * @param locale the locale in which to do the lookup
	 * @return the resolved message (never {@code null} since even a
	 * {@code MessageSourceResolvable}-provided default message needs to be non-null)
	 * @throws NoSuchMessageException if no corresponding message was found
	 * (and no default message was provided by the {@code MessageSourceResolvable})
	 * @see MessageSourceResolvable#getCodes()
	 * @see MessageSourceResolvable#getArguments()
	 * @see MessageSourceResolvable#getDefaultMessage()
	 * @see java.text.MessageFormat
	 */
	String getMessage(MessageSourceResolvable resolvable, Locale locale) throws NoSuchMessageException;

}
```

​	接口中有三个重要的参数：

 +	code：文案模板的编码，可以理解为key，value为文案模板，之所以叫文案模板是因为文案模板中可能含有占位符，当占位符被替换后才是真正的文案内容。
 +	args：文案模板的参数，用来替换文案模板中的占位符，如"{0}", "{1,date}", "{2,time}"。
 +	locale： 地区，根据locale的不同返回的文案也不同，如zh_CN会返回中国的汉语，en_US会返回美国的英语。

​	MessageSourceResolvable包含多组code和arg，还有一个defaultMessage。

#### 层次性MessageSource

​	HierarchicalMessageSource具有层次性，层次性接口一般会提供一个类似getParent的接口去获取上一层次的接口。这样可以扩大查找的范围，如在当前层次找不到时会去上一层次查找。

```java
public interface HierarchicalMessageSource extends MessageSource {

	/**
	 * Set the parent that will be used to try to resolve messages
	 * that this object can't resolve.
	 * @param parent the parent MessageSource that will be used to
	 * resolve messages that this object can't resolve.
	 * May be {@code null}, in which case no further resolution is possible.
	 */
	void setParentMessageSource(@Nullable MessageSource parent);

	/**
	 * Return the parent of this MessageSource, or {@code null} if none.
	 */
	@Nullable
	MessageSource getParentMessageSource();

}
```

​	HierarchicalBeanFactory#containsLocalBean方法提供了只从当前层次查找的接口。

​	ApplicationContext#getParent提供了获取上一次层次。

​	BeanDefinition#getParentName提供了获取上一层次的标识。

#### Java国际化标准 - ResourceBundle

核心特性

+ Key-Value设计
+ 层次性设计
+ 缓存设计
+ 字符编码控制 - Control(@since 1.6)
+ Control SPI扩展 - ResourceBundleControlProvider(@since 1.8)

##### PropertyResourceBundle

```java
public class PropertyResourceBundle extends ResourceBundle {
	...
       
    public PropertyResourceBundle (Reader reader) throws IOException {
        Properties properties = new Properties();
        properties.load(reader);
        lookup = new HashMap(properties);
    }
    
    ...    
}
```

​	基于PropertyResourceBundle资源实现，因为资源加载需要耗时，因此还提供了缓存功能。

##### ListableResourceBundle

```java
public abstract class ListResourceBundle extends ResourceBundle {
	...
        
	protected abstract Object[][] getContents();
    
	...
}
```

​	列举式硬编码的ResourceBundle，实现Object\[][] getContents()方法返回二维数组，其中第一个数组为方案模板的编码，第二个数据为方案模板的内容。

#### Java文本格式化 - MessageFormat

##### 基本用法

+ 设置消息格式模式 - new MessageFormat(...)
+ 格式化 - format(new Object[]{...})

##### 消息格式模式

+ 格式元素：{ArgumentIndex(, FormatType, (FormatStyle))}
+ FormatType：消息格式类型，可选项， 每种类型在 number、date、time、choice类型选其一
+ FormatStyle：消息格式风格，可选项， 包括short、medium、long、full、integer、currency、percent

示例如下

```java
  MessageFormat mf = new MessageFormat("{0,number,#.##}, {0,number,#.#}");
  Object[] objs = {new Double(3.1415)};
  String result = mf.format( objs );
  // result now equals "3.14, 3.1"
```

#### MessageSource内建实现

##### ResourceBundleMessageSource

```java
public class ResourceBundleMessageSource extends AbstractResourceBasedMessageSource implements BeanClassLoaderAware {
    @Override
	public final String getMessage(String code, @Nullable Object[] args, @Nullable String defaultMessage, Locale locale) {
		String msg = getMessageInternal(code, args, locale);
		if (msg != null) {
			return msg;
		}
		if (defaultMessage == null) {
			return getDefaultMessage(code);
		}
		return renderDefaultMessage(defaultMessage, args, locale);
	}
    
    @Nullable
	protected String getMessageInternal(@Nullable String code, @Nullable Object[] args, @Nullable Locale locale) {
		...
		Object[] argsToUse = args;

		if (!isAlwaysUseMessageFormat() && ObjectUtils.isEmpty(args)) {
			...
		}
		else {
			// Resolve arguments eagerly, for the case where the message
			// is defined in a parent MessageSource but resolvable arguments
			// are defined in the child MessageSource.
			argsToUse = resolveArguments(args, locale);

			MessageFormat messageFormat = resolveCode(code, locale);
			if (messageFormat != null) {
				synchronized (messageFormat) {
                    // 使用MessageFormat 格式化
					return messageFormat.format(argsToUse);
				}
			}
		}
		...
		return getMessageFromParent(code, argsToUse, locale);
	}
    
    @Override
	@Nullable
	protected MessageFormat resolveCode(String code, Locale locale) {
		Set<String> basenames = getBasenameSet();
		for (String basename : basenames) {
            // 获取ResourceBundle
			ResourceBundle bundle = getResourceBundle(basename, locale);
			if (bundle != null) {
                // 使用ResourceBundle 获取文案模板
				MessageFormat messageFormat = getMessageFormat(bundle, code, locale);
				if (messageFormat != null) {
					return messageFormat;
				}
			}
		}
		return null;
	}

}
```

​	基于ResourceBundle + MessageFormat的实现，ResourceBundle提供文本模板，MessageFormat负责对模板进行格式化。

##### ReloadResourceBundleMessageSource

```java
public class ReloadableResourceBundleMessageSource extends AbstractResourceBasedMessageSource
		implements ResourceLoaderAware {
    @Override
	@Nullable
	protected MessageFormat resolveCode(String code, Locale locale) {
		if (getCacheMillis() < 0) {
            // 从Properties 中获取
			PropertiesHolder propHolder = getMergedProperties(locale);
			MessageFormat result = propHolder.getMessageFormat(code, locale);
			if (result != null) {
				return result;
			}
		}
		else {
			for (String basename : getBasenameSet()) {
				List<String> filenames = calculateAllFilenames(basename, locale);
				for (String filename : filenames) {
					PropertiesHolder propHolder = getProperties(filename);
					MessageFormat result = propHolder.getMessageFormat(code, locale);
					if (result != null) {
						return result;
					}
				}
			}
		}
		return null;
	}
    
    
    protected PropertiesHolder refreshProperties(String filename, @Nullable PropertiesHolder propHolder) {
		long refreshTimestamp = (getCacheMillis() < 0 ? -1 : System.currentTimeMillis());

		Resource resource = this.resourceLoader.getResource(filename + PROPERTIES_SUFFIX);
		if (!resource.exists()) {
			resource = this.resourceLoader.getResource(filename + XML_SUFFIX);
		}

		if (resource.exists()) {
			long fileTimestamp = -1;
			if (getCacheMillis() >= 0) {
				// Last-modified timestamp of file will just be read if caching with timeout.
				try {
					fileTimestamp = resource.lastModified();
					if (propHolder != null && propHolder.getFileTimestamp() == fileTimestamp) {
						if (logger.isDebugEnabled()) {
							logger.debug("Re-caching properties for filename [" + filename + "] - file hasn't been modified");
						}
						propHolder.setRefreshTimestamp(refreshTimestamp);
						return propHolder;
					}
				}
				catch (IOException ex) {
					// Probably a class path resource: cache it forever.
					if (logger.isDebugEnabled()) {
						logger.debug(resource + " could not be resolved in the file system - assuming that it hasn't changed", ex);
					}
					fileTimestamp = -1;
				}
			}
			try {
				Properties props = loadProperties(resource, filename);
				propHolder = new PropertiesHolder(props, fileTimestamp);
			}
			catch (IOException ex) {
				if (logger.isWarnEnabled()) {
					logger.warn("Could not parse properties file [" + resource.getFilename() + "]", ex);
				}
				// Empty holder representing "not valid".
				propHolder = new PropertiesHolder();
			}
		}

		else {
			// Resource does not exist.
			if (logger.isDebugEnabled()) {
				logger.debug("No properties file found for [" + filename + "] - neither plain properties nor XML");
			}
			// Empty holder representing "not found".
			propHolder = new PropertiesHolder();
		}

		propHolder.setRefreshTimestamp(refreshTimestamp);
		this.cachedProperties.put(filename, propHolder);
		return propHolder;
	}
}
```



​	基于Properties + MessageFormat的实现，使用Properties作为文本模板存储，MessageFormat负责对模板进行格式化。并且可以自动刷新，自动刷新依据lastModified更新，但不一定有用，如有些资源是没有该属性，而且对于在Docker中运行的静态文件来说，不会进行修改。

##### MessageSource内建依赖

```java
protected void initMessageSource() {
		ConfigurableListableBeanFactory beanFactory = getBeanFactory();
		if (beanFactory.containsLocalBean(MESSAGE_SOURCE_BEAN_NAME)) {
			this.messageSource = beanFactory.getBean(MESSAGE_SOURCE_BEAN_NAME, MessageSource.class);
			// Make MessageSource aware of parent MessageSource.
			if (this.parent != null && this.messageSource instanceof HierarchicalMessageSource) {
				HierarchicalMessageSource hms = (HierarchicalMessageSource) this.messageSource;
				if (hms.getParentMessageSource() == null) {
					// Only set parent context as parent MessageSource if no parent MessageSource
					// registered already.
					hms.setParentMessageSource(getInternalParentMessageSource());
				}
			}
			if (logger.isTraceEnabled()) {
				logger.trace("Using MessageSource [" + this.messageSource + "]");
			}
		}
		else {
			// Use empty MessageSource to be able to accept getMessage calls.
			DelegatingMessageSource dms = new DelegatingMessageSource();
			dms.setParentMessageSource(getInternalParentMessageSource());
			this.messageSource = dms;
			beanFactory.registerSingleton(MESSAGE_SOURCE_BEAN_NAME, this.messageSource);
			if (logger.isTraceEnabled()) {
				logger.trace("No '" + MESSAGE_SOURCE_BEAN_NAME + "' bean, using [" + this.messageSource + "]");
			}
		}
	}
```

+ 首先从BeanFactory中查找名为“messageSource”，类型为MessageSource的Bean，找到则使用
+ 找不到则内建一个DelegatingMessageSource，该实现为空实现（没有任何文本模板），只是提供了一个层次性查找MessageSource的功能。

#### SpringBoot MessageSource 自动装配

```java
@Configuration(proxyBeanMethods = false)
@ConditionalOnMissingBean(name = AbstractApplicationContext.MESSAGE_SOURCE_BEAN_NAME, search = SearchStrategy.CURRENT)
@AutoConfigureOrder(Ordered.HIGHEST_PRECEDENCE)
@Conditional(ResourceBundleCondition.class)
@EnableConfigurationProperties
public class MessageSourceAutoConfiguration {

	private static final Resource[] NO_RESOURCES = {};

	@Bean
	@ConfigurationProperties(prefix = "spring.messages")
	public MessageSourceProperties messageSourceProperties() {
		return new MessageSourceProperties();
	}

	@Bean
	public MessageSource messageSource(MessageSourceProperties properties) {
		ResourceBundleMessageSource messageSource = new ResourceBundleMessageSource();
		if (StringUtils.hasText(properties.getBasename())) {
			messageSource.setBasenames(StringUtils
					.commaDelimitedListToStringArray(StringUtils.trimAllWhitespace(properties.getBasename())));
		}
		...
		return messageSource;
	}

	protected static class ResourceBundleCondition extends SpringBootCondition {

		private static ConcurrentReferenceHashMap<String, ConditionOutcome> cache = new ConcurrentReferenceHashMap<>();

		@Override
		public ConditionOutcome getMatchOutcome(ConditionContext context, AnnotatedTypeMetadata metadata) {
			String basename = context.getEnvironment().getProperty("spring.messages.basename", "messages");
			ConditionOutcome outcome = cache.get(basename);
			if (outcome == null) {
				outcome = getMatchOutcomeForBasename(context, basename);
				cache.put(basename, outcome);
			}
			return outcome;
		}

		private ConditionOutcome getMatchOutcomeForBasename(ConditionContext context, String basename) {
			...
		}

		private Resource[] getResources(ClassLoader classLoader, String name) {
			...
		}

	}

}
```

​	MessageSourceAutoConfiguration在ApplicationContext没有名为AbstractApplicationContext.MESSAGE_SOURCE_BEAN_NAME的Bean，且spring.messages.basename对应的文件存在时，会自动装配一个MessageSourceProperties Bean。

#### 面试题

1. Spring 国际化接口有哪些

  +	MessageSource
  +	HierarchicalMessageSource

2. Spring 有哪些MessageSource内建实现

+ ResourceBundleMessageSource
+ ReloadableResourceBundleMessageSource
+ StaticMessageSource
+ DelegatingMessageSource

3. 如何实现配置自动更新MessageSource

### 数据校验

#### 使用场景

##### Spring 常规校验(Validator)

##### Spring 数据绑定(DataBinder)

##### Spring Web 参数绑定(WebDataBinder)

##### Spring WebMVC/WebFlux 处理方法参数校验

#### Validator

```java
public interface Validator {

	boolean supports(Class<?> clazz);

	void validate(Object target, Errors errors);

}
```

+ 接口职责
  + Spring内部校验接口，通过编程的方式校验目标对象
+ 核心方法
  + supports(Class)：校验目标类能否校验
  + validate(Object，Errors)：校验目标对象，并将校验失败的内容输出至Errors对象
+ 配套组件
  + 错误收集器： Errors，用于组织和存储校验失败的信息
  + Validator工具类： ValidationUtils，用于简化重复性的校验操作

​	Validator是面向编程方式的校验器，需要自己根据业务需求去编写校验逻辑，比较繁琐，对于很多常见的判断，我们更倾向于使用声明式的校验方式。

​	Validator一般来说是针对某一个Bean或某个类的对象进行校验，调用Validator#validate对Bean进行校验前，还需要调用Validator#supports去判断是否支持当前Bean的校验，反而使使用场景变狭隘了。

#### Errors

```java
public interface Errors {
    // 获取绑定的校验Bean name
    String getObjectName();
    // 注册Bean校验错误
    void reject(String errorCode, @Nullable Object[] errorArgs, @Nullable String defaultMessage);
    // 注册Bean字段校验错误
    void rejectValue(@Nullable String field, String errorCode,
			@Nullable Object[] errorArgs, @Nullable String defaultMessage);
    // 获取所有的Bean校验错误信息
    List<ObjectError> getGlobalErrors();
    // 获取所有的Bean字段校验错误信息
    List<FieldError> getFieldErrors();
    // 获取所有的Bean校验错误信息和Bean字段校验错误信息
    List<ObjectError> getAllErrors();
}
```

+ 接口职责
  + 用于组织和存储校验失败的信息
+ 核心方法
  + reject：用来生成和存储Bean校验失败相关的信息，使用ObjectError存储
  + rejectValue：用来生成和存储Bean Field校验失败的相关信息，使用FieldError存储

​	使用Validator校验Bean时，一般需要我们将Errors创建出来，而Errors的实现有很多种，使用的时候反而变得复杂了。

##### BindingResult

```java
public interface BindingResult extends Errors {
    // 绑定的目标对象
    @Nullable
	Object getTarget();
    // 类型转换
    @Nullable
	PropertyEditorRegistry getPropertyEditorRegistry();
    // MessageCodesResolver的能力
    String[] resolveMessageCodes(String errorCode);
    void addError(ObjectError error);
}
```



##### BeanPropertyBindingResult

```java
/**
 * Default implementation of the {@link Errors} and {@link BindingResult}
 * interfaces, for the registration and evaluation of binding errors on
 * JavaBean objects.
 *
 * <p>Performs standard JavaBean property access, also supporting nested
 * properties. Normally, application code will work with the
 * {@code Errors} interface or the {@code BindingResult} interface.
 * A {@link DataBinder} returns its {@code BindingResult} via
 * {@link DataBinder#getBindingResult()}.
 */
public class BeanPropertyBindingResult extends AbstractPropertyBindingResult implements Serializable {
    // JavaBean
	@Nullable
	private final Object target;
    // PropertyAccessor
    @Nullable
	private transient BeanWrapper beanWrapper;
}
```



#### ObjectError

```java
public class ObjectError extends DefaultMessageSourceResolvable {
	// 校验Bean的name
	private final String objectName;
	// 校验Bean
	@Nullable
	private transient Object source;
    
    ...
}
```

```java
public class DefaultMessageSourceResolvable implements MessageSourceResolvable, Serializable {

	@Nullable
	private final String[] codes;

	@Nullable
	private final Object[] arguments;

	@Nullable
	private final String defaultMessage;
    
    ...
}
```



​	存储Bean校验失败的相关信息，如Bean不能为null。ObjectError继承于MessageSourceResolvable，包含codes、arguments和defaultMessage与国际化文案相关的属性，用于结合MessageSource# getMessage(MessageSourceResolvable resolvable, Locale locale)获取校验失败时的国际化文案。并且添加了objectName和source，用于绑定校验Bean。

​	通过Errors#getGlobalErrors获取Bean校验失败时所有Bean相关的ObjectError。

##### FieldError

```java
public class FieldError extends ObjectError {
	// 校验失败的属性
	private final String field;

    // 校验失败的属性值
	@Nullable
	private final Object rejectedValue;
    
    ...
}
```



​	存储Bean 属性校验失败的相关信息，如属性不能为null。FieldError继承于ObjectError，并添加了field和rejectedValue，用于定位具体的校验属性以及存储属性校验失败时的值。

​	通过Errors#getFieldErrors获取Bean校验失败时所有属性相关的FieldError。

#### 自定义Validator

+ 实现Validator接口
  + 实现supports方法
  + 实现validate方法
    + 通过Errors对象收集错误信息
      + ObjectError：对象错误信息
      + FieldError：对象属性错误信息
    + 通过ObjectError和Field关联Message获取校验失败的文案

```
// 1. 实现并创建Validator
// 2. 创建校验Bean
// 3. 调用Validator#supports和Validator#validate进行校验
// 4. 创建Errors对象
// 5. 获取ObjectError和FieldError
Errors#getAllErrors()
// 6. 获取MessageSource对象
// 7. 通过ObjectError和FieldError中的codes、arguments和defaultMessage结合MessageSource获取文案
```

​	Spring Framewor对Bean校验时会使用Validator对特定Bean进行校验，为了减少重复的校验操作，Spring Framewor提供了ValidationUtils简化操作；Validator校验出来的错误信息会存储到Errors中，Errors会包含ObjectError或FieldError，两者都包含code和args，结合MessageSource得到错误文案。

#### Spring整合Bean Validation

​	基于Spring Validator使用的复杂性，Spring 团队整合Bean Validation(JSR-303)对Validator进行“救赎”。

```java
public interface SmartValidator extends Validator {
    void validate(Object target, Errors errors, Object... validationHints);

	default void validateValue(
			Class<?> targetType, String fieldName, @Nullable Object value, Errors errors, Object... validationHints) {

		throw new IllegalArgumentException("Cannot validate individual value for " + targetType);
	}
}
```

```java
public class SpringValidatorAdapter implements SmartValidator, javax.validation.Validator {
	@Nullable
	private javax.validation.Validator targetValidator;
    // 只要存在Bean Validation的验证器，就支持校验
    @Override
	public boolean supports(Class<?> clazz) {
		return (this.targetValidator != null);
	}
    // 使用Bean Validation验证器进行校验
    @Override
	public void validate(Object target, Errors errors) {
		if (this.targetValidator != null) {
			processConstraintViolations(this.targetValidator.validate(target), errors);
		}
	}
    
    @Override
	public void validateValue(
			Class<?> targetType, String fieldName, @Nullable Object value, Errors errors, Object... validationHints) {

		if (this.targetValidator != null) {
			processConstraintViolations(this.targetValidator.validateValue(
					(Class) targetType, fieldName, value, asValidationGroups(validationHints)), errors);
		}
	}
	// 将JSR-303 ConstraintViolation的信息添加到Spring Errors对象中。
    protected void processConstraintViolations(Set<ConstraintViolation<Object>> violations, Errors errors) {
        ...
    }
}
```

```java
// Since:3.0
public class LocalValidatorFactoryBean extends SpringValidatorAdapter
		implements ValidatorFactory, ApplicationContextAware, InitializingBean, DisposableBean {
    @Override
	@SuppressWarnings({"rawtypes", "unchecked"})
	public void afterPropertiesSet() {
		...
		// 设置Bean Validation验证器
		setTargetValidator(this.validatorFactory.getValidator());
		...
	}
    
    @Override
	public Validator getValidator() {
		Assert.notNull(this.validatorFactory, "No target ValidatorFactory set");
		return this.validatorFactory.getValidator();
	}
}
```

​	SpringValidatorAdapter负责整合Bean Validation，LocalValidatorFactoryBean提供Bean Validation相关的Validator(Bean Validation由Hibernate Validator支持)。并且SpringValidatorAdapter还会将Bean Validation的ConstraintViolation的信息添加到Spring Errors中，以供结合MessageSource获取文案。

```JAVA
// since 3.1
public class MethodValidationPostProcessor extends AbstractBeanFactoryAwareAdvisingPostProcessor
		implements InitializingBean {

	private Class<? extends Annotation> validatedAnnotationType = Validated.class;
    
    @Nullable
	private Validator validator;
    
    @Override
	public void afterPropertiesSet() {
		Pointcut pointcut = new AnnotationMatchingPointcut(this.validatedAnnotationType, true);
		this.advisor = new DefaultPointcutAdvisor(pointcut, createMethodValidationAdvice(this.validator));
	}
    
    protected Advice createMethodValidationAdvice(@Nullable Validator validator) {
		return (validator != null ? new MethodValidationInterceptor(validator) : new MethodValidationInterceptor());
	}
    
    @Override
	public Object postProcessAfterInitialization(Object bean, String beanName) {
		...
		if (isEligible(bean, beanName)) {
			ProxyFactory proxyFactory = prepareProxyFactory(bean, beanName);
			if (!proxyFactory.isProxyTargetClass()) {
				evaluateProxyInterfaces(bean.getClass(), proxyFactory);
			}
			proxyFactory.addAdvisor(this.advisor);
			customizeProxyFactory(proxyFactory);

			// Use original ClassLoader if bean class not locally loaded in overriding class loader
			ClassLoader classLoader = getProxyClassLoader();
			if (classLoader instanceof SmartClassLoader && classLoader != bean.getClass().getClassLoader()) {
				classLoader = ((SmartClassLoader) classLoader).getOriginalClassLoader();
			}
			return proxyFactory.getProxy(classLoader);
		}

		// No proxy needed.
		return bean;
	}
}
```

​	MethodValidationPostProcessor以AOP的方式进行Bean Validation处理，MethodValidationPostProcessor会生成Advisor，用于拦截标记Validated的类(AnnotationMatchingPointcut)，并使用MethodValidationInterceptor对执行的方法进行拦截处理。MethodValidationPostProcessor继承于BeanPostProcessor，在postProcessAfterInitialization方法中，根据Pointcut筛选候选者，然后为候选者生成代理对象。

```JAVA
@Configuration(proxyBeanMethods = false)
@ConditionalOnClass(ExecutableValidator.class)
@ConditionalOnResource(resources = "classpath:META-INF/services/javax.validation.spi.ValidationProvider")
@Import(PrimaryDefaultValidatorPostProcessor.class)
public class ValidationAutoConfiguration {

	@Bean
	@Role(BeanDefinition.ROLE_INFRASTRUCTURE)
	@ConditionalOnMissingBean(Validator.class)
	public static LocalValidatorFactoryBean defaultValidator() {
		LocalValidatorFactoryBean factoryBean = new LocalValidatorFactoryBean();
		MessageInterpolatorFactory interpolatorFactory = new MessageInterpolatorFactory();
		factoryBean.setMessageInterpolator(interpolatorFactory.getObject());
		return factoryBean;
	}

	@Bean
	@ConditionalOnMissingBean
	public static MethodValidationPostProcessor methodValidationPostProcessor(Environment environment,
			@Lazy Validator validator, ObjectProvider<MethodValidationExcludeFilter> excludeFilters) {
		FilteredMethodValidationPostProcessor processor = new FilteredMethodValidationPostProcessor(
				excludeFilters.orderedStream());
		boolean proxyTargetClass = environment.getProperty("spring.aop.proxy-target-class", Boolean.class, true);
		processor.setProxyTargetClass(proxyTargetClass);
		processor.setValidator(validator);
		return processor;
	}

}
```



​	在Spring Boot中，ValidationAutoConfiguration会自动装配LocalValidatorFactoryBean和MethodValidationPostProcessor。

##### 面试题

1. Spring 校验接口是哪个

​		Validator

 2. Spring有哪些校验核心组件

    Validator

    Errors

    ObjectError

    FieldError

    LocalValidationFactoryBean

 3. 演示Spring Bean的校验

### 数据绑定

#### 使用场景

+ Spring BeanDefinition 到 Bean实例创建
+ Spring 数据绑定(DataBinder)
+ Spring Web 参数绑定(WebDataBinder)

#### DataBinder

+ 标准组件
  + DataBinder
+ Web 组件
  + WebDataBinder
  + ServletRequestDataBinder
  + WebRequestDataBinder
  + WebExchangeDataBinder

```java
public class DataBinder implements PropertyEditorRegistry, TypeConverter {
    // 数据绑定的目标Bean
    @Nullable
	private final Object target;
    // 目标Bean名称
	private final String objectName;
    // 绑定结果
    @Nullable
	private AbstractPropertyBindingResult bindingResult;
    // 类型转换
    @Nullable
	private SimpleTypeConverter typeConverter;
    // Spring 新版本类型转换
    @Nullable
	private ConversionService conversionService;
    // 国际化文案相关
    @Nullable
	private MessageCodesResolver messageCodesResolver;
    // 验证器。如果有嵌套属性，可能嵌套属性需要其他验证器，因此会有多个
    private final List<Validator> validators = new ArrayList<>();
    
    // 控制数据绑定的一些行为参数
    // 忽略未知字段
    private boolean ignoreUnknownFields = true;
	// 忽略无效字段
	private boolean ignoreInvalidFields = false;
	// 允许字段创建嵌套路径。如x.y，设置y时会自动创建x
	private boolean autoGrowNestedPaths = true;
    // 允许绑定的字段
    @Nullable
	private String[] allowedFields;
	// 不允许绑定的字段
	@Nullable
	private String[] disallowedFields;
	// 必须绑定的字段
	@Nullable
	private String[] requiredFields;
    // 进行Bean 数据绑定
    public void bind(PropertyValues pvs) {
		MutablePropertyValues mpvs = (pvs instanceof MutablePropertyValues ?
				(MutablePropertyValues) pvs : new MutablePropertyValues(pvs));
		doBind(mpvs);
	}
}
```

​	DataBinder包含目标Bean，负责将PropertyValues绑定到Bean上，其中还涉及到类型绑定和数据校验。

​	DataBinder还包括一些控制数据绑定过程中的行为的参数、如忽略未知字段、忽略无效字段、允许字段创建嵌套路径等。

#### PropertyValues

| 特征             | 说明                                                         |
| ---------------- | ------------------------------------------------------------ |
| 数据来源         | BeanDefinition，主要来源于XML资源                            |
| 数据结构         | 由一个或多个PropertyValue组成                                |
| 成员结构         | PropertyValue包含属性名称，以及属性值（原始值和转换后的值）  |
| 常见实现         | MultablePropertyValues                                       |
| Web扩展          | ServletConfigPropertyValues、ServletRequestParameterPropertyValues |
| 相关生命周期处理 | InstantiationAwareBeanPostProcessor#postProcessProperties    |

#### JavaBeans替换实现 - BeanWrapper

+ JavaBeans - BeanInfo
  + 属性(Property)
    + PropertyEditor
  + 方法(Method)
  + 事件(Event)
  + 表达式(Expression)
+ Spring替换实现 - BeanWrapper
  + 属性(Property)
    + PropertyEditor
  + 嵌套属性(nested path)

​	BeanWrapper相比于BeanInfo，去掉了方法、事件、表达式，添加了嵌套属性，更加精简了。

#### JavaBeans

| API                           | 说明                                                         |
| ----------------------------- | ------------------------------------------------------------ |
| java.beans.Introspector       | Java Beans 内省API                                           |
| java.beans.BeanInfo           | Java Bean 元信息API，通过Introspector#getBeanInfo()获得J     |
| java.beans.BeanDescriptor     | Java Bean 信息描述符，通过BeanInfo#getBeanDescriptor获得     |
| java.beans.PropertyDescriptor | Java Bean 属性描述符，通过BeanInfo#getPropertyDescriptors获得 |
| java.beans.MethodDescriptor   | Java Bean 方法描述符，通过BeanInfo#getMethodDescriptors获得  |
| java.beans.EventSetDescriptor | Java Bean 事件集合描述符，通过BeanInfo#getEventSetDescriptors获得 |

​	Java语言提供的API集合。

#### BeanWrapper

+ Spring 底层 JavaBeans 基础设施的中心化接口
+ 通常不直接使用，间接用于BeanFactory和DataBinder
+ 提供标准 JavaBeans分析和操作，能够单独或批量存储Java Bean属性(properties)
+ 支持嵌套属性路径(nested path)
+ 实现类 BeanWrapperImpl

####  DataBinder 数据校验

+ DataBinder 与 BeanWrapper
  + bind方法生成BeanPropertyBindingResult
  + BeanPropertyBindingResult关键BeanWrapper(PropertyAccessor)

```java
org.springframework.validation.DataBinder#bind(PropertyValues)
	#doBind(MutablePropertyValues)
		#applyPropertyValues(MutablePropertyValues)
			#getPropertyAccessor
				#getInternalBindingResult
					#createBeanPropertyBindingResult：创建BeanPropertyBindingResult
					AbstractPropertyBindingResult#getPropertyAccessor
						#createBeanWrapper：创建BeanWrapper(is PropertyAccessor)
							PropertyAccessorFactory#forBeanPropertyAccess
			BeanWrapper#setPropertyValues(MutablePropertyValues)
				#setPropertyValue(PropertyValue)
					AbstractNestablePropertyAccessor#setPropertyValue
						#processLocalProperty
							BeanPropertyHandler#setValue
								java.beans.PropertyDescriptor#getWriteMethod
									java.lang.reflect.Method#invoke
```

​	Spring Bean创建时数据绑定

```
org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory#populateBean
	#applyPropertyValues
		BeanWrapper#setPropertyValues
```

#### 面试题

1. Spring 数据绑定API是什么

   DataBinder，细节相关API有BeanPropertyBindingResult和BeanWrapper。

2. BeanWrapper与JavaBeans的关系

   BeanWrapper是Spring 底层 JavaBeans基础设置的中心化接口，是JavaBeans的包装。

3. DataBinder是怎么完成类型转换的

### 类型转换

​	在Spring 3之前，使用基于JavaBeans的PropertyEditor来完成类型转换。Spring 3之后，使用ConvesionService通用类型转换来完成类型转换。

#### 使用场景

| 场景               | PropertyEditor | ConvesionService |
| ------------------ | -------------- | ---------------- |
| 数据绑定           | YES            | YES              |
| BeanWrapper        | YES            | YES              |
| Bean 属性类型转换  | YES            | YES              |
| 外部化属性类型转换 | NO             | YES              |

#### PropertyEditor

```java
// 将String类型转换为目标类型
public interface PropertyEditor {
    // 设置目标类型的值
    void setValue(Object value);
    // 获取目标类型的值
    Object getValue();
    // 获取String类型的值
    String getAsText();
    // 设置String类型的值
    void setAsText(String text) throws java.lang.IllegalArgumentException;
}
```

##### 基于PropertyEditor的类型转换

​	继承PropertyEditor接口的支持类PropertyEditorSupport，实现setAsText和getAsText方法。如自定义String到Properties的类型转换：

```JAVA
public class StringToPropertiesPropertyEditor extends PropertyEditorSupport {
    @Override
    public String getAsText() {
        Properties properties = (Properties)getValue();
        return properties.toString();
    }

    @Override
    public void setAsText(String text) throws IllegalArgumentException {
        Properties properties = new Properties();

        try (StringReader reader = new StringReader(text)){
            properties.load(reader);
        } catch (IOException e) {
            e.printStackTrace();
        }
        setValue(properties);
    }
}
```

##### Spring内建实现

​	Spring Framework中PropertyEditor内建实现位于包org.springframework.beans.propertyeditors，有ByteArrayPropertyEditor、CharArrayPropertyEditor、InputSourceEditor等。

##### 在Spring添加自定义PropertyEditor

###### PropertyEditorRegistrar

​	实现PropertyEditorRegistrar接口，并将PropertyEditorRegistrar注册到Spring容器中。

```java
public interface PropertyEditorRegistrar {
	void registerCustomEditors(PropertyEditorRegistry registry);
}
```

###### PropertyEditorRegistry

​	向PropertyEditorRegistry注册自定义PropertyEditor实现。

```java
public interface PropertyEditorRegistry {
	// 注册为通用类型的类型转换
	void registerCustomEditor(Class<?> requiredType, PropertyEditor propertyEditor);
	// 注册为针对通用类型以及指定的属性路径的类型转换
	void registerCustomEditor(@Nullable Class<?> requiredType, @Nullable String propertyPath, PropertyEditor propertyEditor);

	@Nullable
	PropertyEditor findCustomEditor(@Nullable Class<?> requiredType, @Nullable String propertyPath);

}
```

##### 设计缺陷

+ 违反职责单一原则。PropertyEdito除了类型转换，还包括Java Beans事件和Java GUI交互
+ 实现类型局限。来源类型只能为String类型
+ 缺少类型安全。获取的目标类型为Object，需要强转才能使用，而且仅能通过实现类命名表达语义，缺少强关联

#### Convert

```java
public interface Converter<S, T> {
	@Nullable
	T convert(S source);
}
```

​	Spring基于PropertyEditor的设计缺陷，设计出了Convert接口。

+ 首先，该接口仅提供了一个convert方法用于类型转换，符合职责单一原则
+ 其次， Converter<S, T>提供了两种泛型，S代表source，T代表target，T convert(S source)将S类型转换为T类型，这样来源类型就不仅仅限定于String类型
+ 最后，因为泛型的原因，也保证了目标类型为强类型，省去了强转，也保证了类型安全。

##### 内建实现

| 转换场景            | 实现类所在包名                               |
| ------------------- | -------------------------------------------- |
| 日期/时间相关       | org.springframework.format.datetime          |
| Java8 日期/时间相关 | org.springframework.format.datetime.standard |
| 通用实现            | org.springframework.core.convert.support     |

##### 局限性	

	+	Convert没有前置判断接口，无法判断能否转换传入的来源类型和目标类型。当有很多Convert时，不可能说一个一个取出类型去匹配。
	+	Convert虽然是基于泛型进行类型转换的，但是泛型因为擦写的原因，对集合类型不太友好，如数组类型、Collection、Map等类型。当Convert中的S为Collection\<String>这种集合类型时，因为泛型擦写，Collection中的成员类型String在处理过程中就不可知了。

##### ConditionalConverter

````java
public interface ConditionalConverter {
    
	boolean matches(TypeDescriptor sourceType, TypeDescriptor targetType);

}
````

​	ConditionalConverter是前置判断接口，用于判断传入的来源类型和目标类型是否能够转换，参数使用TypeDescriptor，而非泛型，是因为TypeDescriptor可以更好的描述类型，如原生类型、复合类型等。

​	如果想要实现一个具有前置判断的转换器，需要同时实现ConditionalConverter和Converter接口。

##### GenericConverter

```java
public interface GenericConverter {

	@Nullable
	Set<ConvertiblePair> getConvertibleTypes();

	@Nullable
	Object convert(@Nullable Object source, TypeDescriptor sourceType, TypeDescriptor targetType);
}
```

​	对于集合类型，Spring提供了GenericConverter接口，其中convert方法使用TypeDescriptor来描述类型，可以明确得知集合类型和集合中的成员类型。getConvertibleTypes表示GenericConverter可以转换多种类型。

​	对于集合类型转换，GenericConverter还是使用Convert来对成员类型进行转换。

##### ConditionalGenericConverter

```java
public interface ConditionalGenericConverter extends GenericConverter, ConditionalConverter {
}

```

​	集成了转换接口和前置判断接口。

##### 扩展Converter

+ 实现转换器接口
  + Converter
  + GenericConverter
  + ConverterFactory
+ 注册转换器实现
  + ConversionServiceFactory
  + ConversionService(名称为ConfigurableApplicationContext#CONVERSION_SERVICE_BEAN_NAME)

##### ConversionService

​	使用Converter和GenericConverter统一对外提供转换服务。

```java
public interface ConversionService {
	boolean canConvert(@Nullable Class<?> sourceType, Class<?> targetType);

	boolean canConvert(@Nullable TypeDescriptor sourceType, TypeDescriptor targetType);
	@Nullable
	<T> T convert(@Nullable Object source, Class<T> targetType);

	@Nullable
	Object convert(@Nullable Object source, @Nullable TypeDescriptor sourceType, TypeDescriptor targetType);

}
```

​	ConversionService对外提供转换服务。

```java
public interface ConfigurableConversionService extends ConversionService, ConverterRegistry {

}
```

​	ConfigurableConversionService同时继承ConversionService和ConverterRegistry，ConverterRegistry用于注册Converter和GenericConverter。

```java
public class GenericConversionService implements ConfigurableConversionService {
...
}
```

​	GenericConversionService实现了ConversionService大部分抽象方法，但是没有注册底层Converter和GenericConverter。

```java
public class DefaultConversionService extends GenericConversionService {
...
}
```

​	DefaultConversionService注册了许多底层Converter和GenericConverter，基本满足转换需求。

#### TypeConvert

​	Bean类型转换的底层接口是TypeConvert。

```java
public interface TypeConverter {

	@Nullable
	<T> T convertIfNecessary(@Nullable Object value, @Nullable Class<T> requiredType) throws TypeMismatchException;

	@Nullable
	<T> T convertIfNecessary(@Nullable Object value, @Nullable Class<T> requiredType,
			@Nullable MethodParameter methodParam) throws TypeMismatchException;

	@Nullable
	<T> T convertIfNecessary(@Nullable Object value, @Nullable Class<T> requiredType, @Nullable Field field)
			throws TypeMismatchException;

	@Nullable
	default <T> T convertIfNecessary(@Nullable Object value, @Nullable Class<T> requiredType,
			@Nullable TypeDescriptor typeDescriptor) throws TypeMismatchException {

		throw new UnsupportedOperationException("TypeDescriptor resolution not supported");
	}

}
```

​	convertIfNecessary方法会将需要类型转换的值进行类型转换。

```java

public abstract class TypeConverterSupport extends PropertyEditorRegistrySupport implements TypeConverter {
	@Nullable
	TypeConverterDelegate typeConverterDelegate;
	
	...
}
```

​	TypeConverterSupport实现了TypeConverter，但是具体的类型转换处理委托给TypeConverterDelegate。并且继承了PropertyEditorRegistrySupport，PropertyEditorRegistrySupport具有注册PropertyEditor的功能，并且还关联了一个ConversionService，使用Converter和GenericConverter统一对外提供转换服务。

```java
public abstract class AbstractPropertyAccessor extends TypeConverterSupport implements ConfigurablePropertyAccessor {
    ...
}
```

​	AbstractPropertyAccessor提供了访问PropertyValue的功能，可以进行PropertyValue设置。

```java
public abstract class AbstractNestablePropertyAccessor extends AbstractPropertyAccessor {	protected AbstractNestablePropertyAccessor(boolean registerDefaultEditors) {
		if (registerDefaultEditors) {
			registerDefaultEditors();
		}
		this.typeConverterDelegate = new TypeConverterDelegate(this);
	}
                                                                                            protected AbstractNestablePropertyAccessor(Object object) {
		registerDefaultEditors();
		setWrappedInstance(object);
	}
                                                                                            public void setWrappedInstance(Object object) {
		setWrappedInstance(object, "", null);
	}
                                                                                            public void setWrappedInstance(Object object, @Nullable String nestedPath, @Nullable Object rootObject) {
		this.wrappedObject = ObjectUtils.unwrapOptional(object);
		Assert.notNull(this.wrappedObject, "Target object must not be null");
		this.nestedPath = (nestedPath != null ? nestedPath : "");
		this.rootObject = (!this.nestedPath.isEmpty() ? rootObject : this.wrappedObject);
		this.nestedPropertyAccessors = null;
		this.typeConverterDelegate = new TypeConverterDelegate(this, this.wrappedObject);
	}
                                                                                         	...
}
```

​	AbstractNestablePropertyAccessor提供了嵌套路径的PropertyValue处理，并且提供了注册默认PropertyEditor，以及创建TypeConverterDelegate实现。

```java
class TypeConverterDelegate {
	private final PropertyEditorRegistrySupport propertyEditorRegistry;
	// 目标Bean
	@Nullable
	private final Object targetObject;
    
    public TypeConverterDelegate(PropertyEditorRegistrySupport propertyEditorRegistry, @Nullable Object targetObject) {
		this.propertyEditorRegistry = propertyEditorRegistry;
		this.targetObject = targetObject;
	}
    
    public <T> T convertIfNecessary(@Nullable String propertyName, @Nullable Object oldValue, @Nullable Object newValue,
			@Nullable Class<T> requiredType, @Nullable TypeDescriptor typeDescriptor) throws IllegalArgumentException {
        // 1. 寻找自定义的PropertyEditor
        // 2. 获取绑定的ConversionService(PropertyEditorRegistrySupport#getConversionService)，如果不为null并且可以转换，则进行类型转换
		// 3. 如果自定义PropertyEditor不存在，且ConversionService可以进行类型转换，则使用ConversionService
        // 4. 如果没使用ConversionService进行类型转换，则使用自定义的PropertyEditor/默认的PropertyEditor进行转换
        // 默认的PropertyEditor在AbstractNestablePropertyAccessor提供注册，如果注册，则从PropertyEditorRegistrySupport#getDefaultEditor获取
        // 5. 如果需要转换为集合类型，则需要另外的处理，因为PropertyEditor不支持对集合中的成员进行类型转换
		...
}
```

```java
public class BeanWrapperImpl extends AbstractNestablePropertyAccessor implements BeanWrapper {
    public BeanWrapperImpl(Object object) {
		super(object);
	}
    
    ...
}
```

BeanWrapper创建过程

```java
BeanWrapper bw = new BeanWrapperImpl(beanInstance);
initBeanWrapper(bw);
```

```java
protected void initBeanWrapper(BeanWrapper bw) {
		bw.setConversionService(getConversionService());
		registerCustomEditors(bw);
}
```

```java
protected void registerCustomEditors(PropertyEditorRegistry registry) {
		if (registry instanceof PropertyEditorRegistrySupport) {
			((PropertyEditorRegistrySupport) registry).useConfigValueEditors();
		}
		if (!this.propertyEditorRegistrars.isEmpty()) {
			for (PropertyEditorRegistrar registrar : this.propertyEditorRegistrars) {
				try {
					registrar.registerCustomEditors(registry);
				}
				catch (BeanCreationException ex) {
					...
				}
			}
		}
		if (!this.customEditors.isEmpty()) {
			this.customEditors.forEach((requiredType, editorClass) ->
					registry.registerCustomEditor(requiredType, BeanUtils.instantiateClass(editorClass)));
		}
	}
```

​	BeanWrapperImpl在创建时

+ 会注册默认PropertyEditor，后续会通过PropertyEditorRegistrySupport#getDefaultEditor会获取默认注册的PropertyEditor
+ 会创建一个TypeConverterDelegate，并以自身作为PropertyEditorRegistrySupport绑定到TypeConverterDelegate

​	在initBeanWrapper时

 +	getConversionService()会将AbstractBeanFactory#conversionService绑定到BeanWrapperImpl
   +	AbstractBeanFactory#conversionService在ApplicationContext启动时，通过查找BeanFactory中名称为ConfigurableApplicationContext#CONVERSION_SERVICE_BEAN_NAME，类型为ConversionService绑定(AbstractApplicationContext#finishBeanFactoryInitialization方法)
 +	registerCustomEditors会调用
   +	PropertyEditorRegistrar的实例集合去添加自定义PropertyEditor(通过CustomEditorConfigurer注册)，或者手动注册
   +	AbstractBeanFactory之前绑定的PropertyEditor注册(通过CustomEditorConfigurer注册

#### 面试题

1.  Spring类型转换实现有哪些

   Spring 3.0之前时PropertyEditor，3.0之后是Converter相关接口

2.  Spring类型转换接口有哪些

   Converter、ConditionalConverter、GenericConverter、ConditionalGenericConverter

   ConvertsionService

3. TypeDesriptor是如何处理泛型的

### 泛型处理

### 事件



