---
description: Study briefly about DI and Dagger 2 in Android
---

# Dependency Injection\(DI\) and Dagger 2

> **Reference**  
> : Hari Vignesh Jayapalan.\(2017\). 'Dependency Injection Technique', Medium, _Dagger 2 for Android Beginners — DI part I_. Retrieved from [https://medium.com/@harivigneshjayapalan/dagger-2-for-android-beginners-di-part-i-f5cc4e5ad878](https://medium.com/@harivigneshjayapalan/dagger-2-for-android-beginners-di-part-i-f5cc4e5ad878)

## Dependency Injection\(DI\) and IoC

### What is dependency Injection and IoC?

**Dependency**: an object that can be used\(a service\).  
**Injection**: the passing of a dependency to a dependent object\(a client\) that would use it.  
**Inversion of Control**: a class should get its dependencies from outside. In simple words, no class should instantiate another class but should get the instances from a configuration class.

## Dagger 2

* less dynamic than the others \(no reflection usage at all\) 
* but simplicity and performance of the generated code are on the same level as the hand-written code. 

### Annotations

#### @Inject

* Tell the Dagger what **all the dependencies needed to be transferred** to the dependant.
* Constructor injection
* Field injection
* Method injection

#### @Component

* to build the interface which wires everything together
* define from which modules \(or other Components\) we’re taking dependencies
* bridge between `@Module` and `@Inject`



