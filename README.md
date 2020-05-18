# Spring Boot To-Do Web Application



## Getting Started
### Step 1: Generate our Spring Boot App
 1. Let's start off by going to start.spring.io to generate our project! 
    <br>
    <details>
    <summary> <i> Difference between <b>group</b> and <b>artifact</b> when generating a Spring Boot Maven project? </i> </summary>
  
    `groupID`

    - This element indicates the unique identifier of the organization or group that created the project. The `groupID` is one of the key identifiers of a project and is typically based on the fully qualified domain name of your organization. For exmaple *org.apache.maven.plugins* is the designated `groupID` for all Maven plugins. 

    `artifactID`
    - This element indicates the unique base name of the primary artifact being generated by this project. The primary artifact for a project is typically a JAR file. *A JAR file stands for Java ARchive. It's a file format based on the popular ZIP file format and is used for aggregating many files into one. This way, the .class files, images, and sounds can be downloaded to a browser in a single HTTP transaction.*  Secondary artifacts like source bundles also use the artifactId as part of their final name. A typical artifact produced by Maven would have the form `-` For example `myapp-1.0.jar`
    So along with a version its a way to uniquely identify the artifact in maven. 
    Each and every artifact is stored in repository, the path to the artifact in the repository has a lauout in compliance with group, artifact and version.
      - groupId     = com.example
      - artifactId  = myservice
      - version     = 1.0
      Then in the repository you can expect to see the following directory layout: 
      `com/example/myservice/1.0/myservice-1.0.jar`
     </details>
    <br>
    
    - Project: Maven 
    - Springboot: 2.2.7
    - Our **Group** will be `com.ps.springboot.web`
    - Our **Artifact** will be `spring-boot-first-web-application`
    - Packaging: JAR
    - Java: 8
    - Dependencies: `Spring Web`, `Spring Boot Dev Tools`
    <details>
    <summary> Screenshot of the steps above </summary>
    <image src="assets/step-1.png">

    </details>
    <br>

    **Go ahead, you are now ready to generate your project!** 
    **It will create a zip file which we will then extract from our downloads folder and move into our desktop for now.**
    <br>

    <details> 
    
    <summary> Quick recap of what we have done </summary>
    We created a simple Maven project with Spring Boot. We also added a couple of dependencies, Spring Web, and Spring Boot DevTools. And, we have given a groupId and artifactId.springboot initializer. We then generated our project and we then took that zip file and and extracted it into our Desktop for now. 
    </details>
    <br>
    
 2. Launch up an Eclipse workspace and import the project that we have downloaded just now. 
    - Create a workspace directory path `SpringBootWebApplication[CurrentMonth][Year]` and then `Launch`
      <details>
      <summary> Screenshot of directory created </summary>
          <br>
          <b>Note:</b> Remember an Eclipse workspace is kind of the place where you would store all your projects. You can use any folder on your hard disk as your workspace folder.
          <br>
          <br>
          <image src="assets/eclipse-workspace-directory.png">
      </details>
    - Let's now import our project that we created in start.spring.io . Go to `File` > `Import` > `Existing Maven Projects`. Click `Next` now. 
    - Now we have to choose the folder where the prioject is on the hard desk by `Browse`. For now, it should be in our Desktop. You can click `Finish` once you located it. 
    
      <details>
      <summary> It should look similar to this</summary>
      <image src="assets/final-import-springboot-maven-app.png">
      </details>
    - Go to `src/main/java` and double click to open `SpringBootFirstWebApplication.java` file. `Run As` > `Java Application`
      <details>
      <summary> Screenshot for running java application</summary>
      <image src="assets/run-java-application-step-1-final.png">
      The log will let you know once your SpringBoot application in launched identical to the photo above. 
      </details>
    <br>

    <details>
    <summary> <i> What are the most important project files?</i></summary>
    The 3 main important files to note once you have imported your project is:
    <ul> 
    <li>
    
    `src/main/java` > `com.[groupId]` > `[artifactId].java`
    </li>
    <li> 

      `src/main/resources`   >  `application.properties`
    </li>
    <li>

    `pom.xml`
    </li>
    </ul>
    <br> 

    #### pom.xml
    An important section inside of the `pom.xml` is `<parent>`. `pom` stands for Project Object Model where we describe the characteristics of the project. Here we are using springboot startup parent. Parent is very similar to inheritance in Java. Just like we use inheritance to inherit from one class to another. You can also find the groupId and artifactId with the name we configured in the spring initializer.  Typically in web application we would use the packaging <b> War AKA Web Archive </b> because of some spring magic which we will look into a little later, we are putting a packaging of <b> Jar </b>.

    The next important thing that you will find in the `pom.xml` are the dependencies. There are 3 important dependencies in here. 
    - Spring Boot Web: Starter for developing web applications or RESTful services 
    - Spring Boot Dev Tools: Brings in features which makes developing applications very producti ve. 
    - Spring Boot Starter Test: Helps us to write good unit test and integration testing. 
    <br>

    The `<build>` > `<plugins>` like `spring-boot-maven-plugin` helps us run the application and also it has facilities to create a jar files and war files. 

    #### [artifactId].java
    You will find a simple Spring Boot application annotation and inside the main method which has a `SpringApplication.run()` on the specific class which launches a Spring Boot Application. `@SpringBootApplication` does two things. It initializes Spring (Component Scan) and Spring Boot (Auto Configuration) framework. 

    When you `Run As` > `Java Application` it will launch up a complete SpringBoot application with the server. In the log, you will see that SpringBoot application is launched up in __ seconds and it is on default port 8080. We haven't written any code yet so there is no url that we can work on. 

    #### application.properties
    This can be used as a configuration file. Note that it currently doesn't have any values in there. Let's say you want to run the application not on 8080 but 9000- well we can put a specific property value in here with value as 9000 and then the SpringBoot application will run there. 

    </details>
    <br>


