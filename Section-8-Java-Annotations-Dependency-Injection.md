# Java Annotations Dependency Injection.md

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
