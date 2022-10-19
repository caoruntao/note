# JAVA

## Java代码如何执行

### 执行方式

语言执行一般分为 编译 和 翻译。

#### 编译

​		将 源代码 转换成 机器语言，通常是 二进制形式(机器码) 并保存下来(复用)，等待执行。目的是生成 可执行的程序。
​		优点:
​			因为提前编译生成 机器码，所以直接执行 编译后的文件即可，因此速度较快。
​		缺点:
​			源代码编译后只能在该类机器上运行，无法跨平台。

#### 解释

​		在程序运行时，将源代码转换为 机器语言(机器码)，并立即执行。
​		工作模式:
​			1.分析源代码，并且直接执行。
​			2.把源代码翻译成相对更加高效率的中间码，然后立即执行它。
​			3.执行由解释器内部的编译器预编译后保存的代码。
​		优点:
​			跨平台性，因为无需编译，因此只要解释器支持多平台，就有跨平台性。
​		缺点:
​			运行速度慢，解释器要额外的开销。

### Java执行方式

源代码(.java) - javac -> 字节码(.class) - jvm -> 机器码。先通过javac编译为字节码，执行时将字节码解释为机器码。

运行时属于解释执行，为了提高运行效率(程序符合二八原则，20%的代码占用80%的资源)，JVM也提供了编译执行的方式。因此JVM属于混合执行，可通过JVM参数控制。

#### 编译执行机制		

###### JIT(Just In Time)

即时编译。运行时，以方法为单位，将频繁执行的热点代码编译为机器码保存起来(保存到哪？)，编译完成后(编译时还是解释执行，编译和解释执行可以同时工作)，后续调用则直接调用编译完成后的机器码，提高运行效率。

编译器:

C1:

client模式，将由1500次的收集计算出，启动性能好

C2:

server模式，将根据10000次的收集计算出，峰值性能好

C1:C2 数量 = 1:2，先由C1执行后由C2执行。

###### AOT(Ahead-of-Time Compilation)

运行之前，将应用中或JDK中的字节码编译成机器码(与即时编译器区别)

## 基本数据类型

Java引入八大基本数据类型，为了提高程序执行效率和减少内存占用。

| 类型    | 取值 |      |
| ------- | ---- | ---- |
| boolean |      |      |
| byte    |      |      |
| char    |      |      |
| short   |      |      |
| int     |      |      |
| long    |      |      |
| double  |      |      |
| float   |      |      |

boolean在Java规范中取值true或false，在JVM规范中，使用int存储，true存1，false存0，编码规范会约束这个取值。

if(boolean) 会判断boolean是否为0，0就跳过。if(boolean == true)会判断boolean是否为1，不为1就跳过。



	
	lambda
	 	peek:
	 		Consumer，无返回值，因此返回的Stream和之前的Stream一样。但是修改Stream中元素对象的属性，对象还是会发生变化的
	 	map:
	 		Function，有返回值，因此返回的Stream就是你的返回值组成的Stream。同时修改Stream中元素对象的属性，对象也会发生变化的。
	 	flatmap:
	 		将元素铺平(如Array)。如果你想将一个String，分割为一个个字符，但是你又不想接收一个Array<String>，那么你可以用flatmap，该方法会将Array的各个元素取出铺平。
	 		List<String> collect = stringList.stream().flatMap(s -> Arrays.stream(s.split(""))).collect(Collectors.toList());
	 		List<String[]> collect1 = stringList.stream().map(s -> s.split("")).collect(Collectors.toList());
	
	获取类的方法：
		Class.forName()
		类名.class
		实例.getClass()
	
	线程池执行流程：
		先看当前线程数是否小于corePoolSize
			如果小于则新建线程执行该任务。
			如果不小于，则看是否可以加入任务队列
				如果可以加入，就加入到任务队列
				如果不可以加入，则看当前线程数是否小于maximumPoolSize：
					如果小于则新建线程执行任务
					如果不小于，则选择拒绝策略

