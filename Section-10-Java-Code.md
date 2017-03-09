# Java Code

### Overview
* We don't need an XML anymore
* Annotations still used an XML
* In Annotations, the only thing we had in our applicationContext.xml was enabling context scanning
```xml
<context:component-scan base-package="com.luv2code.springdemo" />
```

### Defining Spring Beans
* We'll create the beans and inject the dependencies in this section

#### Initial Setup
* We're still using spring-demo-annotations from Sections 7-9
* Create a new class SportConfig
  * Add @Configuration to the class
```java
@Configuration
@ComponentScan("com.luv2code.springdemo") // Optional Component scanning
// This works the same way as Component scanning in Annotations 
// Commented out in our example

public class SportConfig {

}
```
* Create a new class SwimCoach.java 
  * Class has a private instance variable for FortuneService
  * And a constructor that takes in a FortuneService
```java
public class SwimCoach implements Coach {

	private FortuneService fortuneService;

	public SwimCoach(FortuneService theFortuneService) {
		fortuneService = theFortuneService;
	}
	
	@Override
	public String getDailyWorkout() {
		return "Swim 1000 meters as a warm up.";
	}

	@Override
	public String getDailyFortune() {
		return fortuneService.getFortune();
	}
}
```
* Create a new implementation of FortuneService interface: sadFortuneService.java
```java
public class SadFortuneService implements FortuneService {

	@Override
	public String getFortune() {
		return "Today is a sad day";
	}
}
```

#### Step 1: Define method to expose bean
* Define a bean in SportConfig.java for our sad fortune service
```java
	@Bean
	public FortuneService sadFortuneService() {
		return new SadFortuneService();
	}
```	
* The method name i.e. sadFortuneService will be the bean id that Spring registers
* We'll use this method name in Step 2

#### Step 2: Inject bean dependencies
* In SportConfig.java, define a bean for the swim coach AND inject dependency
```java
@Bean
public Coach swimCoach() {
  SwimCoach mySwimCoach = new SwimCoach(sadFortuneService());

  return mySwimCoach;
}
```
* We're calling the method sadFortuneService() defined in Step 2 when creating the SwimCoach
* As sadFortuneService was name the bean id in Step 1, the method name swimCoach will be the bean id for the swimCoach
* We'll use swimCoach in step 4

#### Step 3: Read Spring Java configuartion class
* Copy AnnotationDemoApp.java and paste it with name SwimJavaConfigDemoApp.java
* Change the read spring config step to
```java
// read spring config java class
AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext(SportConfig.class);
```
* SpringConfig is the name of the Java Configuration Class we created in Step 1

#### Step 4: Retrieve bean from Spring container
* We're creating a different coach, so we use "swimCoach" instead of "tennisCoach"
```java
// get the bean from spring container
Coach theCoach = context.getBean("swimCoach", Coach.class);
```
* swimCoach is the bean id which was the name of the 

### Injection Values for Properties File

#### Step 1: Create Properties
* Right click src -> new file and use the name sport.properties
* Add these name value pairs to properties to the file
```
foo.email=myeasycoach@luv2code.com
foo.team=Awesome Java Coders
```

#### Step 2: Load Properties file in Spring config
* Add the PropertySource to SportConfig.java
```java
@PropertySource("classpath:sport.properties")
public class SportConfig {
```

#### Step Reference Values from Properties File
* In SwimCoach.java create private instance variables for the email and team
* Add the @Value Annotation (This is Field Injection)
```java
@Value("${foo.email}")
private String email;

@Value("${foo.team}")
private String team;
```
* foo.email and foo.team are the actual property names from sport.properties
* Create getter methods for email and team
```java
public String getEmail() {
	return email;
}

public String getTeam() {
	return team;
}	
```

#### Main.java
* Create a SwimCoach, not a generic coach
	* This is because we want to make use of the new methods getEmail() and getTeam() we just created
	* These methods are not in Coach Interface
```java
SwimCoach theCoach = context.getBean("swimCoach", SwimCoach.class);
```
* Call the new methods
```java
// call our new swim coach methods ... has the props values injected
System.out.println("email: " + theCoach.getEmail());
System.out.println("team: " + theCoach.getTeam());
```
