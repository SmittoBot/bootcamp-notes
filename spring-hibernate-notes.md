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