### Step 2: Create LoginController and render "Hello World"
Let's go to http://localhost:8080/login and notice that we get <b> White Label Error Page </b>.Because we have not created the url, SpringBoot provides this default error page. 

<u>Let's brainstorm</u>
We'd like the url /login to render a page. 
/login <b>⇢</b> "Hello World"

We would need to map slash login to a Java class
/login <b>⇢</b> LoginController 

1. Inside of Eclipse command⌘ N, create `Class`, click `Next`
    - Name: `LoginController`
    - Package: `com.ps.springboot.web.springbootfirstwebapplication.controller`
      <details>
      <summary>Screenshot of LoginController </summary>
      <image src="assets/create-login-controller.png">
      </details>
    - Open your `LoginController` file
    <b>Note:</b> You will notice that your server has restarted automatically. This is part of Spring Boot DevTools magic! 
    - Create a method inside of LoginController class that returns "Hello World"
      <details>
      <summary>loginMessage method </summary>

      ```java 
      public String loginMessage() {
		      return "Hello World";
    	  }
      ```
      </details>
    - Now we need to map /login to this method ... 
      The way we would map that is through an annotation called `@RequestMapping`.
      Above the loginMessage method, add `@RequestMapping` and command⌘ 1 (this will bring up an Eclipse suggestion to import the package), click `Import 'RequestMapping'`. Add `"/login"` inside the parenthesis of the annotation. You should now see the following:
      <details>
      <summary>Include Request Mapping </summary>

      ```java 
        package com.ps.springboot.web.controller;

        import org.springframework.web.bind.annotation.RequestMapping;

        public class LoginController {
          @RequestMapping("/login")
          public String loginMessage() {
            return "Hello World";
          }
          
        }

      ```
      </details>
    - Now we need to get this class to be picked up by spring in order for the url to work properly. We will do that by adding an annotation to create a controller. In line 5, above your class, type `@Controller` followed by command⌘ 1, and proceed with importing it. 
      <details>
      <summary> Include Controller </summary>

      ```java 
      package com.ps.springboot.web.controller;

      import org.springframework.stereotype.Controller;
      import org.springframework.web.bind.annotation.RequestMapping;

      @Controller
      public class LoginController {
        
        @RequestMapping("/login")
        public String loginMessage() {
          return "Hello World";
        }
        
      }

      ```
      </details> 
  2. In `src/main/resources/application.properties` we will add a simple property. 
      <details>
      <summary> Code snippet </summary>

      ```java 
        
        logging.level.org.springframework.web=DEBUG

      ```
        `org.springframework.web` is the package where the spring MVC logic is present. Only for this package alone we will change the login to debug. We will do this inside of `application.properties`. 
      </details> 
  3. We'd like the dispatcher servlet to go and return whatever value I am giving it back (ie. "Hello World") and display it in the browser. We will add `@ResponseBody` below `@RequestMapping`, command⌘ 1 to import `import org.springframework.web.bind.annotation.RequestMapping;
