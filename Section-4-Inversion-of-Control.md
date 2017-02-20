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
* In Main.java (MyApp.java) create an instance of the class, and call getDailyWork()
```java
Coach theCoach = new TrackCoach();
System.out.println(theCoach.getDailyWorkout());	
```

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
* However the type of the coach (new Track Coach, or new BaseBall Coach) is still hardcoded in Main.java. We need to make this configurable using Spring

### Inversion of Control

#### Initial Setup
* Copy applicationContext.xml from spring-core/spring-demo-one/starter-files
* Right click src folder in Eclipse and click paste

#### Step 1: Configure your Spring Beans
* Define a bean in the applicationContext.xml file 
* id is just an alias you can assign (You use this alias in Step 3)
* class is the fully qualified name of the implimentation Java class
```xml
<bean id="myCoach"
	class="com.luv2code.springdemo.TrackCoach">	
</bean>
```

#### Step 2: Create a Spring Container 
* Spring container is generically known as ApplicationContext  
* Has specialized implementations such as 
  * ClassPathXmlApplicationContext (Section 4 and 5)
  * AnnotationConfigApplicationContext
  * GenericWebApplicationContext

##### Coding Steps
* Create a new Main.java (HelloSpringApp.java)
* Application name is the name of the xml config file from Step 1
```java
ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");
```

#### Step 3: Retrieve Beans from Spring Container
* In Main.java retrieve bean from spring container
* "myCoach" maps to the id of the bean
* Coach.class (name of the interface) maps to class of bean
```java
// retrieve bean from spring container
Coach theCoach = context.getBean("myCoach", Coach.class); 
```
* Call methods on the bean and close the context
```java
// call methods on the bean
System.out.println(theCoach.getDailyWorkout());

// close the context
context.close();
```

Now the app is configurable using the xml file

### FAQ
Why do we specify the Coach interface in getBean(), given that the fully qualified class name is being used in applicationContext.xml?
* getBean in Main.java
```java
Coach theCoach = context.getBean("myCoach", Coach.class); 
```
* applicationContext.xml
```xml
<bean id="myCoach"
	class="com.luv2code.springdemo.TrackCoach">	
</bean>
```

* Provides a measure of type safety by throwing a BeanNotOfRequiredTypeException if the bean is not of the required type

