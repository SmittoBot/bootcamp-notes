## Why Spring?
### Spring 
* Very popular framework for building Java applications, lightweight alternative to J2EE, more helper classes
* J2EE provided client-side, server-side, business and database integration, but got messy
* Early versions of Enterprise Java Beans (EJB) were hard to develop, had to define multiple interfaces, poor performance
* Rod Johnson wrote books on J2EE without EJB, spun off into founding Spring
* Since 2013, Spring and Java EE have similar feature sets, but Spring has more momentum
* Spring 5 released in 2017, upgraded min requirements to Java 8
* All code in this course will work on Spring 5, new lectures to cover new features

### Spring Core Framework 
* www.spring.io
* Goals: lightweight development with Java POJOs (Plain Old Java Objects)
  * Dependency injection to promote loose coupling
  * Declarative programming with Aspect-Oriented-Programming (AOP)
  * Minimize boilderplate Java code
* Core Container: manages how things are created, has a bean factory for creating the beans
  * Reads config file for properties and dependencies
  * SpEL: Spring Expression Language, used in config files to refer to other beans
* AOP: application-wide services like logging, security, transactions, can apply these services to objects in declarative fashion
* Data Access Layer: reduce JDBC source code by over 50%
  * ORM: Object to Relational Mapping, allows you to hook into Hibernate
  * JMS: Java Message Service: send messages to message queue in asynchronous fashion
  * Transaction manager, makes heavy use of AOP
* Instrumentation: Java agents to remotely monitor your app with JMX (Java Management Extension)
* TDD: Test Driven Development, mock objects and out-of-container testing, integration tests

### Spring Projects
* Additional Spring modules built on top of the core Spring Framework
* Includes Spring Cloud, Spring Data, for Android, Web Services, etc
* Listing of top projects on spring.io

## Development Environment
* Need JDK installed, Spring 5 requires Java 8 or higher
* Need Java application server such as tomcat, and IDE such as Eclipse
* Tomcat setup: https://wolfpaulus.com/mac/tomcat/ 
* Eclipse download: https://www.eclipse.org/downloads/packages/
* Connecting Eclipse to Tomcat: select `Servers` tab in Eclipse, go to `Apache > Tomcat v9.0`
* Download Spring JAR files: http://repo.spring.io/release/org/springframework/spring/
* Go to `spring-framework > libs` and copy all JAR files
* Create new `lib` folder in Eclipse and paste all JAR files there
* Right click project folder, `Properties > Java Build Path > Libraries > Add JAR Files`, add all, creates new `Referenced Libraries` folder

### Spring Inversion of Control - XML Configuration
* Inversion of Control: the approach of outsourcing the construction and management of objects to an object factory
* Scenario: app calls `getDailyWorkout()` to BaseballCouch, should be configurable for coaches of many other sports
* `src > new package > com.nathan.springdemo`, create a new class called BaseballCoach
* Simple BaseballCoach class:
```
package com.nathan.springdemo;

public class BaseballCoach {
	public String getDailyWorkout() {
		return "Spend 20 minutes on batting practice";
	}
}
```
* Create an Interface: `New > Interface > Coach`, has no implementation code, only a specification!
* After refactoring to interface, can create a coach in `MyApp.java` with the following:
```
Coach coach = new BaseballCoach();
```
* When creating a new class in Eclipse, can set it to implement an existing interface
* Spring provides an object factory, can give us an object based on a configuration file, makes app more configurable
* Spring container functions
  * Create and manage objects (Inversion of Control)
  * Inject object's dependencies (Dependency Injection)
* Spring Development Process:
1. Configure your Spring Beans
```
<beans ... >
 <bean id="myCoach"
  class="com.nathan.springdemo.BaseballCoach">
 </bean>
</beans>
```
2. Create a Spring Container, generically known as `ApplicationContext`
```
ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");
```
3. Retrieve Beans from Container
```
Coach theCoach = context.getBean("myCoach", Coach.class);
```
* When Java objects are created by the Spring Container, then Spring refers to them as "Spring Beans"
* Hover over errors from necessary imports in Eclipse, and it will automatically add in the imports

### Spring Dependency Injection - XML Configuration
