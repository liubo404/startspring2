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











