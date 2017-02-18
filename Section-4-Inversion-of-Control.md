# Inversion of Control

Thee approach of outsourcing the construction and management of objects  

### Lecture 2  
Create a new Package -> Right Click src -> new package  

POJO -> Plain old Java Object  
We want to get getDailyWorkOut() from BaseballCoah.java  

Right click package to create new interface or class
MyApp class to create the Baseball Coach

Right click the java class, and click Run as and pick the MainClass  

Interface doesn't have any implementation of the method

public class BaseballCoach implements Coach {
}
Can create an instance of the class in MyApp.java as Coach coach = new Baseball Coach() //using the name of the interace
@Override to override an interface defined method

### Lecture 3
Add a track coach  
Have handled the change coach for another sport using the iterface  
The App isn't configurable. The type of coach is hard coded still  

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
