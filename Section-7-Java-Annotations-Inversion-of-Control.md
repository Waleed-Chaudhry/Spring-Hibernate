# Java Annotations: Inversion of Control

### Introduction
* Annotations contains meta-data about the class
* We've seen one already: Ovverride
  * At compile time, the compiler checks to make sure that we are in fact overriding the method
* XML configuarion can be verbose. Configuring your Spring beans with Annotations minimizes the XML configuration

### Project Setup
* Create a new Project: spring-demo-annotations
* Copy lib directory from spring-demo-one to spring-demo-annotations
* Add the JARs to the Java Build path
  * Right click the project name
  * Click Java Build Path -> Libraries -> Add JARs -> Select all the JARs -> Click Okay
  * You should see the Referenced Libraries inside the Project Directory
* Copy applicationContext.xml from the previous project to the src folder in the new Project
* Delete all the bean entries
* Right click spring-demo-one project and click close project
* Create a new package (com.luv2code.springdemo)

#### Initial Setup
* Create a coach interface
```java
public interface Coach {

 public String getDailyWorkout();
	
}
```
* Create TennisCoach.java
```java
public class TennisCoach implements Coach {

  @Override
	 public String getDailyWorkout() {
		  return "Practice your backhand volley";
	 }
}
```
* Create Main.java (AnnotationDemoApp.java)

### Component Scanning

#### Step 1: Enable component scanning in Spring config file
* Instead of listing down all the beans we can just have one entry
```xml
<!-- add entry to enable component scanning -->
<context:component-scan base-package="com.luv2code.springdemo" />
<!-- Name of the package, not the project -->
```
* Spring with recursively scan all classes in this package and subpackages
* Identify the components that have the annotation on them
* Will automatically register them with the Spring container

#### Step 2: Add the @Component Annotation to your Java classes 
```java
@Component("thatSillyCoach") //Add this above the public class TennisCoach implements line
```
* Spring will register this class as a bean with bean Id "thatSillyCoach"
* We can chose any Id we want

#### Step 3: Retrieve bean from Spring container
* Happens inside Main.java
* Same as XML Confguration
* getBean uses thatSillyCoach
```java
// read spring config file
ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");

// get the bean from spring container
Coach theCoach = context.getBean("thatSillyCoach", Coach.class);

// call a method on the bean
System.out.println(theCoach.getDailyWorkout());

// close the context
context.close();
```
* Run Main.java

### Default Component Names
* Spring also supports Default Bean IDs
* For TennisCoach.java it will be tennisCoach (class name with the first letter lowercased)

### Step 1: Remove the explicit bean id from TennisCoach.java
```java
@Component //removed ("thatSillyCoach")
```

### Step 2: Change code to use default bean id
* Change the get Bean step in Main.java
```java
// get the bean from spring container
Coach theCoach = context.getBean("tennisCoach", Coach.class); //replaced "thatSillyCoach" with "tennisCoach"
```
* Run Main.java
* If you use a bean id that you haven't defined, you'll see a NoSuchBeanDefinitionException