`


  4. Refresh your http://localhost:8080/login page and you should now see <b>"Hello World" </b>

### Step 3: Render HTML page

<details>
<summary><i> Let's recap and brainstorm what we are going to do next </i></summary>

Until now we have a simple controller called LoginController which has a method called loginMessage and is returning and displaying it onto the screen. 
<br>
What we want now is a View. One of the things Java is good at writing business logic. So if you want to write business logic or if you want to have some controller logic then Java is the right place! But if you want to do some html stuff- if you want to create some html containing the view information then Java is not the right place. All that kind of logic should be in a view (ie. jsp pages or some of the templating language). We are going to use JSP to render the view. 
<br>
So what are we going to do?
Well we are going to create a JSP and we'll jhave the JSP render the view. 
</details>
<br>


1. Inside of `src/main`, right click > `New` > `Folder` > `webapp`. Inside `webapp` folder, create a new folder `WEB-INF`. Right click `WEB-INF` and create a new folder called `jsp`. Our new file `login.jsp` will go inside `jsp`. 
    <details>
    <summary> Screenshot of new folder structure</summary>
    <image src="assets/step3-create-login-jsp.png">
    </details> 
2. We can not put our html content inside `login.jsp`. 
    <details>
    <summary>Login.jsp HTML Code Snippet </summary>

    ```html
    <html>
      <head>
       <title>First Web Application</title>
      </head>
      <body>
        <h2> My first JSP! </h2>
      </body>
    </html>
    
    ```
    </details>

3. Now we want to redirect and map our `loginMesage` method to `login.jsp`. 
    - Replace  `return "Hello World"` inside of loginMessage method to `return "login" `
    - In `application.properties` :
      <details>
      <summary> Add the following code snippet </summary>

      ```java 
        
      spring.mvc.view.prefix: /WEB-INF/jsp/
      spring.mvc.view.suffix: .jsp


      ```
      When you send in login it becomes `/WEB-INF/jsp/login.jsp.`
      </details> 
    - To enable jsp support in embedded tomcat server, go inside `pom.xml file`,
      <details>
      <summary> Add code snipped above dev tools dependency</summary>

      ```java

      <dependency>
          <groupId>org.apache.tomcat.embed</groupId>
          <artifactId>tomcat-embed-jasper</artifactId>
          <scope>provided</scope>
      </dependency>

      ```
      
      </details>
    - In this kind of situation, we will need to restart our server by Terminating it
      <details>
      <summary>Screenshot to Terminate server </summary>
       <image src="assets/terminate-server.png">
      </details>
    - Remove `@ResponseBody` in `LoginController` and open your http://localhost:8080/login page, <b>TA DA!</b>
    
### Step 4: Create our first GET parameter

<details>
<summary><i>Next steps</i> </summary>

We'd like to add a name GET parameter `login?name=yourname` into our url http://localhost:8080/login?name=yourname . How do we the the name parameter and send it in the response? 

Before we send the GET parameter to jsp, the first thing we would need to know is how do we get it to the controller? 

GET Request <b>⇢</b> Controller <b>⇢</b> View
</details>
<br>

1. Inside of our `LoginController` file, we are going to make an annotation call `@RequestParam` in the `loginMessage` method, insert it inside of `loginMessage(@RequestParam)` and remember to command⌘ 1 to import the framework. 
    - Include `String name` after out `@RequestParam` call
      <details>
      <summary> Code snippet </summary>

      ```java
      package com.ps.springboot.web.springbootfirstwebapplication.controller;

      import org.springframework.stereotype.Controller;
      import org.springframework.web.bind.annotation.RequestMapping;
      import org.springframework.web.bind.annotation.RequestParam;

      @Controller
      public class LoginController {
        @RequestMapping("/login")
        public String loginMessage(@RequestParam String name) {
              return "login";
          }
      }

      ```
      </details>
    - Above `return "login"` in our `loginMessage` method, add `System.out.println("name: " + name);`
    - Save your file, go to http://localhost:8080/login?name=yourname and refresh your page. You should now see something identtical to mine in your log: 
      <details>
      <summary> Screenshot of log </summary>

       <image src="assets/console-name.png">
      </details> 
2. Now how do we make it available to the View. <b> Model </b> is used to pass data from <b>Controller</b> to <b>View</b>, in this case it would be our `login.jsp`. 
    <details>
    <summary><b>Note:</b>  </summary>

    These three part Model View and Controller combined create the MVC pattern. 
    The <b>Controller</b> controls the entire flow. Once it has some data it puts it in the <b>Model</b>, redirects it to the <b> View</b>. The <b>View</b> uses the <b>Model</b> to render the data on the screen. 
    </details> 

    - We need to pass the `ModelMap model` into our `loginMessage` method and import `import org.springframework.ui.ModelMap;` outside of our class. We will then add `model.put("name",name);` inside our method
      <details>
      <summary> Code Snippet </summary>

        ```java

        package com.ps.springboot.web.springbootfirstwebapplication.controller;

        import org.springframework.stereotype.Controller;
        import org.springframework.ui.ModelMap; // import ModelMap
        import org.springframework.web.bind.annotation.RequestMapping;
        import org.springframework.web.bind.annotation.RequestParam;

        @Controller
        public class LoginController {
          
          @RequestMapping("/login")
          public String loginMessage(@RequestParam String name, ModelMap model) {
              	model.put("name", name); // putting attribute "name" and value will be name
                return "login";
            }
        }

        ```

      </details>
  3. So now `name` is available in our login.jsp file. But in order to access it, we are going to use something called expression language `${}`. Add `Welcome ${name}` in our heading tag. <b>Refresh your page now.</b>
  

  <b> Exercise: </b> Create a new method try and map a url to it. Try and create a <b>View</b> and send a value to it. 

<details>
<summary> <b><i>MVC Request Flow Information </i> </b> </summary>

One of the important things with Spring MVC is that we have a front controller called <b>DispatcherServlet</b>. In the sense that any request that comes to the web application will first go to the <b>DispatcherServlet</b>. The  <b>DispatcherServlet</b> then searches what are the mappings available. It would know that there is a login controller that was created, with a method can handle this request `/login`. 

- DispatcherServlet receives HTTP Request.
- DispatcherServlet identifies the right Controller based on the URL.
- Controller executes Business Logic (we have not added any yet)
  - It would then be put inside the Model 
- Controller returns a) Model b)View <b>name</b> back to DispatcherServlet.
- DispatcherServlet identifies the correct view (ViewResolver- in charge of looking at `application.properties` for configuration for prefix and suffix)
- DispatcherServlet makes the model available to view and executes it.
- DispatcherServlet returns HTTP response back. 

<image src="https://docs.spring.io/spring-framework/docs/2.0.8/reference/images/mvc.png">

</details>


### Step 5: HTML Form

1. Let's add a form into our HTML page, you can remove the `<h2>` tag from the body. 
    <details>
    <summary> Form </summary>

      ```html

      <body>
        
        <form>
          Name: <input type="text" name="name" /> 
          <input type="submit" />
        </form>
          
      </body>
      ```
    </details>
2. In our `LoginController` file, we will remove `@RequestParam String name` because we are not going to use it now. You can comment out `model.put()`. (All the loginMessage does is now redirects to the login page where we have our Name and submit button)
    <details>
    <summary> Code Snippet</summary>

    ```java

    @RequestMapping("/login")
    public String loginMessage( ModelMap model) {
      //model.put("name", name); 
      return "login";
    }
    ```
    </details> 

3. Add a `Password` input tag with an attribute of `type="password"` and as `name="password"` above the submit button to our form in `login.jsp`
    - Go to http://localhost:8080/login and type in a password. Notice that our GET method is not secure because it displays the password input we entered. 
      <details>
      <summary> Why does it do this?</summary>

        The way the internet works is there are a number of hubs between your browser and the server where your application is deployed. It's not direct connection between a browser and your server. The request goes through a number of intermediate routers. If you have data in your URL, routers can see that information and that's not really good. I mean, you could kind of get over it by using HTP's, but even that's not a perfect solution. 
        
        Sending data out in a GET request is not really a secure way of doing it. The ideal way would be to send data in a POST request. 
      
      </details>

    - Add an attribute `method="post"` in the form tag. It is now being sent as part of the body of our request as form parameters. 
      <details>
      <summary> Current request method </summary>


        Looking at our response from  `Chrome DevTools` > `Network` > `Response`. With GET or POST it is given us back the same html page. Until now we have not specified a request method in our `LoginController`. When you don't specify a request method in `@RequestMapping`, this will then be used for all the requests (GET, POST, PUT, etc.) and the same method will be used. So how do we avoid that? 

      </details>
4. In our `LoginController` file, let's update `@RequestMapping` by adding a new paramaeter. We will update `value="/login` and add `method = RequestMethod.GET ` 
    <details>
    <summary>Updated LoginController code snippet </summary>

    ```java
    package com.ps.springboot.web.springbootfirstwebapplication.controller;

    import org.springframework.stereotype.Controller;
    import org.springframework.ui.ModelMap; 
    import org.springframework.web.bind.annotation.RequestMapping;
    import org.springframework.web.bind.annotation.RequestMethod;

    @Controller
    public class LoginController {
      @RequestMapping(value="/login", method = RequestMethod.GET) 
      public String loginMessage(ModelMap model) {
    //		model.put("name", name);
        return "login";
        }
    }
  
    ```
    
    </details>
    <details>
    <summary> Whitelabel Error Page </summary>

    Notice after refreshing our page and inserting a `Name` and `Password`, we get a <b>Whitelabel Error Page</b> indicating our <b>Request method "POST" not supported. </b>. Inside of our Google DevTools, our Status is a 405 POST method.  

    We don't have a method to support the `POST` and that's the reason why it's causing a problem.
    </details>

