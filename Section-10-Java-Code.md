# Java Code

### Overview
* We don't need an XML anymore
* Annotations still used an XML

#### Step 1: Create a Java class and annotate as @Configuration
* We're still using spring-demo-annotations from Sections 7-9
* Create a new class SportConfig
* Add @Configuration to the class
```java
@Configuration
@ComponentScan("com.luv2code.springdemo") // Step 2
public class SportConfig {

}
```
#### Step 2: Add component scanning support: @ComponentScan (optional)
* This works the same way as Component scanning in Annotations 

#### Step 3: Read Spring Java configuration class
* Copy AnnotationDemoApp.java and paste it with name JavaConfigDemoApp.java
* Change the read spring config step to
```java
// read spring config java class
AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext(SportConfig.class);
```
* SpringConfig is the name of the Java Configuration Class we created in Step 1

#### Step 4: Retrieve bean from Spring container
* Nothing changes here
* Run the App
* We can verify that we're not using applicationContext.xml
* instead we're using our Java Configuration class, as seen in the print logs
* Only thing we had in our applicationContext.xml was enabling context scanning
```xml
<context:component-scan base-package="com.luv2code.springdemo" />
```

### Defining Spring Beans
* Create a new class SwimCoach.java

#### Step 1: Define method to expose bean
* In our Spring Configuration class SportConfig.java we create an instance of SwimCoach.java
```java
@Bean
public Coach swimCoach() {
  SwimCoach mySwimCoach = new SwimCoach();

  return mySwimCoach;
}
```

#### Step 2: Inject bean dependencies
* In SportConfig.java, we create another bean for the dependency i.e. HappyFortuneService
```java
@Bean
public FortuneService happyFortuneService() {
  return new HappyFortuneService();
}
```
* Edit the creation of the instance of SwimCoach from Step 1 to include the dependency being injected
```java
SwimCoach mySwimCoach = new SwimCoach(sadFortuneService());
```

* The method name i.e. happyFortuneService will be the bean id 

#### Step 3: Read Spring Java configuartion class
* Same as the previous section

#### Step 4: Retrieve bean from Spring container
* Same, instead creating a different coach, "swimCoach" and SwimCoach.class instead of "tennisCoach" and Coach.class
