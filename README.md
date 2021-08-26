# note
JAVA:
	跨平台:
		JAVA:源代码(.java) - javac -> 字节码(.class) - jvm -> 机器码。应该算编译和解释混合。
		
		编译器:
			将 源代码 转换成 机器语言，通常是 二进制形式(机器码) 并保存下来(复用)，等待执行。目的是生成 可执行的程序。
			优点:
				因为提前编译生成 机器码，所以直接执行 编译后的文件即可，因此速度较快。
			缺点:
				源代码编译后只能在该类机器上运行，无法跨平台。
		解释器:
			在程序运行时，将源代码转换为 机器语言(机器码)，并立即执行。
			工作模式:
				1.分析源代码，并且直接执行。
				2.把源代码翻译成相对更加高效率的中间码，然后立即执行它。
				3.执行由解释器内部的编译器预编译后保存的代码。
			优点:
				跨平台性，因为无需编译，因此只要解释器支持多平台，就有跨平台性。
			缺点:
				运行速度慢，解释器要额外的开销。

		为了提高运行效率，JAVA也提供了 直接编译为机器码的 机制。
			JIT(Just In Time): 即时编译器
				运行时，将热点代码的字节码 提前编译为机器码并保存下来，后续直接调用机器码，而无需解释执行，提高程序运行效率。
					热点代码:
						运行时，当某一方法调用次数达到即时编译定义的阈值时，可以将该方法认为 热点代码。
						C1编译器，client模式将由1500次的收集计算出，启动性能好
						C2编译器，server模式，将根据10000次的收集计算出，峰值性能好
			AOT(Ahead-of-Time Compilation):
				运行之前，将应用中或JDK中的字节码编译成机器码(与即时编译器有区别)

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