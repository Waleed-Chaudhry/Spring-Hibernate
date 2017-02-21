# Bean Scopes and Lifecycle

### Overview
* Read the lecture slides
Singleton -> Stateless data  
Prototype -> Stateful data  

### Bean Scopes
#### Initial Setup
* Copy the existing Application context, and paste it in src with the name beanScope-applicationContext.xml
* Remove the load properties file, and the bean for myCricketCoach
* Create a new Main.java (BeanScopeDemoApp)
```java
// load the spring configuration file
ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("beanScope-applicationContext.xml");
// We're loading beanScope-applicationContext.xml instead of applicationContext.xml
// Can load muliple xml configs
```

#### Singleton
```java
// retrieve bean from spring container
Coach theCoach = context.getBean("myCoach", Coach.class);

Coach alphaCoach = context.getBean("myCoach", Coach.class);
```
* Check if their object references are the same and that they're pointing pointing to the same memory location
```java
// check if they are the same (same object reference)
boolean result = (theCoach == alphaCoach);

// print out the results
System.out.println("\nPointing to the same object: " + result);

System.out.println("\nMemory location for theCoach: " + theCoach);
System.out.println("\nMemory location for alphaCoach: " + alphaCoach + "\n");

// close the context
context.close();
```
* Insert Image here

#### Prototype
* Change the scope of myCoach in beanScope-applicationContext.xml
```xml
scope="prototype">	<!-- Add this to the myCoach bean -->
```
* Insert second image here
