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

**@Configuration**: Indicates that the class can be used by the Spring IoC container as a source of bean definitions

**@EnableAutoConfiguration**: Enables Spring Boot’s auto-configuration mechanism

**@ComponentScan**: Enables component scanning so that the web controller classes and other components you create will be automatically discovered and registered as beans in Spring's application context

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
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

@Service
public class MyService {
    private final MyRepository myRepository;

    @Autowired
    public MyService(MyRepository myRepository) {
        this.myRepository = myRepository;
    }

    // Other methods
}
```

## 4. @Entity

This annotation is used to mark a class as a **JPA** entity, meaning it is **mapped to a database table**

Explanation:

It indicates that the class is an entity and is mapped to a database table

By default, the table name is the same as the class name

Code Snippet:

```java
import javax.persistence.Entity;
import javax.persistence.Id;

@Entity
public class MyEntity {
    @Id
    private Long id;
    private String name;

    // Getters and setters
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
import org.springframework.stereotype.Service;

@Service
public class MyService {
    public String getServiceMessage() {
        return "Service Layer Message";
    }
}
```

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

## 28. @Retryable

This annotation is used to automatically retry a failed operation

Explanation:

It indicates that a method should be retried in case of a specific exception

Code Snippet:

```java
import org.springframework.retry.annotation.Backoff;
import org.springframework.retry.annotation.Retryable;
import org.springframework.stereotype.Service;

@Service
public class MyRetryableService {

    @Retryable(value = RuntimeException.class, maxAttempts = 3, backoff = @Backoff(delay = 2000))
    public void performRetryableOperation() {
        // Code that may fail and should be retried
        throw new RuntimeException("Operation failed, retrying...");
    }
}
```

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

    @Scheduled(fixedRate = 5000)
    public void performScheduledTask() {
        System.out.println("Scheduled task executed every 5 seconds");
    }
}
```

## 30. @ConditionalOnMissingBean

This annotation is used to conditionally register a bean if a specified bean is not already present

Explanation:

It allows for defining a bean only if another specified bean is missing from the Spring context

Code Snippet:

```java
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Conditional;
import org.springframework.context.annotation.Configuration;

@Configuration
public class MyConditionalBeanConfig {

    @Bean
    @ConditionalOnMissingBean(MyBean.class)
    public MyBean myBean() {
        return new MyBean();
    }
}
```

These advanced annotations provide powerful ways to manage and control the behavior of Spring Boot applications, enhancing flexibility, scalability, and maintainability
