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