5. We are going to add a method to support our password `POST`.
    - Update method name `loginMessage` to `showLoginPage`
    - Create a new method, identical to the method above called `showWelcomePage`. The difference will be`@RequestMapping` parameter will be `method = RequestMethod.POST`. And it will `return "welcome"`
      <details>
      <summary> <b>showWelcomePage</b> code snippet </summary>

      ```java
      @RequestMapping(value="/login", method=RequestMethod.POST) 

      public String showWelcomePage(ModelMap model) {
        return "welcome"; // we will create a welcome page
      }
      ```

      </details>

    - In `../WEB-INF/jsp/`, we will create a `welcome.jsp` file. Add your html template. In the `body`, add `<h1>Welcome!</h1>`


6. What we want do now is pick up the value from the request. Let's start with picking up the value of the name. So we can then display it in our `Welcome` page. 
    - Add and import `@RequestParam` inside the method parameter with a type `String` and name `name`
    - Add `model.put("name", name)` in the body of our `showWelcomePage` method
    - In `welcome.jsp`, add `${name}` to the heading tag


### Step 6: Add hard-coded validation of userId and password

1. Add another request param `@RequestParam String password`in `showWelcomePage` method. 
    - Inside of our `showWelcomePage` method, add `method.put("password", password)`
      <details>
      <summary> updated <b>showWelcomePage</b> code snippet </summary>

      ```java
      @RequestMapping(value="/login", method=RequestMethod.POST) 
      public String showWelcomePage(ModelMap model, @RequestParam String name, @RequestParam String password) {
        model.put("name",name);
        model.put("password",password);
        return "welcome";
        }
      ```
      </details>
    - Let's make sure our password is coming through. Go to `welcome.jsp` page and add `${password}` in our `body` tag. 
    <details>
    <summary> Next steps  </summary>

    Now let's add a bit of validation to our password

    If a user is entering a wrong `user id` and `password`, we will want to send them back to the `log in` page saying <i>Incorrect user ID or password. Type the correct user ID and password, and try again</i>

    We'll create a log in service which would be able to validate the things for us. 
    </details>
