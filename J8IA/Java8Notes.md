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
		参数			   箭头 				lambda主体
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


	 | Tables        | Are           | Cool  |
| ------------- |:-------------:| -----:|
| col 3 is      | right-aligned | $1600 |
| col 2 is      | centered      |   $12 |
| zebra stripes | are neat      |    $1 |

* 什么是函数式接口？
* 类型判断
