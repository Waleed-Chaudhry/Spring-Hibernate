# Java Annotations: Inversion of Control

### Introduction
* Annotations contains meta-data about the class
* We've seen one already: Ovverride
  * At compile time, the compiler checks to make sure that we are in fact overriding the method
* XML configuarion can be verbose. Configuring your Spring beans with Annotations minimizes the XML configuration

### Component Scanning

#### Step 1: Enable component scanning in Spring config file
* Instead of listing down all the beans we can just have one entry
```java
```
* Spring with recursively scan all classes in this package and subpackages
* Identify the components that have the annotation on them
* Will automatically register them with the Spring container

#### Step 2: Add the @Component Annotation to your Java classes 
```java
```
* Spring will register this class as a bean with bean Id "thatSillyCoach"
* We can chose any Id we want

#### Step 3: Retrieve bean from Spring container
* Same as before
```java
```

### Project Setup
