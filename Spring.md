# Spring

Spring Framework版本:5.2.2.RELEASE

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

### 模块化设计

Spring-core:核心模块，包括类型转换

Spring-bean:

Spring-context:

Spring-aop:

Spring-tx:

Spring-jdbc:

Spring-test:

Spring-web mvc:

Spring-web flux:

Spring-web:

### 技术整合

#### Java语言特性

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

## Ioc容器

### Spring IoC容器

### 依赖查找

### 依赖注入

### 依赖来源

### Spring IoC容器生命周期

## Bean

### Bean实例

### Bean作用域

### Bean生命周期

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




