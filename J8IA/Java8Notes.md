## JAVA8 学习笔记 :computer::computer::computer::computer::computer:
### Part1  
* 什么是Lambda表达式?
> 简洁地表示可传递的匿名函数的一种方式：无名称，有参数列表，函数主体，返回类型，可能还有一个可以抛出的异常列表。
* Lambda有什么好处及应用场景?
	最大的好处: 简明地传递代码，是代码更加清晰灵活。例子：  

	*Java8之前*
	```java 
	  	//我要选所有的绿色苹果
	  	public static List<Apple> filterGreenApples(List<Apple> inventory){
	  		List<Apple> result = new ArrayList<>();
	  		for(Apple apple:inventory){
	  			if("green".equals(apple.getColor())){
	  				result.add(apple);
	  			}
	  		}
	  		return result;
	  	}
	```  
	*Java8之后*  

	```java
	List<Apple> result = filter(inventory,(Apple apple)-> "green".equals(apple.getColor()));
	```	

	真是应用场景：
	1. Comparator排序
	```java
	inventory.sort((Apple a1,Apple a2)-> a1.getWeight().compareTo(a2.getWeight()));
	```
	2. 用Runnable执行代码块
	```java
	Thread t = new Thread(()->System.out.println("Hello World"));
	```
	3. 
	```java
	Button button = new Button("Send");
	   button.setOnAction(new EventHandler<ActionEvent>(){
	   		public void handle(ActionEvent event){
	   			label.setText("Sent!");
	   		}
	   });
	```
* Lambda怎么用？  
```java
	(Apple a1,Apple a2) -> a1.getWeight().compareTo(a2.getWeight());
		参数        箭头 		lambda主体
```

举例:  

使用案例				|Lambda示例														
------------------ | ------------------------------------------------------------- 
布尔表达式			|(List<String> list) -> list.isEmpty()							
创建对象				|()->new Apple(10)												
消费一个对象			|(Apple a)->{ System.out.println(a.getWeight())}				
从一个对象中选择/抽取 |(String s) -> s.length()										
组合两个值			|(int a,int b) -> a * b 										
比较两个对象			|(Apple a1, Apple a2)-> a1.getWeight().compareTo(a2.getWeight())
 

* 什么是函数式编程？  
	> 函数式编程是一种抽象程度很高的编程范式(结构化编程)，纯粹的函数式编程语言编写的函数没有变量，因此，任意一个函数只要输入是确定的，输出就是确定的。
	
	> Lambda表达式实现了函数式编程，实际上就是匿名函数。Lambba表达式可以拥有替换广泛使用的内部匿名类实现回调(callback)功能，用于事件响应。 
	
	>Lambda表达式实现了函数式编程，能够让开发者将程序代码如同数据一样使用。方法可以被当作参数传递到其他方法内，如同对象实例或数。

* 函数式接口是什么?
 
>只定义一个抽象方法的,但是可以有多个非抽象方法的接口。

