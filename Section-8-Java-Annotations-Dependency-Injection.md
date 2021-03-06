# Java Annotations: Dependency Injection.md

* Will use the same coach and fortune service example as before. 
* Called Spring AutoWiring
* Spring will look for a class or interface that matches the property and will automatically inject it (autowired)

#### Example
* We need to inject FortuneService into a Coach implementation
* Spring will scan @Components to see if anyone of them (e.g. HappyFortuneService) implements FortuneService Interface
* If so, it will inject them

### Constructor Injection

#### Initial Setup
* Add getDailyFortune method to the interface Coach.java
```java
public String getDailyFortune();
```
* Add an instance variable for the fortune Service to TennisCoach.java
```java
private FortuneService fortuneService;
```
* Add getDailyFortune method to TennisCoach.java
```java
@Override
public String getDailyFortune() {
  return fortuneService.getFortune();
}
```

#### Step 1: Define the dependency interface and class
* Create a new FortuneService.java Interface
```java
public interface FortuneService {

	public String getFortune();
	
}
```
* Create HappyFortuneService.java to implement the FortuneService Interface
```java
@Component //Same as before except we've added the component annotation
public class HappyFortuneService implements FortuneService {

	@Override
	public String getFortune() {
		return "Today is your lucky day!";
	}
}
* The component annotation prompts Spring to register HappyFortuneService.java as a component
```
#### Step 2: Create a constructor in your class for injections

* Add a constructor in the class which gets the dependency injected to it i.e. TennisCoach.java
```java
@Autowired //Step 3
public TennisCoach(FortuneService theFortuneService) {
  fortuneService = theFortuneService;
}
```

#### Step 3: Configure the dependency injection with @Autowired Annotation
* Add the @Autowired annotation above the constructor for TennisCoach.java
```java
@Autowired
```
* Spring will scan @Components to see if anyone of them implements FortuneService Interface
* HappyFortuneService.java does and was declared a component in Step 1, so Spring will inject it

#### Main.java
```java
// call method to get the daily fortune
System.out.println(theCoach.getDailyFortune());
```

#### FAQ: What if there are multiple FortuneService implementations?
* Spring has special support to handle this case using the @Qualifier annotation
* We'll cover that later in the course

#### Notes:
* You need to import springframework libraries for @Autowired and @Component annotations

### Setter Injection

#### Initial Setup
* Comment out the autowired constructor in TennisCoach.java
* Replace it with a default constructor
* We don't need a default constuctor, but we're adding it just to see how Spring works using the print line
```java
// define a default constructor
public TennisCoach() {
	System.out.println(">> TennisCoach: inside default constructor");
}
```

#### Step 1: Create the setter method(s) in your class for injections
* In TennisCoach.java create the setter method
```java
@Autowired //Step 2
public void setFortuneService(FortuneService theFortuneService) {
	System.out.println(">> TennisCoach: setFortuneService() method");
	fortuneService = theFortuneService;
}
```
* This method no longer exists in the final code, since it has been renamed to doSomeCrazyStuff
#### Step 2: Configure the dependency with @Autowired Annotation
* In the previous video, we had autowired annotation in the constructor
* Now we have it on the method 

#### Main.java
* Nothing changes
* Run it -> It creates TennisCoach using the default constructor, and then injects our dependency

#### Inject dependencies by calling ANY method on your class
* The dependency injection doesn't HAVE to happen using a setter method. 
* You can achieve the same effect as described above by renmaing setFortuneService() to doSomeCrazyStuff()
```java
@Autowired
public void doSomeCrazyStuff(FortuneService theFortuneService) {
	System.out.println(">> TennisCoach: inside doSomeCrazyStuff() method");
	fortuneService = theFortuneService;
}
```
* We're also changing the print line to display doSomeCrazyStuff() instead, just to see how Spring works

### Field Injection
* Inject dependencies by setting field values on yur class directly (including private fields)
* Accomplished by using Java Reflection

#### Step 1: Configure the dependency using the @Autowired Annotation
* Applied directly to the field. We don't need setter methods or constructors
* In TennisCoach.java comment out doSomeCrazyStuff()
* Add the @Autowired annotation directly above the private fortuneService instance variable
```java
@Autowired
private FortuneService fortuneService;
```
* Spring will set the field directly behind the scenes, without your having to do any additional work

#### Main.java
* No changes, just run the application

#### Which Injection Should You Use
* Choose a style and stay consistent.
* The functionality is the same across the board for all three injection types

### Qualifiers for Dependency Injection

#### Creating the Exception
What happens if there are muliple implementations of the FortuneService Interface? Which one will Spring choose?
* Create 3 more implementation of FortuneService: HappyFortuneService.java, RandomFortuneService.java and RESTFortuneService
* Make sure you add the @Component to each of the implementations, or Spring won't scan the components
* Make no other changes to TennisCoach.java or Main.java
* Run Main.java
  * We'll get a NoUniqueBeanDefinitionException. Expected single matching bean but found 4
  * The three newly added implementations and HappyFortuneService.java which we already had

#### Fixing the Exception
* We need to tell Spring which bean to use using a Qualifier in TennisCoach.java
```java
@Autowired
@Qualifier("happyFortuneService") #bean id 
private FortuneService fortuneService;
```
* Because we're using the default component name in TennisCoach.java, the bean id is happyFortuneService
* We can change the @Qualifier to use RandomFortuneService.java
```java
@Autowired
@Qualifier("randomFortuneService")
private FortuneService fortuneService;
```
* The @Qualifier can be annotated to all three types on dependency injections
  * However, it can be tricky to use with Constructor Injection
  * See Section 8, lecture 72: Using @Qualifier with Constructors
* You can also use inject values form a properties file using annotations
  * See Section 8, Lecture 73: How to inject properties file using Java annotations
