# SpringBoot: learn annotations with code snippets

Spring Boot offers a variety of **annotations** to **simplify development** by providing concise, declarative code to configure and handle various aspects of Spring applications

Here’s a brief summary of the main **Spring Boot annotations** along with explanations and code snippets for each:

## SpringBoot Annotations summary

**@SpringBootApplication**: to mark the main class of a Spring Boot application

**@RestController**: is used to create RESTful web services. It is a combination of @Controller and @ResponseBody

**@Controller**: marks the class as a web controller

**@ResponseBody**: ensures that the method's return value is written directly to the HTTP response body, rather than being interpreted as a view name

**@Autowired**: automatic dependency injection

**@Entity**: it is used to mark a class as a JPA entity, meaning it is mapped to a database table

**@Repository**: it is used to indicate that the class is a Data Access Object (DAO)

**@Service**: it is used to mark a class as a service provider

**@Component**: it indicates that the class is a Spring component, which can be auto-detected during classpath scanning

**@Configuration**: it indicates that the class can be used by the Spring IoC container as a source of bean definitions

**@Value**: a field should be injected with a value from a properties file

**@RequestMapping**: It can be used at the class level to define a base URI for all request mappings in the class and at the method level to define specific request mappings

**@GetMapping, @PostMapping, @PutMapping, @DeleteMapping, @PatchMapping**: These are specialized versions of @RequestMapping for specific HTTP methods

**@PathVariable**: this annotation is used to extract values from the URI path

**@RequestParam**: it is used to extract query parameters from the URL

**@CrossOrigin**: it is used to enable Cross-Origin Resource Sharing (CORS) on the controller or handler methods

**@ConditionalOnProperty**: it is used to conditionally enable a bean based on a property value

**@Profile**: it is used to specify beans that should only be created in certain environments

**@EnableScheduling**: it is used to enable Spring's scheduled task execution capability

**@EnableAsync**: it is used to enable Spring's asynchronous method execution capability

**@EventListener**: it is used to mark a method as a listener for application events

**@Transactional**: it is used to manage transaction boundaries in a declarative manner

**@Cacheable**: it is used to indicate that the result of a method can be cached

**@Async**: it is used to indicate that a method should be executed asynchronously

**@Conditional**: it is used to conditionally include or exclude beans, configurations, or other components based on specific criteria

**@EnableWebSecurity**: it is used to enable Spring Security's web security support and provide the Spring MVC integration

**@Retryable**: it is used to indicate that a method should be retried automatically if it fails due to a specified exception

**@Scheduled**: it  is used to schedule tasks to be executed at fixed intervals or according to a cron expression

**@ConditionalOnMissingBean**: it is used to conditionally include a bean only if a specified bean does not already exist in the Spring application context

## 1. @SpringBootApplication

This is a convenience annotation that combines **@Configuration**, **@EnableAutoConfiguration**, and **@ComponentScan**

It is used to mark the main class of a Spring Boot application

**Explanation**:

**@SpringBootApplication**: This is a convenience annotation that adds:

**@Configuration**: Tags the class as a source of bean definitions for the application context

**@EnableAutoConfiguration**: Tells Spring Boot to start adding beans based on classpath settings, other beans, and various property settings

**@ComponentScan**: Tells Spring to look for other components, configurations, and services in the specified package, allowing it to find the controllers

Code Snippet:

```java
package com.example.demo;

import org.springframework.boot.CommandLineRunner;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.annotation.Bean;

@SpringBootApplication
public class DemoApplication {

    public static void main(String[] args) {
        SpringApplication.run(DemoApplication.class, args);
    }

    @Bean
    public CommandLineRunner commandLineRunner() {
        return args -> {
            System.out.println("Hello World");
        };
    }
}
```

or

```java
package com.example.demo;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class DemoApplication {

    public static void main(String[] args) {
        SpringApplication.run(DemoApplication.class, args);
        System.out.println("Hello World");
    }

}
```

## 2. @RestController

This annotation is a combination of **@Controller** and **@ResponseBody**

It is used to create **RESTful** web services

**Explanation**:

**@Controller**: Indicates that the class serves the role of a controller

**@ResponseBody**: Indicates that the return value of the methods should be bound to the web response body

Code Snippet:

```java
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class MyRestController {
    @GetMapping("/hello")
    public String sayHello() {
        return "Hello, World!";
    }
}
```

