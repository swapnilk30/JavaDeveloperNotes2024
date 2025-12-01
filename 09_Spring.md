

# 🚀 **INTERVIEW NOTES: @PathVariable vs @RequestParam vs @ModelAttribute**

---

# 1️⃣ **@PathVariable — Extract Value From URL Path**

## ✔ Definition

`@PathVariable` binds a value **directly from the URI path** into a method parameter.

## ✔ Typical Use-Cases

* Identifying a resource (RESTful ID)
* URL-based navigation (e.g., `/orders/10/items`)
* Always required (unless explicitly marked optional)

## ✔ Example

URL: `/users/10`

```java
@GetMapping("/users/{id}")
public String getUser(@PathVariable int id) {
    return "User ID: " + id;
}
```

## ✔ Characteristics

* Source: **URI path segment**
* Best for: **IDs** or mandatory path components
* Works mostly with: **GET**, but can be used in POST/PUT as well
* Syntax tied to URI template: `/user/{id}`

## ✔ When NOT to Use

❌ For filters, sorting, pagination
❌ For form submissions
❌ For optional parameters

---

# 2️⃣ **@RequestParam — Extract Query Parameter / Form Parameter**

## ✔ Definition

`@RequestParam` retrieves values from **query parameters** or **form fields**.

## ✔ Typical Use-Cases

* Optional inputs
* Pagination, sorting, filters
* Search queries
* Simple form submissions (single or few fields)

## ✔ Example

URL: `/users?id=10&active=true`

```java
@GetMapping("/users")
public String getUser(@RequestParam int id,
                      @RequestParam(defaultValue = "false") boolean active) {
    return id + " - " + active;
}
```

## ✔ Characteristics

* Source: **Query string / form field**
* Can be optional (`required=false`)
* Can provide default values (`defaultValue="xyz"`)

## ✔ Special Features

* Supports multiple values:
  `/filter?category=books&category=games`

## ✔ When NOT to Use

❌ When reading complex objects
❌ When the data comes from URL path
❌ When binding full form data (use `@ModelAttribute`)

---

# 3️⃣ **@ModelAttribute — Bind Request Data to a POJO**

## ✔ Definition

`@ModelAttribute` binds **multiple request parameters** into a **model object**
and also adds it to the **Spring MVC Model** automatically.

## ✔ Typical Use-Cases

* HTML form submissions
* Binding request data to DTOs (LoginForm, UserDTO, PaymentDTO)
* Multi-field inputs
* MVC-based projects (Thymeleaf/JSP)

## ✔ Example

URL: `/register?name=Swapnil&age=30`

```java
@PostMapping("/register")
public String register(@ModelAttribute User user) {
    return user.getName() + " - " + user.getAge();
}
```

Spring will automatically populate the POJO using setters.

## ✔ Characteristics

* Source: **Request parameters or form fields**
* Binds directly to Java object
* Great for **MVC + form handling**
* Automatically adds object to the **model** for view rendering

## ✔ Advanced Uses

You can also preload data in the model:

```java
@ModelAttribute("countries")
public List<String> loadCountries() {
    return List.of("India", "USA", "UK");
}
```

---

# 🔥 **INTERVIEW COMPARISON TABLE**

| Feature                | `@PathVariable`         | `@RequestParam`                 | `@ModelAttribute`           |
| ---------------------- | ----------------------- | ------------------------------- | --------------------------- |
| Extracts value from    | URL path                | Query parameters / form fields  | Entire request into a POJO  |
| Typical URL            | `/users/10`             | `/users?id=10`                  | `/register?name=Ram&age=20` |
| Data type              | Single value            | Single / multiple values        | Object                      |
| Required?              | Yes                     | Optional                        | Optional                    |
| Primary use            | Resource identification | Filters, pagination, user input | Form binding / DTO          |
| Adds to model?         | ❌ No                    | ❌ No                            | ✔ Yes                       |
| Works best with        | REST endpoint           | GET/POST filter params          | MVC forms                   |
| Accepts default values | ❌ No                    | ✔ Yes                           | Not needed                  |
| Binding complexity     | Low                     | Low                             | High (POJO)                 |
| Path-specific?         | ✔ Yes                   | ❌ No                            | ❌ No                        |

---

# 🔥 SUPER IMPORTANT INTERVIEW QUESTIONS (WITH ANSWERS)

---

### **1. When do you prefer @PathVariable over @RequestParam?**

Use `@PathVariable` when parameter is part of the **URL structure** and identifies a resource:

```
/orders/100
/customers/5
/products/88/reviews
```

---

### **2. Can @PathVariable be optional?**

Yes, but URL must define optional mapping.
Not recommended for REST.

---

### **3. Can you mix @PathVariable and @RequestParam?**

Yes, very common:

```java
@GetMapping("/users/{id}/orders")
public List<Order> getOrders(
        @PathVariable long id,
        @RequestParam(defaultValue = "asc") String sort) {
    ...
}
```

---

### **4. What is @ModelAttribute doing internally?**

* Creates an instance of the POJO
* Populates it using request parameters
* Adds it to the model
* Makes it available to the view

---

### **5. When would you avoid @ModelAttribute?**

* In pure REST APIs (prefer `@RequestBody`)
* When data is JSON (use `@RequestBody`)
* When only 1 or 2 simple params needed (use `@RequestParam`)

---

# 🧨 **Practical Real-World Example (Payment Gateway Domain)**

(related to your OmanNet & PG integration projects)

### URL

```
/merchant/submit/100?txnType=purchase&currency=OMR
```

### Controller

```java
@PostMapping("/merchant/submit/{txnId}")
public SubmitResponse submitPayment(
        @PathVariable String txnId,                    // identifies the transaction
        @RequestParam String txnType,                  // simple request value
        @ModelAttribute PaymentDTO dto) {              // binds full form data

    dto.setTxnId(txnId);
    dto.setTxnType(txnType);

    return service.process(dto);
}
```

---

# 🎤 **FINAL INTERVIEW SUMMARY (Use This in Interview)**

> **`@PathVariable` extracts values from URI path and is used for resource identification.
> `@RequestParam` extracts query parameters or form inputs, mostly used for filters and optional inputs.
> `@ModelAttribute` binds multiple request parameters to a POJO and adds it to the model, typically used in MVC form submissions or DTO binding.**

---

If you want, I can also give:
✔ One-page PDF summary
✔ Diagram of request flow for all 3
✔ Practice interview questions (20+)
✔ Real code examples using Spring Boot & Thymeleaf (your project stack)




---




### What is Spring Bean?
    The java class which is managed by IOC is called as Spring Bean.

### How to represent java class as Spring Bean?
- Using Xml configuration
```
<bean id="car" class="com.algowebpro.Car" />
```
- Using Annotations
```
@Component , @Service , @Repository
```

### Difference between heavy weight and light weight components

- EJB(enterprise java bean) are **depends on application server.** So it is called as heavy weight components.
- Spring are **not depends on application server.** They just use your JDK and jar file to run application.


## What is @SpringBootApplication ?

- `@SpringBootApplication` is an annotation in the Spring Framework for Java that combines three other annotations into one: 
        @Configuration, @EnableAutoConfiguration, and @ComponentScan.

- It's commonly used to mark the main class of a Spring Boot application.

- Here's a brief overview of what each of these annotations does:

    - 1.`@@SpringBootConfiguration`: Indicates that the class is a source of bean definitions for the application context. It allows defining beans using Java-based configuration instead of XML.

    - 2.`@EnableAutoConfiguration`: Tells Spring Boot to automatically configure the Spring application based on its dependencies. This annotation triggers Spring Boot's auto-configuration mechanism, which attempts to guess and configure beans based on the classpath and various property settings.

    - 3.`@ComponentScan`: Instructs Spring to scan the specified packages for components (such as @Component, @Service, @Repository, etc.) so that they can be automatically registered and used by the Spring application context.

    By combining these three annotations into @SpringBootApplication, developers can create a standalone Spring Boot application with minimal configuration. It's often used to bootstrap a Spring Boot application and launch it from the main method.


### Dependency Injection : Setter Based and Constructor based , and Field Injection.
- Autowiring : ByType , ByName


### 1.@Component
- It is a class-level annotation. It is used to mark a Java class as a bean.
- A Java class annotated with @Component is found during the classpath.
- The Spring Framework pick it up and configure it in the application
context as a Spring Bean.
- allows Spring to detect our custom beans automatically.
- Spring has provided a few specialized stereotype annotations: @Controller, @Service and @Repository.
- They all provide the same function as @Component.

### 2.@Service
- It is also used at class level. It tells the Spring that class contains the business logic.





```
interface IReport{ 
    void generateReport();
}

@Component("pdf")
class PdfReport implements IReport{

    public void generateReport(){
        System.out.print("generating pdf report...");
    }
}

@Component("excel")
//@Primary
class ExcelReport implements IReport{

    public void generateReport(){
        System.out.print("generating excel report...");
    }
}

@Service
class ReportService{

    @Autowired
    @Qualifier("excel")
    private IReport report;

    //private IReport excelReport;
    //private IReport pdfReport;

    public void downloadReport(){
        report.generateReport();
    }

}

### @Autowired
### @Primary
### @Qualifier
```

### @Value Annotation
- '@Value' annotation is used to read the properties from the application.properties file inside the spring boot.
- This annotation can be applied to a fields.
```
@Value("${app.name}")
private String appName;

```
-  If the property is not present in the application.properties file then spring will throw an exception, when we run the application.
- We can also provide default values for properties using @Value annotation
```
@Value("${app.version:version1}")
private String appVersion;
```
- Here, we are providing the default value as version1 seperated with : (colon).
- If the property is not present in the application.properties file then it will take the default value instead of throwing the exception.