2. Create a class and add this line of code `loginService service;` inside of our `LoginController` class before our methods. `command⌘ 1`, click `Create class loginService`. 

    - Before `loginService service`, add import `@Autowired`

    <details>
    <summary> <b>LoginController</b> code snippet </summary>

    ```java
    import org.springframework.beans.factory.annotation.Autowired;
    import org.springframework.stereotype.Controller;

    import com.ps.springboot.web.springbootfirstwebapplication.service.loginService;

    @Controller
    public class LoginController {
      @Autowired
      loginService service;

      <!-- rest of code -->
    }
    ```
    </details>

    <details>
    <summary> Screenshot loginService class </summary>

    <image src="assets/create-login-service-class.png">
    </details>
    

3. Create a boolean method inside of `loginService` class file. It will pass `String userid, String password`
    - Our method will need some logic. So let our `userid` be your name, and add a `password`. 
    - Add `@Component` above our class
    <details>
    <summary> <b>loginService</b> code snippet </summary>


    ```java
    package com.ps.springboot.web.springbootfirstwebapplication.service;

    public class loginService {

      public boolean validateUser(String userid, String password) {
        return userid.equalsIgnoreCase("yourname") && password.equalsIgnoreCase("test");
      }
    }
    ```
    </details>
4. In our `showWelcomePage` method inside our `LoginController` class. Add `service.validateUser(name, password);` in a boolean variable called `isValidUser`
    - In the following line, add an `if statement` whether `isValidUser` is not valid, send them back to the login page. 
    <details>
    <summary> <b>isValidUser</b> code snippet </summary>

    ```java
      boolean isValidUser =  service.validateUser(name, password);

	  if(!isValidUser) {

        return "login";
      }
         
    ```
    </details>
    <br>
    <b> Now check out your website. Log in with the right credentials. You should now see your welcome page display. But now let's go back and refresh the url. Insert another userid and password and notice that the page refreshes back to itself.  </b>