or

```java
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.ResponseBody;

@Controller
public class MyRestController {

    @GetMapping("/hello")
    @ResponseBody
    public String sayHello() {
        return "Hello, World!";
    }
}
```

## 3. @Autowired

This annotation is used for **automatic dependency injection**

It can be applied to constructors, setter methods, or fields

Explanation:

It allows Spring to resolve and inject collaborating beans into your bean

Code Snippet:

```java
package com.example;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class SpringBootAutowiredApplication {

    public static void main(String[] args) {
        SpringApplication.run(SpringBootAutowiredApplication.class, args);
    }
}
```

```java
package com.example.service;

import org.springframework.stereotype.Service;

@Service
public class GreetingService {

    public String greet() {
        return "Hello, World!";
    }
}
```

```java
package com.example.controller;

import com.example.service.GreetingService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class GreetingController {

    @Autowired
    private GreetingService greetingService;

    @GetMapping("/greet")
    public String greet() {
        return greetingService.greet();
    }
}
```

## 4. @Entity

This annotation is used to mark a class as a **JPA** entity, meaning it is **mapped to a database table**

Below is a simple Spring Boot application that demonstrates the use of @Entity to map a Java class to a database table using **JPA (Java Persistence API)**

This application includes an entity, a repository, a service, and a controller to illustrate how to work with a database in a Spring Boot application

Code Snippet:

```java
package com.example;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class SpringBootEntityApplication {

    public static void main(String[] args) {
        SpringApplication.run(SpringBootEntityApplication.class, args);
    }
}
```

```java
package com.example.entity;

import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import javax.persistence.Id;

@Entity
public class User {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String name;
    private String email;

    // Getters and setters

    public Long getId() {
        return id;
    }

    public void setId(Long id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getEmail() {
        return email;
    }

    public void setEmail(String email) {
        this.email = email;
    }
}
```

```java
package com.example.repository;

import com.example.entity.User;
import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.stereotype.Repository;

@Repository
public interface UserRepository extends JpaRepository<User, Long> {
}
```

```java
package com.example.service;

import com.example.entity.User;
import com.example.repository.UserRepository;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

import java.util.List;

@Service
public class UserService {

    @Autowired
    private UserRepository userRepository;

    public List<User> getAllUsers() {
        return userRepository.findAll();
    }

    public User saveUser(User user) {
        return userRepository.save(user);
    }
}
```

```java
package com.example.controller;

import com.example.entity.User;
import com.example.service.UserService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RestController;

import java.util.List;

@RestController
public class UserController {

    @Autowired
    private UserService userService;

    @GetMapping("/users")
    public List<User> getAllUsers() {
        return userService.getAllUsers();
    }

    @PostMapping("/users")
    public User createUser(@RequestBody User user) {
        return userService.saveUser(user);
    }
}
```

## 5. @Repository

This annotation is used to indicate that the class is a **Data Access Object (DAO)**

Explanation:

It indicates that the class provides the mechanism for **storage**, **retrieval**, **search**, **update**, and **delete** operation on objects

Code Snippet:

```java
import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.stereotype.Repository;

@Repository
public interface MyRepository extends JpaRepository<MyEntity, Long> {
    // Custom query methods can be defined here
}
```

## 6. @Service

This annotation is used to mark a class as a service provider

Explanation:

It indicates that the class provides some business functionalities and is a service provider

Code Snippet:

```java
// Java Program to Illustrate MyServiceClass
 
// Importing package module to code module
package com.example.demo.service;
// Importing required classes
import org.springframework.stereotype.Service;
 
// Annotation
@Service
 
// Class
public class MyServiceClass {
 
    // Method
    // To compute factorial
    public int factorial(int n)
    {
        // Base case
        if (n == 0)
            return 1;
 
        return n * factorial(n - 1);
    }
}
```

```java
// Java Program to Illustrate DemoApplication
 
// Importing package module to code fragment
package com.example.demo;
// Importing required classes
import com.example.demo.service.MyServiceClass;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.annotation.AnnotationConfigApplicationContext;
 
// Annotation
@SpringBootApplication
 
// Main class
public class DemoApplication {
 
    // MAin driver method
    public static void main(String[] args)
    {
 
        AnnotationConfigApplicationContext context
            = new AnnotationConfigApplicationContext();
        context.scan("com.example.demo");
 
        context.refresh();
 
        MyServiceClass myServiceClass
            = context.getBean(MyServiceClass.class);
 
        // Testing the factorial method
        int factorialOf5 = myServiceClass.factorial(5);
        System.out.println("Factorial of 5 is: "
                           + factorialOf5);
 
        // Closing the spring context
        // using close() method
        context.close();
    }
}
```