### @Controller Annotation
- @Controller annotation acts as a controller in the MVC design pattern. 
- It indicates that the particular class serves the role of controller.
- It contains methods that are annotated with @RequestMapping annotation with URL mappings that are triggered for web requests.
- It works with view technology, so the method returns ModelAndView.


### @RestController Annotation
- @RestController annotation is mainly used for building restful web services using Spring MVC.
- It is a convenience annotation, this annotation itself annotated with @ResponseBody and @Controller annotation.
- The class annotated with @RestController annotation returns JSON response in all the methods.
- It does not work with view technology so that the method does not return ModelAndView.

### @RequestMapping Annotation
- @RequestMapping is the most common and widely used annotation in Spring MVC.
- It is used to map web requests onto specific handler classes and/or handler methods.
- @RequestMapping can be applied to the controller class as well as methods.
- It has the following optional options
    - name: Assign a name to this mapping.
    - value:  The primary mapping expressed by this annotation.
    - method: The HTTP request methods to map to
    - headers: The headers of the mapped request, narrowing the primary mapping.

```java
@Controller
@RequestMapping("/users")
public class UserController {

	@RequestMapping("/user")
	public String getUser() {
		
	}
    // alternative way 
    @RequestMapping(value={"/user","/user1","/user2"},method=RequestMethod.GET)
	public String getUser() {
		
	}
}
```



## Difference between @Component vs @Bean in Spring Boot
## Difference between @PathVariable and @RequestParam In Spring Boot

### @PathVariable
- Extract values from the URI Path.
### @RequestParam
- Extract values from the query.




## Pagination in Springboot
- Implementing pagination in Spring Boot can be achieved using Spring Data JPA's built-in pagination capabilities. 
- Here is a step-by-step guide on how to do this:
1. Set Up Your Spring Boot Project

2. Define Your Entity

```java
@Entity
public class Employee {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String name;
    private String role;
    
    // Getters and setters
}
```

3. Create a Repository
- Create a repository interface for your entity.
- Extend PagingAndSortingRepository or JpaRepository to get pagination capabilities.

```java
public interface EmployeeRepository extends JpaRepository<Employee, Long> {

}
```
4. Implement the Service Layer
- Create a service class to handle business logic. In this service, you'll use the repository to fetch paginated data.

```java
@Service
public class EmployeeService {
    @Autowired
    private EmployeeRepository employeeRepository;

    public Page<Employee> getEmployees(int page, int size) {
        return employeeRepository.findAll(PageRequest.of(page, size));
    }
}
```
5. Create a Controller
- Create a REST controller to expose an API endpoint for fetching paginated data.
```java
@RestController
public class EmployeeController {
    @Autowired
    private EmployeeService employeeService;

    @GetMapping("/employees")
    public Page<Employee> getEmployees(
            @RequestParam(defaultValue = "0") int page,
            @RequestParam(defaultValue = "10") int size) {
        return employeeService.getEmployees(page, size);
    }
}
```
6. Testing
- Run your Spring Boot application and test the pagination functionality. You can use a tool like Postman or simply navigate to the URL in your browser:

```
http://localhost:8080/employees?page=0&size=10

```


## What Is Spring Boot Actuator? What is its purpose?
- Actuator enables production ready features in a Spring Boot application.
- These features allow us to monitor and manage applications when they are running in production.
- Some of the features are health, metrics, info, dump, env, etc. 
- It uses HTTP endpoints or JMX beans to enable us to interact with it.
- In order to enable Spring Boot Actuator, we just need to add the spring-boot-actuator dependency to our pom.xml as shown below.
```XML
<dependency>
      <groupId>org.springframework.boot</groupId> 
      <artifactId>spring-boot-starter-actuator</artifactId> 
</dependency>
```
- Below are some of the most commonly used built-in endpoints that an Actuator provides:

    env: represents environmental properties
    health: displays application’s health condition
    httptrace: shows HTTP trace information
    info: displays application’s basic information
    metrics: displays application’s metrics information
    mappings: shows a list of all @RequestMapping paths in the application
    beans: displays a complete list of all the Spring beans in the application
    shutdown: allows the application to be gracefully shutdown

## Springboot Logging
- Logging is a process of storing application execution details.
- TRACE => DEBUG => INFO => WARN => ERROR => FATAL
- In SpringBoot the default log level is 'INFO'

```
logging.level.root=debug
```


# Spring Boot

### Create simple search API for your product in spring boot
- https://www.youtube.com/watch?v=QtnS_IqA5iM

### Adding Pagination with Page Number Display in a Spring Boot Application
- https://www.youtube.com/watch?v=CqEvjs3U7Ec
