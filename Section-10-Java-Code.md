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
* We're creating a different coach, so we use "swimCoach" and SwimCoach.class instead of "tennisCoach" and Coach.class
```java
  // get the bean from spring container
  SwimCoach theCoach = context.getBean("swimCoach", SwimCoach.class);
```
* swimCoach is the bean id which was the name of the 

### Injection Values for Properties File