**AnnotationConfigApplicationContext context**: This line creates an instance of AnnotationConfigApplicationContext, which is a Spring context container designed to work with Java-based configuration

**context.scan("com.example.demo")**: This tells the Spring container to scan the com.example.demo package for classes annotated with Spring annotations (like @Component, @Service, etc.)

It is used to detect and register Spring-managed beans

**context.refresh()**: This initializes the Spring context. It processes the scanned classes, creates and configures beans, and prepares the application for use

**context.getBean(MyServiceClass.class)**: This line retrieves a bean of type MyServiceClass from the Spring context

It assumes that MyServiceClass is a Spring-managed bean, annotated with @Component, @Service, or similar

**context.close()**: Closes the Spring application context, releasing all resources and locks that it holds

This is a good practice to ensure that resources are properly cleaned up when the application is done

## 7. @Component

This is a generic stereotype for any Spring-managed component

Explanation:

It indicates that the class is a Spring component, which can be auto-detected during classpath scanning

Code Snippet:

```java
import org.springframework.stereotype.Component;

@Component
public class MyComponent {
    public String getComponentMessage() {
        return "Component Message";
    }
}
```

## 8. @Configuration

This annotation indicates that the class has @Bean definition methods

Explanation:

It indicates that the class can be used by the Spring IoC container as a source of bean definitions

Code Snippet:

```java
Copy code
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class MyConfiguration {
    @Bean
    public MyBean myBean() {
        return new MyBean();
    }
}
```

## 9. @Value

This annotation is used to inject values into fields from a properties file

Explanation:

It indicates that a field should be injected with a value from a properties file

Code Snippet:

```java
import org.springframework.beans.factory.annotation.Value;
import org.springframework.stereotype.Component;

@Component
public class MyComponent {
    @Value("${my.property}")
    private String myProperty;

    public String getMyProperty() {
        return myProperty;
    }
}
```

## 10. @RequestMapping

This annotation is used to map web requests to specific handler classes or methods

Explanation:

It can be used at the class level to define a base URI for all request mappings in the class and at the method level to define specific request mappings

Code Snippet:

```java
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;
import org.springframework.web.bind.annotation.RestController;

@RestController
@RequestMapping("/api")
public class MyApiController {
    
    @RequestMapping(value = "/hello", method = RequestMethod.GET)
    public String sayHello() {
        return "Hello, World!";
    }
}
```

## 11. @GetMapping, @PostMapping, @PutMapping, @DeleteMapping, @PatchMapping

These are specialized versions of @RequestMapping for specific HTTP methods

Explanation:

**@GetMapping** is used for GET requests

**@PostMapping** is used for POST requests

**@PutMapping** is used for PUT requests

**@DeleteMapping** is used for DELETE requests

**@PatchMapping** is used for PATCH requests

Code Snippet:

```java
import org.springframework.web.bind.annotation.*;

@RestController
@RequestMapping("/items")
public class ItemController {

    @GetMapping("/{id}")
    public Item getItem(@PathVariable Long id) {
        // Retrieve item by id
        return new Item(id, "Sample Item");
    }

    @PostMapping
    public Item createItem(@RequestBody Item item) {
        // Create new item
        return item;
    }

    @PutMapping("/{id}")
    public Item updateItem(@PathVariable Long id, @RequestBody Item item) {
        // Update item by id
        item.setId(id);
        return item;
    }

    @DeleteMapping("/{id}")
    public void deleteItem(@PathVariable Long id) {
        // Delete item by id
    }
}
```

## 12. @PathVariable

This annotation is used to extract values from the URI path

Explanation:

It binds the URI template variables to method parameters

Code Snippet:

```java
import org.springframework.web.bind.annotation.*;

@RestController
@RequestMapping("/users")
public class UserController {

    @GetMapping("/{userId}")
    public String getUser(@PathVariable String userId) {
        return "User ID: " + userId;
    }
}
```

## 13. @RequestParam

This annotation is used to extract query parameters from the URL

Explanation:

It binds the query string parameters to method parameters

Code Snippet:

```java
import org.springframework.web.bind.annotation.*;

@RestController
@RequestMapping("/search")
public class SearchController {

    @GetMapping
    public String search(@RequestParam String query) {
        return "Search query: " + query;
    }
}
```

## 14. @RequestBody

This annotation is used to bind the body of the web request to a method parameter

Explanation:

It is used to convert the body of a POST or PUT request to an object

Code Snippet:

```java
import org.springframework.web.bind.annotation.*;

@RestController
@RequestMapping("/orders")
public class OrderController {

    @PostMapping
    public Order createOrder(@RequestBody Order order) {
        // Process the order
        return order;
    }
}
```

## 15. @ResponseBody

This annotation is used to **bind the method return value to the web response body**

Explanation:

It tells Spring to convert the return value and write it to the HTTP response automatically

Code Snippet:

```java
import org.springframework.web.bind.annotation.*;

@RestController
@RequestMapping("/messages")
public class MessageController {

    @GetMapping("/greet")
    @ResponseBody
    public String greet() {
        return "Hello, World!";
    }
}
```

## 16. @CrossOrigin

This annotation is used to enable **Cross-Origin Resource Sharing (CORS)** on the controller or handler methods

Explanation:

It allows for specifying the allowed origins, headers, methods, and other configurations for cross-origin requests

Code Snippet:

```java
import org.springframework.web.bind.annotation.*;

@RestController
@RequestMapping("/api")
@CrossOrigin(origins = "http://example.com")
public class ApiController {

    @GetMapping("/data")
    public String getData() {
        return "Data from server";
    }
}
```

## 17. @ConditionalOnProperty

This annotation is used to conditionally enable a bean based on a property value

Explanation:

It controls bean registration by checking if a specific property is present and has a specific value

Code Snippet:

```java
import org.springframework.boot.autoconfigure.condition.ConditionalOnProperty;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class MyConfiguration {

    @Bean
    @ConditionalOnProperty(name = "my.feature.enabled", havingValue = "true")
    public MyBean myBean() {
        return new MyBean();
    }
}
```

## 18. @Profile

This annotation is used to indicate that a component is eligible for registration when one or more specified profiles are active

Explanation:

It is used to specify beans that should only be created in certain environments

Code Snippet:

```java
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.context.annotation.Profile;

@Configuration
public class MyConfiguration {

    @Bean
    @Profile("dev")
    public MyBean devBean() {
        return new MyBean("Development Bean");
    }

    @Bean
    @Profile("prod")
    public MyBean prodBean() {
        return new MyBean("Production Bean");
    }
}
```

## 19. @EnableScheduling

This annotation is used to enable Spring's scheduled task execution capability

Explanation:

It triggers the scanning of the @Scheduled annotations on any Spring-managed beans

Code Snippet:

```java
import org.springframework.context.annotation.Configuration;
import org.springframework.scheduling.annotation.EnableScheduling;
import org.springframework.scheduling.annotation.Scheduled;

@Configuration
@EnableScheduling
public class SchedulingConfig {

    @Scheduled(fixedRate = 5000)
    public void performTask() {
        System.out.println("Scheduled Task executed every 5 seconds");
    }
}
```

## 20. @EnableAsync

This annotation is used to enable Spring's asynchronous method execution capability

Explanation:

It triggers the scanning of the @Async annotations on any Spring-managed beans

Code Snippet:

```java
import org.springframework.context.annotation.Configuration;
import org.springframework.scheduling.annotation.EnableAsync;
import org.springframework.scheduling.annotation.Async;

@Configuration
@EnableAsync
public class AsyncConfig {

    @Async
    public void performAsyncTask() {
        System.out.println("Executing task asynchronously");
    }
}
```

These additional annotations further enhance Spring Boot's capabilities, providing powerful tools to manage application configurations, handle web requests, and support various features like scheduling and asynchronous processing

## 21. @EventListener

This annotation is used to mark a method as an event listener, allowing it to handle application events

Explanation:

It listens for specific application events and executes the annotated method when such events are published

Code Snippet:

```java
import org.springframework.context.event.EventListener;
import org.springframework.stereotype.Component;

@Component
public class MyEventListener {

    @EventListener
    public void handleContextRefreshedEvent(ContextRefreshedEvent event) {
        System.out.println("Context Refreshed Event received: " + event);
    }
}
```

## 22. @Transactional

