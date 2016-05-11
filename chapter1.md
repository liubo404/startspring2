# Chapter 1 Introduction to Spring Framework


## 1-1 Introduction
In the traditional Java enterprise application development efforts, it was a developer's responsibility to create well-structured, maintainable and easy testable applications. The developers used myriad design patterns to address these non-business requirements of an application. This not only led to low developer productivity, but also adversely affected the quality of developed applications.

Spring Framework (or "Spring" in short) is an open source application framework from SpringSource (http://www.springsource.org) that simplifies developing Java enterprise applications. It provides the infrastructure for developing well-strutured, maintainable and easily tesable application. When using Spring Framework, a developer only needs to focus on writing the business logic of the application, resulting in improved developer productivity. You can use Spring Framework to develop standalone Java applications, web applications, applets, or any other type of Java application.

This chapter starts off with an introduction to Spring Framework modules and its benefits. At the heart of Spring Framework is its Inversion o Control (IoC) container, which provides dependency injection (DI) feature. This chapter introduces Spring's DI feature and IoC container, and shows how to develop a standalone Java application using Spring. Towards the end of this chapter, we'll look at some of the SpringSource's projects that use Spring Framework as their foundation. This chapter will set the stage for the remaining chapters that delve deeper into the Spring Framework.

**NOTE** In this book, we'll use an example Internet Banking application, _MyBank_, to introduce Spring Framework features.


## 1-2 Spring Framework modules
Spring Framework consists of multiple modules that are grouped based on the application development features they address. The following table describes the different module groups in Spring Framework:

Module group|Description
--- | ---
Core container | Contains modules that form the foundation of Spring Framework. The modules in this group provide Spring's DI feature and IoC container implementation.
AOP and instrumentation | Contains modules that support AOP and class instrumentation.
DataAccess/Integration | Contains modules that simplify interaction with databases and messaging providers. This module group also contains modules that support programmtic and declarative transaction management, and object/XML mapping implementations, like JAXB and Castor.
Web | contains modules that simplify developing web and portlet applications.
Test | contains a single module that simplifies creating unit and integration tests.

The above table shows that Spring covers every aspect of enterprise application development; you can use Sprng for developing web applications, accessing databases, managing transactions, creating unit and integration tests, and so on. The Spring Framework modules are designed in sucha a way that you _only_ need to include the modules that your application needs. For instance, to use Spring's DI feature in your application, you only need to include the moduels grouped under _Core Container_. As you progress through this book, you'll find details of some of the modules that are part of Spring, and examples that show how they are used in developing applications.
Thw following figure shows the inter-dependencies of different modules of Spring:

![Local Image](./img/f11.png)
Figure 1-1 Spring modules inter-dependencies

You can infer from the above figure that the moduels contained in the _Core container_ group are central to the Spring Framework, and other moduels depend on it. Equally important are the moduels conatined in the _AOP and instrumentation_ group because they porvide AOP features to other modules in the Spring Framework.

Now, that you have some basic idea  about the areas of application development covered by Spring, let's look at the Spring IoC container.


## 1-3 Spring IoC container
A Ajava application consists of objects that interact with each other to provide applicaton behavior. The objects with which an object interacts are referred to as its _dependencies_. For instance, if an object X interacts with object Y and Z, then Y and Z are dependencies of object X. DI is a design pattern in which the dependencies of an object are typically specified as arguments to its constructor and setter methods. And, these dependencies are injected into the object when it's created.


