# Dependency Injection

If you want to manufacture a new car, you comunicate that request to the factory. The factory then injects the all the dependencies into the car e.g the wheel, tires, windows etc . 

Similarly, Spring has an object factories which can inject all dependencies of the coach object  

#### Requirement Defintion:
* The coach also has to provide a daily fortune
* But it needs a helper class called HappyFortuneService to do that

### Constructor Injection
* Create a constructor Step: Modify the code in the specific coach class (BaseballCoach.java or CricketCoach.java) only
* Configure Dependency Injection Step: Modify the code in applicationContext.xml

Note: You may need to make changes to Main.java

#### Step 1: Define the dependency interface and class
* Create a new interface, FortuneService
* Create a new HappyFortuneService which implements the FortuneService interface
* Add a new empty method getDailyFortune() to Coach interface to force all coaches to implement the method 

#### Step 2: Create a constructor in your class for injections
* Create the instance of the dependency class in BaseballCoach.java
```java
// define a private field for the dependency
private FortuneService fortuneService;

// define a constructor for dependency injection
public BaseballCoach(FortuneService theFortuneService) {
	fortuneService = theFortuneService;
}
```
* Use the dependency/helper class's method in BaseballCoach.java
```java
@Override
public String getDailyFortune() {		
	// use my fortuneService to get a fortune		
	return fortuneService.getFortune();
}
```

#### Step 3: Configure Dependency Injection in Spring config file  
* Define the dependency in applicationContext.xml
```xml
<bean id="myFortuneService"
  	class="com.luv2code.springdemo.HappyFortuneService"> <!--fully qualified class name-->
</bean>
```
* Set up constructor injection: Add this to the bean of the TrackCoach (within the bean tags)
```xml
<constructor-arg ref="myFortuneService" /> <!--ref matches the id of the dependency-->
```

#### Back to Main.java
* HelloSpringApp.java
* Almost everything here (including the creation of the coach class) remains the same as main app in Inversion of Control
* Spring handles the dependency injection for us
* What changes is that we can now call the getDailyFortune() method on our coach
```java
// let's call our new method for fortunes
System.out.println(theCoach.getDailyFortune());
```

### Setter Injection
* Using CricketCoach.java for this
* Port over getDailyWorkout() and getDailyFortune() methods and fortuneService instance variable from BaseballCoach.java

#### Step 1: Create the setter method(s) in your class for injections**  
* Create new no-arg constructor
```java
public CricketCoach() {
	System.out.println("CricketCoach: inside no-arg constructor");
}
```
* Create a setFortuneService method (We don't need a getter method)
```java
public void setFortuneService(FortuneService fortuneService) {
	System.out.println("CricketCoach: inside setter method - setFortuneService");
	this.fortuneService = fortuneService;
}
```

#### Step 2: Configure the dependency injection in Spring config file**  
* Define the dependency in applicationContext.xml (Same as Constructor Injection)
* Set up Setter Injection (Same as Constructor Injection, except that instead of constructor-arg, you have property name)
```xml
<bean id="myCricketCoach"
	class="com.luv2code.springdemo.CricketCoach">
	<!-- set up setter injection -->
	<property name="fortuneService" ref="myFortuneService" /> 
</bean>
```
* property name fortuneService corresponds to setFortuneService method in the class
  * Takes the property name and capitalizes the first letter of the property name
  * prefixes set to it, and calls that method in the class

#### Back to Main.java
* Almost Everything remains the same as Setter Injection (SetterDemoApp.java)
* Difference: We're using CricketCoach class instead of Coach Interface
```java
CricketCoach theCoach = context.getBean("myCricketCoach", CricketCoach.class);
```
* This is simply because the Coach Interface wouldn't have the get or setEmailAddress method we're creating for Injection Literal values
* CricketCoach has all the methods that the Coach Interface has, plus the new getters and setters we will create for Injecting Literal values

### Injecting Literal Values
* For example, adding the team name or email address
* Still part of Setter injection

#### Step 1: Create the setter method(s) in your class for injections
* Create private fields and setter methods for those fields
```java
private String emailAddress;

public void setEmailAddress(String emailAddress) {
	System.out.println("CricketCoach: inside setter method - setEmailAddress");
	this.emailAddress = emailAddress;
}
//Don't need the getter methods for the dependency injection
//However we're still adding them in order to display the values from Main.java
public String getEmailAddress() {
	return emailAddress;
}
```

#### Step 2: Configure the dependency injection in Spring config file
* Define the dependency in applicationContext.xml
* Same as Setter Injection, except instead of ref, you have the actual value
```xml
<!-- inject literal values -->   
<property name="emailAddress" value="thebestcoach@luv2code.com" />
```
* This will call the setEmailAddress method we defined in CricketCoach.java

#### Back to Main.java
* We can now get the literal values we just added
```java
// call our new methods to get the literal values
System.out.println(theCoach.getEmailAddress());
```

### Injecting Values from a Properties file
* The email address thebestcoach@luv2code.com was hardcoded into the applicationContext.xml file
* Instead we want to read the values from a properties file

#### Step 1: Create Properties File
* Create a new file sport.properties in Eclipse (Right Click src -> New -> File)
* Add the value to the file
```
foo.email=myeasycoach@luv2code.com
```
#### Step 2: Load Properties File in Spring config file
* In applicationContext.xml add the properties file before you create your beans
```xml
<!-- load the properties file: sport.properties -->
<context:property-placeholder location="classpath:sport.properties"/>
```

#### Step 3: Reference values from Properties file
* In applicationContext.xml, replace the literal value "thebestcoach@luv2code.com" with "${foo.email}"
* foo.email is the name you chose for the property in sport.properties
```xml
<property name="emailAddress" value="${foo.email}" />
```

#### Back to Main.java 
* Nothing changes here, we just see a different value for the email address as defined in sports.properties
