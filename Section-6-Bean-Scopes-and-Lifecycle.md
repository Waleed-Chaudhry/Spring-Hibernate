# Bean Scopes and Lifecycle

### Overview
Read the lecture slides  
Singleton
* You get the same object reference if you create multiple instances of the bean
* Stateless data (default)   
Prototype 
* You get a new object for each request of creating new object
* Stateful data  

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
* Run the App (Insert Image here)

#### Prototype
* Change the scope of myCoach in beanScope-applicationContext.xml
```xml
scope="prototype">	<!-- Add this to the myCoach bean -->
```
* Run the App (Insert second image here)

### Bean Lifecycle

#### Step 1: Define your methods for init and destroy methods
* Add the new methods to TrackCoach.java
```java
	// add an init method
	public void doMyStartupStuff() {
		System.out.println("TrackCoach: inside method doMyStartupStuff");
	}
	
	// add a destroy method
	public void doMyCleanupStuffYoYo() {
		System.out.println("TrackCoach: inside method doMyCleanupStuffYoYo");		
	}
```

#### Step 2: Configure the method names in Spring config file
* Copy beanScope-applicationContext.xml and paste it to beanLifeCycle-applicationContext.xml in your src folder
* Delete the scope="prototype" entry (We can leave it there if we want)
* Add the methods to the myCoach bean in beanLifeCycle-applicationContext.xml
```xml
init-method="doMyStartupStuff"
destroy-method="doMyCleanupStuffYoYo">
<!-- the methods names match up with the defined methods from Step 1, exactly
```

#### Main.java
* Copy BeanScopeDemoApp.java to BeanLifeCycleDemoApp.java
* Change the xml config name
```java
ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("beanLifeCycle-applicationContext.xml");
```
* Delete the print lines for object reference and memory location, and add a method call
```java
System.out.println(theCoach.getDailyWorkout());
```
* Run the App
  * Loads the xml
  * Runs the init method
  * Calls your method
  * Runs the destroy method while closing the context