5. In our conditional `if statement` inside of `showWelcomePage` method. Add `model.put("errorMessage", "Invalid Credentials");`
6. Go to  `login.jsp`, above the form tag, add `<font color="red">${errorMessage}</font>`
7. Remove `<h3> My password is ${password }</h3>` from `welcome.jsp` file

<b>You can now try the valid and invalid scenario of logging in!</b>


### Step 7: Create To-Do Controller & View

We want to be able to add, delete, modify, to-do's through this application. 
- Create a `ToDoController` and `list-todos.jsp`
- Make `ToDoService` a `@Service` and inject it 

1. Create a new java class named `To Do` with package `com.ps.springboot.web.springbootfirstwebapplication.model`. Copy and past the code below onto the file. 
    <details>
    <summary> Screenshot of new class</summary>
    <image src="assets/create-to-do-class.png">

    </details>

    <details>
    <summary><b>To Do</b> code snippet  </summary>

      ```java
      package com.ps.springboot.web.springbootfirstwebapplication.model;

      import java.util.Date;

      public class Todo {

          private int id;
          private String user;
          private String desc;
          private Date targetDate;
          private boolean isDone;

          public Todo(int id, String user, String desc, Date targetDate,
                  boolean isDone) {
              super();
              this.id = id;
              this.user = user;
              this.desc = desc;
              this.targetDate = targetDate;
              this.isDone = isDone;
          }

          public int getId() {
              return id;
          }

          public void setId(int id) {
              this.id = id;
          }

          public String getUser() {
              return user;
          }

          public void setUser(String user) {
              this.user = user;
          }

          public String getDesc() {
              return desc;
          }

          public void setDesc(String desc) {
              this.desc = desc;
          }

          public Date getTargetDate() {
              return targetDate;
          }

          public void setTargetDate(Date targetDate) {
              this.targetDate = targetDate;
          }

          public boolean isDone() {
              return isDone;
          }

          public void setDone(boolean isDone) {
              this.isDone = isDone;
          }

          @Override
          public int hashCode() {
              final int prime = 31;
              int result = 1;
              result = prime * result + id;
              return result;
          }

          @Override
          public boolean equals(Object obj) {
              if (this == obj) {
                  return true;
              }
              if (obj == null) {
                  return false;
              }
              if (getClass() != obj.getClass()) {
                  return false;
              }
              Todo other = (Todo) obj;
              if (id != other.id) {
                  return false;
              }
              return true;
          }

          @Override
          public String toString() {
              return String.format(
                      "Todo [id=%s, user=%s, desc=%s, targetDate=%s, isDone=%s]", id,
                      user, desc, targetDate, isDone);
          }

      }
      ```
    </details> 