This annotation is used to manage transaction boundaries declaratively

Explanation:

It ensures that the annotated method or all methods within the annotated class are executed within a transaction

Code Snippet:

```java
import org.springframework.stereotype.Service;
import org.springframework.transaction.annotation.Transactional;

@Service
public class MyTransactionalService {

    @Transactional
    public void performTransactionalOperation() {
        // Code that requires transaction management
    }
}
```

## 23. @Cacheable

This annotation is used to indicate that the result of invoking a method (or all methods in a class) can be cached

Explanation:

It allows caching of method results, which can improve performance by reducing the need to recompute or fetch data repeatedly

Code Snippet:

```java
import org.springframework.cache.annotation.Cacheable;
import org.springframework.stereotype.Service;

@Service
public class MyCacheService {

    @Cacheable("items")
    public Item getItemById(Long id) {
        // Code to retrieve item by id
        return new Item(id, "Cached Item");
    }
}
```

## 24. @Async

This annotation is used to indicate that a method should be executed asynchronously

Explanation:

It allows the execution of the method to be offloaded to a separate thread, improving the performance and responsiveness of the application

Code Snippet:

```java
import org.springframework.scheduling.annotation.Async;
import org.springframework.stereotype.Service;

@Service
public class MyAsyncService {

    @Async
    public void performAsyncTask() {
        System.out.println("Executing task asynchronously");
    }
}
```

## 25. @Conditional

This annotation is used to define custom conditions for bean registration

Explanation:

It provides a way to define custom logic to determine whether a bean should be registered in the Spring context

Code Snippet:

```java
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Conditional;
import org.springframework.context.annotation.Configuration;

@Configuration
public class MyConditionalConfig {

    @Bean
    @Conditional(MyCondition.class)
    public MyBean myBean() {
        return new MyBean();
    }
}

import org.springframework.context.annotation.Condition;
import org.springframework.context.annotation.ConditionContext;
import org.springframework.core.type.AnnotatedTypeMetadata;

public class MyCondition implements Condition {
    @Override
    public boolean matches(ConditionContext context, AnnotatedTypeMetadata metadata) {
        // Custom condition logic
        return true; // or false based on the condition
    }
}
```

## 26. @EnableWebSecurity

This annotation is used to enable Spring Security’s web security support

Explanation:

It indicates that the application should use Spring Security for web security configuration

Code Snippet:

```java
import org.springframework.context.annotation.Configuration;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.config.annotation.web.configuration.EnableWebSecurity;
import org.springframework.security.config.annotation.web.configuration.WebSecurityConfigurerAdapter;

@Configuration
@EnableWebSecurity
public class WebSecurityConfig extends WebSecurityConfigurerAdapter {

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http
            .authorizeRequests()
            .anyRequest().authenticated()
            .and()
            .formLogin().and()
            .httpBasic();
    }
}
```

## 27. @Profile

This annotation is used to indicate that a bean is eligible for registration when one or more specified profiles are active

Explanation:

It allows different beans to be registered based on the active profile, enabling environment-specific configurations

Code Snippet:

```java
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.context.annotation.Profile;

@Configuration
public class MyProfileConfig {

    // Bean definition for the "dev" profile
    @Bean
    @Profile("dev")
    public MyBean devBean() {
        return new MyBean("Development Bean");
    }

    // Bean definition for the "prod" profile
    @Bean
    @Profile("prod")
    public MyBean prodBean() {
        return new MyBean("Production Bean");
    }

    // Bean definition for the "test" profile
    @Bean
    @Profile("test")
    public MyBean testBean() {
        return new MyBean("Test Bean");
    }
    
    // Bean definition for both "dev" and "qa" profiles
    @Bean
    @Profile({"dev", "qa"})
    public MyBean devQaBean() {
        return new MyBean("Development and QA Bean");
    }
    
    // Bean definition for "default" profile
    @Bean
    @Profile("default")
    public MyBean defaultBean() {
        return new MyBean("Default Bean");
    }
}

class MyBean {
    private String name;

    public MyBean(String name) {
        this.name = name;
    }

    // Getter and Setter methods
    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    @Override
    public String toString() {
        return "MyBean{name='" + name + '\'' + '}';
    }
}
```

**Activating Profiles**

To activate a specific profile, you can use the spring.profiles.active property. This can be set in several ways:

In the **application.properties** file:

```
spring.profiles.active=dev
```

As a command-line argument:

```
java -jar myapp.jar --spring.profiles.active=prod
```

As an environment variable:

```
export SPRING_PROFILES_ACTIVE=test
```

Using profiles allows you to create and configure beans specifically tailored for different environments, making your application more flexible and easier to manage

## 28. @Retryable

This annotation is used to automatically retry a failed operation

Explanation:

It indicates that a method should be retried in case of a specific exception

Code Snippet:

```java
import org.springframework.retry.annotation.Backoff;
import org.springframework.retry.annotation.Recover;
import org.springframework.retry.annotation.Retryable;
import org.springframework.stereotype.Service;

@Service
public class MyRetryableService {

    // Retryable operation with custom backoff and max attempts
    @Retryable(
        value = { RuntimeException.class, CustomException.class },
        maxAttempts = 3,
        backoff = @Backoff(delay = 2000, multiplier = 1.5)
    )
    public void performRetryableOperation() {
        System.out.println("Attempting operation...");
        // Code that may fail and should be retried
        throw new RuntimeException("Operation failed, retrying...");
    }

    // Retryable operation with fixed delay
    @Retryable(
        value = { RuntimeException.class },
        maxAttempts = 4,
        backoff = @Backoff(delay = 3000)
    )
    public void performFixedDelayRetryableOperation() {
        System.out.println("Attempting fixed delay operation...");
        // Code that may fail and should be retried
        throw new RuntimeException("Operation with fixed delay failed, retrying...");
    }

    // Retryable operation with exponential backoff
    @Retryable(
        value = { RuntimeException.class },
        maxAttempts = 5,
        backoff = @Backoff(delay = 1000, multiplier = 2)
    )
    public void performExponentialBackoffRetryableOperation() {
        System.out.println("Attempting exponential backoff operation...");
        // Code that may fail and should be retried
        throw new RuntimeException("Operation with exponential backoff failed, retrying...");
    }

    // Recover method to handle failures after retries are exhausted
    @Recover
    public void recover(RuntimeException e) {
        System.out.println("Recovery method called after retries are exhausted: " + e.getMessage());
    }

    // Retryable operation with a custom exception
    @Retryable(
        value = { CustomException.class },
        maxAttempts = 3,
        backoff = @Backoff(delay = 2000)
    )
    public void performCustomExceptionRetryableOperation() throws CustomException {
        System.out.println("Attempting custom exception operation...");
        // Code that may fail and should be retried
        throw new CustomException("Custom exception operation failed, retrying...");
    }

    // Recover method for custom exception
    @Recover
    public void recover(CustomException e) {
        System.out.println("Recovery method called for custom exception: " + e.getMessage());
    }

    // Custom exception class
    public static class CustomException extends Exception {
        public CustomException(String message) {
            super(message);
        }
    }
}
```

In this code:

**performRetryableOperation**: Retries the operation up to 3 times with an initial delay of 2000 milliseconds, and each subsequent delay is multiplied by 1.5.

**performFixedDelayRetryableOperation**: Retries the operation up to 4 times with a fixed delay of 3000 milliseconds between attempts

**performExponentialBackoffRetryableOperation**: Retries the operation up to 5 times with an initial delay of 1000 milliseconds, and each subsequent delay is multiplied by 2 (exponential backoff)

**recover(RuntimeException e)**: A recovery method that is called if all retries are exhausted for operations throwing RuntimeException

**performCustomExceptionRetryableOperation**: Retries the operation up to 3 times with a delay of 2000 milliseconds for CustomException

**recover(CustomException e)**: A recovery method that is called if all retries are exhausted for operations throwing CustomException

**CustomException**: A custom exception class used for demonstration

This comprehensive example demonstrates how to configure retryable operations with different backoff strategies, max attempts, and recovery methods

## 29. @Scheduled

This annotation is used to mark a method to be scheduled at fixed intervals or cron expressions

Explanation:

It indicates that the method should be executed according to a fixed rate, fixed delay, or cron expression

Code Snippet:

