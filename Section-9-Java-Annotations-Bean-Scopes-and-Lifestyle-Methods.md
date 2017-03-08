# Java Annotations: Bean Scopes and Lifestyle Methods

### Scope Annotation
* Overview is the same as the Overview, Initial Setup, Singleton and Prototype are the same as in Section 6
* In Initial Setup we pass in applicationContext.xml instead of beanScope-applicationContext.xml
* In ProtoType section, instead of changing the scope in beanScope-applicationContext.xml, add the scope to TennisCoach.java
```java
@Component
@Scope("prototype") // @Scope("singleton")
public class TennisCoach implements Coach {
```
* Can also explicitly specify the singleton scope

Prints out two constuctors in prototype, not 1 (as in singleton)

### Bean Lifecycle
* Step 1 is the same as Section 6 (We add methods to TennisCoach.java and change the print lines accordingly)

#### Step 2: 
* Remove the @Scope form TennisCoach.java (Don't have to do it)
* Add the @PostConstruct and @PreDestroy Annotation in TennisCoach.java
```java
// define my init method
@PostConstruct
public void doMyStartupStuff() {
  System.out.println(">> TennisCoach: inside of doMyStartupStuff()");
}

// define my destroy method
@PreDestroy
public void doMyCleanupStuff() {
  System.out.println(">> TennisCoach: inside of doMyCleanupStuff()");
}
```
