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
* 类型判断



### Appendix

* 终端操作

操作|目的
:-: | :-: 
forEach|消费流中的每个元素并对其应用Lamda.这一操作返回void
count|返回流中元素个数.这一操作返回long
collect|把流规约成一个集合，比如List,Map甚至是Integer.

