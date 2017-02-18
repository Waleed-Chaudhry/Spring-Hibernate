# Dependency Injection

You ask for a car  
The car factory injects the all the dependencies into the car e.g the wheel, tires, windows etc  

Spring has an object Factories. The Spring framework can inject all dependencies of the coach object  

The Spring container has two functions:
* Inversion of Control
* Dependency Injection

**Requirement Defintion:**  
* The coach also has to provide a daily fortune
* But it needs a helper class called HappyFortuneService to do that

### Constructor Injection
**Step 1: Define the dependency interface and class**  
* Create a new interface, FortuneService
* Create a new HappyFortuneService which implements the FortuneService interface
* Add a new method getDailyFortune() to the coach class

**Step 2: Create a constructor in your class for injections**    
* Create the instance of the dependency class in Baseball Coach
```java
// define a private field for the dependency
private FortuneService fortuneService;

// define a constructor for dependency injection
public BaseballCoach(FortuneService theFortuneService) {
  fortuneService = theFortuneService;
}
```
* Use the dependency/helper class's method
```java
	@Override
	public String getDailyFortune() {		
		// use my fortuneService to get a fortune		
		return fortuneService.getFortune();
	}
```

**Step 3: Configure Dependency Injection in Spring config file**    
* Define the dependency in applicationContext.xml
```xml
<bean id="myFortuneService"
  class="com.luv2code.springdemo.HappyFortuneService"> <!--fully qualified class name-->
</bean>
```
* Set up constructor injection: Add this to the bean of the TrackCoach
```xml
<constructor-arg ref="myFortuneService" /> <!--ref matches the id of the dependency-->
```
**Back to Main.java**
* The creation of the coach class remains the same. Spring handles the dependency injection for us
```java
Coach theCoach = context.getBean("myCoach", Coach.class);
```
