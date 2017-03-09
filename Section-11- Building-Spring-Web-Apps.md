# Building Spring Web Apps

### Spring MVC Overview

* Framework for building web applications in Java
* Model View Controller (MVC) Design Pattern
* Levereages features of Core Spring Framework (IoC, DI)

### Spring MVC Configuration

* Change your Eclipse perspective
  * Window > Perspective > Open Perspective > Jave EE
* Create a new Project
  * File > New > Dyanmic Web Project
  * Choose the name spring-mvc-demo
* Download the latest version of Spring
  * Go to https://repo.spring.io/release/org/springframework/spring/
  * Pick a version thats at least 4.3 or higher
  * Download the first .zip file
  * Extract the zip
* Copy over the Spring JARs
  * Copy all the .far files from the extracted zip/libs
  * And paste it to WebContent/WEB-INF/lib
  * Automatically on the build path
* Copy over the Spring starter JARs from source code
  * Go to spring-mvc/starter-files/spring-mvc-demo/lib
  * Copy the 3 jar files ands paste them to WebContent/WEB-INF/lib
* Copy over the starter configs from the course code
  * Go to spring-mvc/starter-files/spring-mvc-demo/config
  * Copy the two .xml files and paste them to WebContent/WEB-INF
* web.xml has the first two steps added to the code already
  * The servlet-name in Step 1 and 2 needs to be the same
* spring-mvc-demo-servlet.xml has steps 3-5 added to it already
 * In Step 3 we have this
```xml
<context:component-scan base-package="com.luv2code.springdemo" />
```
 * What Spring will do is recursively scan for components starting at the base package: "com.luv2code.springdemo"
 * Since our component is defined in com.luv2code.springdemo.mvc, it will work
 * In spring-mvc-demo-servlet.xml, prefix and suffix have already been setup
```xml
<property name="prefix" value="/WEB-INF/view/" />
<property name="suffix" value=".jsp" />
```
  * Final path of the view page: prefix + view name + suffix = /WEB-INF/view/ + show-student-list + .jsp
  * i.e. /WEB-INF/view/show-student-list.jsp
* Create the view folder
  * Right click WebContent/WEB-INF -> New Folder and name it main-menu.jsp'
```html
<!DOCTYPE html>
<html>

<body>

<h2>Spring MVC Demo - Home Page</h2>

</body>

</html>
```

We can configure the Spring Dispatcher Servlet using all Java Code using the documentation at:   http://docs.spring.io/spring/docs/current/spring-framework-reference/html/mvc.html#mvc-container-config

#### Running the App
Right click project name > Run As > Run As Server

### FAQs
* Lecture 101: Restarting Tomcat in case the Spring MVC Controller is not working
* Lecture 102: Stop Tomcat running in case of Ports are in Use Error

### Reading HTML Form Data
* We'll submit a Query using a jsp page, and Spring will return some value based on the Query
* Name of student

We'll need the controller to do two things
* Create 
Add the steps to this page as well