```java
import org.springframework.scheduling.annotation.Scheduled;
import org.springframework.stereotype.Component;

@Component
public class MyScheduledTask {

    // Task with fixed rate of 5 seconds
    @Scheduled(fixedRate = 5000)
    public void performScheduledTask() {
        System.out.println("Scheduled task executed every 5 seconds");
    }

    // Task with fixed delay of 7 seconds
    @Scheduled(fixedDelay = 7000)
    public void performFixedDelayTask() {
        System.out.println("Scheduled task executed 7 seconds after the previous task finished");
    }

    // Task with initial delay of 3 seconds and then fixed rate of 10 seconds
    @Scheduled(initialDelay = 3000, fixedRate = 10000)
    public void performInitialDelayTask() {
        System.out.println("Scheduled task executed after initial delay of 3 seconds and then every 10 seconds");
    }

    // Task with cron expression
    @Scheduled(cron = "0 * * * * *") // Every minute at the start of the minute
    public void performCronTask() {
        System.out.println("Scheduled task executed at the start of every minute");
    }

    // Task with custom fixed rate from application properties
    @Scheduled(fixedRateString = "${custom.fixed.rate}")
    public void performCustomRateTask() {
        System.out.println("Scheduled task executed at custom rate defined in application properties");
    }

    // Task with custom fixed delay from application properties
    @Scheduled(fixedDelayString = "${custom.fixed.delay}")
    public void performCustomDelayTask() {
        System.out.println("Scheduled task executed at custom delay defined in application properties");
    }

    // Task with custom initial delay and fixed rate from application properties
    @Scheduled(initialDelayString = "${custom.initial.delay}", fixedRateString = "${custom.fixed.rate}")
    public void performCustomInitialDelayTask() {
        System.out.println("Scheduled task executed with custom initial delay and rate defined in application properties");
    }
}
```

In this code:

**performFixedDelayTask** runs 7 seconds after the previous task finishes

**performInitialDelayTask** runs first after an initial delay of 3 seconds, then every 10 seconds

**performCronTask** runs at the start of every minute

**performCustomRateTask**, **performCustomDelayTask**, and **performCustomInitialDelayTask** use values defined in the application's properties file

Ensure you have the corresponding properties in your application.properties file if you use the custom scheduled tasks:

```
custom.fixed.rate=5000
custom.fixed.delay=7000
custom.initial.delay=3000
```

## 30. @ConditionalOnMissingBean

I'll provide you with a simple Spring Boot application that demonstrates the use of @ConditionalOnMissingBean
 
This annotation is used to conditionally create a bean if a bean of the same type or name is not already present in the application context

Here's an example Spring Boot application:

**Create a Spring Boot Project**:

You can create a new Spring Boot project using **Spring Initializr (https://start.spring.io/)**

Choose your preferred build tool (**Maven** or **Gradle**), and add the necessary dependencies such as **Spring Web**

**Application.java**

```java
package com.example.demo;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class Application {
    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
}
```

**Create Service Interfaces and Implementations**:

**MyService.java**

```java
package com.example.demo.service;

public interface MyService {
    String serve();
}
```

**DefaultService.java**

```java
package com.example.demo.service;

import org.springframework.stereotype.Service;

@Service
public class DefaultService implements MyService {
    @Override
    public String serve() {
        return "Default Service";
    }
}
```

**CustomService.java**

```java
package com.example.demo.service;

import org.springframework.context.annotation.Conditional;
import org.springframework.stereotype.Service;

@Service
@ConditionalOnMissingBean(MyService.class)
public class CustomService implements MyService {
    @Override
    public String serve() {
        return "Custom Service";
    }
}
```

**Create a Controller to Test the Services**:

**MyController.java**

```java
package com.example.demo.controller;

import com.example.demo.service.MyService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class MyController {

    private final MyService myService;

    @Autowired
    public MyController(MyService myService) {
        this.myService = myService;
    }

    @GetMapping("/serve")
    public String serve() {
        return myService.serve();
    }
}
```

**Run the Application**:

Run your Spring Boot application. If there is no other bean of type MyService defined, CustomService will be used. Otherwise, DefaultService will be used.

**Test the Application**:

Access http://localhost:8080/serve to see which service is being used.

**Explanation**:

@ConditionalOnMissingBean on CustomService ensures that this bean will only be created if there is no other bean of type MyService in the application context

In this setup, DefaultService will be created and used because it is not conditional

If you comment out or remove the DefaultService bean, CustomService will be used

This example demonstrates how you can use @ConditionalOnMissingBean to conditionally define beans in a Spring Boot application

These advanced annotations provide powerful ways to manage and control the behavior of Spring Boot applications, enhancing flexibility, scalability, and maintainability