2. Create a new file named `TodoService.java` in `com.ps.springboot.web.springbootfirstwebapplication.service` and copy and paste the following code there.
    <details>
    <summary> TodoService code snippet</summary>

    ```java
    package com.ps.springboot.web.springbootfirstwebapplication.service;

    import java.util.ArrayList;
    import java.util.Date;
    import java.util.Iterator;
    import java.util.List;

    import org.springframework.stereotype.Service;

    import com.ps.springboot.web.springbootfirstwebapplication.model.Todo;


    @Service
    public class TodoService {
        private static List<Todo> todos = new ArrayList<Todo>();
        private static int todoCount = 3;

        static {
            todos.add(new Todo(1, "yourname", "Learn HTML/CSS/JS", new Date(),
                    false));
            todos.add(new Todo(2, "yourname", "Learn React", new Date(), false));
            todos.add(new Todo(3, "yourname", "Learn Java/SpringBoot", new Date(),
                    false));
        }

        public List<Todo> retrieveTodos(String user) {
            List<Todo> filteredTodos = new ArrayList<Todo>();
            for (Todo todo : todos) {
                if (todo.getUser().equals(user)) {
                    filteredTodos.add(todo);
                }
            }
            return filteredTodos;
        }

        public void addTodo(String name, String desc, Date targetDate,
                boolean isDone) {
            todos.add(new Todo(++todoCount, name, desc, targetDate, isDone));
        }

        public void deleteTodo(int id) {
            Iterator<Todo> iterator = todos.iterator();
            while (iterator.hasNext()) {
                Todo todo = iterator.next();
                if (todo.getId() == id) {
                    iterator.remove();
                }
            }
        }
    }
    ```
    </details> 
3. Let's update our `welcome.jsp` file with the following code
    <details>
    <summary> Body code snippet </summary>

    ```html
    <h2> Welcome ${name}! </h2>
    <h3> <a href="/list-todos"> Click here</a> to manage your todo's </h3>

    ```
    </details>
4. In `Project Explorer` for our project. Copy `LoginController.java` file and paste in in it's parents folder `com.ps.springboot.web.springbootfirstwebapplication.controller`. Change it's name to `TodoController`
    - Update  `LoginService service;` to `TodoService service;` and import and remove the `LoginService`service import.
    - Remove the `POST` method 
    -Update method name to `showTodos`
    - Update `@RequestMapping` value to `"/list-todos"` and `return "list-todos"`
      <details>
      <summary> Todo Controller code snippet </summary>

      ```java
      package com.ps.springboot.web.springbootfirstwebapplication.controller;

      import org.springframework.beans.factory.annotation.Autowired;
      import org.springframework.stereotype.Controller;
      import org.springframework.ui.ModelMap; 
      import org.springframework.web.bind.annotation.RequestMapping;
      import org.springframework.web.bind.annotation.RequestMethod;


      import com.ps.springboot.web.springbootfirstwebapplication.service.TodoService;

      @Controller
      public class TodoController {
        @Autowired
        TodoService service;
        
        @RequestMapping(value="/list-todos", method=RequestMethod.GET) 
        public String showTodos(ModelMap model) {
      //		model.put("name", name);
          return "list-todos";
          }
        

      }

      ```
      </details> 
