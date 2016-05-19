# Chapter 2 Sprig Framework basics

## 2-1 Introduction
In the previous chapter, we saw that the Spring container invokes the no-argument constructor of a bean class to create a bean instance, and setter-based DI is used to set bean dependencies. In this chapter, we'll go a step further and look at:
- Spring's support for 'programming to interfaces' design principle
- differenct approaches to instantiationg Spring beans
- constructor-based DI for passing bean dependencies as constuctor arguments
- constructor- and setter-based DI for passing simple String values to beans, and bean scopes

Lets' begin this chapter with looking at how Spring improves testablility of applications by supporting 'programming to interfaces' design principle.

## 2-2 Programming to interfaces design principle
In section 1-5 of chapter 1, we saw that a dependent POJO class contained reference to the concrete class of the dependency. For example, the FixedDipositConstroller class contained reference to the FixedDepositService class, and the FixedDepositService class contained reference to the FixedDepositDao class. If a dependent class has direct reference to the concrete class of the dependency, it results in tight coupling between the classes. This means that if you want to substitue a  differenct implementation of the dependency, it'd require changing the dependent class.
Let's now look at a scenario in which a dependent class contains direct refernce to the concrete class of the denpendency.

**Scenario: Dependent class contains reference to the concrete class of dependency**

Let's say that the FixedDepositDao class makes use of plain JDBC to interact with the database. To simplify database interaction, you create another DAO implementation, FixedDepositHibernateDao, which uses Hibernate ORM for database interaction. Now, to witch from plain JDBC to Hibernate ORM implementation, you'll need to change FixedDepositService class to use FixedDepositHibernateDao class instead of FixedDepositDao, as shown in the follwing example listing:

**Example listing 2-1** --FixedDepositService class
```java
public class FixedDepositService {
       private FixedDepositHibernateDao fixedDespositDao;
       public void setFixedDepositDao(FixedDepositHibernateDao fixedDepositDao){
              this.fixedDepositDao = fixedDepositDao;
              }
              public FixedDepositDetails getFixedDepositDetails(long id){
                     return fixedDepositDao.getFixedDepositDetails(id);
                     }
                     public boolean createFixedDeposit(FixedDipositDetails fixedDepositDetails){
                            return fixedDepositDao.createFixedDeposit(fixedDepositDetails);
}
}
```
The above example listing shows that reference to FixedDepositDao class was replaced by FixedDepositHibernateDao so that Hibernate ORM can be used for database interaction. This shows that if a dependent class refers to the concrete implementation class of the dependency, then substituting a different implementation requires changes in the dependent class.

Lte's now look at a scenario in which a dependent class contains reference to the interface implemented by the dependency.

**Scenario: Dependent class contains reference to the interface implemented by the dependency**
We know that a Java interface defines a contrat to which the implementation classes conform. So, iff a class depends on the interface implemented by the dependency, no changes is required in the class if a different implementation of the dependency is substituted. The application design approach in which a class depends on the interface implemented by the dependency is referred to as 'programming to interfaces'. The interface implemented by dependency class is referred to as a _dependency interface_.

As it is a good design practice to 'program to interfaces' thant to 'program to classes', the following class diagram shows that it is good design if ABean class depends on BBean interface and _not_ on BBeanImpl class that implements BBean interface:

![f21](.img/f21.png)
**Figure 2-1** - 'program to interfaces' is good design practice than 'program to class'

The following class diagram shows how FixedDepositService class can make use of 'programming to interfaces' design approach to easily switch the strategy used for database interaction:
![f22](.img/f22.png)
**Figure 2-2** -- The FixedDepositService depends on FixedDepositDao interface, which is implemented by FixedDepositJdbcDao and FixedDepositHibernateDao classes.

The above figure shows that the FixedDepositService class is not directly dependent on the FixedDepositJdbcDao or FixedDepositHibernateDao class. Instead, FixedDepositService dependson the FixedDepositDao interface (the dependency interface) implemented by FixedDepositJdbcDao and FixedDepositHibernateDao classes. Now, depending on whether you want to use plain JDBC or Hibernate ORM framework, you supply an instance of FixedDepositJdbcDao or FixedDepositHibernateDao to the FixedDepositService instance.

As FixedDepositService depends on FixedDepositDao interface, you can support other databse interaction strategies in the future. Let's say that you decide to use iBATIS(now renamed to MyBatis) persistence framework for database interaction. You can use iBATIS without making any changes to FixedDepositService class by simply creating a new FixedDepositIbatisDao class that implements FixedDepositDao interface, and supplying an instance of FixedDepositIbatisDao to the FixedDepositService instance.

So far we have seen that 'programming to interface' design approach results in loose coupling between a dependent class and its dependencies. Let's now look at how this design approach improves testability of the dependent classes.

## Improved testability of dependent classes
