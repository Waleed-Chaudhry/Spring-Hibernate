# Creating Controllers and Views

#### Initial Setup
* Create a new package inside the src directory called com.luv2code.springdemo.mvc
#### Step 1: Create Controller class
* Create a class called HomeController
* Annotate the class with @Controller
```java
@Controller
public class HomeController {

}
```
* @Controller extends from @Component so Spring will register this as a component 

#### Step 2: Define Controller Method
```java
@RequestMapping("/") //Step 3
public String showPage() {
  return "main-menu"; //Step 4
}
* Can call the method anything you want
```

#### Step 3: Add Request Mapping to Controller Method
* Annotation maps a path to a method
* That's why we could chose any method in Step 2

### Step 4: Return View Name
* We just return the view name
* Spring will use the prefix and suffix behind the scenes to return a view page
* In this case the view page will be: /WEB-INF/view/main-menu.jsp
  * main-menu was the name returned by the view method
  * /WEB-INF/view/ was the prefix
  * .jsp was the suffix

### Step 5: Develop View Page
* Create the page page /WEB-INF/view/main-menu.jsp
  * Right click /WEB-INF/view > New File and name is main-menu.jsp