5. Let's copy `welcome.jsp` and create `list-todos.jsp` page. Add this to the body `<h3> Here are your list of your todos:</h3>
`
6. In `TodoController` file we want to show the list of todo's. Let's add the information through the `model`. For now, we will grab our user's list first. 
    <details>
    <summary> Need a clue </summary>
    ```java

    @RequestMapping(value="/list-todos", method=RequestMethod.GET) 
    public String showTodos(ModelMap model) {
    model.put("todos", service.retrieveTodos("yourname"));
    return "list-todos";
    }
    ```

    </details>

7. To display our todo list onto the website. We must first update our `list-todos.jsp` body page. 

    <details>
    <summary> Need a clue </summary>

    ```java
    ${todos}
    ```
    </details>
8. Let's also get access to our name param. Add and import `@SessionAttributes("name")` below `@Controller` in our `LoginController` file
9. Add `${name}` to our `<h2></h2>` tag inside of our `list-todos.jsp` file
    <details>
    <summary><b>List Todos</b> code snippet </summary>

    ```html
    <html>
    <head>
     <title>First Web Application</title>
    </head>

    <body>
      <h2> Here are the list of ${name} todos:</h2>
      ${todos}
    </html>
    ```

    </details> 

Note: Refresh your page to `/login` and sign back in to see the changes 

### Step 8: Add a new to do

1. In `list-todos.jsp` file, add an `<a>` tag with an href attribute of `/add-todo` and content with `Add a Todo`. We still need to add a controller to our href link. 

2. Copy and paste `showTodos` method inside of our `TodoController`. Update name of method to `addTodo`. Our `@RequestMapping` value will be updated to `add-todos`. Remove `model.put..`. Have it `return "add-todo"`

3. Let's create a `add-todo.jsp` file. Add the following code: 
    <details>
    <summary> <b>Add todo</b> page code snippet</summary>

    ```html
    <html>
    <head>
      <title>First Web Application</title>
    </head>
    <body>
     <h2> Add Todo Page for ${name } </h2>

    </html>
    ```
    </details>
    - Let's create a form with a post method inside our page, make an `Description` input tag and submit input button
    <details>
    <summary><b>Form</b> code snippet </summary>

    ```html
    <form method="post">
      Description: <input name="desc" type="text"/>
      <input type="submit"/>
    </form>
    ```
    </details>

4. We want to use the same page for add a todo and update a todo as well. So let's update our `add-todo.jsp` file name to `todo.jsp`. 
    - We will need to update our `TodoController` method `addTodo` view name to `return "todo"`.
5. Copy and paste `addTodo` method below it. 
    - Update the method to `POST`
    - Update `addTodo` original method name to `showAddTodoPage`
    - Leave the duplicated method as `addTodo`
    - Add and import `@RequestParam String descr` to our method
    - Insert the following `service.addTodo((String) model.get("name"), desc, new Date(), false);` onto the body of our method. Note that you will need to import Date, make sure it's java.utils and not java.sql
    - It will `return "redirect:/list-todos";`
6. We will need to add the following code inside our `showTodos` method within our `TodoController`
    <details>
    <summary> ShowTodos Code snippet</summary>

    ```java
      String name = (String) model.get("name");
      model.put("todos", service.retrieveTodos(name));

    ```
    </details>
7. Make sure you also have `@SessionAttributes("name")` imported below `@Controller`
    <details>
    <summary> <b>TodoController</b> code snippet file</summary>

    ```java
    package com.ps.springboot.web.springbootfirstwebapplication.controller;

    import java.util.Date;

    import org.springframework.beans.factory.annotation.Autowired;
    import org.springframework.stereotype.Controller;
    import org.springframework.ui.ModelMap; 
    import org.springframework.web.bind.annotation.RequestMapping;
    import org.springframework.web.bind.annotation.RequestMethod;
    import org.springframework.web.bind.annotation.RequestParam;
    import org.springframework.web.bind.annotation.SessionAttributes;

    import com.ps.springboot.web.springbootfirstwebapplication.service.TodoService;

    @Controller
    @SessionAttributes("name")
    public class TodoController {
      @Autowired
      TodoService service;
      
      @RequestMapping(value="/list-todos", method=RequestMethod.GET) 
      public String showTodos(ModelMap model ) {
        String name = (String) model.get("name");
        model.put("todos", service.retrieveTodos(name));
        return "list-todos";
        }
      
      @RequestMapping(value="/add-todo", method=RequestMethod.GET) 
      public String showAddTodoPage(ModelMap model) {
        return "todo";
        }
      
      @RequestMapping(value="/add-todo", method=RequestMethod.POST) 
      public String addTodo(ModelMap model, @RequestParam String desc) { 
        
        service.addTodo((String) model.get("name"), desc, new Date(), false);
        return "redirect:/list-todos";
        }
    }
    ```
    </details>


### Step 9: Display Todos in a table using JSTL Tags

<!-- 
<details>
<summary> </summary>
</details> -->

 <!-- <image src="assets/create-login-service-class.png"> -->