* 函数式接口的用法 
	1. 函数式接口的抽象方法的签名基本上就是Lambada表达式的签名。
	2. 用 ’@FunctionalInterface‘标注用于表示该接口会设计成一个函数式接口. 
	3. **Sample**：
		
		1.定义
		
		```java
		@FunctionalInterface
		interface GreetingService 
		{
    		void sayMessage(String message);
		}
		``` 
		2. 应用
		
		```java  
		GreetingService greetService1 = message -> System.out.println("Hello " + message);

		```
		[详细链接，内置接口列表](http://www.runoob.com/java/java8-functional-interfaces.html) 
	4. IntPredicate函数式接口：保证输入和输出的时候都是原始类型避免自动装箱的操作
	5. 任何函数接口都不允许抛出受检异常(checked exception).
	[为什么这么说？](http://www.runoob.com/java/java8-functional-interfaces.html)
		* 定义一个自己的函数式接口，并声明受检异常
		* 把Lambda包在一个try/catch块中

* 类型检查 

> Lambda的类型是从使用Lambda的上下文推断出来的。上下文中（比如，接受它传递的方法的参数，或接受它的值得局部变量）中Lambda表达式需要的类型称为**_目标类型_**。


* 流(stream)介绍
	> 流是一系列数据项，不是一种数据结构，它允许你以声明性的方式处理数据集合。暂且可以理解为一种遍历数据集的高级迭代器。官方定义是从支持数据处理操作的源生成的元素序列。流可以进行相关的算法和计算，只是它并没有显示地表现，而是在内部进行隐式地操作。
	
	* 有关流的名词 
		 * 源。流会使用一个提供数据的源，如集合，数组或输入/输出资源。有序集合生成流时会顺序不变。
		 * 数据处理操作-类似数据库CRUD，以及函数式编程语言中的常用操作。filter,map,reduce,find,match,sort.
		 * 流水线 很多操作本身会返回一个流。这样多个操作可以链接起来，形成一个大的流水线。
		 	
	* 流的特点
		1. 只能遍历一次。遍历完之后，我们就说这个流被消费掉了。
		
		```java
		List<String> title = Arrays.asList("Java8","In","Action");
		Stream<String> s = title.stream();
		s.forEach(System.out::println);
		s.forEach(System.out::println);//流已经被操作或关闭。
		```
		
		2. 采用内部迭代方式。
		Stream库使用内部迭代。帮使用者完成了迭代，并且把得到的流值用在了某个地方。
		
		for-each循环外部迭代/显示迭代
		```java 
		List<String> names = new ArrayList<>();
		for(Dish d: menu){
			names.add
		}
		```
		
		用背后的迭代器做背后迭代/显示迭代
		
		```java
		List<String> names = new ArrayList<>();
		Iterator<String> iterator = menu.iterator();
		while(iterator.hasNext()){
			Dish d = iterator.next();
			names.add(d.getName());
		}
		```
		
		流/内部迭代
		
		```java
		List<String> names = menu.stream().map(Dish::getName).collect(toList());
		```
* 流的使用
	* 筛选  

	
		```java
		filter
		List<Dish> vegetarianMenu = menu.stream().filter(Dish::isVegetarian).collect(toList()); 
		检查菜肴是否适合素食者。
		```
	* 去重	
	
		```java
		distinct
		List<Integer> numbers = Arrays.asList(1,2,1,3,3,2,4);
		numbers.stream().filter(i -> i % 2 ==0).distinct().forEach(System.out::println);
		
		```
	* 切片	 

	```java
	
	List<Dish> dishes = menu.stream().filter(d -> d.getCalories() > 300).limit(3).collect(toList());
	
	  符合filter内条件的头三个元素
	```
	
		
	* 跳过元素 
	
	```java	
	List<Dish> dishes = menu.stream().(d->d.getCalories() > 300).skip(2).collect(toList()); 
	
	返回一个扔掉了前n个元素的流。如果流中元素不足n个，则返回一个空流。limit(n)和skip(n)是互补的

	```	 
	
	* 映射
	
	```java
	map方法会接受一个函数作为参数。这个函数会被应用到每个元素上，并将其映射成一个新的元素(创建新版本)
	
	List<String> dishNames = menu.stream().map(Dish::getName).collect(toList());
	List<String> words = Arrays.asList("Java 8", "Lambdas", "In", "Action");
	List<Integer> wordLengths = words.stream().map(String::length).collect(toList());
	List<Integer> dishNameLengths = menu.stream().map(Dish::getName).map(String::length).collect(toList());
	```
	
	```java
	流的扁平化
	List<String> uniqueCharacters = word.stream().map(w->w.split("")).flatMap(Arrays::stream).distinct().collect(Collectors.toList());
	```
	
	* 查找和匹配
		
		* 匹配
		
		```java
			匹配一个元素
			boolean flag = menu.stream().anyMatch(Dish::isVegetarian);
		```
		
		```java
			匹配所有元素
			boolean isHealthy = menu.stream().allMatch(d -> d.getCalories() < 1000);
		```
		
		```java
			没有任何匹配
			boolean isHealthy = menu.stream().noneMatch(d -> d.getCalories() >= 1000);
		```
		
		短路操作， && 和 || 运算符在流中的版本。
	
	
	
	
		

### Appendix

* 终端操作

操作|目的
:-: | :-: 
forEach|消费流中的每个元素并对其应用Lamda.这一操作返回void
count|返回流中元素个数.这一操作返回long
collect|把流规约成一个集合，比如List,Map甚至是Integer.

