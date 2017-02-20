# Inversion of Control

The approach of outsourcing the construction and management of objects to an object factory. 

#### Requirement
* We want the App to get getDailyWorkOut() from BaseballCoah.java
* Two sub requirements:
  1. App should be able to work for a coach in another sport (CricketCoach, BaseballallCoach etc)
  2. The App should be configurable: 

### Initial Setup
* Create a new Package (Right Click src -> new package) 
* Create a class BaseballCoach.java which has getDailyWorkOut() method
* In Main.java (HelloSpringApp.java) create an instance of the class, and call getDailyWork()

### Supporting a coach in another sport
* Create an interface Coach
```java
public interface Coach {
	public String getDailyWorkout();
}
/// The interface doesn't have the implementation of the method
```
* Modify BaseballCoach.java to implement the interface coach
```java
public class BaseballCoach implements Coach {
}
```
* In BaseballCoach.java add the implementation to the method
```java
@Override #to override an interface defined method
public String getDailyWorkout() {
	return "Spend 30 minutes on batting practice";
}
```
* In Main.java we can now create an instance of the class using the name of the interface
```java
Coach coach = new Baseball Coach() //using the name of the interace
```
* We can simply create a Track by modifying Main.java to
```java
Coach coach = new Track Coach()
```
* However the type of the coach (new Track Coach, or new BaseBall Coach) is still hardcoded. We need to make this configurable using Spring

### Lecture 4
Look through the lecture slides for this  

### Lecture 5
Paste the applicationCotext.xml into the src folder. You define your beans in this class
```code
 	<bean id="myCoach"
 		class="com.luv2code.springdemo.TrackCoach">	//Full Class path
```

In your main class  
```java
// load the spring configuration file
		ClassPathXmlApplicationContext context = 
				new ClassPathXmlApplicationContext("applicationContext.xml");
				
		// retrieve bean from spring container
		Coach theCoach = context.getBean("myCoach", Coach.class); //id of the bean, and name of the interface
		
		// call methods on the bean
		System.out.println(theCoach.getDailyWorkout());
				
		// close the context
		context.close();
```
Now the app is configurable using the xml file

### Lecture 7
Why do we specify the Coach interface in getBean()?  //Given that its already been defined in the appllicationContext.xml
```code
Behaves the same as getBean(String), but provides a measure of type safety by throwing a BeanNotOfRequiredTypeException if the bean is not of the required type. This means that ClassCastException can't be thrown on casting the result correctly, as can happen with getBean(String).
```
